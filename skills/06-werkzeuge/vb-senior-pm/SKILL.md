---
name: "vb-senior-pm"
description: "VB-adaptierter Skill. Ursprung: skills/project-management/senior-pm/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-senior-pm

## VB-Einordnung

Methoden-Skill für Projektmanagement, Portfolio-Betrachtungen, Risiken, Ressourcen und Management-Reporting.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ursprüngliche Detailanweisung (Referenz)

---

# Senior Project Management Experte

## Überblick

Strategisches Projektmanagement für Unternehmenssoftware, SaaS und digitale Transformationsinitiativen. Bietet Fähigkeiten zum Portfoliomanagement, quantitative Analysewerkzeuge und Berichtsrahmen auf Managementebene für komplexe Portfolios mit mehreren Projekten.

### Kernkompetenzbereiche

**Portfoliomanagement & Strategische Ausrichtung**
- Optimierung von Portfolios mit mehreren Projekten unter Verwendung fortgeschrittener Priorisierungsmodelle (WSJF, RICE, ICE, MoSCoW).
- Entwicklung strategischer Roadmaps, die auf Geschäftsziele und Marktbedingungen abgestimmt sind.
- Planung der Ressourcenkapazität und Optimierung der Zuweisung über das Portfolio hinweg.
- Überwachung der Portfolio-Gesundheit mit multidimensionalen Bewertungssystemen.

**Quantitatives Risikomanagement**
- EMV-Analyse (Expected Monetary Value) zur Quantifizierung finanzieller Risiken.
- Monte-Carlo-Simulation zur Modellierung von Zeitplanrisiken und Konfidenzintervallen.
- Implementierung von Rahmenbedingungen für die Risikobereitschaft mit Schwellenwerten auf Unternehmensebene.
- Analyse der Korrelation von Portfoliorisiken und Diversifizierungsstrategien.

**Management-Kommunikation & Governance**
- Management-Berichte mit RAG-Status (Ampel) und strategischen Empfehlungen.
- Stakeholder-Abstimmung durch detaillierte RACI-Matrizen und Eskalationspfade.
- Verfolgung der finanziellen Leistung mit risikobereinigten ROI- und NPV-Berechnungen.
- Change-Management-Strategien für groß angelegte digitale Transformationen.

## Methodik & Frameworks

### Drei-Stufen-Analyse-Ansatz

**Stufe 1: Portfolio-Gesundheitsbewertung**
Nutzt das `project_health_dashboard.py`, um eine umfassende multidimensionale Bewertung zu erstellen:

```bash
python3 scripts/project_health_dashboard.py assets/sample_project_data.json
```

**Gesundheitsdimensionen (Gewichtete Bewertung):**
- **Zeitplan-Performance** (25% Gewichtung): Einhaltung des Zeitplans, Erreichung von Meilensteinen, Analyse des kritischen Pfads.
- **Budget-Management** (25% Gewichtung): Ausgabenabweichung, Prognosegenauigkeit, Kosteneffizienz-Metriken.
- **Scope-Delivery (Umfang)** (20% Gewichtung): Abschlussraten von Features, Erfüllung von Anforderungen, Änderungskontrolle.
- **Qualitätsmetriken** (20% Gewichtung): Testabdeckung, Fehlerdichte, technische Schulden, Sicherheitsstatus.
- **Risikoexposition** (10% Gewichtung): Risikowert, Wirksamkeit der Schadensbegrenzung, Trends der Exposition.

**Berechnung des RAG-Status:**
- 🟢 Grün: Gesamtpunktzahl >80, alle Dimensionen >60.
- 🟡 Gelb: Gesamtpunktzahl 60-80, oder eine Dimension 40-60.
- 🔴 Rot: Gesamtpunktzahl <60, oder eine Dimension <40.

**Stufe 2: Risikomatrix & Strategie zur Schadensbegrenzung**
Nutzt den `risk_matrix_analyzer.py` für die quantitative Risikobewertung:

```bash
python3 scripts/risk_matrix_analyzer.py assets/sample_project_data.json
```

**Quantitativer Risikoprozess:**
1. **Wahrscheinlichkeitsbewertung** (Skala 1-5): Historische Daten, Expertenurteil, Monte-Carlo-Inputs.
2. **Auswirkungsanalyse** (Skala 1-5): Finanzielle, zeitliche, qualitative und strategische Auswirkungsvektoren.
3. **Kategorie-Gewichtung**: Technisch (1.2x), Ressourcen (1.1x), Finanziell (1.4x), Zeitplan (1.0x).
4. **EMV-Berechnung**:

```python
# Berechnung des EMV und des risikobereinigten Budgets
def calculate_emv(risks):
    category_weights = {"Technical": 1.2, "Resource": 1.1, "Financial": 1.4, "Schedule": 1.0}
    total_emv = 0
    for risk in risks:
        score = risk["probability"] * risk["impact"] * category_weights[risk["category"]]
        emv = risk["probability"] * risk["financial_impact"]
        total_emv += emv
        risk["score"] = score
    return total_emv

def risk_adjusted_budget(base_budget, portfolio_risk_score, risk_tolerance_factor):
    risk_premium = portfolio_risk_score * risk_tolerance_factor
    return base_budget * (1 + risk_premium)
```

**Risikoantwortstrategien (nach Schwellenwerten):**
- **Vermeiden** (>18): Durch Änderungen am Umfang oder Ansatz eliminieren.
- **Mindern** (12-18): Wahrscheinlichkeit oder Auswirkung durch aktive Intervention reduzieren.
- **Übertragen** (8-12): Versicherungen, Verträge, Partnerschaften.
- **Akzeptieren** (<8): Beobachten mit Notfallplanung.

**Stufe 3: Optimierung der Ressourcenkapazität**
Setzt den `resource_capacity_planner.py` für die Portfolio-Ressourcenanalyse ein:

```bash
python3 scripts/resource_capacity_planner.py assets/sample_project_data.json
```

**Rahmen für die Kapazitätsanalyse:**
- **Optimierung der Auslastung**: Zielwert 70-85% für nachhaltige Produktivität.
- **Skill-Matching**: Algorithmus-basierte Ressourcenzuweisung zur Effizienzmaximierung.
- **Engpass-Identifikation**: Ressourcenbeschränkungen auf dem kritischen Pfad über das Portfolio hinweg.
- **Szenarioplanung**: What-if-Analyse für Strategien zur Ressourcenneuverteilung.

### Fortgeschrittene Priorisierungsmodelle

Wende jedes Modell in dem spezifischen Kontext an, in dem es das beste Signal liefert:

**Weighted Shortest Job First (WSJF)** — Ressourcenbeschränkte agile Portfolios mit quantifizierbaren Verzögerungskosten.
```python
def wsjf(user_value, time_criticality, risk_reduction, job_size):
    return (user_value + time_criticality + risk_reduction) / job_size
```

**RICE** — Kundenorientierte Initiativen, bei denen Reichweitenmetriken quantifizierbar sind.
```python
def rice(reach, impact, confidence_pct, effort_person_months):
    return (reach * impact * (confidence_pct / 100)) / effort_person_months
```

**ICE** — Schnelle Priorisierung während des Brainstormings oder wenn die Zeit für Analysen begrenzt ist.
```python
def ice(impact, confidence, ease):
    return (impact + confidence + ease) / 3
```

**Modellauswahl — Nutze diese Entscheidungslogik:**
```
if ressourcenbeschränkt and agile_methodik and verzoegerungskosten_quantifizierbar:
    → WSJF
elif kundenorientiert and reichweitenmetriken_verfuegbar:
    → RICE
elif schnelle_priorisierung_noetig or ideenfindungsphase:
    → ICE
elif mehrere_stakeholdergruppen_mit_unterschiedlichen_prioritaeten:
    → MoSCoW
elif komplexe_abwaegungen_ueber_nicht_vergleichbare_kriterien:
    → Multi-Criteria Decision Analysis (MCDA)
```

Referenz: `references/portfolio-prioritization-models.md`

### Framework für das Risikomanagement

Referenz: `references/risk-management-framework.md`

**Schritt 1: Risikoklassifizierung nach Kategorien**
- Technisch: Architektur, Integration, Performance.
- Ressourcen: Verfügbarkeit, Skills, Fluktuation.
- Zeitplan: Abhängigkeiten, kritischer Pfad, externe Faktoren.
- Finanziell: Budgetüberschreitungen, Währung, wirtschaftliche Faktoren.
- Geschäftlich: Marktveränderungen, Wettbewerbsdruck, strategische Verschiebungen.

**Schritt 2: Drei-Punkt-Schätzung für Monte-Carlo-Inputs**
```python
def three_point_estimate(optimistic, most_likely, pessimistic):
    expected = (optimistic + 4 * most_likely + pessimistic) / 6
    std_dev = (pessimistic - optimistic) / 6
    return expected, std_dev
```

**Schritt 3: Korrelation der Portfoliorisiken**
```python
import math

def portfolio_risk(individual_risks, correlations):
    # individual_risks: Liste der EMV-Werte der Risiken
    # correlations: Liste von (i, j, Korrelationskoeffizient) Tupeln
    sum_sq = sum(r**2 for r in individual_risks)
    sum_corr = sum(2 * c * individual_risks[i] * individual_risks[j]
                   for i, j, c in correlations)
    return math.sqrt(sum_sq + sum_corr)
```

**Rahmen für die Risikobereitschaft:**
- **Konservativ**: Risikowerte 0-8, 25-30% Management-Reserve.
- **Moderat**: Risikowerte 8-15, 15-20% Management-Reserve.
- **Aggressiv**: Risikowerte 15+, 10-15% Management-Reserve.

## Vorlagen & Assets

### Projekt-Charter Vorlage
Referenz: `assets/project_charter_template.md`

**Umfassende Charter mit 12 Abschnitten, einschließlich:**
- Management-Summary mit strategischer Ausrichtung.
- Erfolgskriterien mit KPIs und Quality Gates.
- RACI-Matrix mit Entscheidungsbefugnissen.
- Risikobewertung mit Strategien zur Schadensbegrenzung.
- Budgetaufstellung mit Reserve-Analyse.
- Zeitplan mit Abhängigkeiten auf dem kritischen Pfad.

### Management-Bericht Vorlage
Referenz: `assets/executive_report_template.md`

**Portfolio-Berichterstattung auf Managementebene mit:**
- RAG-Status-Dashboard mit Trendanalyse.
- Finanzielle Leistung vs. strategische Ziele.
- Risiko-Heatmap mit Status der Schadensbegrenzung.
- Ressourcenauslastung und Kapazitätsanalyse.
- Zukunftsgerichtete Empfehlungen mit ROI-Prognosen.

### RACI-Matrix Vorlage
Referenz: `assets/raci_matrix_template.md`

**Zuweisung von Verantwortlichkeiten auf Unternehmensebene mit:**
- Detaillierter Stakeholder-Liste mit Entscheidungsbefugnissen.
- Phasenbasierte RACI-Zuweisungen (Initiierung bis Bereitstellung).
- Eskalationspfade mit Zeitplan und Befugnisstufen.
- Kommunikationsprotokolle und Besprechungsrahmen.
- Konfliktlösungsprozesse mit Governance-Integration.

### Portfolio-Beispieldaten
Referenz: `assets/sample_project_data.json`

**Realistisches Portfolio mit mehreren Projekten, einschließlich:**
- 4 Projekte in verschiedenen Phasen und Prioritäten.
- Vollständige Finanzdaten (Budgets, Ist-Werte, Prognosen).
- Ressourcenzuweisung mit Auslastungsmetriken.
- Risikoregister mit Wahrscheinlichkeits-/Auswirkungsbewertung.
- Qualitätsmetriken und Daten zur Stakeholder-Zufriedenheit.
- Abhängigkeiten und Meilenstein-Tracking.

### Beispiele für erwartete Ergebnisse
Referenz: `assets/expected_output.json`

**Demonstriert die Skript-Fähigkeiten mit:**
- Portfolio-Gesundheitswerten und RAG-Status.
- Visualisierung der Risikomatrix und Prioritäten zur Schadensbegrenzung.
- Ressourcenkapazitätsanalyse mit Optimierungsempfehlungen.
- Integrationsbeispiele, die zeigen, wie die Ausgaben einander ergänzen.

## Implementierung-Workflows

### Überprüfung der Portfolio-Gesundheit (Wöchentlich)

1. **Datenerhebung & Validierung**
   ```bash
   python3 scripts/project_health_dashboard.py current_portfolio.json
   ```
   ⚠️ Wenn ein Gesamtprojektwert <60 ist oder ein kritisches Datenfeld fehlt: STOPP und Datenintegritätsprobleme lösen, bevor fortgefahren wird.

2. **Update der Risikobewertung**
   ```bash
   python3 scripts/risk_matrix_analyzer.py current_portfolio.json
   ```
   ⚠️ Wenn ein Risikowert >18 ist (Schwelle für "Vermeiden"): STOPP und Eskalation an den Projektsponsor einleiten, bevor fortgefahren wird.

3. **Kapazitätsanalyse**
   ```bash
   python3 scripts/resource_capacity_planner.py current_portfolio.json
   ```
   ⚠️ Wenn eine Teamauslastung >90% oder <60% ist: Für eine sofortige Umverteilungsdiskussion vor Schritt 4 markieren.

4. **Erstellung der Management-Zusammenfassung**
   - Ergebnisse in das Format des Management-Berichts synthetisieren.
   - Kritische Probleme und Empfehlungen hervorheben.
   - Stakeholder-Kommunikation vorbereiten.

### Monatlicher strategischer Review

1. **Review der Portfolio-Priorisierung**
   - WSJF/RICE/ICE Modelle anwenden, um aktuelle Prioritäten zu bewerten.
   - Strategische Ausrichtung an den Geschäftszielen prüfen.
   - Optimierungspotenziale identifizieren.

2. **Risiko-Portfolio-Analyse**
   - Risikobereitschaft und Toleranzschwellen aktualisieren.
   - Korrelation und Konzentration der Portfoliorisiken prüfen.
   - Investitionen in die Schadensbegrenzung anpassen.

3. **Planung der Ressourcenoptimierung**
   - Kapazitätsbeschränkungen für das kommende Quartal analysieren.
   - Strategien für Ressourcenneuverteilung und Einstellungen planen.
   - Skill-Gaps und Schulungsbedarf identifizieren.

4. **Stakeholder-Abstimmungssitzung**
   - Portfolio-Gesundheit und strategische Empfehlungen präsentieren.
   - Feedback zur Priorisierung und Ressourcenzuweisung einholen.
   - Abstimmung über die Prioritäten und Investitionen des kommenden Quartals.

### Quartalsweise Portfolio-Optimierung

1. **Bewertung der strategischen Ausrichtung**
   - Beitrag des Portfolios zu den Geschäftszielen bewerten.
   - Veränderungen der Markt- und Wettbewerbsposition prüfen.
   - Strategische Prioritäten und Erfolgskriterien aktualisieren.

2. **Review der finanziellen Leistung**
   - Risikobereinigten ROI über das Portfolio hinweg analysieren.
   - Budgetleistung und Prognosegenauigkeit prüfen.
   - Investitionsallokation für maximalen Wert optimieren.

3. **Analyse von Fähigkeitslücken (Capability Gaps)**
   - Neue Technologie- und Skill-Anforderungen identifizieren.
   - Investitionen in den Kompetenzaufbau planen.
   - Make-vs-Buy-vs-Partner Entscheidungen bewerten.

4. **Portfolio-Rebalancing**
   - Drei-Horizonte-Modell für Innovationsgleichgewicht anwenden.
   - Risiko-Rendite-Profil mittels Efficient Frontier optimieren.
   - Neue Initiativen planen und Entscheidungen zur Beendigung von Projekten treffen.

## Integrationsstrategien

### Atlassian Integration
- **Jira**: Portfolio-Dashboards, projektübergreifende Metriken, Risikoverfolgung.
- **Confluence**: Strategische Dokumentation, Management-Berichte, Wissensmanagement.
- MCP-Integrationen nutzen, um Datenerhebung und Berichterstellung zu automatisieren.

### Integration von Finanzsystemen
- **Budgetverfolgung**: Echtzeit-Ausgabendaten für die Abweichungsanalyse.
- **Ressourcenkosten**: Stundensätze und Auslastung für die Kapazitätsplanung.
- **ROI-Messung**: Verfolgung der Wertrealisierung gegenüber den Prognosen.

### Stakeholder-Management
- **Management-Dashboards**: Echtzeit-Visualisierung der Portfolio-Gesundheit.
- **Team-Scorecards**: Leistungsmetriken für einzelne Projekte.
- **Risikoregister**: Kollaboratives Risikomanagement mit automatisierter Eskalation.

## Übergabeprotokolle

### AN Scrum Master
**Kontexttransfer:**
- Strategische Prioritäten und Erfolgskriterien.
- Ressourcenzuweisung und Teamzusammensetzung.
- Risikofaktoren, die Aufmerksamkeit auf Sprint-Ebene erfordern.
- Qualitätsstandards und Akzeptanzkriterien.

**Laufende Zusammenarbeit:**
- Wöchentlicher Review der Velocity- und Gesundheitsmetriken.
- Erkenntnisse aus Sprint-Retrospektiven für das Lernen im Portfolio.
- Unterstützung bei Eskalation und Lösung von Hindernissen (Impediments).
- Feedback zur Teamkapazität und -auslastung.

### AN Product Owner
**Strategischer Kontext:**
- Marktpriorisierung und Wettbewerbsanalyse.
- Rahmen für den Nutzerwert und Messkriterien.
- Feature-Priorisierung abgestimmt auf die Portfolio-Ziele.
- Ressourcen- und Zeitplanbeschränkungen.

**Entscheidungsunterstützung:**
- ROI-Analyse für Feature-Investitionen.
- Risikobewertung für Produktentscheidungen.
- Marktbeobachtung und Integration von Kundenfeedback.
- Abstimmung der strategischen Roadmap und Abhängigkeiten.

### VON der Geschäftsführung (Executive Team)
**Strategische Richtung:**
- Updates zu Geschäftszielen und Prioritätsänderungen.
- Entscheidungen zur Budgetallokation und Ressourcengenehmigung.
- Anpassungen der Risikobereitschaft und Toleranzschwellen.
- Marktstrategie und Entscheidungen zur Wettbewerbsreaktion.

**Leistungserwartungen:**
- Ziele für die Portfolio-Gesundheit und Wertschöpfung.
- Erwartungen an Zeitplan- und Meilenstein-Commitments.
- Qualitätsstandards und Compliance-Anforderungen.
- Standards für Stakeholder-Zufriedenheit und Kommunikation.

## Erfolgsmetriken & KPIs

Referenz: `references/portfolio-kpis.md` für vollständige Definitionen und Messhinweise.

### Portfolio-Leistung
- Pünktliche Lieferquote: >80% innerhalb von 10% des geplanten Zeitplans.
- Budgetabweichung: <5% Durchschnitt über das Portfolio.
- Qualitätsscore: >85 Gesamtbewertung.
- Abdeckung der Risikominderung: >90% der Risiken mit aktiven Plänen.
- Ressourcenauslastung: 75-85% Durchschnitt.

### Strategischer Wert
- ROI-Erreichung: >90% der Projekte erfüllen die Prognosen innerhalb von 12 Monaten.
- Strategische Ausrichtung: >95% der Investitionen sind an Geschäftsprioritäten ausgerichtet.
- Innovationsbalance: 70% operativ / 20% Wachstum / 10% transformativ.
- Stakeholder-Zufriedenheit: >8.5/10 Durchschnitt Management.
- Time-to-Value: <6 Monate Durchschnitt nach Abschluss.

### Risikomanagement
- Risikoexposition: Innerhalb der genehmigten Bereiche halten.
- Lösungszeit: <30 Tage (mittel), <7 Tage (hoch).
- Kosteneffizienz der Minderung: <20% des gesamten EMV des Portfoliorisikos.
- Genauigkeit der Risikovorhersage: >70% Genauigkeit bei der Wahrscheinlichkeitsbewertung.

## Rahmen für kontinuierliche Verbesserung

### Integration von Portfolio-Lerneffekten
- Lessons Learned aus abgeschlossenen Projekten erfassen.
- Wahrscheinlichkeitsbewertungen von Risiken basierend auf historischen Daten aktualisieren.
- Genauigkeit der Schätzungen durch retrospektive Analysen verfeinern.
- Best Practices über die Projektteams hinweg teilen.

### Weiterentwicklung der Methodik
- Regelmäßiger Review der Wirksamkeit von Priorisierungsmodellen.
- Update der Risiko-Frameworks basierend auf Branchen-Best-Practices.
- Integration neuer Werkzeuge und Technologien für die Analyse-Effizienz.
- Benchmarking gegen Branchenstandards für die Portfolio-Leistung.

### Stakeholder Feedback Integration
- Quartalsweise Umfragen zur Stakeholder-Zufriedenheit.
- Feedback aus Management-Interviews zur Qualität der Entscheidungsunterstützung.
- Team-Feedback zur Effizienz und Wirksamkeit der Prozesse.
- Bewertung der Auswirkungen von Portfolio-Entscheidungen auf die Kunden.

## Verwandte Skills

- **Product Strategist** (`product-team/product-strategist/`) — Produkt-OKRs richten sich nach den Portfolio-Zielen aus.
- **Scrum Master** (`project-management/scrum-master/`) — Daten zur Sprint-Velocity speisen die Projekt-Gesundheits-Dashboards.

