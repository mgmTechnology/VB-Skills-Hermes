# Gruppensteckbrief – Webservices & Strategie

## Einordnung in die Organisation

| Feld | Wert |
|---|---|
| Abteilung | IT-AE |
| Bereich | Lebensversicherungen |
| Gruppe | Webservices & Strategie |
| Zielordner skills/ | 02-technik/it-ae/lebensversicherungen/ws-strategy |

## Ziel und Zweck

Fach-, Diagnose-, Onboarding- und Releasewissen rund um BiPRO TAA Leben und die zugehörigen Webservices anwendbar machen.

## Kernaufgaben

- BiPRO-/TAA-Leben-Kontext analysieren
- Webservice-Störungen diagnostizieren
- technische Dokumentation erstellen und pflegen
- neue Entwickler einarbeiten
- Releases und Betas planen und finalisieren

## Abgrenzung (Nicht-Aufgaben)

- Bewertung von KI-Werkzeugen (gehört zu DevScouts)
- allgemeine Use-Case-Findung für KI (gehört zu DevScouts)

## Zielgruppen der Skills

Entwickler, vertretende Entwickler, neue Mitarbeitende, Gruppenleitung.

## Inhaltlich Verantwortliche

| Verantwortung | Person oder Rolle |
|---|---|
| Fachliche Verantwortung | Gruppenleitung Webservices & Strategie |
| Pflege der Referenzen | Skill-Entwickler / Release-Verantwortliche |
| Pflege der Skills | Skill-Entwickler |
| Pilotkoordination | Skill-Entwickler |
| Freigabeentscheidung | Gruppenleitung Webservices & Strategie |

## Verfügbare Skills der Gruppe

| Skill | Aufgabe | Status | Pilot? |
|---|---|---|---|
| `vb-bipro-analysis` | BiPRO-/TAA-Leben-Analyse (fachlich & technisch) | Entwurf | ja |
| `vb-webservice-diagnostics` | Fehler-/Trace-/Performanceanalyse | Entwurf | ja |
| `vb-release-planning` | Release- und Meilensteinplanung | Pilot | ja |
| `vb-release-finalization` | Technische Release-Durchführung & Checklisten | Entwurf | ja |
| `vb-webservice-documentation` | Erstellung technischer Dokumentation | Entwurf | nein |
| `vb-onboarding-webservices` | Einarbeitung neuer Entwickler (Wochenpläne) | Entwurf | nein |

## Einstieg in die Arbeit mit den Skills

Um mit einem Skill zu arbeiten, nutzen Sie die folgenden Einstiegsprompts. Starten Sie idealerweise immer mit dem `vb-lotse`, wenn Sie unsicher sind, welcher Skill am besten passt.

### 1. BiPRO-Analyse starten
**Prompt:**
```text
Nutze den Skill vb-bipro-analysis.

Analysiere die Operation [Name, z. B. getQuote] in Version [Version].

Ziel: [z. B. Verstehen / Änderung vorbereiten / Mapping prüfen]
Marke: [VBL / DOL / beide]

Kontext:
- [Ausschnitt aus XML-Request/Response oder XSD]
- [Betroffene Modellklasse oder Mappingregel, falls bekannt]

Bitte liefere:
1. Operationskarte (fachlicher Zweck, Journey),
2. Einstiegspunkte im Java-Code (Provider-Modell),
3. Technischer Datenfluss,
4. XSD- und VU-Erweiterungsanalyse,
5. Mapping- und Konverter-Check (Eingabe vs. Ausgabe),
6. Test- und Absicherungsstrategie (Roundtrip-Tests),
7. Risiken und offene Punkte.
```

### 2. Fehlerdiagnose starten
**Prompt:**
```text
Nutze den Skill vb-webservice-diagnostics.

Diagnostiziere folgenden Fehler in [Umgebung, z. B. PROD]: [Kurzbeschreibung].

Details:
- Symptom: [z. B. HTTP 500 / Wert fehlt / Performance]
- Trace-ID: [correlation_trace_id, falls vorhanden]
- Erwartet: [Soll-Verhalten]
- Beobachtet: [Ist-Verhalten]
- Zeitfenster: [Datum/Uhrzeit]

Bitte führe eine systematische Analyse durch:
1. Problem Statement & Klassifikation,
2. Rekonstruktion der Diagnosekette (Phasen-Befunde),
3. Root-Cause-Analyse (technisch & fachlich),
4. Sofortmaßnahmen & nachhaltige Korrekturvorschläge,
5. Plan für Regressionstests und Monitoring.
```

### 3. Release-Planung starten
**Prompt:**
```text
Nutze den Skill vb-release-planning.

Plane bitte einen Release für Webservices & Strategie.

Go-Live: Donnerstag, 25.06.2026

Rahmen:
- NRW-Feiertage als Nicht-Arbeitstage behandeln.
- NRW-Schulferien als Kapazitätsrisiko markieren.
- Die offizielle NRW-Ferienordnung ist maßgeblich.
- Brückentage zunächst nur als Risiko markieren.
- Bewegliche Ferientage sind nicht bekannt.
- Teamurlaube sind noch nicht geprüft.

Bitte liefere:
1. Ergebnisbewertung,
2. Meilensteintabelle,
3. kritische Phasen / Urlaubssperre,
4. Kalender- und Kapazitätsrisiken,
5. offene Punkte,
6. konkrete Rückfragen,
7. falls nötig alternative Go-Live-Termine.
```

### 4. Release-Finalisierung vorbereiten
**Prompt:**
```text
Nutze den Skill vb-release-finalization.

Bereite die Finalisierung für [Version, z. B. 2.4.7] vor.

Kontext:
- Typ: [Vollversion / Beta / Hotfix]
- Vorgängerversion: [z. B. 2.4.6]
- Betroffene Apps: [z. B. VBL Webservice, Rechenkern]
- Geplantes Deployment: [Datum]

Bitte erstelle:
1. Release-Steckbrief & Freigabestatus,
2. Checkliste für externe Projekte (SNAPSHOTs),
3. Vorbereitungsplan für Endpoints und Smoketests,
4. Schritt-für-Schritt-Plan für Rechenkern- und mono-elsa-Finalisierung,
5. Lieferschein-Entwürfe und Cluster-Anpassungen,
6. Monitoring-Plan für nach dem Livegang.
```

### 5. Dokumentation erstellen/aktualisieren
**Prompt:**
```text
Nutze den Skill vb-webservice-documentation.

Erstelle/Aktualisiere die Dokumentation für [Service/Operation] in Version [Version].

Schwerpunkt: [z. B. Betrieb / Entwicklung / Onboarding]
Basis: [Link zu Confluence / Code-Ausschnitt / Incident-Bericht]

Erwartete Struktur:
1. Service-Steckbrief (Marke, WSDL, Repositories),
2. Architektur-Übersicht (Phasenpipeline, DTOs),
3. Detaillierter Request-Ablauf (Mermaid oder Text),
4. Mapping-Tabelle (XML -> Modell -> XML),
5. Betriebs- und Diagnosehandbuch (Endpoints, Monitoring, Trace-IDs),
6. Bekannte Risiken und offene Punkte.
```

### 6. Onboarding planen
**Prompt:**
```text
Nutze den Skill vb-onboarding-webservices.

Erstelle einen Einarbeitungsplan für [Name/Rolle] für [Dauer, z. B. 4 Wochen].

Profil:
- Java/Maven: [z. B. sehr gut]
- XML/SOAP/BiPRO: [z. B. Grundkenntnisse]
- Versicherung/LV: [z. B. neu]

Bitte liefere:
1. Kompetenz-Einschätzung und Zielprofil,
2. Strukturierter Wochenplan (Lernziele & Aufgaben),
3. Fokus-Themen (Provider-Modell, Phasen, Mapping),
4. Konkrete praktische Übungsaufgaben am Code,
5. Lernkontrollen und Meilensteine.
```
