# VB Lotse — Skill-Plattform

Zentrale Skill-Plattform fuer den Volkswohl-Bund. Enthaelt 40 VB-Skills aus dem Projektmanagement-Handbuch, Architekturvorgaben und Fachbereichs-Know-how — nutzbar in Hermes, Claude Code, IntelliJ/Junie und weiteren KI-Werkzeugen.

---

## Schnellstart (Hermes)

```
Lade vb-lotse
```

Der Lotse analysiert deine Aufgabe und empfehlt 1-3 passende Skills. **Nie alle 40 laden — 95% Token-Ersparnis.**

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

**Voraussetzung:** Junie-Plugin installiert (Settings → Plugins → Junie)

**Installation:**
```bash
# In der Git-Bash / Terminal:
cd C:\Dev\Github\VB Lotse

# 1. Junie-Regeldatei anlegen
mkdir -p .junie
cat > .junie/rules.md << 'EOF'
# VB Skill-Plattform

Du arbeitest beim Volkswohl-Bund. Bei jeder Aufgabe zuerst den Kontext analysieren,
dann die passenden VB-Skills aus skills/ laden.

## Verfuegbare Skills (40 — nie alle laden!)

### Immer zuerst:
- skills/01-rollen/vb-lotse/SKILL.md — Router, empfehlt 1-3 Skills

### PM-Rollen (30):
- skills/01-rollen/vb-projektleitung/SKILL.md
- skills/01-rollen/vb-anforderungsmanager/SKILL.md
- skills/01-rollen/vb-business-analyst/SKILL.md
- skills/01-rollen/vb-testmanager/SKILL.md
- skills/01-rollen/vb-it-ae-architekt/SKILL.md
- ... (alle 30 Rollen in skills/01-rollen/)

### Architektur (2):
- skills/01-rollen/vb-architektur-randbedingungen/SKILL.md — VB-Architekturvorgaben
- skills/01-rollen/vb-architektur-arc42/SKILL.md — arc42 Template

## Regeln
1. Immer mit vb-lotse starten
2. Nur 1-3 Skills laden
3. Keine VB-Standards erfinden — nur was in den Skills steht
4. Bei Unsicherheit nachfragen
5. Code-Aenderungen erst nach Bestaetigung
6. Antworten auf Deutsch, spezifikationsgetrieben

## Arbeitsweise
- Vor jeder Aenderung: vb-lotse → Kontext → passende Skills laden
- Waehrend der Arbeit: Skills als Referenz nutzen
- Nach Abschluss: Ergebnisse dokumentieren
EOF

# 2. IntelliJ konfigurieren
# Settings → Tools → Junie → Additional Context:
#   Pfad: C:\Dev\Github\VB Lotse\
#   Haken: "Scan subdirectories for rules"
```

**So nutzt du es in IntelliJ:**
1. Projekt oeffnen
2. Junie-Panel oeffnen (View → Tool Windows → Junie)
3. Prompt starten mit: `Nutze die VB Skills. Starte mit vb-lotse. [Aufgabe]`
4. Junie laedt automatisch die .junie/rules.md und den Lotse
5. Lotse empfehlt 1-3 Skills, die du dann im Prompt referenzierst

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
└── skills/                      ← 40 VB-Fachskills
    └── 01-rollen/  40 Skills   (PM-Rollen + Architektur)
```

---

## Hermes-Skills (installiert)

40 VB-Skills in Hermes registriert. Alle per `skill_view(name)` ladbar:

| Kategorie | Skills |
|---|---|
| PM-Rollen | vb-projektleitung, vb-multi-projekt-management-mpm, vb-f1er, vb-vorstand, vb-sonderfunktion, vb-fachexperten, vb-fachbereichs-koordinator, vb-fuehrungskraft-fachabteilung, vb-anforderungsmanager, vb-business-analyst, vb-it-ae-koordinator, vb-it-ae-architekt, vb-it-ae-anwendungsentwickler, vb-it-ae-testautomatisierer, vb-it-ae-fuehrungskraft, vb-it-betrieb-koordinator, vb-it-betrieb-administrator, vb-it-betrieb-produktion, vb-it-betrieb-client-service, vb-it-betrieb-change-manager, vb-it-betrieb-fuehrungskraft, vb-testmanager, vb-fehlermanager, vb-testdatenmanager, vb-tester-fachabteilung, vb-tester-it-betrieb, vb-priorunde, vb-lenkungsausschuss-la, vb-externe-mitarbeiter |
| Architektur | vb-architektur-randbedingungen, vb-architektur-arc42 |
| Plattform | vb-lotse, vb-skill-befueller, vb-tool-installation, vb-jira-experte, vb-lean-six-sigma-black-belt, marc-vb-profile |
| BiPRO | bipro-taa-leben-webservice, bipro-taa-leben-einarbeitung |

---

## Token-Strategie

| Ansatz | Token |
|---|---|
| Alle 40 Skills laden | ~200 KB (unmoeglich) |
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