---
name: vb-anonymisierung
description: Anonymisierung strukturierter Daten (CSV, Excel, JSON, XML) — personenbezogene Daten durch realistische, deutsche Ersatzdaten ersetzen.
---

# vb-anonymisierung

## Ziel
Anonymisiert strukturierte Daten aus CSV-, Excel-, JSON- oder XML-Dateien so, dass personenbezogene Daten nicht mehr einer realen Person zugeordnet werden können. Die anonymisierten Daten sollen weiterhin realistisch wirken, fachlich plausibel bleiben und für Tests, Entwicklung, Schulung, Qualitätssicherung und Demonstrationen nutzbar sein. Einsetzbar bei Entwicklung, Test, Schulung und Qualitätssicherung. Keine Mappingtabellen ausgeben. Bei Excel alle Arbeitsblätter prüfen. Bei JSON/XML auch verschachtelte Strukturen prüfen.

## Vorgehen

### Erkennung und Klassifikation
- Erkenne das Eingabeformat (CSV, XLSX, JSON, XML).
- Identifiziere personenbezogene Felder anhand von Feldnamen (z. B. `name`, `nachname`, `vorname`, `adresse`, `plz`, `ort`, `telefon`, `email`, `iban`, `bic`, `geburtsdatum`, `geschlecht`) und per Mustererkennung (Regex für E-Mail, IBAN, Telefonnummer).
- Prüfe auch Kommentare und Freitextfelder auf personenbezogene Daten.
- Bei Excel alle Arbeitsblätter und versteckte Tabellenblätter prüfen.
- Bei JSON/XML rekursiv alle Objekte, Arrays, Attribute und Textinhalte prüfen.

### Anonymisierung durchführen
- **Personendaten**: Vorname, Nachname, vollständiger Name, Geburtsname, Benutzername, Kunden-/Personal-/Versicherungsnummern, Ausweisnummern, Steuer-ID, Sozialversicherungsnummer ersetzen.
- **Adressdaten**: Straße, Hausnummer, PLZ, Ort, Bundesland durch plausible deutsche Adressen ersetzen.
- **Kommunikationsdaten**: Mobil-/Festnetz-/Faxnummern mit deutschen Formaten, E-Mail mit Test-Domains (`example.de`, `test.invalid`, `anonymisiert.local`) ersetzen.
- **Bankdaten**: IBAN, BIC, Kontonummer, Bankleitzahl, Kreditkartennummer, Karteninhaber, SEPA-Mandatsreferenzen durch Testwerte ersetzen.
- **Geburtsdaten**: Nur um -21 bis +21 Tage verschieben, Schaltjahre und Monatsgrenzen korrekt behandeln.
- **Geschlecht**: Beibehalten (m/w/d in gleicher Codierung).
- **Namen**: Anfangsbuchstaben von Vor- und Nachnamen beibehalten. Ersatznamen zum Geschlecht passend wählen.
- **Sprache**: Grundsätzlich beibehalten, nur bei Identifikationsrisiko auf gröbere Kategorie reduzieren.
- Ersatzdaten sollen typisch deutsch wirken (Namen, Adressen, Telefonnummern).

### Strukturerhalt
- Ausgabeformat identisch zum Eingabeformat.
- Spaltennamen, Feldnamen, Elementnamen und Attributnamen erhalten.
- Anzahl und Reihenfolge der Datensätze erhalten.
- Datentypen, Pflichtfelder und technische Formate unverändert lassen.

### Konsistenz sicherstellen
- Innerhalb eines Datensatzes: zusammengehörende Daten konsistent ersetzen (z. B. Name → E-Mail → Kontoinhaber).
- Über mehrere Datensätze: dieselbe reale Person konsistent auf dieselbe anonymisierte Person abbilden (nur innerhalb des aktuellen Verarbeitungslaufs).

### Qualitätsprüfung nach Anonymisierung
- Keine ursprünglichen Namen, Telefonnummern, E-Mail-Adressen, IBANs oder vollständigen Adressen mehr enthalten.
- Geburtsdaten maximal wenige Wochen verschoben.
- Geschlecht und Namensinitialen erhalten.
- Ausgabeformat valide.
- Datensatzanzahl unverändert.

## Regeln / Qualitätskriterien

### Grundprinzipien
- Direkte Identifikatoren ersetzen, nicht nur schwärzen oder löschen.
- Pseudonymisierung allein reicht nicht — keine Mappingtabellen ausgeben oder speichern.
- Personenbezogene Daten dürfen nach der Anonymisierung nicht mehr auf reale Personen zurückführbar sein.

### Sicherheitsregeln
- Keine Originalwerte in Kommentaren, Logs oder Metadaten ausgeben.
- Keine echten personenbezogenen Daten als Ersatzwerte verwenden.
- Keine produktiven E-Mail-Domains, realen Bankverbindungen oder echten Telefonnummern verwenden.
- Bei Unsicherheit lieber stärker anonymisieren als zu wenig.

### VB-spezifische Hinweise
- Keine Mappingtabellen ausgeben.
- Bei Excel alle Arbeitsblätter prüfen.
- Bei JSON/XML auch verschachtelte Strukturen prüfen.
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen explizite Nutzerbestätigung einholen.
- Konkrete Produkte, Frameworks, Cloud-Dienste oder Toolketten aus dem Ursprungsskill nur als verbindlich behandeln, wenn im Projektkontext bestätigt oder in `docs/referenzen/standards-mapping.md` aufgeführt.

## Ressourcen
Keine
