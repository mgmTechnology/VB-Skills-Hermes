---
name: vb-scrum-master
description: "VB-adaptierter Skill für Scrum-nahe Teamarbeit, Sprint-Analysen, probabilistische Vorhersagen und Teamentwicklung. Ursprung: skills/project-management/scrum-master/SKILL.md."
---

# VB Scrum Master

## Ziel

Datengetriebener Scrum-Master-Skill für Sprint-Analysen, Velocity-Prognosen und Coaching zur Teamentwicklung. Wird verwendet für Sprint Planning, Daily Standups, Reviews und Retrospektiven. Dieser Skill ist in die VB-Skill-Struktur übernommen; nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard. Vor schreibenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

## Vorgehen

### Sprint Planning

1. Velocity-Analyse: `python velocity_analyzer.py sprint_data.json --format text`
2. 70%-Konfidenzintervall als empfohlene Obergrenze für das Sprint-Commitment verwenden
3. Commitment Reliability und Scope Stability des Health Scorers prüfen
4. Bei hoher Volatilität (CV >20%): Bereichsschätzungen statt Punktvorhersagen kommunizieren
5. Kapazitätsannahmen dokumentieren

### Daily Standup

1. Teilnahme und Hilfemuster verfolgen → in Health Scorer einspeisen
2. Jede Blockade mit Eröffnungsdatum protokollieren
3. Blockaden nach 2 Tagen proaktiv eskalieren

### Sprint Review

1. Velocity-Trend und Health Score gemeinsam mit der Demo präsentieren
2. Scope-Änderungen erfassen und für nächsten Bewertungszyklus aufzeichnen

### Sprint Retrospektive

1. Vor der Sitzung ausführen:
   ```bash
   python sprint_health_scorer.py sprint_data.json --format text > health.txt
   python retrospective_analyzer.py sprint_data.json --format text > retro.txt
   ```
2. Mit Health Score und kritischsten Dimensionen eröffnen
3. Erledigungsrate nutzen: Ziel ≤3 neue Maßnahmen wenn Rate <60%
4. Jeder Maßnahme Verantwortlichen + messbares Erfolgskriterium zuweisen
5. Neue Maßnahmen in sprint_data.json erfassen

### Teamentwicklung

- Reife-Ausgabe des Retrospective Analyzer auf Entwicklungsphase mappen (Forming → Storming → Norming → Performing)
- Bei Forming/Storming: Sicherheit und Konfliktmoderation vor Prozessoptimierung priorisieren
- Phasenspezifische Moderation anwenden (Details: `references/team-dynamics-framework.md`)

### Analyse-Werkzeuge

**Velocity Analyzer** (`scripts/velocity_analyzer.py`):
- Berechnet gleitende Durchschnitte, Trend-Erkennung (lineare Regression), Monte-Carlo-Simulationen
- Ausgaben: Velocity-Trend, Variationskoeffizient (CV), 6-Sprint-Vorhersage (50/70/85/95%), Anomalie-Markierungen
- Mindestens 3 Sprints erforderlich; 6+ für statistisch signifikante Ergebnisse

**Sprint Health Scorer** (`scripts/sprint_health_scorer.py`):
- 6 gewichtete Dimensionen (0–100): Commitment Reliability (25%), Scope Stability (20%), Blocker Resolution (15%), Ceremony Engagement (15%), Story Completion (15%), Velocity Predictability (10%)
- 2+ Sprints erforderlich

**Retrospective Analyzer** (`scripts/retrospective_analyzer.py`):
- Verfolgt Maßnahmen-Erledigung, wiederkehrende Themen, Sentiment-Trends, Teamreife
- 3+ Retrospektiven erforderlich

### Input-Schema

Alle Skripte erwarten JSON gemäß `assets/sample_sprint_data.json`:
```json
{
  "team_info": { "name": "string", "size": "number", "scrum_master": "string" },
  "sprints": [{ "sprint_number": "number", "planned_points": "number", "completed_points": "number", "stories": [...], "blockers": [...], "ceremonies": {...} }],
  "retrospectives": [{ "sprint_number": "number", "went_well": ["string"], "to_improve": ["string"], "action_items": [...] }]
}
```

## Regeln / Qualitätskriterien

### Metriken & Ziele

| Metrik | Zielwert |
|---|---|
| Health Score | >80/100 |
| Psychologische Sicherheit | >4.0/5.0 |
| Velocity CV | <20% |
| Commitment Reliability | >85% |
| Scope Stability | <15% Änderungen |
| Blocker-Lösungszeit | <3 Tage |
| Ceremony-Beteiligung | >90% |
| Maßnahmen-Erledigung | >70% |

### Einschränkungen

- <6 Sprints reduzieren Vertrauen in Monte-Carlo-Simulationen → Konfidenzintervalle statt Punktschätzungen
- Fehlende Felder unterdrücken betroffene Bewertungsdimensionen → Lücken explizit melden
- Metriken ersetzen keine qualitativen Beobachtungen
- Für Teams von 5–9 Mitgliedern optimiert
- Externe Faktoren werden durch Einzelteam-Metriken nicht vollständig abgebildet

## Ressourcen

- `scripts/velocity_analyzer.py` – Velocity-Trend, Monte-Carlo-Simulation
- `scripts/sprint_health_scorer.py` – 6-dimensionale Team-Gesundheitsbewertung
- `scripts/retrospective_analyzer.py` – Maßnahmenverfolgung, Teamreife
- `assets/sample_sprint_data.json` – Beispiel-Sprint-Daten
- `assets/expected_output.json` – Erwartete Ergebnisse
- `references/team-dynamics-framework.md` – Teamentwicklungs-Framework
- `references/velocity-forecasting-guide.md` – Velocity-Prognose-Leitfaden
