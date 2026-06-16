---
name: vb-devscouts-evaluation
description: Bewertet KI-Tools, KI-Use-Cases und Enablement-Maßnahmen für die IT-Anwendungsentwicklung im Kontext der DevScouts-Initiative.
---

# vb-devscouts-evaluation

## Ziel
Bewertet KI-Tools, KI-Use-Cases und Enablement-Maßnahmen für die IT-Anwendungsentwicklung im Kontext der DevScouts-Initiative. Erzeugt eine nachvollziehbare Entscheidungsvorlage mit Use-Case-Katalog, Tool-Strategie, Risiko-/Compliance-Bewertung, Schulungskonzept, Stakeholder-Votum und priorisierter Roadmap. Einsetzbar zur Bewertung von IntelliJ AI Assistant, Junie, Cursor, Windsurf, Gemini, n8n oder ähnlichen Tools. Benötigt: Tool oder Use Case, Zielgruppe, Einsatzkontext, Daten-/Code-Kontext, Integrationsbedarf, bekannte Vorgaben von ISB/Betriebsrat/KI-Abteilung/Datenschutz. NICHT verwenden für BiPRO-Analyse (`vb-bipro-analysis`), Webservice-Diagnose (`vb-webservice-diagnostics`) oder Release-Finalisierung (`vb-release-finalization`).

## Vorgehen

### 1. Bewertungsgegenstand abgrenzen
- Kläre: Tool, Use Case oder Schulungsmaßnahme? Pilot, Markt-Screening oder Entscheidungsvorlage?
- Ist AE-spezifische Zuarbeit oder Unternehmens-Governance? Beschaffung ja/nein?

### 2. Use Cases strukturieren
- Erstelle einen Use-Case-Katalog mit Spalten: Use Case, Zielgruppe, Geschäftlicher Hebel, Datenrisiko, Tool-Fit, Reifegrad.
- Berücksichtige: Code-Generierung, Tests, Refactoring, Dokumentation, Prozessoptimierung/n8n.

### 3. Tool-Bewertung durchführen
- Bewerte mindestens: Security, Datenschutz, Cloud-Policy, Entwicklerproduktivität, Integration, Kontrollierbarkeit, Akzeptanz, Schulungsaufwand, Kosten/Nutzen.

### 4. Stakeholder-Votum vorbereiten
- Berücksichtige IT-AE Entwickler, KI-Abteilung, ISB/Datensicherheit, Betriebsrat, IT-Betrieb, IT-Leitung.

### 5. Pilot- und Enablement-Plan erstellen
- Phase 1 – Analyse und Zieldefinition: Brainstorming, SIPOC, Stakeholder-Interviews, Gap-Analyse, SWOT/Pareto.
- Phase 2 – Planung und Pilotprojekte: Pilotumfang, FMEA-Risikobewertung, PDCA-Zyklus, KPIs.
- Phase 3 – Skalierung und Verbesserung: Lessons Learned, Regelkarten/KPIs, Retrospektiven, Übertragung auf weitere Use Cases.

### 6. Entscheidungsvorlage formulieren
- Verwende eine der Kategorien: `beibehalten`, `erweitern`, `ergänzen`, `pilotieren`, `nicht einsetzen`, `zurückstellen bis Klärung`.
- Output als strukturierter Bericht mit: Kurzempfehlung, Bewertungsgegenstand, Use-Case-Katalog, Tool-Bewertung, Risiken/Compliance/Datenschutz, Stakeholder-Votum, Schulungs- und Enablement-Konzept, Pilotplan, Roadmap, Offene Entscheidungen.

## Regeln / Qualitätskriterien
- Entscheidung muss nachvollziehbar und stakeholderfähig sein.
- Security, Datenschutz und Betriebsrat nicht nachgelagert behandeln.
- Use Cases priorisieren, nicht nur sammeln.
- Schulungskonzept unterscheidet Einsteiger, Fortgeschrittene und Experten.
- Empfehlung trennt Pilot, Skalierung und Beschaffung.
- Typische Fehler vermeiden: Tools nur nach Features vergleichen, Datenschutz und Betriebsrat zu spät einbinden, keine messbaren Erfolgskriterien definieren, Schulungskonzept mit Tool-Einweisung verwechseln.
- Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, als `offen`, `zu verifizieren` oder `Annahme` kennzeichnen. Erfinde keine VB-Standards.

## Ressourcen
- `docs/referenzen/DevScouts/basisinformationen-zur-arbeitsgruppe.txt`
- `docs/referenzen/DevScouts/ki-einfuehrung-phasen.docx`
- `docs/referenzen/DevScouts/REFERENZEN.md`
