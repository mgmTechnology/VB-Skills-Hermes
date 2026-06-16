# vb-webservice-documentation

## Zweck
Erstellt oder aktualisiert technische Dokumentation für VBL/DOL BiPRO-Webservices so, dass sie für Entwicklung, Betrieb, Onboarding und Fehleranalyse nutzbar ist. Der Skill erzeugt keine lose Beschreibung, sondern eine belastbare Service-Dokumentation mit Aussageklassen, Quellenbezug, Architektur, Datenfluss, Mapping, Tests, Betrieb und offenen Punkten.

## Wann verwenden
- Neue oder bestehende Webservice-Dokumentation erstellen.
- Confluence-/HTML-Dokumentation aktualisieren.
- Änderung an Operation, XSD, Mapping, Konverter oder Test dokumentieren.
- Dokumentation nach Incident oder Release nachziehen.
- Onboarding-Dokumentation für neue Entwickler verbessern.

## Wann NICHT verwenden
- Reine API-Spezifikation ohne Betriebs-/Architekturkontext.
- Release-Finalisierung; dafür `vb-release-finalization` verwenden.


## Verbindliche Referenzen
Nutze bei Bedarf diese lokalen Referenzen im Repository:

- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Gesamtdokumentation_v3.html`
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Einarbeitungsplan.html`
- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf`
- `docs/referenzen/Webservices-Strategie/REFERENZEN.md`

Regel: Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`. Erfinde keine VB-Standards.


## Benötigte Eingaben
- Service/Operation/Version.
- vorhandene Dokumentation oder Codeausschnitt.
- Änderung oder Analyseziel.
- relevante Requests/Responses, Mappingregeln, Tests oder Tracebeispiele.

## Vorgehen

### 1. Dokumentationsziel klären
Klassifiziere:

- Entwicklerleitfaden
- Betriebsdokumentation
- Schnittstellendokumentation
- Release-/Änderungsdokumentation
- Onboarding-Kapitel
- Incident-/Lessons-Learned-Dokumentation

### 2. Aussageklassen verwenden
Jede nicht triviale Aussage bekommt, falls nötig, eine Einordnung:

| Klasse | Bedeutung |
|---|---|
| Belegt | durch Code, Doku, Test, Trace oder Artefakt gestützt |
| Plausibel | konsistent, aber nicht abschließend geprüft |
| Zu verifizieren | relevant, aber Quelle/Aktualität unklar |
| Diskrepanz | widersprüchliche Aussagen vorhanden |
| Empfehlung | abgeleitete Maßnahme |

### 3. Service-Steckbrief erstellen
Pflichtfelder:

```markdown
## Service-Steckbrief
- Marke: VBL/DOL/beide
- Version:
- Operationen:
- WSDL/XSD:
- Repository/Module:
- Runtime/Deployment:
- externe Abhängigkeiten:
- Monitoring/Reporting:
- Ansprechpartner/offene Zuständigkeiten:
```

### 4. Architektur dokumentieren
Dokumentiere mindestens:

- Web/Transport-Schicht (`TarifrechnerService`, JAX-WS Provider).
- BiPRO-Adapter.
- Phasenpipeline.
- DTO-Hierarchie.
- Mapping und Konverter.
- Rechenkern, IAM, E-Antrag, Reporting.

### 5. Request-Ablauf beschreiben
Nutze eine textuelle Sequenz oder Mermaid:

```text
Client -> SOAP Endpoint -> Provider.invoke -> DTO -> Phasen -> Mapping -> Rechenkern -> Export -> Response -> Reporting
```

### 6. Mapping dokumentieren
Für jedes relevante Feld:

| Feld | XSD | XML-Pfad | Modellpfad | Eingabe-Mapping | Ausgabe-Mapping | Konverter | Test |
|---|---|---|---|---|---|---|---|

### 7. Test- und Qualitätsabsicherung dokumentieren
Beschreibe:

- Roundtrip-Testklasse.
- Testressourcen.
- XPath-Assertions.
- Sonderfälle: `xsi:type`, `xsd:sequence`, Encoding, PDF, Versicherungsbeginn.

### 8. Betrieb und Diagnose dokumentieren
Dokumentiere:

- relevante Endpunkte.
- `/wsversion`, falls verfügbar.
- Reporting-Tabelle/Felder.
- typische Diagnosekette.
- Monitoring-Dashboards.
- typische Fehlerbilder und Erstprüfung.

### 9. Offene Punkte und Risiken sichtbar machen
Liste Diskrepanzen, z. B. Java-Version, Runtime-Modell, Endpunkte, Security-Zuordnung, Versions-/Pfadvarianten.

## Output-Format

```markdown
# [Service/Operation] – Technische Dokumentation

## 0. Dokumentstatus und Quellen
## 1. Kurzüberblick
## 2. Fachlicher Kontext
## 3. Architektur
## 4. Request-Ablauf
## 5. WSDL/XSD/Namespaces
## 6. Mapping und Konverter
## 7. Tests
## 8. Betrieb / Monitoring / Diagnose
## 9. Security
## 10. Entwickleranleitungen
## 11. Offene Punkte / Risiken
## 12. Änderungsverlauf
```

## Qualitätskriterien
- Dokumentation ist für neue Entwickler verständlich und für erfahrene Entwickler prüfbar.
- Statische Sicht (Code/XSD/Mapping/Test) und dynamische Sicht (Trace/Monitoring) sind getrennt.
- Offene Punkte werden nicht versteckt.
- Jede Anleitung enthält Prüfkriterium und typischen Fehler.
- Beispiele sind datenschutzkonform und ohne produktive Kundendaten.

## Typische Fehler
- Nur fachlich beschreiben, aber Provider-/Phasenmodell weglassen.
- Mapping ohne Tests dokumentieren.
- Veraltete Setup-Hinweise unmarkiert übernehmen.
- Laufzeitwerte ohne Datum/Umgebung dokumentieren.
