---
name: vb-onboarding-webservices
description: Erstellt einen strukturierten 4-6-Wochen-Einarbeitungsplan für neue Entwickler in der Gruppe Webservices & Strategie mit Fokus auf BiPRO TAA Leben.
---

# VB Onboarding Webservices

## Ziel

Erstellt einen strukturierten 4–6-Wochen-Einarbeitungsplan für neue Entwicklerinnen und Entwickler in der Gruppe Webservices & Strategie mit Fokus auf BiPRO TAA Leben, Provider-Modell, Phasenpipeline, Mapping, Tests, Diagnose, Security, Betrieb und Releaseverständnis.

Verwenden bei:
- Neues Teammitglied startet im Bereich Webservices & Strategie
- Ein erfahrener Java-Entwickler ist neu im BiPRO-/Versicherungsumfeld
- Ein bestehender Entwickler soll gezielt in BiPRO TAA Leben, Mapping oder Diagnose eingearbeitet werden
- Ein Mentor benötigt Wochenplan, Lernziele, Aufgaben und Lernkontrollen

NICHT verwenden bei:
- Allgemeinem Unternehmens-Onboarding
- Reinem Scrum-/Projekt-Onboarding
- Spezialtraining für Release-Finalisierung; dafür ergänzend `vb-release-finalization` verwenden

## Vorgehen

### 1. Profil einschätzen
Erzeuge eine Einschätzung zu: Java/Maven/Git, XML/SOAP/WSDL/XSD, BiPRO/TAA, ELSA/VB-Modell, Mapping/Konverter, Tests/Roundtrip, Betrieb/Monitoring, Release/Deployment

### 2. Lernlogik anwenden
Der Plan folgt nicht blind der Dokumentationsreihenfolge:
1. Big Picture und erster Request
2. Provider-Modell verstehen
3. Phasenpipeline und DTO-Hierarchie verstehen
4. Mapping und Konverter verstehen
5. Ein Attribut end-to-end umsetzen
6. Trace, Log, Monitoring und Fehlerdiagnose
7. Security, Betrieb und Release-Kontext

### 3. Wochenplan erzeugen (Standard 6 Wochen)
- **Woche 1** – Fachlich ankommen und lauffähig werden: Marken VBL/DOL, Operationen, WSDL/XSD, Setup, ersten Request ausführen
- **Woche 2** – Provider, Phasen, DTO: generisches `invoke` statt `getOffer()`, Provider-Modell, Phasenpipeline, DTO-Hierarchie
- **Woche 3** – Mapping und Konverter: Eingabe-/Ausgabe-Mapping, XML-Regel-DSL, Converter vs Transformer, Roundtrip-Test
- **Woche 4** – Ein Attribut end-to-end: XSD erweitern, Modellklasse, Mapping, Konverter, Roundtrip-Test
- **Woche 5** – Diagnose, Tests und Datenhaltung: Trace + Log, Schema-Validierungsfehler, Reporting, IAM/Rechenkern
- **Woche 6** – Security, Betrieb und Konsolidierung: SCT/IAM/STS, Dokumentenfluss, Diskrepanzen, Abschlussaufgabe

### 4. Verdichtung auf 4 Wochen (erfahrene Entwickler)
- Woche 1: Big Picture + Setup + Provider
- Woche 2: Phasen + Mapping + Konverter
- Woche 3: Attribut end-to-end + Roundtrip
- Woche 4: Diagnose + Security + Abschlussaufgabe

### 5. Mentoring und Lernkontrolle einplanen
Jede Woche enthält: Lernziele, konkrete Aufgaben, Doku-Kapitel/Referenzen, praktische Übung, Meilenstein, Lernkontrolle

## Regeln / Qualitätskriterien

- Plan enthält praktische Aufgaben, nicht nur Leseliste
- Provider-Modell wird früh erklärt
- Ein Attribut wird end-to-end umgesetzt
- Diagnosefähigkeit ist explizites Lernziel
- Doku-Verbesserungen aus dem Onboarding werden zurückgeführt
- Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`

### Typische Fehler
- Zu viel Theorie in Woche 1
- Provider-Modell zu spät erklären
- Keine echte Übungsaufgabe
- Kein Mentor/kein Feedback-Rhythmus
- Release-/Betriebskontext vollständig ausblenden

## Ressourcen

- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Gesamtdokumentation_v3.html`
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Einarbeitungsplan.html`
- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf`
- `docs/referenzen/Webservices-Strategie/REFERENZEN.md`