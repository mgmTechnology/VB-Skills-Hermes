# vb-lotse

## Zweck

Der Lotse ist der zentrale Einstiegspunkt der VB-Skill-Plattform. Er analysiert Anliegen, Nutzerrolle, Zielartefakt und Kontext und schlägt eine passende Skill-Kette vor.

Zusätzlich unterstützt der Lotse Anwender, die **noch nicht wissen, wie sie VB Skills in ihrem Werkzeug** (ChatGPT, Claude, Cursor, IntelliJ Junie, Gemini) nutzen sollen.

## Wann verwenden?

Immer verwenden, wenn:

- unklar ist, welcher Skill passend ist,
- ein Vorhaben am Anfang steht,
- der Nutzer unsicher ist, **in welchem Tool** er arbeiten soll,
- der Nutzer nicht weiß, **wie er Skills bereitstellt** (Upload, Projektintegration, Prompt),
- ein Skill „nicht gefunden“ wird – oft fehlt dann der Dateizugriff, nicht der Skill im Repository.

## Typische Eingaben

- eigene Rolle
- Ziel
- betroffene Systeme
- gewünschtes Ergebnis
- bekannte Rahmenbedingungen
- Termin- oder Scopevorgaben
- vorhandene Dokumente oder Codeausschnitte
- **genutztes Werkzeug** (ChatGPT, Claude Code, Cursor, Junie, Gemini, unsicher)

## Vorgehensmodell

### Schritt 0: Tool-Einstieg prüfen (vor Skill-Routing)

Bevor die fachliche Skill-Kette vorgeschlagen wird, prüfen:

1. **Welches Werkzeug nutzt der Anwender?**
2. **Hat das Werkzeug Zugriff auf die Skill-Dateien?**
   - Projekt lokal geöffnet (Claude Code, Cursor, Junie) → meist ja
   - Weboberfläche ohne Upload (ChatGPT, Gemini) → meist nein
3. **Ist die Frage fachlich oder technisch?**
   - technisch: „Wie nutze ich VB Skills in …?“ → Tool-Anleitung liefern (siehe unten)
   - fachlich: „Welcher Skill für …?“ → ab Schritt 1 fortfahren

Wenn Dateizugriff fehlt, **nicht** mit fachlicher Skill-Arbeit beginnen. Zuerst klären, wie das Skill-Paket bereitgestellt wird.

#### Tool-Routing

| Werkzeug | Dateizugriff | Erste Hilfe | Detailanleitung |
| :--- | :--- | :--- | :--- |
| **ChatGPT** | Nur via Upload im Chat oder kuratierte Dateien in Custom GPT | Projekt-ZIP in **normalen Chat** hochladen (nicht Custom-GPT-Wissensbasis) | `HOWTO-CHATGPT-VB-SKILLS.md` |
| **Claude Code** | Direkt im Repository | `CLAUDE.md` lesen, dann `/vb-lotse` oder Skill-Pfad | `docs/02-benutzung/HOWTO.md` Abschnitt 7.1 |
| **Cursor** | Direkt im Repository | Regeln unter `.cursor/rules/` | `docs/02-benutzung/HOWTO.md` Abschnitt 7.2 |
| **IntelliJ / Junie** | Direkt im Projekt | `.junie/AGENTS.md` laden | `HOWTO-JUNIE-VB-SKILLS.md` |
| **Gemini** | Nur via Upload / Kontext | Skill-Paket oder relevante `.md`-Dateien hochladen | `HOWTO-GEMINI-VB-SKILLS.md` (Entwurf) |
| **Unsicher** | – | Kurz die Optionen erklären und nach Werkzeug fragen | `docs/02-benutzung/HOWTO.md` |

#### Typische Tool-Probleme erkennen

| Symptom | Wahrscheinliche Ursache | Lotse-Antwort |
| :--- | :--- | :--- |
| „Kein Zugriff auf Skill vb-…“ | Skill-Dateien nicht im Kontext | Upload-/Setup-Anleitung für das Werkzeug |
| ChatGPT nennt nur PDF/DOCX/Slides-Skills | Verwechslung ChatGPT-Skills vs. VB Skills | `HOWTO-CHATGPT-VB-SKILLS.md` Abschnitt 3 |
| Custom GPT findet Skills nicht | ZIP in Wissensbasis statt Einzeldateien | `HOWTO-CHATGPT-VB-SKILLS.md` Abschnitt 6 |
| Junie ignoriert VB-Vorgaben | `.junie/AGENTS.md` nicht geladen | `HOWTO-JUNIE-VB-SKILLS.md` Abschnitt 13 |
| KI erfindet VB-Standards | Kein Skill-Paket geladen | Dateizugriff herstellen, dann erneut mit vb-lotse starten |

#### Kurz-Einstieg pro Werkzeug (wenn HOWTO nicht geladen ist)

**ChatGPT:** ZIP des Projekts in den Chat hochladen, dann Startprompt aus `HOWTO-CHATGPT-VB-SKILLS.md`.

**Claude Code:** `Lies CLAUDE.md. Starte mit skills/00-prozess/vb-lotse/SKILL.md.`

**Cursor:** `Nutze die VB Skills. Starte mit vb-lotse.`

**Junie:** `Nutze die VB Skills aus diesem Projekt. Beginne mit vb-lotse.`

**Gemini:** Relevante Skill-Dateien oder ZIP hochladen, dann Startprompt aus `HOWTO-GEMINI-VB-SKILLS.md`.

Wenn die HOWTO-Datei im Kontext verfügbar ist, die **detaillierte Anleitung** bevorzugen – nicht paraphrasieren oder Regeln erfinden.

### Schritte 1–9: Fachliches Skill-Routing

1. Anliegen in eigenen Worten zusammenfassen.
2. Nutzerrolle identifizieren.
3. Zielartefakt bestimmen.
4. Kontexttyp bestimmen.
5. Fehlende Informationen benennen (inkl. Werkzeug, falls noch unklar).
6. Skill-Kette vorschlagen.
7. Für jeden empfohlenen Skill begründen, warum er benötigt wird.
8. Nutzer um Bestätigung oder Korrektur bitten.
9. Danach schrittweise mit den bestätigten Skills arbeiten.

## Typische Ausgaben

- **Tool-Einstieg:** gewähltes Werkzeug, Setup-Schritte, Verweis auf HOWTO
- Kontextzusammenfassung
- empfohlene Skill-Kette
- Begründung
- offene Fragen
- vorgeschlagene nächste Schritte
- erwartete Ergebnisartefakte

## Qualitätskriterien

- klare und kurze Einordnung
- keine unnötige Komplexität
- keine erfundenen Rollen oder Standards
- explizite offene Fragen
- nachvollziehbare Skill-Auswahl
- nutzerfreundliche Sprache
- bei Tool-Fragen: konkrete nächste Schritte, nicht nur Verweis ohne Hilfe

## Grenzen / Nicht-Aufgaben

- keine verbindlichen Entscheidungen treffen
- keine nicht belegten Standards erfinden
- fehlende Informationen als offene Fragen markieren
- keine Tool-spezifischen Behauptungen ohne HOWTO-Grundlage

## Übergaben an andere Skills

- bei unklarem Kontext: vb-lotse
- bei Plattform-/Workflow-Orientierung: vb-hilfe
- bei Dokumentationsbedarf: vb-dokumentation
- bei Reviewbedarf: vb-review oder vb-qualitaetspruefung

## Beispielprompts

**Fachlicher Einstieg:**

```text
Bitte unterstütze mich mit diesem Skill und frage zuerst die fehlenden Informationen ab.
```

**Tool-Unsicherheit:**

```text
Ich weiß nicht, wie ich VB Skills in ChatGPT nutze. Bitte hilf mir beim Einstieg.
```

**Skill nicht gefunden:**

```text
ChatGPT sagt, es hat keinen Zugriff auf vb-release-planning. Was soll ich tun?
```

**Kombination Tool + fachlich:**

```text
Ich nutze Gemini. Ich möchte einen Release-Plan mit vb-release-planning erstellen.
Bitte erkläre zuerst den Einstieg, dann den passenden Skill.
```
