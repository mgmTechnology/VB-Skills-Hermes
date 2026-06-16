---
name: "vb-scrum-master"
description: "VB-adaptierter Skill. Ursprung: skills/project-management/scrum-master/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-scrum-master

## VB-Einordnung

Methoden-Skill für Scrum-nahe Teamarbeit, Sprint-Auswertung, Retrospektiven und agile Teamgesundheit.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ursprüngliche Detailanweisung (Referenz)

---

# Scrum Master Experte

Datengetriebener Scrum Master Skill, der Sprint-Analysen, probabilistische Vorhersagen und Coaching zur Teamentwicklung kombiniert. Der besondere Wert liegt in den drei Python-Analyseskripten und deren Workflows — siehe `references/` und `assets/` für tiefere Framework-Details.

---

## Inhaltsverzeichnis

- [Analyse-Werkzeuge & Nutzung](#analyse-werkzeuge-nutzung)
- [Anforderungen an den Input](#anforderungen-an-den-input)
- [Workflows zur Sprint-Durchführung](#workflows-zur-sprint-durchführung)
- [Workflow zur Teamentwicklung](#workflow-zur-teamentwicklung)
- [Wichtige Metriken & Ziele](#wichtige-metriken-ziele)
- [Einschränkungen](#einschränkungen)

---

## Analyse-Werkzeuge & Nutzung

### 1. Velocity Analyzer (`scripts/velocity_analyzer.py`)

Berechnet gleitende Durchschnitte, Trend-Erkennung mittels linearer Regression und Monte-Carlo-Simulationen über die Sprint-Historie.

```bash
# Textbericht
python velocity_analyzer.py sprint_data.json --format text

# JSON-Ausgabe für die Weiterverarbeitung
python velocity_analyzer.py sprint_data.json --format json > analysis.json
```

**Ausgaben**: Velocity-Trend (verbessernd/stabil/rückläufig), Variationskoeffizient (CV), 6-Sprint Monte-Carlo-Vorhersage bei 50 / 70 / 85 / 95% Konfidenzintervallen, Anomalie-Markierungen mit Vorschlägen zur Ursachenanalyse.

**Validierung**: Wenn weniger als 3 Sprints im Input vorhanden sind, stoppen und den Nutzer fragen: *"Die Velocity-Analyse benötigt mindestens 3 Sprints. Bitte stellen Sie zusätzliche Sprint-Daten bereit."* Für statistisch signifikante Monte-Carlo-Ergebnisse werden 6+ Sprints empfohlen.

---

### 2. Sprint Health Scorer (`scripts/sprint_health_scorer.py`)

Bewertet die Teamgesundheit (Health) über 6 gewichtete Dimensionen und erstellt eine Gesamtnote von 0–100.

| Dimension | Gewichtung | Zielwert |
|---|---|---|
| Zuverlässigkeit der Zusage (Commitment Reliability) | 25% | >85% Sprint-Ziele erreicht |
| Umfangsstabilität (Scope Stability) | 20% | <15% Änderungen während des Sprints |
| Blockade-Lösung (Blocker Resolution) | 15% | <3 Tage im Durchschnitt |
| Beteiligung an Zeremonien (Ceremony Engagement) | 15% | >90% Teilnahme |
| Verteilung der Story-Abschlüsse | 15% | Hoher Anteil vollständig erledigter Stories |
| Vorhersehbarkeit der Velocity | 10% | CV <20% |

```bash
python sprint_health_scorer.py sprint_data.json --format text
```

**Ausgaben**: Gesamt-Gesundheitswert + Note, Einzelbewertungen pro Dimension mit Empfehlungen, Trend über die Sprints, Matrix für Interventionsprioritäten.

**Validierung**: Erfordert 2+ Sprints mit Daten zu Zeremonien und Story-Abschlüssen. Falls Daten fehlen, berichten, welche Dimensionen nicht bewertet werden können, und den Nutzer bitten, die Lücken zu füllen.

---

### 3. Retrospective Analyzer (`scripts/retrospective_analyzer.py`)

Verfolgt die Erledigung von Maßnahmen (Action Items), wiederkehrende Themen, Sentiment-Trends und die Entwicklung der Teamreife.

```bash
python retrospective_analyzer.py sprint_data.json --format text
```

**Ausgaben**: Erledigungsrate von Maßnahmen nach Priorität/Verantwortlichem, Persistenzwerte für wiederkehrende Themen, Teamreife-Level (Forming/Storming/Norming/Performing), Trend der Verbesserungsgeschwindigkeit.

**Validierung**: Erfordert 3+ Retrospektiven mit Maßnahmenverfolgung. Bei weniger Retrospektiven auf die Einschränkung hinweisen und nur eine partielle Themenanalyse anbieten.

---

## Anforderungen an den Input

Alle Skripte akzeptieren JSON gemäß dem Schema in `assets/sample_sprint_data.json`:

```json
{
  "team_info": { "name": "string", "size": "number", "scrum_master": "string" },
  "sprints": [
    {
      "sprint_number": "number",
      "planned_points": "number",
      "completed_points": "number",
      "stories": [...],
      "blockers": [...],
      "ceremonies": {...}
    }
  ],
  "retrospectives": [
    {
      "sprint_number": "number",
      "went_well": ["string"],
      "to_improve": ["string"],
      "action_items": [...]
    }
  ]
}
```

Jira und ähnliche Werkzeuge können Sprint-Daten exportieren; die exportierten Felder müssen vor der Ausführung der Skripte auf dieses Schema gemappt werden. Siehe `assets/sample_sprint_data.json` für ein vollständiges 6-Sprint-Beispiel und `assets/expected_output.json` für die entsprechenden erwarteten Ergebnisse (Velocity-Schnitt 20.2 Pkt, CV 12.7%, Health Score 78.3/100, Erledigungsrate Maßnahmen 46.7%).

---

## Workflows zur Sprint-Durchführung

### Sprint Planning

1. Velocity-Analyse ausführen: `python velocity_analyzer.py sprint_data.json --format text`
2. Das 70% Konfidenzintervall als empfohlene Obergrenze für das Commitment im Sprint Backlog verwenden.
3. Die Werte für Commitment Reliability und Scope Stability des Health Scorers prüfen, um die Verhandlung mit dem Product Owner zu kalibrieren.
4. Falls die Monte-Carlo-Ausgabe hohe Volatilität zeigt (CV >20%), dies den Stakeholdern mit Bereichsschätzungen statt Punktvorhersagen kommunizieren.
5. Kapazitätsannahmen (Urlaub, Abhängigkeiten) für den Vergleich in der Retrospektive dokumentieren.

### Daily Standup

1. Teilnahme und Muster bei der Hilfesuche verfolgen — Zeremoniendaten am Sprintende in den `sprint_health_scorer.py` einspeisen.
2. Jede Blockade mit Eröffnungsdatum protokollieren; die Lösungszeit fließt in die Dimension Blocker Resolution ein.
3. Wenn eine Blockade nach 2 Tagen nicht gelöst ist, proaktiv eskalieren und in den Sprint-Daten vermerken.

### Sprint Review

1. Velocity-Trend und Health Score zusammen mit der Demo präsentieren, um den Stakeholdern Lieferkontext zu geben.
2. Während des Reviews geäußerte Änderungswünsche am Scope erfassen; als Scope-Change-Ereignisse in den Sprint-Daten für den nächsten Bewertungszyklus aufzeichnen.

### Sprint Retrospektive

1. Alle drei Skripte vor der Sitzung ausführen:
   ```bash
   python sprint_health_scorer.py sprint_data.json --format text > health.txt
   python retrospective_analyzer.py sprint_data.json --format text > retro.txt
   ```
2. Mit dem Health Score und den am kritischsten markierten Dimensionen eröffnen, um die Diskussion zu fokussieren.
3. Die Erledigungsrate des Retrospective Analyzers nutzen, um zu bestimmen, wie viele neue Maßnahmen das Team realistisch aufnehmen kann (Ziel: ≤3, wenn Erledigungsrate <60%).
4. Jeder Maßnahme einen Verantwortlichen und ein messbares Erfolgskriterium zuweisen, bevor die Sitzung beendet wird.
5. Neue Maßnahmen in `sprint_data.json` erfassen, um sie im nächsten Zyklus zu verfolgen.

---

## Workflow zur Teamentwicklung

### Bewertung (Assessment)

```bash
python sprint_health_scorer.py team_data.json > health_assessment.txt
python retrospective_analyzer.py team_data.json > retro_insights.txt
```

- Die Reife-Ausgabe des Retrospective Analyzers auf die entsprechende Entwicklungsphase mappen.
- Ergänzung durch eine anonyme Umfrage zur psychologischen Sicherheit (Edmondson 7-Punkt-Skala) und individuelle 1:1 Beobachtungen.
- Wenn die Reife-Ausgabe `Forming` oder `Storming` ist, Interventionen zur Sicherheit und Konfliktmoderation vor der Prozessoptimierung priorisieren.

### Intervention

Phasenspezifische Moderation anwenden (Details in `references/team-dynamics-framework.md`):

| Phase | Fokus |
|---|---|
| Forming | Struktur, Prozesstraining, Vertrauensaufbau |
| Storming | Konfliktmoderation, Erhalt der psychologischen Sicherheit |
| Norming | Aufbau von Autonomie, Übertragung der Prozessverantwortung |
| Performing | Einführung von Herausforderungen, Innovationsförderung |

### Fortschrittsmessung

- **Sprint-Rhythmus**: Health Scorer erneut ausführen; Ziel ist eine Verbesserung des Gesamtwertes um ≥5 Punkte pro Quartal.
- **Monatlich**: Umfrage zur psychologischen Sicherheit; Zielwert >4.0/5.0.
- **Quartalsweise**: Vollständige Neubewertung der Reife via Retrospective Analyzer.
- Falls die Werte für 2 aufeinanderfolgende Sprints stagnieren oder sinken, die Interventionsstrategie eskalieren (siehe `references/team-dynamics-framework.md`).

---

## Wichtige Metriken & Ziele

| Metrik | Zielwert |
|---|---|
| Gesamter Health Score | >80/100 |
| Psychologischer Sicherheitsindex | >4.0/5.0 |
| Velocity CV (Vorhersehbarkeit) | <20% |
| Commitment Reliability (Zuverlässigkeit Zusage) | >85% |
| Umfangsstabilität (Scope Stability) | <15% Änderungen im Sprint |
| Lösungszeit für Blockaden | <3 Tage |
| Beteiligung an Zeremonien | >90% |
| Erledigung von Retrospektiv-Maßnahmen | >70% |

---

## Einschränkungen

- **Stichprobengröße**: Weniger als 6 Sprints reduzieren das Vertrauen in Monte-Carlo-Simulationen; immer Konfidenzintervalle statt Punktschätzungen angeben.
- **Datenvollständigkeit**: Fehlende Felder zu Zeremonien oder Story-Abschlüssen unterdrücken betroffene Bewertungsdimensionen — Lücken explizit melden.
- **Kontextsensitivität**: Empfehlungen der Skripte müssen zusammen mit dem organisatorischen und teambezogenen Kontext interpretiert werden, der nicht in den JSON-Daten erfasst ist.
- **Quantitativer Bias**: Metriken ersetzen keine qualitativen Beobachtungen; Bewertungen mit direkter Teaminteraktion kombinieren.
- **Teamgröße**: Die Techniken sind für Teams von 5–9 Mitgliedern optimiert; größere Gruppen erfordern Anpassungen.
- **Externe Faktoren**: Projektübergreifende Abhängigkeiten und organisatorische Einschränkungen werden durch Metriken eines einzelnen Teams nicht vollständig abgebildet.

---

## Verwandte Skills

- **Agile Product Owner** (`product-team/agile-product-owner/`) — User Stories und Backlog speisen das Sprint-Planning.
- **Senior PM** (`project-management/senior-pm/`) — Kontext zur Portfolio-Gesundheit informiert die Sprint-Prioritäten.

---

*Für tiefergehende Framework-Referenzen siehe `references/velocity-forecasting-guide.md` und `references/team-dynamics-framework.md`. Für Vorlagen siehe `assets/sprint_report_template.md` und `assets/team_health_check_template.md`.*

