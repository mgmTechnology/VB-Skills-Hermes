---
name: vb-tool-installation
description: Installation und Nutzung der VB-Skill-Plattform in 6 KI-Werkzeugen: Junie, Claude Code, OpenAI Codex, IntelliJ, Cursor und Windsurf.
---

# VB Skills — Installation & Nutzung in KI-Werkzeugen

## Übersicht: Welches Werkzeug für wen?

| Werkzeug | Am besten für | Skill-Methode |
|---|---|---|
| **Claude Code** | Vollständige Repository-Workflows, Architektur, Dokumentation | `CLAUDE.md` + `skills/` im Repo |
| **Cursor** | Codeanalyse, Refactoring, tägliches Entwickeln | `.cursorrules` + `skills/` im Repo |
| **Junie (IntelliJ)** | Java/Spring Boot, IDE-nahe Arbeit, Debugging | `.junie/rules.md` + Skill-Verzeichnis |
| **OpenAI Codex** | Schnelle Implementierung, PR-Erstellung, Code-Generation | `AGENTS.md` + `skills/` im Repo |
| **Windsurf** | KI-gestützte Entwicklung mit Kontext | `.windsurf/rules` + Projekt-Kontext |
| **Hermes** | Desktop-Agent, Skill-Plattform, Cron-Jobs | `skill_view()` + Memory |

---

## 1. Claude Code

### Installation

```bash
# Claude Code installieren (falls nicht vorhanden)
npm install -g @anthropic-ai/claude-code

# Im Projektverzeichnis
cd mein-projekt
claude
```

### Skills einbinden — Variante A: Im Repo (empfohlen)

```
mein-projekt/
├── CLAUDE.md              ← Claude liest das beim Start
├── .claude/
│   └── settings.json      ← Claude-Konfiguration
├── skills/                ← VB Skills hierher kopieren
│   ├── 00-prozess/
│   ├── 01-rollen/
│   └── ...
```

**`CLAUDE.md` Inhalt:**
```markdown
# Arbeitsanweisung

Bei jeder Aufgabe: Starte mit skills/00-prozess/vb-lotse/SKILL.md
Der Lotse empfiehlt die passenden Skills.

Keine Erfindungen. Keine VB-Standards erfinden.
Bei Unklarheit: nachfragen.
```

### Skills einbinden — Variante B: Externer Pfad

```text
Nutze die VB Skills aus C:\Dev\Github\VB Lotse\skills\
Starte mit vb-lotse.
[Deine Aufgabe]
```

### Slash Commands

```text
/vb-lotse [Anliegen]
/vb-projektstart [Projektidee]
/vb-code-review [Reviewauftrag]
/vb-release-planning [Go-Live-Datum]
```

### Typischer Start

```text
Lies zuerst CLAUDE.md.
Starte danach mit skills/00-prozess/vb-lotse/SKILL.md.
Ich möchte [Aufgabe beschreiben].
```

---

## 2. Cursor

### Installation

Cursor liest automatisch `.cursorrules` im Projekt-Root.

### Skills einbinden

```
mein-projekt/
├── .cursorrules            ← Cursor liest das automatisch
├── skills/                 ← VB Skills hierher kopieren
│   ├── 00-prozess/
│   ├── 01-rollen/
│   └── ...
```

**`.cursorrules` Inhalt:**
```markdown
Du arbeitest mit der VB-Skill-Plattform.
Skills liegen unter skills/

Bei jeder Aufgabe:
1. Lies zuerst skills/00-prozess/vb-lotse/SKILL.md
2. Der Lotse empfiehlt die passenden Skills
3. Lade nur die empfohlenen Skills — nie alle auf einmal

Keine VB-Standards erfinden.
Bei fehlenden Informationen: nachfragen, als "offen" markieren.
```

### Typischer Start

```text
Nutze die VB Skills.
Starte mit vb-lotse.
[Deine Aufgabe]
```

### Cursor-spezifische Tipps

- Cursor eignet sich besonders für Codeanalyse und Refactoring
- `@folder:skills/` im Chat verweist auf den Skill-Ordner
- `@file:CLAUDE.md` lädt die Arbeitsanweisung

---

## 3. Junie (IntelliJ)

### Installation

Junie liest `.junie/rules.md` im Projekt automatisch.

### Skills einbinden

```
mein-projekt/
├── .junie/
│   ├── rules.md            ← Junie liest das automatisch
│   └── skills/             ← Nur die wichtigsten Skills
│       ├── vb-lotse.md
│       ├── vb-code-review.md
│       └── vb-bipro-analysis.md
```

**`.junie/rules.md` Inhalt:**
```markdown
# Junie VB Skill-Regeln

Du arbeitest mit Java/Spring Boot im Volkswohl-Bund Kontext.

Bei unklaren Aufgaben:
1. Analysiere das Anliegen
2. Empfiehl passende Skills aus der VB-Skill-Plattform
3. Frage nach Bestätigung vor dem Laden

Verfügbare Skills liegen unter:
- C:\Dev\Github\VB Lotse\skills\  (extern, voller Katalog)
- .junie/skills/                    (Projekt-lokal, Auswahl)

Arbeitsprinzipien:
- Erst verstehen, dann bauen
- Keine VB-Standards erfinden
- Nachfragen statt raten
- Code-Änderungen erst nach Bestätigung
```

### Junie in IntelliJ konfigurieren

1. **Settings → Tools → Junie**
2. **Additional Context:** `C:\Dev\Github\VB Lotse\skills\` hinzufügen
3. **Rules File:** `.junie/rules.md` (wird automatisch erkannt)

### Typischer Start

```text
Nutze die VB Skills aus diesem Projekt.
Beginne mit vb-lotse.
Mein Use Case: [Aufgabe]
```

### Junie-spezifische Tipps

- Junie hat direkten Zugriff auf den Java-Code → perfekt für Code-Review und Refactoring
- Kann Maven-Builds ausführen und Testergebnisse analysieren
- IDE-Integration: Breakpoints, Debugging, Run Configurations

---

## 4. OpenAI Codex

### Installation

```bash
# Codex CLI installieren
npm install -g @openai/codex

# Im Projektverzeichnis
cd mein-projekt
codex
```

### Skills einbinden

Codex liest `AGENTS.md` im Projekt-Root.

```
mein-projekt/
├── AGENTS.md               ← Codex liest das beim Start
├── skills/                 ← VB Skills hierher kopieren
│   ├── 00-prozess/
│   └── ...
```

**`AGENTS.md` Inhalt:**
```markdown
# Arbeitsanweisung für Codex

Bei jeder Aufgabe: Starte mit skills/00-prozess/vb-lotse/SKILL.md
Der Lotse entscheidet, welche weiteren Skills sinnvoll sind.

Arbeitsweise:
1. Anliegen verstehen
2. Kontext einordnen (Projektleitung, Analyse, Architektur, Entwicklung, Test)
3. Passende Skills vorschlagen
4. Nutzer fragen, ob der Ablauf ausgeführt werden soll
5. Skills nacheinander anwenden
6. Ergebnisse dokumentieren

Keine Erfindungen. Keine VB-Standards erfinden.
```

### Typischer Start

```text
Lies zuerst AGENTS.md.
Starte danach mit skills/00-prozess/vb-lotse/SKILL.md.
[Aufgabe]
```

---

## 5. Windsurf

### Installation

Windsurf liest `.windsurf/rules` im Projekt.

### Skills einbinden

```
mein-projekt/
├── .windsurf/
│   └── rules               ← Windsurf-Kontextregeln
├── skills/                 ← VB Skills hierher kopieren
│   └── ...
```

**`.windsurf/rules` Inhalt:**
```markdown
VB Skill-Plattform ist aktiv.
Skills liegen unter skills/

Immer mit vb-lotse starten, wenn die Aufgabe unklar ist.
Der Lotse empfiehlt 1-3 Skills — nie alle laden.

VB-Kontext:
- Java 21, Spring Boot, Maven
- Volkswohl Bund, IT-AE Lebensversicherungen
- Keine Standards erfinden, nachfragen bei Unklarheit
```

### Typischer Start

```text
@skills/00-prozess/vb-lotse/SKILL.md
[Deine Aufgabe]
```

---

## 6. Hermes (Desktop Agent)

### Installation

Skills werden via `skill_manage` installiert oder als Dateien in `%LOCALAPPDATA%\hermes\skills\` abgelegt.

### Skills laden

```text
Lade vb-lotse
```

Der Lotse analysiert deine Aufgabe und empfiehlt passende Skills. Nur 1-3 werden geladen — 95% Token-Ersparnis.

### Memory (automatisch)

Hermes speichert deinen Kontext im Memory und lädt ihn automatisch in jede Session:
- Wer du bist (VB, IT-AE, Webservices & Strategie)
- Tech-Stack, Arbeitsweise, Projekt-Pfade
- Lean Six Sigma Black Belt

### Typischer Start

```text
Lade vb-lotse
Ich muss [Aufgabe]
```

---

## Gemeinsame Prinzipien (alle Werkzeuge)

1. **Immer mit dem Lotsen starten** — wenn der Kontext unklar ist
2. **Nur 1-3 Skills laden** — nie den ganzen Katalog
3. **Keine VB-Standards erfinden** — unbekanntes als `offen` markieren
4. **Erst analysieren, dann ändern** — besonders bei existierenden Projekten
5. **Nachfragen statt raten** — offene Punkte sichtbar machen

## Verzeichnisstruktur für die Projekt-Integration

```
mein-projekt/
├── README.md
├── CLAUDE.md               ← Claude Code
├── AGENTS.md               ← OpenAI Codex
├── .cursorrules            ← Cursor
├── .junie/rules.md         ← Junie (IntelliJ)
├── .windsurf/rules         ← Windsurf
├── .claude/                ← Claude Code Config
├── skills/                 ← VB Skills (Auswahl, nicht alle!)
│   ├── 00-prozess/
│   │   └── vb-lotse/       ← Minimum: der Lotse
│   ├── 02-technik/
│   │   └── ...             ← Projektrelevante Fach-Skills
│   └── ...
├── docs/
├── reference/
└── src/
```

## Skill-Auswahl für die Projekt-Integration

Nicht alle 76 Skills ins Repo kopieren! Nur was das Team wirklich braucht:

| Immer | Bei Bedarf |
|---|---|
| `vb-lotse` (Router) | `vb-release-planning` |
| `vb-code-review` | `vb-release-finalization` |
| `vb-umsetzung` | `vb-webservice-diagnostics` |
| `vb-test` | `vb-anonymisierung` |
| `vb-bipro-analysis` (ws-strategy) | `vb-dsgvo-pruefung` |

---

*Erstellt: 15.06.2026 · VB Lotse Plattform · C:\Dev\Github\VB Lotse\*