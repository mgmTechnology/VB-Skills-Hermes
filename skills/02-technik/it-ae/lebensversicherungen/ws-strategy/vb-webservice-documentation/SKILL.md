---
name: vb-webservice-documentation
description: Erstellt oder aktualisiert technische Dokumentation für VBL/DOL BiPRO-Webservices. Belastbare Service-Dokumentation mit Aussageklassen, Quellenbezug, Architektur, Datenfluss, Mapping, Tests und Betrieb.
---

# VB Webservice Documentation

## Ziel

Erstellt oder aktualisiert technische Dokumentation für VBL/DOL BiPRO-Webservices so, dass sie für Entwicklung, Betrieb, Onboarding und Fehleranalyse nutzbar ist. Der Skill erzeugt keine lose Beschreibung, sondern eine belastbare Service-Dokumentation mit Aussageklassen, Quellenbezug, Architektur, Datenfluss, Mapping, Tests, Betrieb und offenen Punkten.

Verwenden bei:
- Neue oder bestehende Webservice-Dokumentation erstellen
- Confluence-/HTML-Dokumentation aktualisieren
- Änderung an Operation, XSD, Mapping, Konverter oder Test dokumentieren
- Dokumentation nach Incident oder Release nachziehen
- Onboarding-Dokumentation für neue Entwickler verbessern

NICHT verwenden bei:
- Reiner API-Spezifikation ohne Betriebs-/Architekturkontext
- Release-Finalisierung; dafür `vb-release-finalization` verwenden

## Vorgehen

### 1. Dokumentationsziel klären
Klassifiziere: Entwicklerleitfaden, Betriebsdokumentation, Schnittstellendokumentation, Release-/Änderungsdokumentation, Onboarding-Kapitel, Incident-/Lessons-Learned-Dokumentation

### 2. Aussageklassen verwenden
Jede nicht triviale Aussage einordnen als: Belegt, Plausibel, Zu verifizieren, Diskrepanz, Empfehlung

### 3. Service-Steckbrief erstellen
Pflichtfelder: Marke (VBL/DOL/beide), Version, Operationen, WSDL/XSD, Repository/Module, Runtime/Deployment, externe Abhängigkeiten, Monitoring/Reporting, Ansprechpartner

### 4. Architektur dokumentieren
Mindestens: Web/Transport-Schicht, BiPRO-Adapter, Phasenpipeline, DTO-Hierarchie, Mapping und Konverter, Rechenkern, IAM, E-Antrag, Reporting

### 5. Request-Ablauf beschreiben
Nutze textuelle Sequenz oder Mermaid: Client → SOAP Endpoint → Provider.invoke → DTO → Phasen → Mapping → Rechenkern → Export → Response → Reporting

### 6. Mapping dokumentieren
Für jedes relevante Feld Tabelle mit: Feld, XSD, XML-Pfad, Modellpfad, Eingabe-Mapping, Ausgabe-Mapping, Konverter, Test

### 7. Test- und Qualitätsabsicherung dokumentieren
Roundtrip-Testklasse, Testressourcen, XPath-Assertions, Sonderfälle

### 8. Betrieb und Diagnose dokumentieren
Relevante Endpunkte, `/wsversion`, Reporting-Tabelle/Felder, Diagnosekette, Monitoring-Dashboards, typische Fehlerbilder

### 9. Offene Punkte und Risiken sichtbar machen
Diskrepanzen listen (Java-Version, Runtime-Modell, Endpunkte, Security-Zuordnung, Versions-/Pfadvarianten)

## Regeln / Qualitätskriterien

- Dokumentation ist für neue Entwickler verständlich und für erfahrene Entwickler prüfbar
- Statische Sicht (Code/XSD/Mapping/Test) und dynamische Sicht (Trace/Monitoring) sind getrennt
- Offene Punkte werden nicht versteckt
- Jede Anleitung enthält Prüfkriterium und typischen Fehler
- Beispiele sind datenschutzkonform und ohne produktive Kundendaten
- Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`

### Typische Fehler
- Nur fachlich beschreiben, aber Provider-/Phasenmodell weglassen
- Mapping ohne Tests dokumentieren
- Veraltete Setup-Hinweise unmarkiert übernehmen
- Laufzeitwerte ohne Datum/Umgebung dokumentieren

## Ressourcen

- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Gesamtdokumentation_v3.html`
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Einarbeitungsplan.html`
- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf`
- `docs/referenzen/Webservices-Strategie/REFERENZEN.md`