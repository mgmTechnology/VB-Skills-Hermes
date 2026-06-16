---
name: vb-release-planning
description: Erstellt aus einem geplanten Liveschaltungsdatum einen vollständigen, regelkonformen Release-Plan für die Gruppe Webservices & Strategie.
---

# VB Release Planning

## Ziel

Erstellt aus einem geplanten Liveschaltungsdatum einen vollständigen, regelkonformen Release-Plan für die Gruppe **Webservices & Strategie**. Der Skill plant und prüft Meilensteintermine, kritische Release-Phasen, Urlaubssperren, NRW-Feiertage, NRW-Schulferien, potenzielle Brückentage, bewegliche Ferientage, optionale Teamabwesenheiten sowie Kalender- und Kapazitätsrisiken. Dient ausschließlich der Planung, führt keine Deployments, Freigaben oder produktiven Aktionen aus.

Verwenden bei:
- Ein Release-Termin oder Go-Live-Datum steht fest oder soll geprüft werden
- Ein Release-Plan soll aus einem Go-Live-Datum rückwärts berechnet werden
- Meilensteine und kritische Phasen sollen geplant werden
- Urlaubssperren, Feiertage, Brückentage und NRW-Ferien sollen berücksichtigt werden
- Bei kritischen Terminen sollen alternative Go-Live-Termine vorgeschlagen werden

NICHT verwenden für: tatsächliche Deployments, produktive Aktionen, verbindliche Release-Freigaben.

## Vorgehen

### 1. Eingabedatum prüfen
- Go-Live-Datum parsen, Wochentag bestimmen
- Muss Mittwoch oder Donnerstag sein; bei Freitag: Termin ablehnen und nächsten gültigen vorschlagen

### 2. Planungszeitraum bestimmen
- Go-Live als Tag 0 setzen, Release-Meilensteine gemäß Referenztabelle rückwärts berechnen
- Kalenderprüfzeitraum: frühester Meilenstein minus 14 Tage bis Go-Live plus 14 Tage

### 3. Kalenderdaten laden
- Gesetzliche Feiertage NRW, NRW-Schulferien, potenzielle Brückentage
- Bevorzugt maschinenlesbare Quellen (JSON-API, iCal/ICS)
- Offizielle NRW-Ferienordnung ist fachlich maßgeblich

### 4. Meilensteine berechnen
- Jeden Meilenstein gemäß Referenztabelle rückwärts berechnen
- Auf festen Wochentag justieren, relative Regeln aus Ankermeilensteinen ableiten
- Werktagsberechnungen: Samstag, Sonntag, NRW-Feiertage überspringen
- NRW-Schulferien nicht überspringen, sondern als Kapazitätsrisiko markieren

### 5. Kritische Phasen bestimmen
- Beta-Woche, Finalisierungs-Woche, Go-Live-Tag
- Jede Phase prüfen auf: Schulferien, Feiertage, Brückentage, interne Nicht-Arbeitstage, Abwesenheiten

### 6. Brückentage berechnen
- Aus Feiertagen und Wochenenden: Freitag nach Donnerstag-Feiertag, Montag vor Dienstag-Feiertag
- Standardmäßig nur als Risiko markieren, nicht automatisch als arbeitsfrei

### 7. Interaktive Klärung
- Fragen ob Brückentage als arbeitsfrei behandelt werden sollen
- Fragen nach internen Betriebsruhen, Urlauben von Schlüsselpersonen, beweglichen Ferientagen
- Bei Blockern: nächsten gültigen Termin vorschlagen

### 8. Konsistenz prüfen
- Go-Live ist Mittwoch oder Donnerstag, kein Freitag-Deployment
- Kein Meilenstein auf NRW-Feiertag, Wochentage eingehalten, Reihenfolge plausibel, Konflikte sichtbar

## Regeln / Qualitätskriterien

- Go-Live ist Mittwoch oder Donnerstag, kein Freitag-Deployment
- Gesetzliche NRW-Feiertage werden nicht als normale Arbeitstage behandelt
- NRW-Schulferien werden gegen die offizielle NRW-Ferienordnung validiert
- Brückentage werden nicht ungefragt als arbeitsfrei angenommen
- Bewegliche Ferientage werden nicht erfunden
- Maximal ein lokales Resource-/Referenzfile wird verwendet
- Quelle, Abrufstatus und Annahmen sind sichtbar
- Bei fehlenden oder widersprüchlichen Daten wird interaktiv nachgefragt
- Keine erfundenen Regeln, keine produktiven Aktionen, keine verbindlichen Freigaben
- Entscheidung bleibt bei den Verantwortlichen

## Ressourcen

- `docs/referenzen/Webservices-Strategie/release-planung-regeln.md` — maßgebliche lokale Regeln
- Kalenderdaten: OpenHolidays API, iCal/ICS-Feeds, offizielle NRW-Ferienordnung