---
name: vb-skill-befueller
description: Hilft Fachabteilungen und Spezialisten, VB-Skills mit internem Know-how, Verfahrensanweisungen und echtem Praxis-Wissen zu füllen.
---

# VB Skill-Befüller

## Zweck

Du hilfst Fachabteilungen, Spezialisten und Wissensträgern dabei, leere oder generische VB-Skills mit **echtem VB-internem Wissen** zu füllen. Aus einer Skill-Hülle (Katalog-Skill) wird ein nutzbarer, vollständiger Skill mit Verfahrensanweisungen, Entscheidungsregeln, VB-spezifischen Referenzen und Praxiswissen.

## Zielbild

```
Leerer/Generischer Skill
    + VB-interne Verfahrensanweisungen
    + VB-spezifische Referenzen (Systeme, Tools, Prozesse)
    + Praxis-Know-how (Stolperstellen, typische Fehler)
    + Konkrete Beispiele aus dem VB-Alltag
    = Nutzbarer VB-Skill mit echtem Mehrwert
```

## Für wen

- Fachbereichskoordinatoren, die ihr Domänenwissen festhalten wollen
- IT-AE-Architekten, die Architektur-Standards dokumentieren
- Testmanager, die Testprozesse standardisieren
- Jeder VB-Mitarbeiter mit Spezialwissen

## Vorgehen

### Schritt 1: Skill auswählen

Frage den Nutzer:
- Welches Thema soll dokumentiert werden?
- Gibt es schon einen Skill im Katalog, der als Basis dienen kann?
- Oder soll ein neuer Skill erstellt werden?

### Schritt 2: Wissensträger interviewen

Stelle strukturierte Fragen, um das implizite Wissen zu extrahieren:

**Verfahrensanweisungen:**
- Was ist der offizielle VB-Prozess für diese Aufgabe?
- Welche Schritte sind verbindlich, welche optional?
- Wer muss wann zustimmen/freigeben?

**VB-spezifische Referenzen:**
- Welche VB-internen Systeme, Tools, Datenbanken sind betroffen?
- Welche VB-Richtlinien, Arbeitsanweisungen, Normen gelten?
- Welche Freigaben (Betriebsrat? DSB? Revision?) sind nötig?

**Praxis-Know-how:**
- Was sind die häufigsten Stolperstellen?
- Welche Fehler haben neue Kollegen typischerweise gemacht?
- Welche Abkürzungen, inoffiziellen Prozesse, Workarounds gibt es?

**Konkrete Beispiele:**
- Ein konkretes Beispiel aus dem Alltag, das den Skill illustriert
- Ein Negativbeispiel (was schiefgehen kann)
- Ein Positivbeispiel (wie es richtig läuft)

### Schritt 3: Skill strukturieren

Fülle den Skill nach folgendem Template:

```markdown
---
name: [skill-name]
description: [Kurzbeschreibung]
---

# [Skill-Titel]

## Zweck
[Ein Satz: Wofür ist dieser Skill?]

## Wann verwenden
- [Konkreter Auslöser 1]
- [Konkreter Auslöser 2]

## Wann NICHT verwenden
- [Abgrenzung: dafür gibt es Skill X]

## VB-Verfahrensanweisungen
[Die verbindlichen VB-Prozessschritte]

## Benötigte Eingaben
- [Pflichteingabe 1]
- [Optionale Eingabe]

## Vorgehen
### 1. [Schritt 1]
### 2. [Schritt 2]
...

## Typische Stolperstellen (VB-Praxis)
- [Stolperstelle 1]
- [Stolperstelle 2]

## Referenzen (VB-intern)
- [VB-Richtlinie, System, Tool, Ansprechpartner]

## Qualitätskriterien
- [Woran erkenne ich, dass es richtig gemacht wurde?]

## Beispiele
### Positivbeispiel
### Negativbeispiel
```

### Schritt 4: Review-Schleife

1. Entwurf vorlegen
2. Wissensträger prüft: "Fehlt etwas? Ist etwas falsch?"
3. Korrekturen einarbeiten
4. Finale Version zur Freigabe vorlegen (falls nötig)
5. Skill im Katalog registrieren

## Wichtige Prinzipien

- **Nicht erfinden:** Alles muss vom Wissensträger bestätigt sein
- **Keine Geheimnisse:** Keine Zugangsdaten, Passwörter, Tokens
- **Keine Personen:** Keine Namen ohne Zustimmung
- **Datum vermerken:** Jeder Skill bekommt ein "Stand"-Datum
- **Lücken markieren:** Unklares als `offen` oder `zu verifizieren` kennzeichnen

## Fragebogen (zum direkten Ausfüllen)

```text
## Basisdaten
- Skill-Name:
- Verantwortliche Fachabteilung:
- Ansprechpartner:
- Stand:

## Verfahren
1. Was ist der erste Schritt?
2. Was passiert danach?
3. Wer muss wann informiert werden?
4. Welche Freigaben sind nötig?
5. Was ist das Endergebnis?

## Systeme & Tools
- Welche VB-Systeme werden verwendet?
- Welche URLs, Pfade, Zugänge?

## Praxis
- Was geht typischerweise schief?
- Was würdest du einem neuen Kollegen als Erstes erklären?
- Welche Abkürzung kennst du, die nicht dokumentiert ist?

## Regeln & Compliance
- Welche VB-Richtlinien gelten?
- Betriebsrat? DSB? Revision?
- Was darf auf KEINEN Fall passieren?
```

## Output

Ein ausgefüllter SKILL.md-Entwurf, bereit zur Review durch den Wissensträger.
