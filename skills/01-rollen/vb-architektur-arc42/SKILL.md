---
name: vb-architektur-arc42
description: arc42 Template v8.2 DE mit Erläuterungen. VB-adaptiertes Template zur Dokumentation von Software- und Systemarchitekturen.
---

# arc42 Template (VB-adaptiert)

## Ziel
arc42 Template v8.2 DE zur Dokumentation von Software- und Systemarchitekturen. Nach dem Bausteinprinzip — nur relevante Abschnitte übernehmen. Verwenden, wenn eine Software- oder Systemarchitektur dokumentiert werden soll.

## Vorgehen
- Vor dem Befüllen immer die `vb-architektur-randbedingungen` laden, um VB-spezifische Vorgaben zu berücksichtigen.
- Nur die für das Projekt relevanten Abschnitte des arc42-Templates übernehmen.

Die zu befüllenden Abschnitte:

1. **Einführung und Ziele** — Aufgabenstellung, Qualitätsziele (ISO 25010, Top 3-5, priorisiert mit Szenarien), Stakeholder.
2. **Randbedingungen** — Technische, organisatorische und politische Randbedingungen (siehe `vb-architektur-randbedingungen`).
3. **Kontextabgrenzung** — Fachlicher Kontext (Kommunikationsbeziehungen, Ein-/Ausgabedaten) und technischer Kontext (Schnittstellen, Protokolle).
4. **Lösungsstrategie** — Technologieentscheidungen, Top-Level-Zerlegung, Architekturmuster, organisatorische Entscheidungen.
5. **Bausteinsicht** — Whitebox Gesamtsystem (Ebene 1), ggf. Ebenen 2 und 3 mit Begründung der Zerlegung.
6. **Laufzeitsicht** — Wichtige Abläufe/Features, Interaktionen an kritischen Schnittstellen, Betrieb/Administration, Fehlerszenarien.
7. **Verteilungssicht** — Infrastruktur (Standorte, Umgebungen, Rechner), Mapping Software zu Infrastruktur.
8. **Querschnittliche Konzepte** — UX, Sicherheit, Architektur-/Entwurfsmuster, Entwicklungs-/Betriebskonzepte.
9. **Architekturentscheidungen** — Wichtige, riskante Entscheidungen als ADR mit Begründung und Alternativen.
10. **Qualitätsanforderungen** — Qualitätsbaum mit Prioritäten, Qualitätsszenarien.
11. **Risiken und technische Schulden** — Priorisierte Liste mit Maßnahmen.
12. **Glossar** — Fachbegriffe und Definitionen.

## Regeln / Qualitätskriterien
- Nur relevante Abschnitte übernehmen (Bausteinprinzip).
- Immer VB-Randbedingungen vorab prüfen.
- ADR für wichtige Architekturentscheidungen verwenden.

## Ressourcen
- `vb-architektur-randbedingungen` — VB-weite Architekturvorgaben
- https://arc42.org — Original arc42 Template

*Quelle: arc42 Template v8.2 DE (Januar 2023), Dr. Peter Hruschka, Dr. Gernot Starke*