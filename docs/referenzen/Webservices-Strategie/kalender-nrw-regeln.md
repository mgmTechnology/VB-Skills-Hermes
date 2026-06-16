# kalender-nrw-regeln.md

## Zweck

Diese Referenz beschreibt, wie der Skill `vb-release-planning`
kalenderabhängige Informationen für Nordrhein-Westfalen behandelt.

Sie umfasst:
- gesetzliche NRW-Feiertage,
- NRW-Schulferien,
- Brückentage,
- bewegliche Ferientage,
- interne Nicht-Arbeitstage,
- Quellenpriorität,
- Fehler- und Fallbackverhalten.

## Grundsatz

Release-Planung bleibt fachliche Planung.
Kalenderdaten unterstützen die Risikoerkennung, ersetzen aber keine
verbindliche Freigabe durch die Verantwortlichen.

## Quellenpriorität

### 1. Maßgebliche Quelle für NRW-Schulferien

Für NRW-Schulferien ist die offizielle Ferienordnung des Landes
Nordrhein-Westfalen fachlich maßgeblich.

Wenn eine technische Quelle andere Daten liefert als die offizielle
NRW-Ferienordnung, ist der Konflikt auszuweisen. Fachlich ist die offizielle
NRW-Ferienordnung vorzuziehen.

### 2. Maschinenlesbare technische Quellen

Für die technische Verarbeitung sind bevorzugt Quellen zu verwenden, die
strukturierte Kalenderdaten liefern:

1. JSON-API
2. iCal/ICS
3. RSS/Atom als Fallback
4. HTML nur zur manuellen Plausibilisierung

RSS ist nur Fallback, weil Ferien und Feiertage Kalenderdaten sind und keine
klassischen Nachrichtenmeldungen.

### 3. Mögliche technische Quellen

Geeignete technische Quellen können sein:

- OpenHolidays API  
  Nutzung: bevorzugte technische Quelle für Feiertage und Ferien, sofern
  verfügbar.

- iCal/ICS-Kalenderfeeds  
  Nutzung: Fallback oder Crosscheck.

- kalender.digital  
  Nutzung: Fallback oder Crosscheck, sofern ein stabiler Feed verfügbar ist.

- uhrzeit.org  
  Nutzung: nur Plausibilisierung, falls keine stabile maschinenlesbare Quelle
  verfügbar ist.

## Relevanter Kalenderzeitraum

Der Skill lädt Kalenderdaten nicht nur für das Go-Live-Datum, sondern für den
gesamten relevanten Release-Planungszeitraum.

```text
kalenderStart = frühester Meilenstein minus 14 Tage
kalenderEnde  = Go-Live plus 14 Tage