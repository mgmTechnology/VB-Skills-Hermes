---
name: vb-meeting-analyzer
description: Analysiert Meeting-Transkripte auf Kommunikationsmuster, Sprechdynamik, Fuhrungsverhalten und Entscheidungsfindung.
---

# vb-meeting-analyzer

## Ziel
Methoden-Skill zur Analyse von Meeting-Transkripten und Kommunikationsmustern. Wandelt Transkripte in evidenzbasiertes Feedback zu Sprechdynamik, Konfliktmustern, Fullwort-Nutzung, Fragequalitat, Moderation und Sentiment um. Unterstutzt Formate: .txt, .md, .vtt, .srt, .docx, .json.

## Vorgehen

### 1. Aufnahme und Inventur
- Scanne das Zielverzeichnis nach Transkript-Dateien. Extrahiere Meeting-Datum, Sprecher-Labels, Nutzeridentitat.
- Erstelle eine Inventurtabelle (Dateiname, Datum, Dauer, Teilnehmer, Wortzahl) zur Bestatigung vor tiefergehender Analyse.

### 2. Transkripte normalisieren
- Normalisiere in gemeinsame Struktur: {speaker, timestamp_sec, text}[]
- Behandle VTT/SRT (Cue-Zeitstempel + Text), Klartext (Sprecher-Prafixe), Markdown, DOCX, JSON (Otter/Fireflies Export).

### 3. Analysemodule ausfuhren

#### Sprechdynamik
- Berechne pro Sprecher: Wortzahl/Prozent, Beitragsanzahl, durchschnittliche Beitragslange, langster Monolog.
- Erkenne Unterbrechungen. Red Flags: Nutzer >60% (dominierend), <15% (unbeteiligt), jemand spricht nie.

#### Konflikt und Direktheit
- Scanne nach Weichmachern (vielleicht, irgendwie), Erlaubnis-Einholung, Ausweichen, Abschwachung vor Widerspruch.
- Markiere Konfliktvermeidung mit Schweregrad (low/medium/high) und Umformulierungsvorschlag.

#### Fullworter und sprachliche Gewohnheiten
- Zahle ah, ahm, halt, quasi, eigentlich. Berechne Rate pro 100 Worter.
- Nur als Problem markieren wenn Rate >3/100 Worter.

#### Fragequalitat und Zuhoren
- Klassifiziere Fragen: geschlossen, suggestiv, offen, klarend, aufbauend.
- Indikatoren fur gutes/schlechtes Zuhoren bewerten.

#### Moderation und Entscheidungsfindung
- Bewerte Agendaeinhaltung, Zeitmanagement, Inklusion, Entscheidungsklarheit, Aufgaben-Zuweisung.

#### Sentiment und Energie
- Verfolge emotionalen Bogen: positiv (Zustimmung, Humor), negativ (Frustration, Sarkasmus), neutral/flach.

### 4. Bericht ausgeben
- Strukturierter Bericht mit: Top-3-Erkenntnissen, detaillierter Analyse, Starken, Entwicklungspotenzialen, Vergleich zum Vorzeitraum.

## Regeln / Qualitatskriterien
- Ohne Sprecher-Labels: Nutzer warnen, textbasierte Analyse durchfuhren, sprecherbezogene Metriken uberspringen.
- Kurze Meetings (<500 Worter): analysieren aber auf eingeschrankte Reprasentativitat hinweisen.
- Mindestens 3 Meetings fur trendbasiertes Coaching. Sprechanteile nach Meeting-Typ und Rolle gewichten.
- Vollstandigen Kontext liefern (Zitate mit 2 Beitragen davor/danach).
- Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ressourcen
- Senior-PM: vb-senior-pm
- Scrum-Master: vb-scrum-master
