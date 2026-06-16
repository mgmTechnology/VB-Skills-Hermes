# vb-webservice-diagnostics

## Zweck
Systematische Diagnose von Fehlern, Laufzeitproblemen und Produktionsauffälligkeiten in VBL/DOL BiPRO-Webservices. Der Skill führt von Symptom über Operation, Request, Trace, Phasenpipeline, Mapping, externe Services und Reportingdaten zu Root Cause und Maßnahmenplan.

## Wann verwenden
- Produktions- oder Testfehler in VBL/DOL Webservices.
- Performanceproblem bei `getQuote`, `getOffer`, `getOrder`, `setOrder` oder `setOrderQualified`.
- Schema-/Validierungsfehler im XML.
- Wert fehlt im internen Modell oder in der Response.
- Fehler im Security-Kontext, IAM, Rechenkern, E-Antrag oder Dokumentenfluss.
- Analyse anhand von `correlation_trace_id`, Logs, Kibana/APM, Grafana oder Reporting-Tabelle.

## Wann NICHT verwenden
- Reine Fachklärung ohne technisches Fehlerbild.
- Release-Finalisierung; dafür `vb-release-finalization` verwenden.
- KI-Tool-Bewertung; dafür `vb-devscouts-evaluation` verwenden.


## Verbindliche Referenzen
Nutze bei Bedarf diese lokalen Referenzen im Repository:

- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Gesamtdokumentation_v3.html`
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Einarbeitungsplan.html`
- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf`
- `docs/referenzen/Webservices-Strategie/REFERENZEN.md`

Regel: Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`. Erfinde keine VB-Standards.


## Benötigte Eingaben
- Fehlerbeschreibung und erwartetes Verhalten.
- Umgebung: DEV, QA, Integration, PROD.
- Operation und Version, sofern bekannt.
- Request/Response oder Ausschnitt.
- Logauszug, Stacktrace oder Trace-ID.
- Zeitfenster und Consumer/Partner, falls vorhanden.

## Vorgehen

### 1. Problem Statement formulieren
Erzeuge zuerst eine präzise Fehlerbeschreibung:

```text
Bei [Operation] in [Umgebung] tritt [Symptom] auf.
Betroffen sind [Consumer/Produkt/Fall].
Erwartet wäre [Soll-Verhalten].
Beobachtet wurde [Ist-Verhalten].
```

### 2. Fehlerklasse bestimmen
Klassifiziere das Problem:

| Klasse | Typische Hinweise |
|---|---|
| Endpoint / Routing | falsche URL, falsche Version, falscher Cluster |
| SOAP / Schema | Namespace, `xsi:type`, `xsd:sequence`, Encoding |
| Security | SCT, IAM, STS, Token, Partnerauthentifizierung |
| Mapping Input | Wert kommt nicht im Modell an |
| Konverter | Code/Enum/Datentyp passt nicht |
| Berechnung | Rechenkern, Tarif, AVB/ELSA-Daten |
| Mapping Output | Wert fehlt in Response |
| Dokument / E-Antrag | PDF, `setOrder`, `setOrderQualified`, Dateiabruf |
| Performance | IAM, Rechenkern, Export, Reporting, DB |

### 3. Operation und Version verifizieren
Prüfe:

- `bipro_operation`, falls in Reportingdaten vorhanden.
- Service-URL und Version, z. B. `2026-06`, `VBLService_2.4.6.1.12`.
- `/wsversion`, sofern verfügbar.
- Cluster/Branch: VBL/DOL, `a`/`b`, Current/Preversion.

### 4. Request-Weg rekonstruieren
Baue eine Diagnosekette:

```text
Client
 -> SOAP Endpoint
 -> Provider.invoke
 -> Vorverarbeitung / Validierung
 -> AuthenticationPhase / SecurityContext
 -> EingabeUnmarshallen
 -> Import / Mapping
 -> Berechnung / Rechenkern
 -> ExportJava / ExportXML
 -> SOAPVorbereitung / LoggingXML
 -> Reporting DB
```

### 5. Trace und Logs korrelieren
Nutze, falls vorhanden:

- `correlation_trace_id`
- Zeitstempel
- `bipro_consumerid`
- `bipro_operation`
- Produkt/Tarif
- `duration` und `time_calculation`
- Phase / Span-Namen, insbesondere `*.durchlaufe`

Frage pro Phase:

- tritt der Fehler vor oder nach der Validierung auf?
- ist der IAM/Security-Abschnitt auffällig?
- ist der Rechenkern-Aufruf langsam oder fehlerhaft?
- tritt der Fehler erst bei Export/Response auf?
- wird ein Reporting-Eintrag geschrieben?

### 6. Root-Cause-Analyse
Verwende nur so viel Methodik wie nötig. Standard:

- 5-Why für technische Ursache.
- Ishikawa nur bei unklarer Mehrursachenlage.
- Pareto nur bei mehreren wiederkehrenden Fehlerbildern.

Struktur:

```markdown
Symptom:
Direkte Ursache:
Technische Root Cause:
Fachliche Root Cause, falls relevant:
Beleg:
Nicht belegte Annahmen:
```

### 7. Maßnahmen definieren
Trenne:

| Maßnahme | Ziel |
|---|---|
| Sofortmaßnahme | Betrieb stabilisieren |
| Korrektur | Fehlerursache beseitigen |
| Regressionstest | Wiederauftreten verhindern |
| Dokumentationsupdate | Wissen sichern |
| Monitoring-Anpassung | frühere Erkennung ermöglichen |

## Output-Format

```markdown
# Webservice-Diagnose

## 1. Problem Statement

## 2. Klassifikation

## 3. Betroffene Umgebung / Operation / Version

## 4. Diagnosekette

## 5. Befunde je Phase

## 6. Root Cause

## 7. Maßnahmenplan

## 8. Regressionstest / Monitoring

## 9. Offene Punkte
```

## Qualitätskriterien
- Ursache und Symptom werden getrennt.
- Diagnose ist anhand Trace/Log/Request reproduzierbar.
- Jede Empfehlung enthält Begründung und Prüfschritt.
- Kein Wechsel auf Mappinganalyse vor bestandener Schemavalidierung.
- Security, Rechenkern und Reporting werden als externe Abhängigkeiten berücksichtigt.

## Typische Fehler
- Nur Stacktrace lesen und Request/Operation ignorieren.
- `getQuote`/`getOffer` nicht über Provider-/Phasenmodell denken.
- Werteverlust fälschlich als Berechnungsfehler deuten, obwohl Eingabe-Mapping fehlt.
- Laufzeitproblem im Webservice suchen, obwohl IAM oder Rechenkern dominiert.
