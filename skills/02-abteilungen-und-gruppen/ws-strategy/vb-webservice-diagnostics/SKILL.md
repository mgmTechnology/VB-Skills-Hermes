---
name: vb-webservice-diagnostics
description: Systematische Diagnose von Fehlern, Laufzeitproblemen und Produktionsauffälligkeiten in VBL/DOL BiPRO-Webservices.
---

# VB Webservice Diagnostics

## Ziel

Systematische Diagnose von Fehlern, Laufzeitproblemen und Produktionsauffälligkeiten in VBL/DOL BiPRO-Webservices. Der Skill führt von Symptom über Operation, Request, Trace, Phasenpipeline, Mapping, externe Services und Reportingdaten zu Root Cause und Maßnahmenplan.

Verwenden bei:
- Produktions- oder Testfehler in VBL/DOL Webservices
- Performanceproblem bei `getQuote`, `getOffer`, `getOrder`, `setOrder` etc.
- Schema-/Validierungsfehler im XML
- Wert fehlt im internen Modell oder in der Response
- Fehler im Security-Kontext, IAM, Rechenkern, E-Antrag oder Dokumentenfluss
- Analyse anhand von `correlation_trace_id`, Logs, Kibana/APM, Grafana oder Reporting-Tabelle

NICHT verwenden bei:
- Reiner Fachklärung ohne technisches Fehlerbild
- Release-Finalisierung; dafür `vb-release-finalization` verwenden

## Vorgehen

### 1. Problem Statement formulieren
Erzeuge eine präzise Fehlerbeschreibung: Operation, Umgebung, Symptom, betroffene Consumer/Produkte, Soll- vs. Ist-Verhalten

### 2. Fehlerklasse bestimmen
Klassifiziere das Problem: Endpoint/Routing, SOAP/Schema, Security, Mapping Input, Konverter, Berechnung, Mapping Output, Dokument/E-Antrag, Performance

### 3. Operation und Version verifizieren
Prüfe `bipro_operation`, Service-URL/Version, `/wsversion`, Cluster/Branch (VBL/DOL, a/b, Current/Preversion)

### 4. Request-Weg rekonstruieren
Baue Diagnosekette: Client → SOAP Endpoint → Provider.invoke → Validierung → Auth/Security → EingabeUnmarshallen → Import/Mapping → Berechnung/Rechenkern → Export → SOAPVorbereitung → Reporting

### 5. Trace und Logs korrelieren
Nutze `correlation_trace_id`, Zeitstempel, `bipro_consumerid`, `bipro_operation`, Produkt/Tarif, `duration`, Phasen/Spans. Frage pro Phase: Tritt der Fehler vor/nach Validierung, beim Rechenkern, bei Export/Response auf?

### 6. Root-Cause-Analyse
5-Why für technische Ursache, Ishikawa nur bei unklarer Mehrursachenlage, Pareto nur bei mehreren wiederkehrenden Fehlerbildern. Dokumentiere: Symptom, direkte Ursache, technische Root Cause, fachliche Root Cause, Beleg, nicht belegte Annahmen

### 7. Maßnahmen definieren
Trenne: Sofortmaßnahme (Betrieb stabilisieren), Korrektur (Fehlerursache beseitigen), Regressionstest, Dokumentationsupdate, Monitoring-Anpassung

## Regeln / Qualitätskriterien

- Ursache und Symptom werden getrennt
- Diagnose ist anhand Trace/Log/Request reproduzierbar
- Jede Empfehlung enthält Begründung und Prüfschritt
- Kein Wechsel auf Mappinganalyse vor bestandener Schemavalidierung
- Security, Rechenkern und Reporting werden als externe Abhängigkeiten berücksichtigt
- Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`

### Typische Fehler
- Nur Stacktrace lesen und Request/Operation ignorieren
- `getQuote`/`getOffer` nicht über Provider-/Phasenmodell denken
- Werteverlust fälschlich als Berechnungsfehler deuten, obwohl Eingabe-Mapping fehlt
- Laufzeitproblem im Webservice suchen, obwohl IAM oder Rechenkern dominiert

## Ressourcen

- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Gesamtdokumentation_v3.html`
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Einarbeitungsplan.html`
- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf`
- `docs/referenzen/Webservices-Strategie/REFERENZEN.md`