# vb-devscouts-evaluation

## Zweck
Bewertet KI-Tools, KI-Use-Cases und Enablement-Maßnahmen für die IT-Anwendungsentwicklung im Kontext der DevScouts-Initiative. Der Skill erzeugt eine nachvollziehbare Entscheidungsvorlage mit Use-Case-Katalog, Tool-Strategie, Risiko-/Compliance-Bewertung, Schulungskonzept, Stakeholder-Votum und priorisierter Roadmap.

## Wann verwenden
- Bewertung von IntelliJ AI Assistant, Junie, Cursor, Windsurf, Gemini, n8n oder ähnlichen Tools.
- Erstellen eines Use-Case-Katalogs für KI in der Entwicklung.
- Ableitung eines Schulungskonzepts für Einsteiger, Fortgeschrittene, Experten.
- Vorbereitung einer Entscheidung für AL/HAL/IT-Leitung.
- Abstimmung mit ISB, Betriebsrat, KI-Abteilung, IT-Betrieb.

## Wann NICHT verwenden
- Bewertung eines BiPRO-Service; dafür `vb-bipro-analysis`.
- Diagnose eines Webservicefehlers; dafür `vb-webservice-diagnostics`.
- Release-Finalisierung; dafür `vb-release-finalization`.


## Verbindliche Referenzen
Nutze bei Bedarf diese lokalen Referenzen im Repository:

- `docs/referenzen/DevScouts/basisinformationen-zur-arbeitsgruppe.txt`
- `docs/referenzen/DevScouts/ki-einfuehrung-phasen.docx`
- `docs/referenzen/DevScouts/REFERENZEN.md`

Regel: Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`. Erfinde keine VB-Standards.


## Benötigte Eingaben
- Tool oder Use Case.
- Zielgruppe und Einsatzkontext.
- Daten-/Code-Kontext: intern, vertraulich, personenbezogen, produktiv, synthetisch.
- Integrationsbedarf: IntelliJ, Cursor, GitLab, Jira, Confluence, n8n.
- bekannte Vorgaben von ISB, Betriebsrat, KI-Abteilung oder Datenschutz.

## Vorgehen

### 1. Bewertungsgegenstand abgrenzen
Kläre:

- Tool, Use Case oder Schulungsmaßnahme?
- Pilot, Markt-Screening oder Entscheidungsvorlage?
- AE-spezifische Zuarbeit oder Unternehmens-Governance?
- Beschaffung ja/nein? Hinweis: finale Beschaffung/Lizenzkauf ist nicht Bestandteil der AG-Phase.

### 2. Use Cases strukturieren
Erstelle einen Use-Case-Katalog:

| Use Case | Zielgruppe | Geschäftlicher Hebel | Datenrisiko | Tool-Fit | Reifegrad |
|---|---|---|---|---|---|
| Code-Generierung | Entwickler |  |  |  |  |
| Tests | Entwickler/QA |  |  |  |  |
| Refactoring | Entwickler |  |  |  |  |
| Dokumentation | Team/Onboarding |  |  |  |  |
| Prozessoptimierung/n8n | Fach/IT |  |  |  |  |

### 3. Tool-Bewertung durchführen
Bewerte mindestens:

| Kriterium | Leitfrage |
|---|---|
| Security | Kann das Tool in geschütztem Rahmen genutzt werden? |
| Datenschutz | Werden personenbezogene oder vertrauliche Daten verarbeitet? |
| Cloud-Policy | Passt das Betriebsmodell zu den Vorgaben? |
| Entwicklerproduktivität | Welcher konkrete Zeit-/Qualitätshebel ist plausibel? |
| Integration | IntelliJ, Junie, Cursor, GitLab, Jira, Confluence? |
| Kontrollierbarkeit | Logging, Admin, Policies, Rechte? |
| Akzeptanz | Wie reagieren Entwickler, Betriebsrat, Führung? |
| Schulungsaufwand | Welche Trainingsmodule sind nötig? |
| Kosten/Nutzen | Grobe Wirtschaftlichkeit und Skalierbarkeit? |

### 4. Stakeholder-Votum vorbereiten
Berücksichtige:

- IT-AE Entwickler: Bedarf und Akzeptanz.
- KI-Abteilung: Konzernstrategie.
- ISB/Datensicherheit: Datenschutz, Cloud-Policy.
- Betriebsrat: Verhaltens-/Leistungskontrolle.
- IT-Betrieb: Tool-Bereitstellung, Sandboxen.
- IT-Leitung: Entscheidung und Budget.

### 5. Pilot- und Enablement-Plan erstellen
Nutze Phasenlogik:

#### Phase 1 – Analyse und Zieldefinition
- Brainstorming, SIPOC, Multivoting.
- Stakeholder-Interviews, Gap-Analyse.
- Priorisierung mit SWOT/Pareto.

#### Phase 2 – Planung und Pilotprojekte
- Pilotumfang definieren.
- Risiken mit FMEA bewerten.
- PDCA-Zyklus für Pilotbetrieb.
- KPIs definieren.

#### Phase 3 – Skalierung und Verbesserung
- Lessons Learned.
- Regelkarten/KPIs für Stabilität.
- Retrospektiven.
- Übertragung auf weitere Use Cases.

### 6. Entscheidungsvorlage formulieren
Empfehlung muss eine der Kategorien haben:

- `beibehalten`
- `erweitern`
- `ergänzen`
- `pilotieren`
- `nicht einsetzen`
- `zurückstellen bis Klärung`

## Output-Format

```markdown
# DevScouts Bewertung

## 1. Kurzempfehlung
## 2. Bewertungsgegenstand
## 3. Use-Case-Katalog
## 4. Tool-Bewertung
## 5. Risiken / Compliance / Datenschutz
## 6. Stakeholder-Votum
## 7. Schulungs- und Enablement-Konzept
## 8. Pilotplan
## 9. Roadmap
## 10. Offene Entscheidungen
```

## Qualitätskriterien
- Entscheidung ist nachvollziehbar und stakeholderfähig.
- Security, Datenschutz und Betriebsrat werden nicht nachgelagert behandelt.
- Use Cases sind priorisiert, nicht nur gesammelt.
- Schulungskonzept unterscheidet Einsteiger, Fortgeschrittene und Experten.
- Empfehlung trennt Pilot, Skalierung und Beschaffung.

## Typische Fehler
- Tools nur nach Features vergleichen.
- Datenschutz und Betriebsrat zu spät einbinden.
- Keine messbaren Erfolgskriterien definieren.
- Schulungskonzept mit Tool-Einweisung verwechseln.
