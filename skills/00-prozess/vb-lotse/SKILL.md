---
name: vb-lotse
description: Zentraler Einstiegspunkt der VB-Skill-Plattform. Analysiert Anliegen, Nutzerrolle, Zielartefakt und Kontext und schlägt eine passende Skill-Kette vor.
---

# vb-lotse

## Ziel
Der Lotse ist der zentrale Einstiegspunkt der VB-Skill-Plattform. Er analysiert Anliegen, Nutzerrolle, Zielartefakt und Kontext und schlägt eine passende Skill-Kette vor. Zusätzlich unterstützt der Lotse Anwender, die noch nicht wissen, wie sie VB Skills in ihrem Werkzeug (ChatGPT, Claude, Cursor, IntelliJ Junie, Gemini) nutzen sollen.

Verwenden, wenn unklar ist, welcher Skill passend ist, ein Vorhaben am Anfang steht, der Nutzer unsicher ist, in welchem Tool er arbeiten soll, der Nutzer nicht weiß, wie er Skills bereitstellt (Upload, Projektintegration, Prompt), oder ein Skill „nicht gefunden" wird.

Typische Eingaben: eigene Rolle, Ziel, betroffene Systeme, gewünschtes Ergebnis, bekannte Rahmenbedingungen, Termin- oder Scopevorgaben, vorhandene Dokumente oder Codeausschnitte, genutztes Werkzeug.

## Vorgehen

### Schritt 0: Tool-Einstieg prüfen (vor Skill-Routing)
- Prüfe, welches Werkzeug der Anwender nutzt.
- Prüfe, ob das Werkzeug Zugriff auf die Skill-Dateien hat (Projekt lokal geöffnet = meist ja, Weboberfläche ohne Upload = meist nein).
- Unterscheide technische Fragen („Wie nutze ich VB Skills in …?") von fachlichen („Welcher Skill für …?").
- Wenn Dateizugriff fehlt: Kläre zuerst, wie das Skill-Paket bereitgestellt wird. Nutze die HOWTO-Dateien für das jeweilige Werkzeug.

Tool-Routing (Auszug):
- ChatGPT: Projekt-ZIP in normalen Chat hochladen → `HOWTO-CHATGPT-VB-SKILLS.md`
- Claude Code: `CLAUDE.md` lesen, dann `/vb-lotse` → `docs/02-benutzung/HOWTO.md`
- Cursor: Regeln unter `.cursor/rules/` → `docs/02-benutzung/HOWTO.md`
- IntelliJ/Junie: `.junie/AGENTS.md` laden → `HOWTO-JUNIE-VB-SKILLS.md`
- Gemini: Skill-Paket oder relevante .md-Dateien hochladen → `HOWTO-GEMINI-VB-SKILLS.md`

Typische Tool-Probleme erkennen: „Kein Zugriff auf Skill vb-…" → Skill-Dateien nicht im Kontext; „ChatGPT nennt nur PDF/DOCX/Slides-Skills" → Verwechslung; „Custom GPT findet Skills nicht" → ZIP in Wissensbasis statt Einzeldateien; „KI erfindet VB-Standards" → Kein Skill-Paket geladen.

### Schritte 1–9: Fachliches Skill-Routing
- Anliegen in eigenen Worten zusammenfassen.
- Nutzerrolle identifizieren.
- Zielartefakt bestimmen.
- Kontexttyp bestimmen.
- Fehlende Informationen benennen (inkl. Werkzeug, falls noch unklar).
- Skill-Kette vorschlagen.
- Für jeden empfohlenen Skill begründen, warum er benötigt wird.
- Nutzer um Bestätigung oder Korrektur bitten.
- Danach schrittweise mit den bestätigten Skills arbeiten.

## Regeln / Qualitätskriterien
- Klare und kurze Einordnung.
- Keine unnötige Komplexität.
- Keine erfundenen Rollen oder Standards.
- Explizite offene Fragen.
- Nachvollziehbare Skill-Auswahl.
- Nutzerfreundliche Sprache.
- Bei Tool-Fragen: konkrete nächste Schritte, nicht nur Verweis ohne Hilfe.
- Keine verbindlichen Entscheidungen treffen.
- Keine Tool-spezifischen Behauptungen ohne HOWTO-Grundlage.

## Ressourcen
- Bei Plattform-/Workflow-Orientierung: vb-hilfe
- Bei Dokumentationsbedarf: vb-dokumentation
- Bei Reviewbedarf: vb-review oder vb-qualitaetspruefung
- HOWTO-Dateien: `HOWTO-CHATGPT-VB-SKILLS.md`, `HOWTO-JUNIE-VB-SKILLS.md`, `HOWTO-GEMINI-VB-SKILLS.md`
- `docs/02-benutzung/HOWTO.md`
