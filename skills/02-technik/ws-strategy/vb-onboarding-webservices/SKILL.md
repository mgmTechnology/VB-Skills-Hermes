# vb-onboarding-webservices

## Zweck
Erstellt einen strukturierten 4–6-Wochen-Einarbeitungsplan für neue Entwicklerinnen und Entwickler in der Gruppe Webservices & Strategie mit Fokus auf BiPRO TAA Leben, Provider-Modell, Phasenpipeline, Mapping, Tests, Diagnose, Security, Betrieb und Releaseverständnis.

## Wann verwenden
- Neues Teammitglied startet im Bereich Webservices & Strategie.
- Ein erfahrener Java-Entwickler ist neu im BiPRO-/Versicherungsumfeld.
- Ein bestehender Entwickler soll gezielt in BiPRO TAA Leben, Mapping oder Diagnose eingearbeitet werden.
- Ein Mentor benötigt Wochenplan, Lernziele, Aufgaben und Lernkontrollen.

## Wann NICHT verwenden
- Allgemeines Unternehmens-Onboarding.
- Reines Scrum-/Projekt-Onboarding.
- Spezialtraining für Release-Finalisierung; dafür ergänzend `vb-release-finalization` verwenden.


## Verbindliche Referenzen
Nutze bei Bedarf diese lokalen Referenzen im Repository:

- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Gesamtdokumentation_v3.html`
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Einarbeitungsplan.html`
- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf`
- `docs/referenzen/Webservices-Strategie/REFERENZEN.md`

Regel: Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`. Erfinde keine VB-Standards.


## Benötigte Eingaben
- Zielperson: Erfahrung mit Java, XML/SOAP, Versicherungsfachlichkeit, Betrieb.
- gewünschte Dauer: 4, 5 oder 6 Wochen.
- Rolle: Entwickler, technischer Lead, Betrieb/Support, DevScout.
- verfügbare Mentoren und reale Übungsaufgaben.
- Schwerpunkt: BiPRO, Diagnose, Dokumentation, Release, KI/DevScouts.

## Vorgehen

### 1. Profil einschätzen
Erzeuge eine Einschätzung:

| Kompetenzfeld | Stand | Konsequenz für Plan |
|---|---|---|
| Java/Maven/Git |  |  |
| XML/SOAP/WSDL/XSD |  |  |
| BiPRO/TAA |  |  |
| ELSA/VB-Modell |  |  |
| Mapping/Konverter |  |  |
| Tests/Roundtrip |  |  |
| Betrieb/Monitoring |  |  |
| Release/Deployment |  |  |

### 2. Lernlogik anwenden
Der Plan folgt nicht blind der Dokumentationsreihenfolge. Nutze diese Reihenfolge:

1. Big Picture und erster Request.
2. Provider-Modell verstehen.
3. Phasenpipeline und DTO-Hierarchie verstehen.
4. Mapping und Konverter verstehen.
5. Ein Attribut end-to-end umsetzen.
6. Trace, Log, Monitoring und Fehlerdiagnose.
7. Security, Betrieb und Release-Kontext.

### 3. Wochenplan erzeugen
Standard 6 Wochen:

#### Woche 1 – Fachlich ankommen und lauffähig werden
- Marken VBL/DOL und TAA verstehen.
- Operationen und typische Journeys verstehen.
- WSDL/XSD, Namespaces und VU-Erweiterungen lesen.
- Setup prüfen, bekannte Diskrepanzen markieren.
- ersten Request ausführen oder nachvollziehen.

#### Woche 2 – Provider, Phasen, DTO
- zentrale Einstiegshürde klären: keine `getOffer(...)`-Methode, sondern generisches `invoke`.
- Request im Provider-Modell verfolgen.
- Phasenpipeline und `*.durchlaufe` verstehen.
- DTO-Hierarchie verstehen.
- einfachen Trace lesen.

#### Woche 3 – Mapping und Konverter
- Eingabe-/Ausgabe-Mapping unterscheiden.
- XML-Regel-DSL und XPath/JXPath verstehen.
- Converter vs Transformer vs MappingPhase trennen.
- vorhandenen Roundtrip-Test lesen.

#### Woche 4 – Ein Attribut end-to-end
- fachliche Verortung bestimmen.
- XSD erweitern.
- Modellklasse und `@Property` prüfen.
- Eingabe- und Ausgabe-Mapping ergänzen.
- ggf. Konverter erstellen/registrieren.
- Roundtrip-Test schreiben.

#### Woche 5 – Diagnose, Tests und Datenhaltung
- Trace + Log kombiniert analysieren.
- Schema-Validierungsfehler reproduzieren.
- Reportingdaten und `correlation_trace_id` nutzen.
- IAM/Rechenkern/Datenhaltung einordnen.
- produktionsnahe Diagnose durchführen.

#### Woche 6 – Security, Betrieb und Konsolidierung
- SCT, IAM, STS und Einreichung unterscheiden.
- Dokumentenfluss / E-Antrag verstehen.
- Diskrepanzen und Risiken bewusst machen.
- Abschlussaufgabe und Walkthrough durchführen.

### 4. Verdichtung auf 4 Wochen
Bei erfahrenen Entwicklern:

- Woche 1: Big Picture + Setup + Provider.
- Woche 2: Phasen + Mapping + Konverter.
- Woche 3: Attribut end-to-end + Roundtrip.
- Woche 4: Diagnose + Security + Abschlussaufgabe.

### 5. Mentoring und Lernkontrolle einplanen
Jede Woche enthält:

- Lernziele.
- konkrete Aufgaben.
- Doku-Kapitel/Referenzen.
- praktische Übung.
- Meilenstein.
- Lernkontrolle.

## Output-Format

```markdown
# Einarbeitungsplan Webservices & Strategie

## Zielprofil
## Dauer und Schwerpunkt
## Voraussetzungen
## Mentor-/Begleitmodell
## Wochenplan
### Woche 1
### Woche 2
### Woche 3
### Woche 4
### Woche 5
### Woche 6
## Übungen
## Lernkontrollen
## Abschlussaufgabe
## Offene Voraussetzungen
```

## Qualitätskriterien
- Plan enthält praktische Aufgaben, nicht nur Leseliste.
- Provider-Modell wird früh erklärt.
- Ein Attribut wird end-to-end umgesetzt.
- Diagnosefähigkeit ist explizites Lernziel.
- Doku-Verbesserungen aus dem Onboarding werden zurückgeführt.

## Typische Fehler
- Zu viel Theorie in Woche 1.
- Provider-Modell zu spät erklären.
- Keine echte Übungsaufgabe.
- Kein Mentor/kein Feedback-Rhythmus.
- Release-/Betriebskontext vollständig ausblenden.
