---
name: vb-tm-anforderungsspezifikation
description: "Vorlage und Qualitätskriterien für Technisches Marketing: einwandfreie Anforderungen mit Vorbedingungen, Testfällen und erwarteten Ergebnissen. Ziel: Entwicklung, Test und Fachbereich verstehen dasselbe."
---

# VB Technisches Marketing – Anforderungsspezifikation

## Ziel

Einheitliche, testbare Anforderungen schreiben, die von Entwicklung, Test und Fachbereich gleich verstanden werden. Kein Interpretationsspielraum. Wird verwendet, wenn eine neue fachliche Anforderung aufgesetzt wird, bei der Übergabe an die Entwicklung, oder als Grundlage für Testfälle und Abnahme.

## Vorgehen

### 1. Pflicht-Bestandteile prüfen

Jede Anforderung muss **vier Elemente** enthalten:

| # | Element | Leitfrage |
|---|---------|-----------|
| 1 | **Anforderung** | Was soll das System tun? |
| 2 | **Vorbedingung** | Was muss vorher erfüllt sein? |
| 3 | **Testfall** | Wie prüfe ich die Anforderung konkret? |
| 4 | **Erwartetes Ergebnis** | Was muss sichtbar/passieren, damit der Test bestanden ist? |

### 2. Template ausfüllen

```
| ID                   | TM-<laufende Nummer>          |
| Titel                | <aussagekräftiger Kurztitel>  |
| Anforderung          | Das System muss …             |
| Vorbedingung         | Gegeben ist …                 |
| Testfall             | Wenn … dann …                 |
| Erwartetes Ergebnis  | Es wird …                     |
| Akzeptanzkriterium   | Die Anforderung gilt als      |
|                      | erfüllt, wenn …               |
| System               | <betroffenes VB-System>       |
| Release              | <Release-Nummer oder -Name>   |
| Testdaten            | <vorhanden? Wo? Welche?>      |
| Fachlicher           | <Name oder Rolle>             |
| Ansprechpartner      |                               |
| Beta-Relevanz        | <Ja / Nein – mit Begründung>  |
```

### 3. Im Gegeben–Wenn–Dann-Stil formulieren

> **Gegeben** ein angemeldeter Benutzer mit Produktzugriff,
> **wenn** er ein Produkt auswählt und die technischen Unterlagen öffnet,
> **dann** werden nur die für dieses Produkt gültigen Unterlagen angezeigt.

### 4. Vollständiges Beispiel liefern

| Feld | Inhalt |
|------|--------|
| ID | TM-001 |
| Titel | Technische Unterlagen anzeigen |
| Anforderung | Das System muss dem Benutzer nach Auswahl eines Produkts die zugehörigen technischen Unterlagen anzeigen. |
| Vorbedingung | Der Benutzer ist angemeldet und hat Zugriff auf das Produkt. |
| Testfall | Produkt auswählen und Bereich „Technische Unterlagen" öffnen. |
| Erwartetes Ergebnis | Die passenden Unterlagen werden vollständig angezeigt; nicht relevante Unterlagen werden nicht angezeigt. |
| Akzeptanzkriterium | Die Anforderung gilt als erfüllt, wenn für jedes wählbare Produkt die korrekten Unterlagen angezeigt werden und keine fremden Unterlagen erscheinen. |
| System | Produktportal (MVP) |
| Release | R3.1 |
| Testdaten | Produkt „BasisRente Classic" (BU-00042) mit 3 verknüpften PDFs im Testmandanten |
| Fachlicher Ansprechpartner | [Rolle: Produktmanager Leben] |
| Beta-Relevanz | Nein – reine Anzeigefunktion, kein kritisches Feature |

### 5. Review-Checkliste durchgehen

Vor der Übergabe an Entwicklung prüfen:

- [ ] Alle vier Pflichtfelder gefüllt?
- [ ] Testfall bildet genau die Anforderung ab?
- [ ] Erwartetes Ergebnis ist messbar/beobachtbar?
- [ ] Keine „sollte"/„könnte"/„eventuell"-Formulierungen?
- [ ] Akzeptanzkriterium definiert?
- [ ] ID vergeben?
- [ ] System und Release benannt?
- [ ] Testdaten vorhanden/benannt?
- [ ] Fachlicher Ansprechpartner hinterlegt?
- [ ] Beta-Relevanz geprüft?

## Regeln / Qualitätskriterien

Jede Anforderung muss **eindeutig, testbar, vollständig und atomar** sein.

- Kein Interpretationsspielraum, kein „sollte", kein „eventuell"
- Der Testfall muss mit Ja/Nein beantwortbar sein
- Alle vier Pflicht-Bestandteile sind ausgefüllt
- Eine Anforderung pro Ticket – nicht mehrere Anforderungen vermischen

**Typische Fehler:**

- Anforderung und Testfall vermischt („Ich teste, dass das System X tut")
- Vorbedingungen fehlen → Test scheitert an der Umgebung, nicht an der Funktion
- Erwartetes Ergebnis schwammig („es funktioniert") statt konkret („die Liste enthält genau 3 Einträge")
- Mehrere Anforderungen in einer Zeile → nicht einzeln testbar
- System/Release fehlt → Entwicklung weiß nicht, wo und wann umsetzen
- Keine Testdaten benannt → Entwickler blockiert, Tester kann nicht prüfen

## Ressourcen

*Keine*
