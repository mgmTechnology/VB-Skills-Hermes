---
name: vb-senior-pm
description: "VB-adaptierter Skill für Projektmanagement, Portfolio-Betrachtungen, Risiken, Ressourcen und Management-Reporting. Ursprung: skills/project-management/senior-pm/SKILL.md."
---

# VB Senior Projektmanagement

## Ziel

Strategisches Projektmanagement für Unternehmenssoftware und digitale Transformationsinitiativen – Portfolio-Gesundheit, quantitatives Risikomanagement und Management-Reporting. Wird verwendet für Portfolio-Reviews, Risikobewertungen, Ressourcenplanung und strategische Entscheidungsunterstützung. Dieser Skill ist in die VB-Skill-Struktur übernommen; nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard. Vor schreibenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

## Vorgehen

### Portfolio-Gesundheitsbewertung (wöchentlich)

1. Daten erheben und validieren:
   ```bash
   python3 scripts/project_health_dashboard.py current_portfolio.json
   ```
   ⚠️ Bei Gesamtwert <60 oder fehlenden kritischen Feldern: STOPP, Datenintegrität klären

2. Risikobewertung aktualisieren:
   ```bash
   python3 scripts/risk_matrix_analyzer.py current_portfolio.json
   ```
   ⚠️ Bei Risikowert >18 (Schwelle "Vermeiden"): STOPP, Eskalation an Projektsponsor

3. Kapazitätsanalyse:
   ```bash
   python3 scripts/resource_capacity_planner.py current_portfolio.json
   ```
   ⚠️ Bei Teamauslastung >90% oder <60%: sofortige Umverteilungsdiskussion

4. Management-Zusammenfassung erstellen: Ergebnisse synthetisieren, kritische Issues + Empfehlungen hervorheben

### Gesundheitsdimensionen (gewichtet)

- **Zeitplan** (25%): Meilensteine, kritischer Pfad
- **Budget** (25%): Abweichung, Prognosegenauigkeit
- **Scope** (20%): Feature-Abschluss, Änderungskontrolle
- **Qualität** (20%): Testabdeckung, Fehlerdichte, technische Schulden
- **Risiko** (10%): Risikowert, Wirksamkeit der Schadensbegrenzung

### RAG-Status

- 🟢 Grün: Gesamt >80, alle Dimensionen >60
- 🟡 Gelb: Gesamt 60–80 oder eine Dimension 40–60
- 🔴 Rot: Gesamt <60 oder eine Dimension <40

### Risikomanagement

**Quantitativer Prozess:**
1. Wahrscheinlichkeit (1–5) und Auswirkung (1–5) bewerten
2. Kategorie-Gewichtung anwenden: Technisch (1.2x), Ressourcen (1.1x), Finanziell (1.4x), Zeitplan (1.0x)
3. EMV berechnen: EMV = Wahrscheinlichkeit × finanzielle_Auswirkung
4. Risikobereinigtes Budget: Basis-Budget × (1 + Risikoprämie)

**Risikoantwort nach Score:**
- Vermeiden (>18): durch Scope-Änderung eliminieren
- Mindern (12–18): Wahrscheinlichkeit/Auswirkung reduzieren
- Übertragen (8–12): Versicherung, Verträge
- Akzeptieren (<8): beobachten mit Notfallplan

**Risikobereitschaft:**
- Konservativ (0–8): 25–30% Reserve
- Moderat (8–15): 15–20% Reserve
- Aggressiv (15+): 10–15% Reserve

### Priorisierungsmodelle

- **WSJF**: ressourcenbeschränkte agile Portfolios mit quantifizierbaren Verzögerungskosten → `(UserValue + TimeCriticality + RiskReduction) / JobSize`
- **RICE**: kundenorientierte Initiativen → `(Reach × Impact × Confidence%) / Effort`
- **ICE**: schnelle Priorisierung, Brainstorming → `(Impact + Confidence + Ease) / 3`
- **MoSCoW**: mehrere Stakeholdergruppen mit unterschiedlichen Prioritäten
- **MCDA**: komplexe Abwägungen über nicht vergleichbare Kriterien

Referenz: `references/portfolio-prioritization-models.md`

### Monatlicher strategischer Review

1. Portfolio-Priorisierung mit WSJF/RICE/ICE bewerten
2. Risiko-Portfolio: Risikobereitschaft, Toleranzschwellen, Korrelationen prüfen
3. Ressourcenoptimierung für kommendes Quartal planen, Skill-Gaps identifizieren
4. Stakeholder-Abstimmung: Gesundheit präsentieren, Feedback einholen, Prioritäten abstimmen

### Quartalsweise Portfolio-Optimierung

1. Strategische Ausrichtung an Geschäftszielen bewerten
2. Finanzielle Leistung: risikobereinigten ROI analysieren, Investitionsallokation optimieren
3. Fähigkeitslücken identifizieren, Make-vs-Buy-vs-Partner bewerten
4. Portfolio-Rebalancing: Drei-Horizonte-Modell (70% operativ / 20% Wachstum / 10% transformativ)

### Übergabeprotokolle

- **An Scrum Master**: strategische Prioritäten, Ressourcenzuweisung, Risikofaktoren für Sprint-Ebene
- **An Product Owner**: Marktpriorisierung, ROI-Analyse, Feature-Priorisierung
- **Von Geschäftsführung**: strategische Richtung, Budgetallokation, Risikobereitschaft

## Regeln / Qualitätskriterien

### Portfolio-Leistungs-KPIs

| Metrik | Zielwert |
|---|---|
| Pünktliche Lieferung | >80% innerhalb 10% des Plans |
| Budgetabweichung | <5% Durchschnitt |
| Qualitätsscore | >85 |
| Risikoabdeckung | >90% mit aktiven Plänen |
| Ressourcenauslastung | 75–85% |
| ROI-Erreichung | >90% innerhalb 12 Monate |
| Strategische Ausrichtung | >95% an Geschäftsprioritäten |

### Risikomanagement-KPIs

| Metrik | Zielwert |
|---|---|
| Risikoexposition | innerhalb genehmigter Bereiche |
| Lösungszeit (mittel) | <30 Tage |
| Lösungszeit (hoch) | <7 Tage |
| Kosteneffizienz Minderung | <20% des Portfolio-EMV |
| Vorhersagegenauigkeit | >70% |

## Ressourcen

- `scripts/project_health_dashboard.py` – multidimensionale Gesundheitsbewertung
- `scripts/risk_matrix_analyzer.py` – quantitative Risikobewertung + EMV
- `scripts/resource_capacity_planner.py` – Portfolio-Ressourcenanalyse
- `assets/sample_project_data.json` – Beispiel-Portfolio-Daten
- `assets/expected_output.json` – Erwartete Ergebnisse
- `assets/project_charter_template.md` – Projekt-Charter Vorlage
- `assets/executive_report_template.md` – Management-Bericht Vorlage
- `assets/raci_matrix_template.md` – RACI-Matrix Vorlage
- `references/portfolio-prioritization-models.md` – Priorisierungsmodelle
- `references/risk-management-framework.md` – Risikomanagement-Framework
- `references/portfolio-kpis.md` – KPI-Definitionen
