---
name: "vb-meeting-analyzer"
description: "VB-adaptierter Skill. Ursprung: skills/project-management/meeting-analyzer/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-meeting-analyzer

## VB-Einordnung

Methoden-Skill zur Analyse von Meeting-Transkripten und Kommunikationsmustern.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ursprüngliche Detailanweisung (Referenz)

---

# Meeting-Insights-Analyzer

Wandelt Meeting-Transkripte in konkretes, evidenzbasiertes Feedback zu Kommunikationsmustern, Führungsverhalten und zwischenmenschlicher Dynamik um.

## Kern-Workflow

### 1. Aufnahme & Inventur

Scannt das Zielverzeichnis nach Transkript-Dateien (`.txt`, `.md`, `.vtt`, `.srt`, `.docx`, `.json`).

Für jede Datei:
- Extrahiert das Meeting-Datum aus dem Dateinamen oder Inhalt (erwartet `JJJJ-MM-TT` Präfix oder eingebettete Zeitstempel).
- Identifiziert Sprecher-Labels — sucht nach Mustern wie `Sprecher 1:`, `[John]:`, `John Smith 00:14:32`, VTT/SRT Cue-Formatierung.
- Erkennt die Identität des Nutzers: fragt bei Unklarheiten nach, leitet sie andernfalls vom häufigsten Sprecher oder Dateinamen-Hinweisen ab.
- Protokolliert: Dateiname, Datum, Dauer (aus Zeitstempeln), Teilnehmerzahl, Wortzahl.

Gibt eine kurze Inventurtabelle aus, damit der Nutzer den Umfang bestätigt, bevor die tiefergehende Analyse beginnt.

### 2. Transkripte normalisieren

Verschiedene Werkzeuge produzieren sehr unterschiedliche Formate. Alles wird vor der Analyse in eine gemeinsame interne Struktur normalisiert:

```
{ speaker: string, timestamp_sec: number | null, text: string }[]
```

Umgang mit Formaten:
- **VTT/SRT**: Parst Cue-Zeitstempel + Text. Sprecher-Labels können inline (`<v Sprecher>`) oder als Präfix vorhanden sein.
- **Klartext**: Sucht nach `Name:` oder `[Name]` Präfixen pro Zeile. Wenn keine Sprecher-Labels vorhanden sind, den Nutzer warnen, dass die sprecherbezogene Analyse eingeschränkt ist.
- **Markdown**: Entfernt Formatierungen und behandelt es dann wie Klartext.
- **DOCX**: Extrahiert den Textinhalt und behandelt ihn dann wie Klartext.
- **JSON**: Erwartet ein Array von Objekten mit `speaker`/`text` Feldern (üblicher Otter/Fireflies Export).

Falls Zeitstempel fehlen, wird die Analyse eingeschränkt — zeitabhängige Metriken (Sprechgeschwindigkeit, Pausenanalyse) werden übersprungen, aber die textbasierte Analyse wird dennoch durchgeführt.

### 3. Analysieren

Führt alle anwendbaren Analysemodule unten aus. Jedes Modul ist unabhängig — überspringt Module, die nicht anwendbar sind (z.B. Sprechanteile überspringen, wenn keine Sprecher-Labels vorhanden sind).

---

#### Modul: Sprechdynamik

Berechnet pro Sprecher:
- **Wortzahl & Prozentsatz** der gesamten Meeting-Wörter.
- **Anzahl der Sprechbeiträge** — wie oft jede Person das Wort hatte.
- **Durchschnittliche Beitragslänge** — Wörter pro ununterbrochenem Sprechbeitrag.
- **Längster Monolog** — markiert Beiträge, die 60 Sekunden oder 200 Wörter überschreiten.
- **Erkennung von Unterbrechungen** — ein Beitrag, der innerhalb von 2 Sekunden nach dem letzten Zeitstempel des vorherigen Sprechers beginnt, oder Unterbrechungen mitten im Satz.

Erstellt eine Zusammenfassung pro Meeting und einen Durchschnitt über alle Meetings, falls mehrere Transkripte vorliegen.

Kritische Anzeichen (Red Flags):
- Nutzer spricht > 60% in einem 1:n Meeting (dominierend).
- Nutzer spricht < 15% in einem Meeting, das er moderiert (unbeteiligt oder delegiert zu stark).
- Ein Teilnehmer sagt nie etwas (ausgeschlossene Stimme).
- Unterbrechungsverhältnis > 2:1 (Nutzer unterbricht andere doppelt so oft, wie er selbst unterbrochen wird).

---

#### Modul: Konflikt & Direktheit

Scannt die Sprache des Nutzers nach Weichmachern (Hedging) und Anzeichen für Ausweichverhalten:

**Weichmacher/Absicherung** (Bewertung pro Instanz, Aggregation pro Meeting):
- Relativierungen: "vielleicht", "irgendwie", "gewissermaßen", "ich schätze", "potenziell", "wohl".
- Einholung von Erlaubnis: "wenn das okay ist", "wäre es in Ordnung, wenn", "ich weiß nicht, ob das richtig ist, aber".
- Ausweichen: "was auch immer ihr denkt", "liegt bei euch", "ich bin da flexibel".
- Abschwächung vor Widerspruch: "ich möchte nicht widersprechen, aber", "das ist vielleicht eine dumme Frage".

**Muster der Konfliktvermeidung** (erfordert mehr Kontext, Markierung mit Konfidenzniveau):
- Themenwechsel nach Spannungen (Sprecher A nennt ein Problem → Nutzer wechselt zu Logistikthemen).
- Zustimmung ohne Verbindlichkeit: "ja total", gefolgt von keiner Aktion oder Nachverfolgung.
- Herunterspielen der Sorgen anderer: "es ist wahrscheinlich keine so große Sache".
- Fehlendes Feedback in 1:1 Gesprächen, in denen Leistungsthemen zu erwarten wären.

Für jede markierte Instanz wird extrahiert:
- Das vollständige Zitat (mit Kontext — 2 Beiträge davor und danach).
- Ein Schweregrad-Tag: `low` (einzelnes Absicherungswort), `medium` (Muster in einem Austausch), `high` (notwendiges Gespräch klar vermieden).
- Ein Umformulierungsvorschlag: wie eine direktere Version klingen würde.

---

#### Modul: Füllwörter & sprachliche Gewohnheiten

Zählt Vorkommen von: "äh", "ähm", "halt", "quasi", "eigentlich", "sozusagen", "genau", "richtig?", "so ja", "ich meine".

Berichtet:
- Gesamtzahl pro Meeting.
- Rate pro 100 gesprochene Wörter (normalisiert über die Meeting-Länge).
- Aufschlüsselung nach Füllwort-Typ.
- Kontextuelle Spitzen — nehmen Füllwörter in spezifischen Situationen zu? (z.B. bei Antworten an Senior Stakeholder, bei negativem Feedback, bei unvorbereiteten Fragen).

Dies wird nur als Problem markiert, wenn die Rate ~3 pro 100 Wörter überschreitet. Darunter gilt es als normale Sprache.

---

#### Modul: Qualität der Fragen & Zuhören

Klassifiziert die Fragen des Nutzers:
- **Geschlossen** (ja/nein): "Hast du den Bericht fertiggestellt?"
- **Suggestiv** (Antwort eingebettet): "Glaubst du nicht auch, wir sollten früher releasen?"
- **Offen & aufrichtig**: "Was blockiert dich hierbei?"
- **Klärend** (bezieht sich auf Vorredner): "Als du X sagtest, meintest du damit Y?"
- **Aufbauend** (erweitert die Idee eines anderen): "Das ist interessant — was wäre, wenn wir auch Z?"

Indikatoren für gutes Zuhören:
- Klärende und aufbauende Fragen (zeigt aktive Verarbeitung).
- Paraphrasieren: "Was ich also höre, ist..."
- Bezugnahme auf einen Punkt, den jemand früher im Meeting gemacht hat.
- Einbeziehung ruhigerer Teilnehmer durch gezielte Nachfragen.

Indikatoren für schlechtes Zuhören:
- Eine Frage stellen, die bereits beantwortet wurde.
- Den eigenen Punkt wiederholen, ohne auf die Antwort einzugehen.
- Auf eine Frage mit einem völlig anderen Thema antworten.

Berichtet das Verhältnis von offenen/klärenden/aufbauenden zu geschlossenen/suggestiven Fragen.

---

#### Modul: Moderation & Entscheidungsfindung

Wird nur angewendet, wenn der Nutzer der Organisator oder Moderator des Meetings ist.

Bewertet:
- **Einhaltung der Agenda**: Folgte das Meeting einer Struktur oder driftete es ab?
- **Zeitmanagement**: Wie lange dauerte jedes Thema im Vergleich zur Erwartung?
- **Inklusion**: Hat der Moderator aktiv ruhige Teilnehmer einbezogen?
- **Klarheit der Entscheidung**: Wurden Entscheidungen explizit formuliert? ("Wir entscheiden uns also für Option B — Sarah übernimmt die Nachverfolgung bis Freitag.")
- **Aufgaben (Action Items)**: Wurden sie mit Verantwortlichen und Fristen zugewiesen oder vage gelassen?
- **Themenspeicher (Parking Lot)**: Wurden Off-Topic-Punkte anerkannt und vertagt oder haben sie das Meeting gestört?

---

#### Modul: Sentiment & Energie

Verfolgt den emotionalen Bogen der Sprache des Nutzers während des Meetings:
- **Positive Marker**: begeisterte Zustimmung, Ermutigung, Humor, Lob.
- **Negative Marker**: Frustration, Herablassung, Sarkasmus, knappe Antworten.
- **Neutral/flach**: energiearme Antworten, einsilbige Antworten.

Markiert Energieabfälle — Momente, in denen das Engagement des Nutzers sichtlich abnimmt (kürzere Beiträge, weniger gehaltvolle Antworten). Diese korrelieren oft mit Unbehagen, Langeweile oder Ausweichverhalten.

---

### 4. Ausgabe des Berichts

Strukturiert die finale Ausgabe als einen zusammenhängenden Bericht. Nutzt dieses Gerüst — lasst Abschnitte weg, in denen die Datenlage unzureichend war:

```markdown
# Meeting-Insights-Bericht

**Zeitraum**: [frühestes Datum] – [spätestes Datum]
**Analysierte Meetings**: [Anzahl]
**Gesamtzahl Wörter in Transkripten**: [Anzahl]
**Dein Sprechanteil (Schnitt)**: [X%]

---

## Top 3 Erkenntnisse

[Nach Relevanz geordnet. Jede Erkenntnis erhält 2-3 Sätze + ein konkretes Beispiel mit direktem Zitat und Zeitstempel.]

## Detaillierte Analyse

### Sprechdynamik
[Statistik-Tabelle + narrative Interpretation + markierte Red Flags]

### Direktheit & Konfliktmuster
[Markierte Instanzen gruppiert nach Mustertyp, mit Zitaten und Umformulierungen]

### Sprachliche Gewohnheiten
[Füllwort-Statistiken, kontextuelle Spitzen, nur wenn Rate > 3/100 Wörter]

### Zuhören & Fragen
[Aufschlüsselung der Fragetypen, Indikatoren für Zuhören, spezifische Beispiele]

### Moderation
[Nur falls zutreffend — Agenda, Entscheidungen, Aufgaben]

### Energie & Sentiment
[Zusammenfassung des Bogens, markierte Abfälle]

## Stärken
[3 spezifische Dinge, die der Nutzer gut macht, mit Belegen]

## Entwicklungspotenziale
[3 nach Auswirkung geordnete Punkte, jeweils mit: was zu ändern ist, warum es wichtig ist, eine konkrete Aktion für "nächstes Mal ausprobieren"]

## Vergleich zum vorherigen Zeitraum
[Nur falls eine frühere Analyse existiert — Veränderungen bei den Kernmetriken]
```

### 5. Follow-Up Optionen

Bietet nach der Übergabe des Berichts an:
- Tiefes Eintauchen in ein spezifisches Meeting oder Muster.
- Ein 1-seitiges "Kommunikations-Cheat-Sheet" mit den Top 3 Gewohnheiten, die der Nutzer ändern sollte.
- Einrichtung eines Trackings — Speichern der aktuellen Metriken als Baseline für zukünftige Vergleiche.
- Export als Markdown oder strukturiertes JSON für die Verwendung in Mitarbeitergesprächen.

---

## Sonderfälle

- **Keine Sprecher-Labels**: Den Nutzer vorab warnen. Textbasierte Analyse durchführen (Füllwörter, Fragetypen im gesamten Transkript), aber sprecherbezogene Metriken überspringen. Empfehlung: Erneuter Export mit aktivierter Sprechererkennung (Diarization).
- **Sehr kurze Meetings** (< 5 Minuten oder < 500 Wörter): Analysieren, aber darauf hinweisen, dass Muster aus kurzen Meetings möglicherweise nicht repräsentativ sind.
- **Nicht-englische Transkripte**: Die Wörterbücher für Füllwörter und Weichmacher sind auf Englisch und Deutsch optimiert. Für andere Sprachen die Einschränkung vermerken und auf strukturelle Analysen konzentrieren (Sprechanteile, Sprecherwechsel, Fragenanzahl).
- **Einzelnes Meeting vs. Korpus**: Wenn nur ein Transkript vorliegt, Trend- und Vergleichsaussagen weglassen. Erkenntnisse nur auf dieses Meeting beziehen.
- **Nutzer nicht identifiziert**: Falls nach dem Scan nicht bestimmt werden kann, welcher Sprecher der Nutzer ist, vor dem Fortfahren nachfragen. Nicht raten.

## Tipps zur Transkript-Quelle

Diesen Abschnitt nur ausgeben, wenn der Nutzer unsicher ist, wie er Transkripte erhält:

- **Zoom**: Einstellungen → Aufzeichnung → "Audio-Transkript" aktivieren. `.vtt` von Cloud-Aufzeichnungen herunterladen.
- **Google Meet**: Automatische Transkription speichert in Google Docs im Drive-Ordner des Kalender-Events.
- **Granola**: Exportiert nach Markdown. Beste Sprecher-Label-Qualität bei Consumer-Tools.
- **Otter.ai**: Export als `.txt` oder `.json` aus dem Web-Dashboard.
- **Fireflies.ai**: Export als `.docx` or `.json` — beides funktioniert.
- **Microsoft Teams**: Transcripts appear in the meeting chat. Download as `.vtt`.

Empfehlung: `JJJJ-MM-TT - Meeting Name.ext` Namenskonvention für eine einfache chronologische Analyse.

---

## Anti-Muster

| Anti-Muster | Warum es scheitert | Besserer Ansatz |
|---|---|---|
| Analyse ohne Sprecher-Labels | Personenbezogene Metriken unmöglich — Ergebnisse sind generische Wortwolken | Nutzer bitten, mit aktivierter Sprecheridentifikation erneut zu exportieren |
| Alle Module bei einem 5-min-Standup | Übertrieben — Füllwort- und Konfliktanalyse benötigen 20+ min Meetings | Meeting-Länge automatisch erkennen und irrelevante Module überspringen |
| Reine Metriken ohne Kontext | "Du hast 47-mal 'äh' gesagt" ist entmutigend ohne Benchmarks | Immer mit Normwerten vergleichen und den Verlauf über die Zeit zeigen |
| Analyse eines einzelnen Meetings isoliert | Ein Meeting ist eine Momentaufnahme, kein Muster — Schlussfolgerungen unzuverlässig | Mindestens 3 Meetings für ein trendbasiertes Coaching anfordern |
| Gleichheit der Sprechzeit als Ziel | Ein Moderator SOLLTE weniger reden; ein Präsentator SOLLTE mehr reden | Sprechanteile nach Meeting-Typ und Rolle gewichten |
| Jedes Absicherungswort negativ werten | "Ich denke" und "vielleicht" sind im Brainstorming angemessen | Zwischen Entscheidungs-Meetings (Absicherungen schlecht) und Ideenfindung unterscheiden |

---

## Verwandte Skills

| Skill | Beziehung |
|-------|-------------|
| `project-management/senior-pm` | Breiterer PM-Fokus — Projektplanung, Risiken, Stakeholder |
| `project-management/scrum-master` | Agile Zeremonien — ergänzt meeting-analyzer für Retro-Qualität |
| `project-management/confluence-expert` | Speichern der Meeting-Analyse-Ergebnisse als Confluence-Seiten |
| `c-level-advisor/executive-mentor` | Coaching für Management-Kommunikation — ergänzende Perspektive |

