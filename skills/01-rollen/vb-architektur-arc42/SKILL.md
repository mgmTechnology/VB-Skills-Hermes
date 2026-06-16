---
name: vb-architektur-arc42
description: arc42 Template v8.2 DE mit Erlaeuterungen. VB-adaptiertes Template zur Dokumentation von Software- und Systemarchitekturen.
---

# arc42 Template (VB-adaptiert)

arc42 Template v8.2 DE zur Dokumentation von Software- und Systemarchitekturen. Nach dem Bausteinprinzip — nur relevante Abschnitte uebernehmen.

> **Wichtig**: Vor dem Befuellen immer die `vb-architektur-randbedingungen` laden, um VB-spezifische Vorgaben zu beruecksichtigen.

## 1. Einfuehrung und Ziele

### 1.1 Aufgabenstellung
- Kurzbeschreibung der fachlichen Aufgabenstellung
- Extrakt der Anforderungen mit Verweis auf Anforderungsdokumente

### 1.2 Qualitaetsziele
- Top-3 bis Top-5 Qualitaetsanforderungen (ISO 25010)
- Moeglichst konkret mit Szenarien, priorisiert

### 1.3 Stakeholder
| Rolle | Kontakt | Erwartungshaltung |
|---|---|---|
| ... | ... | ... |

## 2. Randbedingungen

Technische, organisatorische und politische Randbedingungen. **Siehe `vb-architektur-randbedingungen` fuer VB-weite Vorgaben.**

## 3. Kontextabgrenzung

### 3.1 Fachlicher Kontext
- Alle Kommunikationsbeziehungen (Nutzer, IT-Systeme)
- Fachliche Ein- und Ausgabedaten, Schnittstellen

### 3.2 Technischer Kontext
- Technische Schnittstellen (Kanaele, Uebertragungsmedien)
- Mapping fachliche auf technische Schnittstellen

## 4. Loesungsstrategie

- Technologieentscheidungen
- Top-Level-Zerlegung, Architekturmuster
- Entscheidungen zur Erreichung der Qualitaetsanforderungen
- Organisatorische Entscheidungen

## 5. Bausteinsicht

### 5.1 Whitebox Gesamtsystem (Ebene 1)
- Uebersichtsdiagramm, Begruendung der Zerlegung
- Blackbox-Beschreibungen der enthaltenen Bausteine
- Wichtige Schnittstellen

### 5.2 Ebene 2
- Whitebox ausgewaehlter Bausteine aus Ebene 1

### 5.3 Ebene 3
- Whitebox ausgewaehlter Bausteine aus Ebene 2

## 6. Laufzeitsicht

- Wichtige Ablaeufe / Features
- Interaktionen an kritischen externen Schnittstellen
- Betrieb und Administration (Start, Stop)
- Fehler- und Ausnahmeszenarien

## 7. Verteilungssicht

### 7.1 Infrastruktur Ebene 1
- Verteilung auf Standorte, Umgebungen, Rechner
- Physische Verbindungskanaele
- Zuordnung von Softwareartefakten zu Infrastruktur

### 7.2 Infrastruktur Ebene 2
- Innerer Aufbau einzelner Infrastrukturelemente

## 8. Querschnittliche Konzepte

- Fachliche Konzepte, UX
- Sicherheitskonzepte (Safety und Security)
- Architektur- und Entwurfsmuster
- Entwicklungs- und Betriebskonzepte

## 9. Architekturentscheidungen

- Wichtige, teure, grosse oder riskante Entscheidungen
- ADR (Architecture Decision Records) empfohlen
- Jeweils mit Begruendung und Alternativen

## 10. Qualitaetsanforderungen

### 10.1 Qualitaetsbaum
- Baumartige Verfeinerung mit Prioritaeten

### 10.2 Qualitaetsszenarien
- Nutzungsszenarien (Performance, Effizienz)
- Aenderungsszenarien (Modifikationen)

## 11. Risiken und technische Schulden

- Nach Prioritaeten geordnete Liste
- Vorgeschlagene Massnahmen zur Risikovermeidung

## 12. Glossar

| Begriff | Definition |
|---|---|
| ... | ... |

---

*Quelle: arc42 Template v8.2 DE (Januar 2023), erstellt von Dr. Peter Hruschka, Dr. Gernot Starke*
*https://arc42.org*