---
name: vb-release-planning
gruppe: Webservices & Strategie
status: Entwurf
version: 0.2
---

# vb-release-planning

## Zweck

Erstellt aus einem geplanten Liveschaltungsdatum einen vollständigen, regelkonformen Release-Plan für die Gruppe **Webservices & Strategie**.

Der Skill plant und prüft:

- Meilensteintermine,
- kritische Release-Phasen,
- Urlaubssperren,
- NRW-Feiertage,
- NRW-Schulferien,
- potenzielle Brückentage,
- bewegliche Ferientage, sofern bekannt,
- optionale Teamabwesenheiten,
- Kalender- und Kapazitätsrisiken,
- optionale Alternativtermine.

Der Skill dient ausschließlich der Planung. Er führt keine Deployments, Freigaben oder produktiven Aktionen aus.

## Gruppenkontext

Gruppe **Webservices & Strategie**  
Bereich: **IT-AE, Lebensversicherungen**

## Wann verwenden

- Ein Release-Termin oder Go-Live-Datum steht fest oder soll geprüft werden.
- Ein Release-Plan soll aus einem Go-Live-Datum rückwärts berechnet werden.
- Meilensteine und kritische Phasen sollen geplant werden.
- Urlaubssperren sollen sichtbar gemacht werden.
- Feiertage, Brückentage und NRW-Ferien sollen in der Planung berücksichtigt werden.
- Es soll geprüft werden, ob ein Release-Termin aus Kalender- oder Kapazitätssicht kritisch ist.
- Bei kritischen Terminen sollen alternative Go-Live-Termine vorgeschlagen werden.

## Wann nicht verwenden

- Nicht für tatsächliche Deployments.
- Nicht für produktive Aktionen.
- Nicht für verbindliche Release-Freigaben.
- Nicht für Gruppen mit abweichenden Release-Regeln.
- Nicht für verbindliche Aussagen zur tatsächlichen Personalverfügbarkeit ohne Bestätigung durch die Verantwortlichen.

## Referenzgrundlage

Es soll maximal **ein lokales Resource-/Referenzfile** verwendet werden:

```text
docs/referenzen/Webservices-Strategie/release-planung-regeln.md
```

Dieses Referenzfile enthält die maßgeblichen lokalen Regeln für:

- Release-Meilensteine,
- feste Wochentage,
- relative Terminregeln,
- kritische Phasen,
- Urlaubssperren,
- Kalenderlogik NRW,
- Quellenpriorität für Feiertage und Ferien,
- Fallback- und Fehlerverhalten.

Regel:

Aussagen, die nicht aus dieser Referenz oder aus den dynamisch geladenen Kalenderdaten ableitbar sind, sind als `offen`, `Annahme` oder `zu prüfen` zu kennzeichnen.

Keine Regeln erfinden.

## Externe Kalendergrundlagen

Der Skill darf Kalenderdaten dynamisch laden oder aus einem geprüften Cache verwenden.

Für NRW-Schulferien ist die **offizielle Ferienordnung des Landes Nordrhein-Westfalen** fachlich maßgeblich.

Für die technische Verarbeitung sollen bevorzugt maschinenlesbare Quellen verwendet werden:

1. JSON-API
2. iCal/ICS
3. RSS/Atom nur als Fallback
4. HTML-Seiten nur zur Plausibilisierung

RSS ist nicht der bevorzugte Standard, weil Feiertage und Ferien Kalenderdaten sind. JSON oder iCal/ICS sind für maschinelle Verarbeitung geeigneter.

Geeignete technische Quellen können sein:

- OpenHolidays API für Feiertage und Schulferien,
- iCal/ICS-Kalenderfeeds für Feiertage und Ferien,
- kalender.digital als Fallback oder Crosscheck,
- uhrzeit.org nur zur visuellen Plausibilisierung, sofern kein stabiler maschinenlesbarer Feed verfügbar ist.

Bei widersprüchlichen Ferienangaben ist die offizielle NRW-Ferienordnung fachlich vorzuziehen.

## Verwendung

Der Skill wird verwendet, indem ein geplantes Go-Live-Datum angegeben wird.

- Das Go-Live-Datum muss Mittwoch oder Donnerstag sein.
- Der Skill prüft den Termin, berechnet Meilensteine rückwärts und bewertet Kalender- und Kapazitätsrisiken.
- NRW-Feiertage werden als Nicht-Arbeitstage behandelt.
- NRW-Schulferien werden als Kapazitätsrisiko markiert.
- Die offizielle NRW-Ferienordnung ist fachlich maßgeblich.
- Brückentage werden zunächst nur als Risiko markiert, sofern nichts anderes angegeben ist.
- Bewegliche Ferientage und Teamurlaube werden nur berücksichtigt, wenn sie angegeben sind.

### Beispielprompt

```text
Nutze den Skill vb-release-planning.

Plane bitte einen Release für Webservices & Strategie.

Go-Live: Donnerstag, 25.06.2026

Rahmen:
- NRW-Feiertage als Nicht-Arbeitstage behandeln.
- NRW-Schulferien als Kapazitätsrisiko markieren.
- Die offizielle NRW-Ferienordnung ist maßgeblich.
- Brückentage zunächst nur als Risiko markieren.
- Bewegliche Ferientage sind nicht bekannt.
- Teamurlaube sind noch nicht geprüft.

Bitte liefere:
1. Ergebnisbewertung,
2. Meilensteintabelle,
3. kritische Phasen / Urlaubssperre,
4. Kalender- und Kapazitätsrisiken,
5. offene Punkte,
6. konkrete Rückfragen,
7. falls nötig alternative Go-Live-Termine.
```

## Benötigte Eingaben

### Pflichtangabe

- Liveschaltungsdatum / Go-Live-Datum.

Das Go-Live-Datum muss ein Mittwoch oder Donnerstag sein.

### Optionale Angaben

- Soll ein Kick-off berücksichtigt werden?
- Sollen Brückentage nur markiert oder als arbeitsfrei behandelt werden?
- Gibt es bekannte interne Nicht-Arbeitstage oder Betriebsruhe?
- Gibt es bekannte Urlaube von Schlüsselpersonen?
- Sind bewegliche Ferientage bekannt?
- Sollen bei Ferien- oder Feiertagskonflikten alternative Go-Live-Termine berechnet werden?
- Soll ein textueller Zeitstrahl erzeugt werden?

## Standardannahmen

Wenn keine Rückfrage möglich ist, gelten folgende Annahmen:

```text
Gesetzliche NRW-Feiertage werden als Nicht-Arbeitstage behandelt.
NRW-Schulferien werden als Kapazitätsrisiko markiert.
Brückentage werden nur als Risiko markiert, nicht automatisch als arbeitsfrei.
Bewegliche Ferientage sind nicht bekannt.
Interne Nicht-Arbeitstage sind nicht bekannt.
Teamurlaube sind nicht geprüft.
```

Diese Annahmen sind im Ergebnis sichtbar auszuweisen.

## Vorgehen

### 1. Eingabedatum prüfen

1. Go-Live-Datum parsen.
2. Wochentag bestimmen.
3. Prüfen, ob das Datum ein Mittwoch oder Donnerstag ist.
4. Falls das Datum ein Freitag oder anderer Wochentag ist:
    - Termin ablehnen.
    - Grundregel nennen: kein Freitag-Deployment bzw. Go-Live nur Mittwoch oder Donnerstag.
    - nächsten gültigen Mittwoch oder Donnerstag vorschlagen.
    - zusätzlich prüfen, ob der Alternativtermin Feiertags-, Ferien- oder Brückentagsrisiken enthält.

### 2. Planungszeitraum bestimmen

1. Go-Live als Tag 0 setzen.
2. Release-Meilensteine gemäß Referenztabelle rückwärts berechnen.
3. Frühesten Meilenstein bestimmen.
4. Kalenderprüfzeitraum erweitern:

```text
kalenderStart = frühester Meilenstein minus 14 Tage
kalenderEnde  = Go-Live plus 14 Tage
```

5. Wenn der Zeitraum mehrere Kalenderjahre umfasst, alle betroffenen Jahre laden.

### 3. Kalenderdaten laden

Kalenderdaten abhängig vom relevanten Planungszeitraum laden:

- gesetzliche Feiertage NRW,
- NRW-Schulferien,
- potenzielle Brückentage berechnen,
- bewegliche Ferientage nur berücksichtigen, wenn angegeben,
- interne Nicht-Arbeitstage nur berücksichtigen, wenn angegeben oder in der Referenz enthalten.

Jeder Kalendereintrag wird intern normalisiert:

```yaml
calendarEvent:
  name: "Fronleichnam"
  type: "PUBLIC_HOLIDAY"
  startDate: "2026-06-04"
  endDate: "2026-06-04"
  state: "NRW"
  source: "OpenHolidays API"
  sourceType: "JSON"
  sourceConfidence: "hoch"
  loadedAt: "YYYY-MM-DD"
  notes: ""
```

Erlaubte Typen:

```text
PUBLIC_HOLIDAY
SCHOOL_HOLIDAY
BRIDGE_DAY
MOVABLE_SCHOOL_DAY
COMPANY_CLOSURE
UNKNOWN
```

### 4. Meilensteine berechnen

Jeden Meilenstein gemäß Referenztabelle rückwärts berechnen:

1. Groben Abstand in Tagen vor Go-Live anwenden.
2. Auf den festen Wochentag justieren.
3. Relative Regeln aus bereits berechneten Ankermeilensteinen ableiten:
    - z. B. 1 Werktag vor Beta,
    - 3 Werktage vor Finalisierung,
    - Montag vor Beta-Version.
4. Bei Werktagsberechnungen folgende Tage überspringen:
    - Samstag,
    - Sonntag,
    - gesetzliche NRW-Feiertage,
    - bestätigte interne Nicht-Arbeitstage,
    - bestätigte arbeitsfreie Brückentage.
5. NRW-Schulferien nicht automatisch überspringen, sondern als Kapazitätsrisiko markieren.
6. Nicht bestätigte Brückentage nicht automatisch überspringen, sondern als Risiko markieren.

### 5. Kritische Phasen bestimmen

Folgende kritische Phasen bestimmen:

- Beta-Woche = Montag bis Freitag der Woche der Beta-Version.
- Finalisierungs-Woche = Montag bis Freitag der Woche vor Go-Live.
- Go-Live-Tag.
- Optional: erweiterte Stabilisierungsphase nach Go-Live, wenn in der Referenz vorgesehen.

Für jede kritische Phase prüfen:

- Liegt sie ganz oder teilweise in NRW-Schulferien?
- Enthält sie einen gesetzlichen NRW-Feiertag?
- Enthält sie einen potenziellen Brückentag?
- Enthält sie einen bestätigten internen Nicht-Arbeitstag?
- Liegt sie direkt vor oder nach einem langen Wochenende?
- Sind bekannte Schlüsselpersonen abwesend?

### 6. Brückentage berechnen

Potenzielle Brückentage werden aus Feiertagen und Wochenenden berechnet.

Regeln:

- Freitag nach einem Donnerstag-Feiertag,
- Montag vor einem Dienstag-Feiertag,
- Arbeitstag zwischen Feiertag und Wochenende,
- Arbeitstag zwischen zwei arbeitsfreien Tagen.

Brückentage sind standardmäßig keine harten Blocker.

Standardklassifikation:

```text
Brückentage werden nur als Risiko markiert, nicht automatisch als arbeitsfrei.
```

Wenn Brückentage im relevanten Zeitraum liegen, interaktiv fragen:

```text
Im Planungszeitraum liegen potenzielle Brückentage.
Soll ich diese Tage als arbeitsfrei behandeln oder nur als Kapazitätsrisiko markieren?

Option 1: nur als Risiko markieren
Option 2: als arbeitsfrei behandeln
Option 3: einzeln entscheiden
```

### 7. NRW-Schulferien behandeln

NRW-Schulferien sind kein automatischer Blocker.

Behandlung:

- Release bleibt formal möglich.
- Ferien werden als Kapazitätsrisiko markiert.
- Überschneidung mit Beta-Woche, Finalisierungs-Woche oder Go-Live-Woche ist ein hohes Risiko.
- Bei Ferienüberschneidung interaktiv fragen, ob alternative Go-Live-Termine außerhalb der Ferien berechnet werden sollen.

Standardfrage:

```text
Der Release-Plan überschneidet sich mit NRW-Schulferien.
Soll ich den Plan beibehalten und als Risiko markieren oder alternative Go-Live-Termine außerhalb der Ferien berechnen?
```

Für die fachliche Bewertung der Ferienzeiträume ist die offizielle NRW-Ferienordnung maßgeblich.

### 8. Bewegliche Ferientage behandeln

Bewegliche Ferientage sind nicht landesweit eindeutig.

Behandlung:

- nur verwenden, wenn vom Anwender angegeben oder in der Referenz gepflegt,
- nicht aus NRW-Schulferien ableiten,
- nicht erfinden,
- bei fehlender Information als offener Punkt markieren.

Standardhinweis:

```text
Bewegliche Ferientage sind nicht landesweit eindeutig bekannt.
Bitte prüfen, ob für relevante Mitarbeitende oder Standorte bewegliche Ferientage betroffen sind.
```

### 9. Interaktive Klärung

Der Skill soll gezielt Rückfragen stellen, wenn Entscheidungen oder Daten fehlen.

#### Immer fragen, wenn relevant

- Sollen Brückentage als arbeitsfrei behandelt oder nur als Risiko markiert werden?
- Sind interne Betriebsruhe oder reduzierte Besetzung bekannt?
- Gibt es bekannte Urlaube von Schlüsselpersonen in Beta-, Finalisierungs- oder Go-Live-Woche?
- Sind bewegliche Ferientage relevant oder bekannt?
- Soll bei einem Konflikt der Go-Live verschoben oder nur ein Risiko-Hinweis ausgegeben werden?
- Sollen alternative Go-Live-Termine außerhalb von Ferien und Feiertagsnähe berechnet werden?

#### Bei Blockern fragen

```text
Der Termin ist nach den Release-Regeln nicht gültig.
Soll ich den nächstmöglichen gültigen Mittwoch oder Donnerstag vorschlagen?
```

#### Bei hohem Risiko fragen

```text
Der Plan enthält ein hohes Kalender- oder Kapazitätsrisiko.
Soll ich den Plan beibehalten, als Risiko markieren oder alternative Go-Live-Termine berechnen?
```

### 10. Konsistenz prüfen

Prüfen:

- Go-Live ist Mittwoch oder Donnerstag.
- Kein Freitag-Deployment.
- Go-Live liegt nicht auf gesetzlichem NRW-Feiertag.
- Kein zwingender Meilenstein liegt auf gesetzlichem NRW-Feiertag.
- Feste Wochentage je Meilenstein sind eingehalten.
- Relative Meilensteine sind korrekt abgeleitet.
- Reihenfolge ist plausibel.
- Kritische Phasen sind vollständig ausgewiesen.
- Feiertage, Brückentage und Ferienkonflikte sind sichtbar markiert.
- Offene Punkte und Annahmen sind explizit aufgeführt.
- Beispiel Go-Live Donnerstag, 25.06.2026 reproduziert exakt die Referenztabelle, sofern die Referenz dies so vorgibt.

## Risikoklassifikation

### Blocker

- Go-Live liegt auf Freitag.
- Go-Live liegt nicht auf Mittwoch oder Donnerstag.
- Go-Live liegt auf gesetzlichem NRW-Feiertag.
- Zwingender Meilenstein liegt auf gesetzlichem NRW-Feiertag.
- Kalenderdaten sind widersprüchlich und der Konflikt betrifft einen kritischen Termin.
- Reihenfolge der Meilensteine ist logisch widersprüchlich.

### Hohes Risiko

- Beta-Woche überschneidet sich mit NRW-Schulferien.
- Finalisierungs-Woche überschneidet sich mit NRW-Schulferien.
- Go-Live-Woche enthält Feiertag oder Brückentag.
- Kritische Phase enthält bestätigte interne Nicht-Arbeitstage.
- Schlüsselpersonen fehlen in kritischer Phase.
- Kalenderdaten konnten nicht zuverlässig geladen werden.
- Go-Live liegt direkt nach Feiertag, Brückentag oder Ferienende.

### Mittleres Risiko

- Vorbereitender Meilenstein liegt in NRW-Schulferien.
- Potenzieller Brückentag liegt nahe an einem Meilenstein.
- Bewegliche Ferientage sind nicht bekannt.
- Kalenderdaten stammen nur aus einer Fallbackquelle.
- Teamurlaube wurden nicht geprüft.

### Hinweis

- Ferien liegen im erweiterten Planungszeitraum, aber nicht in kritischer Phase.
- Brückentage wurden nur markiert.
- Keine Informationen zu beweglichen Ferientagen vorhanden.
- Keine Informationen zu Teamabwesenheiten vorhanden.

## Fehler- und Fallbackverhalten

### Kalenderdaten nicht ladbar

Wenn Kalenderdaten nicht geladen werden können:

1. Fallbackquelle verwenden.
2. Wenn keine Fallbackquelle verfügbar ist:
    - Release-Plan rechnerisch erstellen,
    - Kalenderprüfung als `offen` markieren,
    - Warnung ausgeben.

Standardhinweis:

```text
Kalenderdaten für NRW konnten nicht zuverlässig geladen werden.
Die Release-Termine wurden berechnet, aber Feiertage und Ferien konnten nicht vollständig geprüft werden.
```

### Quellenkonflikte

Wenn Quellen widersprüchliche Daten liefern:

1. Konflikt sichtbar ausweisen.
2. Für NRW-Schulferien die offizielle NRW-Ferienordnung bevorzugen.
3. Bei kritischen Terminen interaktiv nachfragen.
4. Keine stillschweigende Korrektur ohne Hinweis.

Standardhinweis:

```text
Es gibt widersprüchliche Kalenderdaten.
Für NRW-Schulferien wird die offizielle Ferienordnung des Landes Nordrhein-Westfalen als maßgeblich behandelt.
```

## Erwarteter Output

### 1. Zusammenfassung

Enthält:

- Go-Live-Datum,
- Bewertung: gültig / ungültig / gültig mit Risiko,
- wichtigste Konflikte,
- wichtigste Annahmen,
- verwendete Kalendergrundlage,
- Hinweis auf offene Punkte.

### 2. Meilensteintabelle

Pflichtspalten:

```text
Meilenstein | Datum | Wochentag | Phase | Kalenderstatus | Risiko | Quelle | Hinweis
```

Mögliche Kalenderstatus:

- regulärer Arbeitstag,
- gesetzlicher NRW-Feiertag,
- NRW-Schulferien,
- potenzieller Brückentag,
- bestätigter Brückentag,
- beweglicher Ferientag,
- interne Betriebsruhe,
- Kalenderdaten offen.

### 3. Urlaubssperre / kritische Phasen

Pflichtspalten:

```text
Phase | Zeitraum | Bedeutung | Kalenderkonflikte | Kapazitätsrisiko | Empfehlung
```

### 4. Konflikt- und Risikoliste

Pflichtspalten:

```text
Konflikt | Kategorie | Betroffener Termin/Zeitraum | Auswirkung | Vorschlag
```

Kategorien:

- Blocker,
- hohes Risiko,
- mittleres Risiko,
- Hinweis.

### 5. Interaktive Rückfragen

Falls Eingaben fehlen oder Risiken bestehen:

- konkrete Rückfragen stellen,
- keine stillschweigenden Annahmen treffen,
- Entscheidungsoptionen anbieten,
- Alternativberechnung anbieten, wenn sinnvoll.

### 6. Optionaler Zeitstrahl

Text- oder Markdown-Zeitstrahl mit Markierung:

- Meilenstein,
- kritische Phase,
- Feiertag,
- Brückentag,
- Ferienzeit,
- offener Klärungspunkt.

### 7. Hinweise

Enthält:

- angewandte Annahmen,
- gerundete Abstände,
- offene Punkte,
- nicht geprüfte Abwesenheiten,
- verwendete Kalenderquellen,
- Abrufstatus der Kalenderdaten.

## Ausgabeformat

Die Antwort soll klar strukturiert sein:

1. Ergebnisbewertung
2. Meilensteintabelle
3. Kritische Phasen / Urlaubssperre
4. Kalender- und Kapazitätsrisiken
5. Offene Punkte
6. Rückfragen oder Entscheidungsoptionen
7. optional Zeitstrahl

## Qualitätskriterien

- Go-Live ist Mittwoch oder Donnerstag.
- Kein Freitag-Deployment.
- Gesetzliche NRW-Feiertage werden nicht als normale Arbeitstage behandelt.
- NRW-Schulferien werden gegen die offizielle NRW-Ferienordnung validiert.
- Brückentage werden nicht ungefragt als arbeitsfrei angenommen.
- Bewegliche Ferientage werden nicht erfunden.
- Maximal ein lokales Resource-/Referenzfile wird verwendet.
- Quelle, Abrufstatus und Annahmen sind sichtbar.
- Bei fehlenden oder widersprüchlichen Daten wird interaktiv nachgefragt oder ein offener Punkt ausgewiesen.
- Beispiel Go-Live Donnerstag, 25.06.2026 reproduziert exakt die Referenztabelle, sofern die Referenz dies so vorgibt.
- Keine erfundenen Regeln.

## Sicherheits- und Freigabegrenzen

- Nur Planung.
- Keine produktiven Aktionen.
- Keine Deployments.
- Keine verbindlichen Freigaben.
- Keine verbindliche Aussage zur tatsächlichen Personalverfügbarkeit ohne Bestätigung.
- Keine stillschweigende Verschiebung eines Go-Live-Termins ohne Hinweis.
- Entscheidung bleibt bei den Verantwortlichen.

## Beispiele

### Einstiegsbeispiel

Eingabe:

```text
Go-Live Donnerstag, 25.06.2026.
```

Erwartung:

- Meilensteintabelle gemäß Referenz.
- Kritische Phasen vollständig.
- NRW-Feiertage geprüft.
- NRW-Schulferien geprüft.
- Brückentage geprüft.
- Hinweise zu offenen beweglichen Ferientagen.
- Optional Zeitstrahl.

### Grenzfall: Freitag

Eingabe:

```text
Go-Live Freitag, 26.06.2026.
```

Erwartung:

- Ablehnung mit Begründung: kein Freitag-Deployment.
- Vorschlag des nächsten gültigen Mittwoch oder Donnerstag.
- Kalenderprüfung des Alternativtermins.

### Kalenderkonflikt: Feiertag

Eingabe:

```text
Go-Live Donnerstag, 04.06.2026.
```

Erwartung:

- Ablehnung oder Blocker-Hinweis, wenn das Datum ein gesetzlicher NRW-Feiertag ist.
- Vorschlag alternativer Mittwoch/Donnerstag.
- Hinweis auf betroffenen Feiertag.

### Kapazitätsrisiko: Ferien

Eingabe:

```text
Go-Live Mittwoch, 22.07.2026.
```

Erwartung:

- Formaler Wochentag ist gültig.
- Hinweis: Go-Live liegt in NRW-Schulferien, sofern laut offizieller Ferienordnung zutreffend.
- Risiko: mögliche reduzierte Besetzung.
- Rückfrage, ob alternative Go-Live-Termine außerhalb der Ferien berechnet werden sollen.

### Brückentag

Eingabe:

```text
Go-Live Donnerstag, 11.06.2026.
```

Erwartung:

- Kalenderprüfung der kritischen Phasen.
- Prüfung, ob vorbereitende Termine auf oder um potenzielle Brückentage fallen.
- Rückfrage, ob Brückentage als arbeitsfrei behandelt oder nur als Risiko markiert werden sollen.

## Pflege

Verantwortlich:

Gruppe Webservices & Strategie.

Prüfen bei Änderung:

- Release-Regeln,
- Wochentagslogik,
- Feiertagsgrundlagen,
- offizieller NRW-Ferienordnung,
- internen Betriebsruhe-Regeln,
- Team- oder Vertreterregelungen,
- technischer Kalenderquellen.

Kalenderdaten sollten dynamisch geladen oder jährlich aus geprüften Quellen validiert werden.

Bewegliche Ferientage und Teamabwesenheiten müssen projektspezifisch ergänzt werden.
