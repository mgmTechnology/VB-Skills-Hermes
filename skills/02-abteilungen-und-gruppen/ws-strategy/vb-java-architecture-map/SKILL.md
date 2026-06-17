---
name: java-architecture-map
description: Analyze an existing Java project (Maven/Gradle) and produce a visual architecture map — modules, subsystems, components, and their dependencies — as an interactive zoomable topology viewer plus exportable Mermaid diagrams. Use when asked to understand, document, or visualize the structure of a Java codebase ("show me the modules", "map the architecture", "which components depend on what", "Modulübersicht", "Teilsysteme erkennen").
---

# Java Architecture Map

Analyze a Java project and render its structure visually: build modules,
subsystems/domains, components, and the dependencies between them. Works on a
single repo, a multi-module Maven/Gradle build, or a Spring application.

You produce two things from one analysis:
1. **`topology.json`** — a machine-readable model of the system.
2. **`ARCHITECTURE.html`** — an interactive, offline, zoomable map built from
   the viewer template that ships with this plugin.
3. Small exportable **Mermaid** diagrams for docs and PRs.

## Step 0 — Greet, explain, and gather options

On invocation, **first** tell the user in one or two sentences what this skill
does (analyzes a Java project and renders an interactive architecture map of
modules / subsystems / components / dependencies, plus Mermaid diagrams). Then
gather the inputs and options **before** doing any analysis.

Use the `AskUserQuestion` tool to ask — every option below is a defined set, so
present them as selectable lists, not free-form prose. Skip any value the user
already provided in their request, and state the default for anything they don't
care about. Ask the two free-text inputs (project dir, output dir) directly in
your message if they weren't given.

Required inputs (ask directly if missing):
- **Project directory** — root of the Java codebase. Default: current working dir.
- **Output directory** — where `ARCHITECTURE.html` lands. Default
  `analysis/<project-name>/`.

Options (ask via `AskUserQuestion`; defaults in **bold**):
| Option | Choices |
| --- | --- |
| **Granularity** | **Build module** · Package · Component (Spring stereotype) |
| **Subsystem grouping** | **Auto** (build module if multi-module, else package) · By package hierarchy · By layer (controller/service/repository) |
| **Scope** *(multi-select)* | **Exclude tests** · **Exclude generated/build output** · Include datastores · Include UI/templates |
| **Persona flows** | **Yes** (2–4 walkthroughs) · No |
| **Text language** | **English** · German |
| **Theme** | **Dark** · Light |
| **Accent color** | **Anthropic `#cc785c`** · choose a hex (free text) |
| **Mermaid exports** *(multi-select)* | **module-graph** · **component-deps** · **data-access** · None |

Confirm the chosen settings back in one line, then proceed.

## Step 1 — Identify the build structure

Detect how the project is organized before reading source:

- **Maven**: find every `pom.xml`. The root `<modules>` list (or any reactor
  parent) defines build modules. Each module's `artifactId` is its id.
- **Gradle**: parse `settings.gradle`/`settings.gradle.kts` `include(...)`
  entries for subprojects; each `build.gradle` is a module.
- **Single module / plain `src/`**: there is one build module — treat the
  top-level packages (or `src/main/java/<group>/<area>`) as the subsystems.

If both are absent, fall back to top-level source packages as the grouping.

## Step 2 — Extract the four datasets

Write a re-runnable analysis script (Python preferred) saved as
`<out>/extract_architecture.py`, so the result can be audited and re-run. It
parses the Java sources and emits `<out>/topology.json`. Extract:

- **Modules / components** — leaf units of the map. Granularity, coarsest that
  is still useful:
  - multi-module build → one leaf per build module;
  - single large module → one leaf per top-level package (e.g.
    `com.acme.billing.invoice`), or per Spring component where annotations make
    that clearer.
  Record `loc` (lines of `.java`, excluding blanks/comments) per leaf — it
  drives circle size in the viewer. Record the representative `file` path.
- **Dependency edges** — resolve real coupling, not just text matches:
  - **module deps**: Maven `<dependency>` between reactor modules; Gradle
    `project(":...")` dependencies → edge kind `call`.
  - **package/import deps**: `import` statements crossing component boundaries,
    aggregated to the leaf level → edge kind `call`.
  - **injection / dispatch**: Spring `@Autowired`, constructor injection,
    `@Component`/`@Service`/`@Repository`/`@Controller` wiring, and
    `@FeignClient`/REST clients between components → edge kind `dispatch`.
    These are the edges a plain import scan misses.
  - **data access**: JPA `@Entity`/`@Repository`, JDBC, MyBatis mappers →
    edge kind `read`/`write` toward a datastore leaf (the table/schema or
    logical DB name). Group datastores under a `dom:data` domain.
- **Entry points** — `public static void main`, Spring
  `@SpringBootApplication`, `@RestController`/`@Controller` request mappings,
  `@Scheduled`/`@KafkaListener`/`@RabbitListener`/JMS consumers, servlet
  `web.xml` mappings. Without these, every leaf looks unreachable.
- **Dead-end candidates** — leaves with no inbound edges. **Suppress** anything
  reachable by dynamic wiring (Spring beans, reflection, `@Component` scanned
  classes, dispatcher targets) — those are not dead. Record the uncertainty in
  `observations` instead of marking them dead.

Aggregate package-level edges to the leaf granularity you chose; never emit an
edge whose endpoint id is not a leaf in the tree.

## Step 3 — topology.json schema

The viewer expects exactly this shape:

```json
{
  "system": "<display name>",
  "root": {
    "id": "sys", "name": "<system>", "kind": "system",
    "children": [
      { "id": "dom:<subsystem>", "name": "<Subsystem>", "kind": "domain",
        "children": [
          { "id": "<component-id>", "name": "<Component>", "kind": "module",
            "language": "java", "loc": 1234, "file": "src/.../X.java" }
        ] },
      { "id": "dom:data", "name": "Data stores", "kind": "domain",
        "children": [
          { "id": "ds:<NAME>", "name": "<NAME>", "kind": "datastore" }
        ] }
    ]
  },
  "edges": [ { "source": "<id>", "target": "<id>", "kind": "call" } ],
  "entryPoints": ["<id>"],
  "deadEnds": ["<id>"],
  "observations": ["<architect observation>"],
  "flows": [
    { "name": "<business flow>", "persona": "<who experiences it>",
      "description": "<one plain-language sentence>",
      "steps": [ { "label": "<business-language step>", "nodes": ["<id>","<id>"] } ] }
  ]
}
```

- **Subsystems** (`kind: "domain"`) group the components. Derive them from build
  modules, from the package hierarchy (`com.acme.<subsystem>.*`), or from
  obvious layer/feature boundaries — whichever the codebase actually uses.
- Leaf `kind`: `module` (component), `datastore`, `screen` (UI/template).
- Edge kinds: `call`, `dispatch`, `read`, `write`.
- `observations`: 3–7 architect notes — tight-coupling clusters, a component
  every subsystem depends on (a god-module), datastores with too many writers,
  cyclic dependencies between modules, candidates for extraction.
- `flows`: 2–4 end-to-end flows anchored to a **persona** (the end user, the
  operator, the integrator — not the maintainer), each 3–8 business-language
  steps listing the component/datastore ids that implement them. This is what
  makes the map readable to non-engineers.

Do not put credentials or raw config values (JDBC URLs with passwords, etc.)
into datastore names or observations — use logical names only; the file is
shareable and the viewer renders names verbatim.

Run the script and show a short human summary (cap ~150 lines for large repos).

## Step 4 — Render the interactive map

Build `ARCHITECTURE.html` from the shipped template — do **not** hand-write the
viewer. **Honor the Step 0 options here**:

- **Theme = Light**: after injecting the data, also replace the dark `:root`
  CSS variables with light equivalents (e.g. `--bg:#ffffff; --panel:#f3f3f3;
  --panel-2:#e8e8e8; --text:#1e1e1e; --muted:#666; --border:#d0d0d0`), keeping
  `--accent`/`--blue`/`--green` unless overridden.
- **Accent color**: replace `--accent: #cc785c` with the chosen hex.
- **Title**: set `<title>` and the HUD heading to the system name.

Apply these as additional `.replace(...)` calls on the template string in the
same script below.

```bash
python3 - "${CLAUDE_PLUGIN_ROOT}/assets/topology-viewer.html" <out-dir> <<'EOF'
import json, sys
tpl_path, out_dir = sys.argv[1], sys.argv[2]
tpl = open(tpl_path, encoding="utf-8").read()
marker = "/*__TOPOLOGY_DATA__*/ null"
assert marker in tpl, f"injection marker not found in {tpl_path}"
data = json.dumps(json.load(open(f"{out_dir}/topology.json", encoding="utf-8")))
open(f"{out_dir}/ARCHITECTURE.html", "w", encoding="utf-8").write(
    tpl.replace(marker, "/*__TOPOLOGY_DATA__*/ " + data))
print(f"wrote {out_dir}/ARCHITECTURE.html")
EOF
```

The viewer is fully self-contained (its d3 subset is inlined) — it works offline
and on air-gapped networks. If the `python3` call can't find the template,
`${CLAUDE_PLUGIN_ROOT}` was not substituted — report that, don't improvise a
viewer.

Also export the Mermaid diagrams the user selected in Step 0 (keep each under
~40 edges; collapse to subsystem level if larger):

- `<out>/module-graph.mmd` — subsystem-level `graph TD`, entry points highlighted
- `<out>/component-deps.mmd` — `graph LR` of component dependencies
- `<out>/data-access.mmd` — `graph LR`, components → datastores, read vs write marked

Write `observations`, flow descriptions, and any prose in the **text language**
chosen in Step 0. If persona flows were turned off, leave `flows` empty.

## Step 5 — Present

Tell the user to open `<out>/ARCHITECTURE.html` in a browser, and to try:
search for a component, click it to see its inbound/outbound dependencies,
toggle edge kinds, and pick a persona flow from the walkthrough dropdown.
Surface the 3–7 observations directly in your reply — those are the findings
that need a human eye.
