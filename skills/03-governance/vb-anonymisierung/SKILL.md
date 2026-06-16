---
name: "vb-anonymisierung"
description: "VB-adaptierter Skill. Ursprung: skills/anon/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-anonymisierung

## VB-Einordnung

Governance-Skill für Anonymisierung strukturierter Daten, Testdaten, personenbezogene Daten, Adressen, Kommunikationsdaten, Bankdaten und Geburtsdaten. Dieser Skill ist im VB-Kontext besonders relevant für Entwicklung, Test, Schulung und Qualitätssicherung.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

Zusätzlicher VB-Hinweis: Keine Mappingtabellen ausgeben. Bei Excel alle Arbeitsblätter prüfen. Bei JSON/XML auch verschachtelte Strukturen prüfen.

## Ursprüngliche Detailanweisung (Referenz)

Dieser Abschnitt enthält die ursprüngliche Anweisung, auf der dieser VB-Skill basiert.

---

# Skill: Anonymisierung strukturierter Daten

## Zweck

Dieser Skill anonymisiert strukturierte Daten aus CSV-, Excel-, JSON- oder XML-Dateien so, dass personenbezogene Daten nicht mehr einer realen Person zugeordnet werden können.

Die anonymisierten Daten sollen weiterhin realistisch wirken, fachlich plausibel bleiben und insbesondere für Tests, Entwicklung, Schulung, Qualitätssicherung und Demonstrationen nutzbar sein.

## Grundprinzipien

1. Personenbezogene Daten dürfen nach der Anonymisierung nicht mehr auf reale Personen zurückführbar sein.
2. Die Struktur der Eingabedaten muss erhalten bleiben.
3. Datentypen, Pflichtfelder, Feldnamen und technische Formate sollen möglichst unverändert bleiben.
4. Ersatzwerte sollen realistisch und typisch für deutsche Testdaten sein.
5. Geschlecht soll beibehalten werden.
6. Anfangsbuchstaben von Vor- und Nachnamen sollen beibehalten werden.
7. Geburtsdaten sollen nur geringfügig verschoben werden: maximal wenige Wochen Abweichung vom Originaldatum.
8. Direkte Identifikatoren müssen ersetzt werden, nicht nur geschwärzt oder gelöscht werden.
9. Pseudonymisierung allein reicht nicht aus, wenn eine Rückzuordnung über Mappingtabellen möglich wäre. Es dürfen keine Mappingtabellen ausgegeben werden.

## Unterstützte Eingabeformate

Der Skill verarbeitet grundsätzlich folgende Datenformate:

- CSV
- Excel, insbesondere XLSX
- JSON
- XML

Bei Excel-Dateien sind alle Arbeitsblätter zu prüfen und zu anonymisieren.

Bei JSON und XML sind auch verschachtelte Objekte, Arrays, Attribute und Textinhalte zu prüfen.

## Erhalt der Datenstruktur

Die Ausgabe soll dasselbe Format wie die Eingabe behalten, sofern nichts anderes verlangt wird.

Beispiele:

- CSV bleibt CSV.
- XLSX bleibt XLSX.
- JSON bleibt valides JSON.
- XML bleibt valides XML.

Spaltennamen, Feldnamen, Elementnamen und Attributnamen sollen erhalten bleiben.

Die Anzahl der Datensätze soll erhalten bleiben.

Die Reihenfolge der Datensätze soll erhalten bleiben, sofern sie nicht ausdrücklich geändert werden soll.

## Zu anonymisierende Datenarten

Folgende Datenarten sind immer zu anonymisieren, wenn sie direkt oder indirekt erkennbar sind.

### Personendaten

Zu ersetzen sind insbesondere:

- Vorname
- Nachname
- vollständiger Name
- Geburtsname
- Benutzername, sofern personenbezogen
- Kundennummern, sofern personenbezogen interpretierbar
- Personalnummern
- Versicherungsnummern
- Ausweisnummern
- Steuer-ID
- Sozialversicherungsnummer

### Adressdaten

Zu ersetzen sind insbesondere:

- Straße
- Hausnummer
- Postleitzahl
- Ort
- Bundesland, falls notwendig
- vollständige Adresse
- Lieferadresse
- Rechnungsadresse

Die Ersatzadressen müssen typisch deutsche Adressen sein.

### Kommunikationsdaten

Zu ersetzen sind insbesondere:

- Mobilnummern
- Festnetznummern
- Faxnummern
- E-Mail-Adressen
- private URLs oder personenbezogene Webseiten

Telefonnummern sollen wie plausible deutsche Telefonnummern aussehen.

E-Mail-Adressen sollen realistische Testadressen sein, aber keine real existierenden privaten Postfächer verwenden.

Empfohlene Domain:

- example.de
- test.invalid
- anonymisiert.local

### Bankdaten

Zu ersetzen sind insbesondere:

- IBAN
- BIC
- Kontonummer
- Bankleitzahl
- Kreditkartennummer
- Karteninhaber
- SEPA-Mandatsreferenzen, sofern personenbezogen

Bankdaten müssen plausibel formatiert sein, dürfen aber nicht zu realen Personen gehören.

Für deutsche IBANs ist das Format `DEkk bbbb bbbb kkkk kkkk kk` einzuhalten, wobei `kk` Prüfziffern sind. Wenn keine echte Prüfziffernberechnung erfolgt, muss klar sein, dass es sich um Testdaten handelt.

### Geburtsdaten

Geburtsdaten dürfen nicht komplett zufällig ersetzt werden.

Regel:

- Das Geburtsdatum wird um einen zufälligen Wert zwischen -21 und +21 Tagen verschoben.
- Das Alter bleibt dadurch nahezu unverändert.
- Das Datum muss gültig bleiben.
- Schaltjahre und Monatsgrenzen sind korrekt zu behandeln.

Wenn nur Geburtsjahr oder Geburtsmonat vorhanden ist, darf der Wert unverändert bleiben oder minimal plausibel angepasst werden, sofern dadurch keine Rückidentifikation möglich bleibt.

### Geschlecht

Das Geschlecht ist beizubehalten.

Beispiele:

- `männlich` bleibt `männlich`
- `weiblich` bleibt `weiblich`
- `divers` bleibt `divers`
- `m`, `w`, `d` bleiben in derselben Codierung erhalten

Der Ersatzvorname muss zum Geschlecht passen, soweit das Feld dies erlaubt.

### Sprache

Sprache soll grundsätzlich erhalten bleiben, sofern sie nicht selbst personenbezogen oder identifizierend ist.

Beispiele:

- `Deutsch` bleibt `Deutsch`
- `Englisch` bleibt `Englisch`
- `Polnisch` bleibt `Polnisch`

Wenn Sprache gemeinsam mit seltenen Merkmalen eine Identifikation erleichtert, kann sie auf eine gröbere Kategorie reduziert werden, z. B. `Deutsch`, `EU-Sprache`, `Sonstige`.

### Kommentare und Freitextfelder

Kommentare, Notizen und Freitexte sind besonders sorgfältig zu prüfen.

Darin enthaltene personenbezogene Daten müssen ersetzt werden, auch wenn das Feld selbst nicht entsprechend benannt ist.

Zu anonymisieren sind beispielsweise:

- Namen
- Orte
- Adressen
- Telefonnummern
- E-Mail-Adressen
- Bankdaten
- Versicherungsnummern
- konkrete Arbeitgeber
- konkrete Schulen
- konkrete medizinische Hinweise
- konkrete familiäre Angaben

Wenn ein Kommentar beispielsweise den letzten Urlaubsort enthält, soll dieser durch einen plausiblen Urlaubsort ersetzt werden.

Beispiel:

Original:

```text
Letzter Urlaubsort: Marbella
```

Anonymisiert:

```text
Letzter Urlaubsort: Ostsee
```

## Ersatzdaten für deutsche Personen

Personenbezogene Ersatzdaten sollen typisch deutsch wirken.

### Vornamen

Der Anfangsbuchstabe des ursprünglichen Vornamens muss beibehalten werden.

Beispiele:

- `Anna` → `Amelie`
- `Bernd` → `Björn`
- `Claudia` → `Carina`
- `Thomas` → `Tobias`

Der Ersatzvorname soll zum Geschlecht passen.

Bei unbekanntem oder diversem Geschlecht sollen neutrale oder geeignete Namen verwendet werden.

### Nachnamen

Der Anfangsbuchstabe des ursprünglichen Nachnamens muss beibehalten werden.

Beispiele:

- `Müller` → `Meier`
- `Schneider` → `Scholz`
- `Fischer` → `Frank`

### Europäische Namen mit deutschem Wohnsitz

Wenn die ursprüngliche Person erkennbar einen europäischen Namen hat oder ein entsprechender Datensatz erzeugt werden soll, darf der Name weiterhin europäisch wirken, der Wohnsitz muss aber in Deutschland liegen.

Beispiele:

- `Kowalski`, `Nowak`, `Rossi`, `Bianchi`, `Dubois`, `Garcia`, `Novak`, `Jansen`, `O'Connor`

Auch hier gilt:

- Anfangsbuchstaben beibehalten.
- Geschlecht beibehalten.
- Adresse in Deutschland verwenden.

## Ersatzadressen

Adressen müssen plausibel deutsch sein.

Beispiele für Straßen:

- Hauptstraße
- Bahnhofstraße
- Gartenstraße
- Schulstraße
- Lindenweg
- Kirchstraße
- Marktstraße
- Feldstraße
- Buchenweg
- Rosenstraße

Beispiele für Orte:

- Dortmund
- Essen
- Köln
- Düsseldorf
- Münster
- Bochum
- Hamburg
- Bremen
- Hannover
- Leipzig
- Dresden
- Nürnberg
- Stuttgart
- München
- Frankfurt am Main

Postleitzahlen sollen zum Ort passen, soweit möglich.

Beispiele:

- Dortmund: 44135, 44137, 44139
- Essen: 45127, 45128, 45130
- Köln: 50667, 50668, 50670
- Düsseldorf: 40210, 40211, 40212
- Münster: 48143, 48145, 48147
- Hamburg: 20095, 20097, 20146
- München: 80331, 80333, 80335

## Telefonnummern

Telefonnummern müssen deutsche Formate verwenden.

### Mobilnummern

Beispiele:

- `+49 151 23456789`
- `+49 152 34567890`
- `+49 157 45678901`
- `+49 160 56789012`
- `+49 171 67890123`

### Festnetznummern

Die Vorwahl soll zum Ort passen, soweit möglich.

Beispiele:

- Dortmund: `+49 231 1234567`
- Köln: `+49 221 1234567`
- Düsseldorf: `+49 211 1234567`
- Essen: `+49 201 1234567`
- Münster: `+49 251 1234567`
- Hamburg: `+49 40 1234567`
- München: `+49 89 1234567`

## E-Mail-Adressen

E-Mail-Adressen sollen aus anonymisierten Namen gebildet werden.

Formatbeispiele:

- `amelie.meier@example.de`
- `tobias.schulz@example.de`
- `carina.frank@test.invalid`

Keine echten Domains verwenden, die produktiv erreichbar sein könnten, sofern dies vermeidbar ist.

## Bankdaten

Bankdaten sind vollständig durch Testwerte zu ersetzen.

Beispiele:

```text
IBAN: DE02120300000000202051
BIC: TESTDEDDXXX
Kontoinhaber: anonymisierter Name
```

Bei mehreren Datensätzen müssen Bankdaten variieren, damit Tests mit Dublettenlogik nicht verfälscht werden.

## Konsistenz innerhalb eines Datensatzes

Innerhalb eines Datensatzes müssen zusammengehörende Daten konsistent bleiben.

Beispiel:

Wenn aus `Anna Müller` die Person `Amelie Meier` wird, dann sollen auch zugehörige Felder konsistent sein:

- E-Mail: `amelie.meier@example.de`
- Kontoinhaber: `Amelie Meier`
- Kommentar: keine Erwähnung von `Anna Müller`

## Konsistenz über mehrere Datensätze

Wenn dieselbe reale Person mehrfach in den Eingabedaten vorkommt, soll sie innerhalb derselben Verarbeitung konsistent auf dieselbe anonymisierte Person abgebildet werden.

Beispiel:

`Anna Müller` kommt in drei Zeilen vor. Alle drei Vorkommen werden zu `Amelie Meier`.

Wichtig:

- Diese Konsistenz gilt nur innerhalb des aktuellen Verarbeitungslaufs.
- Es wird keine dauerhafte Mappingtabelle gespeichert oder ausgegeben.

## Erkennung personenbezogener Felder

Der Skill soll personenbezogene Felder anhand von Feldnamen und Inhalten erkennen.

### Typische Feldnamen für Namen

- `name`
- `nachname`
- `surname`
- `lastname`
- `vorname`
- `firstname`
- `givenName`
- `fullName`
- `personName`
- `kunde`
- `customerName`

### Typische Feldnamen für Adressen

- `adresse`
- `address`
- `strasse`
- `straße`
- `street`
- `hausnummer`
- `plz`
- `zip`
- `postalCode`
- `ort`
- `city`

### Typische Feldnamen für Kontaktinformationen

- `telefon`
- `phone`
- `mobil`
- `mobile`
- `handy`
- `festnetz`
- `fax`
- `email`
- `mail`

### Typische Feldnamen für Bankdaten

- `iban`
- `bic`
- `konto`
- `kontonummer`
- `bankleitzahl`
- `blz`
- `bank`
- `mandatsreferenz`
- `sepa`

### Typische Feldnamen für Geburtsdaten

- `geburtsdatum`
- `birthdate`
- `dateOfBirth`
- `dob`

### Typische Feldnamen für Geschlecht

- `geschlecht`
- `gender`
- `sex`

## Mustererkennung unabhängig vom Feldnamen

Auch ohne passenden Feldnamen sind folgende Muster zu anonymisieren:

- E-Mail-Adressen per Regex
- Telefonnummern per Regex
- IBANs per Regex
- deutsche Postleitzahlen in Adresskontexten
- Datumswerte in Geburtsdatumskontexten
- vollständige Namen in Freitexten, soweit erkennbar

## Empfohlene Regex-Muster

### E-Mail

```regex
\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b
```

### IBAN Deutschland

```regex
\bDE[0-9]{2}[ ]?[0-9]{4}[ ]?[0-9]{4}[ ]?[0-9]{4}[ ]?[0-9]{4}[ ]?[0-9]{2}\b
```

### Internationale IBAN grob

```regex
\b[A-Z]{2}[0-9]{2}[A-Z0-9 ]{11,30}\b
```

### Telefonnummer grob

```regex
(\+49|0049|0)[\s\-/]?[0-9]{2,5}[\s\-/]?[0-9]{3,12}
```

### Datum deutsch

```regex
\b\d{1,2}\.\d{1,2}\.\d{4}\b
```

### Datum ISO

```regex
\b\d{4}-\d{2}-\d{2}\b
```

## Verarbeitung von CSV

1. Zeichencodierung erkennen oder UTF-8 annehmen.
2. Trennzeichen erkennen, z. B. Komma, Semikolon oder Tabulator.
3. Header erkennen.
4. Spalten anhand des Headers klassifizieren.
5. Alle Zellen prüfen, auch Freitextzellen.
6. Werte anonymisieren.
7. CSV valide wieder ausgeben.

## Verarbeitung von Excel

1. Alle Tabellenblätter laden.
2. Formeln nach Möglichkeit erhalten.
3. Zellformate nach Möglichkeit erhalten.
4. Personenbezogene Zellwerte anonymisieren.
5. Versteckte Tabellenblätter ebenfalls prüfen.
6. Kommentare, Notizen und Zellkommentare prüfen, sofern technisch zugänglich.
7. Ergebnis als XLSX speichern.

## Verarbeitung von JSON

1. JSON vollständig parsen.
2. Rekursiv alle Objekte, Arrays und Werte durchlaufen.
3. Feldnamen zur Klassifikation verwenden.
4. Stringwerte zusätzlich per Mustererkennung prüfen.
5. Datentypen erhalten.
6. Ergebnis als valides, formatiertes JSON ausgeben.

## Verarbeitung von XML

1. XML vollständig parsen.
2. Elemente, Attribute und Textknoten rekursiv prüfen.
3. Element- und Attributnamen zur Klassifikation verwenden.
4. Textinhalte zusätzlich per Mustererkennung prüfen.
5. Namespaces erhalten.
6. Ergebnis als valides XML ausgeben.

## Qualitätsprüfung nach der Anonymisierung

Nach der Anonymisierung ist eine Prüfung durchzuführen:

1. Keine ursprünglichen Namen dürfen mehr enthalten sein.
2. Keine ursprünglichen Telefonnummern dürfen mehr enthalten sein.
3. Keine ursprünglichen E-Mail-Adressen dürfen mehr enthalten sein.
4. Keine ursprünglichen IBANs oder Kontodaten dürfen mehr enthalten sein.
5. Keine vollständigen ursprünglichen Adressen dürfen mehr enthalten sein.
6. Geburtsdaten dürfen maximal wenige Wochen abweichen.
7. Geschlecht muss erhalten bleiben.
8. Namensinitialen müssen erhalten bleiben.
9. Ausgabeformat muss valide sein.
10. Anzahl der Datensätze muss gleich bleiben.

## Sicherheitsregeln

- Keine Originalwerte in Kommentaren, Logs oder Metadaten ausgeben.
- Keine Mappingtabelle speichern oder mitliefern.
- Keine echten personenbezogenen Daten als Ersatzwerte verwenden.
- Keine produktiven E-Mail-Domains verwenden, wenn Testdomains ausreichen.
- Keine realen Bankverbindungen verwenden.
- Keine echten Telefonnummern verwenden, wenn Nummern nur Testdaten sein sollen.
- Bei Unsicherheit lieber stärker anonymisieren als zu wenig.

## Ausgabeanforderung

Die Ausgabe soll enthalten:

1. Die anonymisierte Datei oder den anonymisierten Dateninhalt.
2. Eine kurze Zusammenfassung der durchgeführten Anonymisierung.
3. Hinweise auf Felder, die nicht eindeutig klassifiziert werden konnten.
4. Eine Warnung, falls eine vollständige Anonymisierung nicht sicher bestätigt werden kann.

## Beispiel

### Eingabe

```json
{
  "vorname": "Anna",
  "name": "Müller",
  "adresse": "Kaiserstraße 12, 44135 Dortmund",
  "mobilnummer": "+49 171 9876543",
  "festnetznummer": "+49 231 7654321",
  "email": "anna.mueller@example.com",
  "geschlecht": "weiblich",
  "geburtsdatum": "1985-04-12",
  "sprache": "Deutsch",
  "kommentar": "Letzter Urlaubsort: Marbella"
}
```

### Ausgabe

```json
{
  "vorname": "Amelie",
  "name": "Meier",
  "adresse": "Lindenweg 24, 44137 Dortmund",
  "mobilnummer": "+49 151 2345678",
  "festnetznummer": "+49 231 3456789",
  "email": "amelie.meier@example.de",
  "geschlecht": "weiblich",
  "geburtsdatum": "1985-04-29",
  "sprache": "Deutsch",
  "kommentar": "Letzter Urlaubsort: Ostsee"
}
```

## Zielverhalten des Skills

Wenn der Benutzer eine Datei oder Daten in CSV, Excel, JSON oder XML bereitstellt, soll der Skill automatisch:

1. Das Format erkennen.
2. Personenbezogene Felder identifizieren.
3. Geeignete deutsche oder europäische Ersatzdaten erzeugen.
4. Geschlecht und Namensinitialen erhalten.
5. Geburtsdaten nur minimal verschieben.
6. Das ursprüngliche Format valide wieder ausgeben.
7. Eine kurze Prüf- und Änderungsliste ergänzen.

