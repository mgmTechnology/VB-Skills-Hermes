# VB Lotse — Skill-Plattform

Zentrale Skill-Plattform fuer den Volkswohl-Bund. Enthaelt 77 VB-Skills aus dem Projektmanagement-Handbuch, Architekturvorgaben, Webservices-Strategie und Fachbereichs-Know-how — nutzbar in Hermes, Claude Code, IntelliJ/Junie und weiteren KI-Werkzeugen.

---

## Welche Skills brauche ich?

**Einfach den vb-lotse fragen.** In Hermes:

```
Lade vb-lotse
```

Der Lotse fragt nach deiner Rolle und Aufgabe – und empfiehlt dir 1-3 passende Skills. **Nur diese laden. 95% Token-Ersparnis.**

### Schnellauswahl per Rolle

| Du bist... | Starte mit |
|---|---|
| Release-Verantwortlicher | `vb-release-planning` + `vb-release-finalization` |
| BiPRO-Entwickler | `vb-bipro-analysis` + `bipro-taa-leben-webservice` |
| Projektleitung | `vb-projektleitung` + `vb-anforderungsmanager` |
| Architekt | `vb-it-ae-architekt` + `vb-architektur-randbedingungen` + `vb-architekturprozess` |
| Tester / Testmanager | `vb-testmanager` + `vb-test` |
| Fachbereich / Produkt | `vb-business-analyst` + `vb-feature-spezifikation` |
| Fehlerdiagnose (Prod.) | `vb-webservice-diagnostics` |
| Neuer Entwickler (Onboarding) | `vb-onboarding-webservices` |
| Prozess analysieren/verbessern | `vb-analyse` + `vb-lean-six-sigma-black-belt` |

**Faustregel:** `vb-lotse` + die 1-3 Skills fuer deine Aufgabe. Den Rest bei Bedarf nachladen.

---

## Installation in KI-Werkzeugen

### 1. Hermes (Desktop-GUI) — ✅ bereits eingerichtet

Die Skills sind bereits registriert. Nichts zu installieren.

**So nutzt du es:**
```
Lade vb-lotse
```

Der Lotse routet automatisch. Fertig.

**Skills verwalten:**
```bash
hermes skills list                    # Alle Skills anzeigen
hermes skills info vb-testmanager     # Details zu einem Skill
```

---

### 2. IntelliJ IDEA mit Junie

**Voraussetzung:** Junie-Plugin installiert

**Die `.junie/rules.md` liegt bereits im Repo.** Zwei Wege, sie einzubinden:

#### Weg A: Referenzieren (empfohlen – nichts kopieren)

In IntelliJ: `Settings → Tools → Junie → Additional Context`:
```
Pfad: C:\Dev\Github\VB Lotse\
☑ Subdirectories scannen
```

IntelliJ neu starten. Fertig – Junie liest `.junie/rules.md` und alle Skills direkt aus dem Repo.

#### Weg B: Kopieren (standalone)

```bash
cp -r C:/Dev/Github/VB\ Lotse/.junie C:/Dev/Github/DEIN-PROJEKT/
cp -r C:/Dev/Github/VB\ Lotse/skills C:/Dev/Github/DEIN-PROJEKT/
cp -r C:/Dev/Github/VB\ Lotse/docs/referenzen C:/Dev/Github/DEIN-PROJEKT/docs/
```

#### Test-Prompt

In Junie eingeben:
```
Nutze die VB Skills. Starte mit vb-lotse.
```
Der Lotse empfehlt 1-3 Skills. Fertig.

---

### 3. Claude Code (CLI)

**Voraussetzung:** Claude Code installiert (`npm install -g @anthropic-ai/claude-code`)

**Installation:**
```bash
cd C:\Dev\Github\VB Lotse

# CLAUDE.md anlegen (wird von Claude Code automatisch geladen)
cat > CLAUDE.md << 'EOF'
# VB Skill-Plattform

Du arbeitest beim Volkswohl-Bund. Immer mit skills/01-rollen/vb-lotse/SKILL.md starten.

## Vorgehen
1. vb-lotse laden → analysiert Aufgabe → empfehlt 1-3 passende Skills
2. Nur die empfohlenen Skills aus skills/01-rollen/ laden
3. Nie mehr als 3 Skills gleichzeitig
4. Keine VB-Standards erfinden
5. Antworten auf Deutsch

## Slash Commands
/vb-lotse          → Lotse laden und starten
/vb-architektur    → Architektur-Skills laden
/vb-test           → Test-Skills laden
/vb-pm             → PM-Rollen laden

## Skills-Verzeichnis
Alle Skills liegen unter skills/01-rollen/
EOF

# Slash Commands in .claude/commands/ anlegen
mkdir -p .claude/commands

cat > .claude/commands/vb-lotse.md << 'EOF'
Lade und folge der Anleitung in skills/01-rollen/vb-lotse/SKILL.md.
Analysiere $ARGUMENTS und empfehle die passenden VB-Skills.
EOF

cat > .claude/commands/vb-architektur.md << 'EOF'
Lade skills/01-rollen/vb-architektur-randbedingungen/SKILL.md
und skills/01-rollen/vb-architektur-arc42/SKILL.md.
Bearbeite dann: $ARGUMENTS
EOF
```

**So nutzt du es:**
```bash
cd C:\Dev\Github\VB Lotse
claude                    # Startet Claude Code, laedt CLAUDE.md automatisch

# Oder direkt mit Prompt:
claude -p "/vb-lotse Ich brauche ein Testkonzept fuer VBLife"
```

---

### 4. Claude Desktop

**Installation:**
1. Claude Desktop oeffnen
2. Settings → Developer → Edit Config
3. `claude_desktop_config.json` oeffnen

```json
{
  "projects": {
    "VB Lotse": {
      "path": "C:\\Dev\\Github\\VB Lotse",
      "instructions": "Du arbeitest beim Volkswohl-Bund. Starte immer mit skills/01-rollen/vb-lotse/SKILL.md. Lade nie mehr als 3 Skills auf einmal."
    }
  }
}
```

**So nutzt du es:**
1. Claude Desktop starten
2. Projekt "VB Lotse" auswaehlen
3. Prompt: `Nutze die VB Skills. Starte mit vb-lotse. [Aufgabe]`
4. Claude liest automatisch die project instructions und findet die Skills

---

### 5. Weitere Werkzeuge

| Werkzeug | Konfigurationsdatei |
|---|---|
| Cursor | `.cursorrules` im Projekt-Root |
| OpenAI Codex | `AGENTS.md` im Projekt-Root |
| Windsurf | `.windsurf/rules` im Projekt-Root |
| GitHub Copilot | `.github/copilot-instructions.md` |

Fuer alle gilt das gleiche Prinzip: `skills/01-rollen/vb-lotse/SKILL.md` als Einstieg.

---

## Umgang mit Referenzen (BiPRO-Doku, Release-Regeln, Kalender)

Einige Skills nutzen **Referenzdokumente** unter `docs/referenzen/Webservices-Strategie/`:
- `BiPRO_TAA_Leben_Gesamtdokumentation_v3.html` (136 KB)
- `BiPRO_TAA_Leben_Einarbeitungsplan.html` (51 KB)
- `release-java-anwendungen-vsl-finalisierung.md` (12 KB)
- `release-planung-regeln.md` (2,8 KB)
- `kalender-nrw-regeln.md` (2 KB)

**Diese Dateien muessen je nach Werkzeug unterschiedlich behandelt werden:**

| Werkzeug | Referenzen verfuegbar? | Was tun? |
|---|---|---|
| **Hermes** | ✅ Automatisch | Nichts – Referenzen werden bei `skill_view()` mitgeladen |
| **Junie – Weg A** (Referenzieren) | ✅ Automatisch | Additional Context auf `C:\Dev\Github\VB Lotse\` → Referenzen sind da |
| **Junie – Weg B** (Kopieren) | ❌ Muss kopiert werden | `cp -r docs/referenzen/` ins Projekt |
| **Claude Code** | ✅ Wenn aus Repo gestartet | `cd C:\Dev\Github\VB Lotse && claude` – Referenzen liegen dann relativ |
| **Claude Desktop** | ❌ Nur wenn Projekt-Pfad gesetzt | Project-Path auf Repo setzen (siehe oben) |
| **ChatGPT / Gemini** | ❌ Im ZIP mitliefern | `docs/referenzen/` mit in das ZIP packen |

**Faustregel:** Wenn du das Repo referenzierst (empfohlen), sind Referenzen automatisch da.
Wenn du kopierst (standalone), `docs/referenzen/` mitkopieren.

---

## Verzeichnisstruktur

```
C:\Dev\Github\VB Lotse\
├── README.md                    ← diese Datei
├── DOKUMENTATION.md             ← vollstaendige Plattform-Doku
├── CLAUDE.md                    ← Claude Code Projekt-Konfiguration
├── .junie/rules.md              ← Junie/IntelliJ Konfiguration
├── .claude/commands/            ← Claude Code Slash Commands
│
├── vb-lotse/                    ← Der Router (~3 KB)
│   └── SKILL.md                    Kennt alle 40 Skills, laedt keinen
│
├── vb-skill-befueller/          ← Skill-Befueller (~4 KB)
│   └── SKILL.md                    Hilft Fachabteilungen, Skills zu befuellen
│
├── vb-tool-installation/        ← Tool-Installation (~9 KB)
│   └── SKILL.md                    Installation in allen KI-Werkzeugen
│
├── Quellen/                     ← Original-Confluence-Exporte
│   └── HTML/
│       ├── Projektmanagement/      (Rollenbeschreibung, Prozesse...)
│       └── Architektur/            (Randbedingungen, arc42...)
│
├── docs/referenzen/Webservices-Strategie/
│   ├── BiPRO_TAA_Leben_Gesamtdokumentation_v3.html
│   ├── BiPRO_TAA_Leben_Einarbeitungsplan.html
│   ├── GRUPPENSTECKBRIEF.md
│   ├── kalender-nrw-regeln.md
│   ├── REFERENZEN.md
│   ├── release-java-anwendungen-vsl-finalisierung.md
│   └── release-planung-regeln.md
│
├── skills/                      ← 77 VB-Fachskills
│   ├── 00-prozess/  13 Skills  (vb-analyse, vb-test, vb-review...)
│   ├── 01-rollen/   32 Skills  (PM-Rollen + Architektur)
│   ├── 02-technik/  18 Skills  (ws-strategy, Java, Deployment...)
│   ├── 03-governance/ 6 Skills
│   ├── 04-standards/  4 Skills
│   ├── 05-plattform/  6 Skills
│   └── 06-werkzeuge/  9 Skills  (Jira, Confluence, Scrum...)
```

---

## Hermes-Skills (installiert)

77 VB-Skills in Hermes registriert. Alle per `skill_view(name)` ladbar:

| Kategorie | Skills |
|---|---|
| **vb-prozess** (13) | vb-analyse, vb-anforderungen, vb-architekturprozess, vb-dokumentation, vb-feature-spezifikation, vb-projekt-initialisierung, vb-review, vb-spezifikation-verfeinern, vb-test, vb-umsetzung, vb-architektur, vb-klickjourney-test, vb-qualitaetspruefung |
| **ws-strategy** (6) | vb-release-planning, vb-release-finalization, vb-bipro-analysis, vb-webservice-diagnostics, vb-webservice-documentation, vb-onboarding-webservices |
| PM-Rollen (30) | vb-projektleitung, vb-multi-projekt-management-mpm, vb-f1er, vb-vorstand, vb-sonderfunktion, vb-fachexperten, vb-fachbereichs-koordinator, vb-fuehrungskraft-fachabteilung, vb-anforderungsmanager, vb-business-analyst, vb-it-ae-koordinator, vb-it-ae-architekt, vb-it-ae-anwendungsentwickler, vb-it-ae-testautomatisierer, vb-it-ae-fuehrungskraft, vb-it-betrieb-koordinator, vb-it-betrieb-administrator, vb-it-betrieb-produktion, vb-it-betrieb-client-service, vb-it-betrieb-change-manager, vb-it-betrieb-fuehrungskraft, vb-testmanager, vb-fehlermanager, vb-testdatenmanager, vb-tester-fachabteilung, vb-tester-it-betrieb, vb-priorunde, vb-lenkungsausschuss-la, vb-externe-mitarbeiter |
| Architektur (2) | vb-architektur-randbedingungen, vb-architektur-arc42 |
| Plattform (8) | vb-lotse, vb-skill-befueller, vb-tool-installation, vb-jira-experte, vb-lean-six-sigma-black-belt, marc-vb-profile, bipro-taa-leben-webservice, bipro-taa-leben-einarbeitung |

---

## Token-Strategie

| Ansatz | Token |
|---|---|
- Alle 77 Skills laden | ~350 KB (unmoeglich) |
| Lotse + 1-3 Fach-Skills | ~10-18 KB (produktiv) |
| **Ersparnis** | **95%** |

```
Deine Frage → vb-lotse (3 KB) → Empfehlung (1-3 Skills) → Du bestaetigst → Skills geladen
```

---

## Skills selbst befuellen (fuer Fachabteilungen)

1. `Lade vb-skill-befueller`
2. Strukturiertes Interview: VB-Verfahrensanweisungen, Referenzen, Praxis-Know-how
3. SKILL.md-Entwurf erstellen
4. Review durch Wissenstraeger
5. Im passenden Kategorie-Ordner ablegen

---

*Stand: 16.06.2026 · Betreut von Marc, Webservices & Strategie · VB Lotse*