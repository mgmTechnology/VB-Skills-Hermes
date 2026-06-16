---
name: vb-spezifikation-verfeinern
description: Prozess-Skill zur Überarbeitung, Erweiterung oder kritischen Prüfung bestehender Feature-Spezifikationen.
---

# vb-spezifikation-verfeinern

## Ziel
Überarbeitung, Erweiterung oder kritische Prüfung bestehender Feature-Spezifikationen. Änderungen an Scope, Akzeptanzkriterien oder fachlichen Vorgaben müssen als offene Entscheidung oder Änderungsbedarf markiert werden, sofern sie nicht bestätigt sind.

## Vorgehen

### Vor dem Start
- Lies die Feature-Spezifikation `features/PROJ-X-*.md` — verstehe den aktuellen Stand vollständig.
- Lies `features/INDEX.md` — verstehe Abhängigkeiten, Status und Kontext.
- Lies `docs/PRD.md` — behalte die Projektvision im Blick.
- Falls keine PROJ-X ID angegeben: Frage, welche Spezifikation verfeinert werden soll, und liste vorhandene Features auf.

### Eröffnungsfrage (IMMER zuerst stellen)
- Frage: „Was führt dich zurück zu dieser Spezifikation?"
- Die Antwort bestimmt den weiteren Pfad.

### Drei Pfade

**Pfad 1: Etwas hat sich geändert** (Scope, Nutzer-Feedback, Business-Logik, Stakeholder-Vorgaben)
- Führe ein gezieltes Interview nur zu den betroffenen Bereichen.
- Kläre: Was genau hat sich geändert? Welche User-Stories sind betroffen? Welche Akzeptanzkriterien müssen aktualisiert werden? Ändern sich Edge-Cases oder Abhängigkeiten?

**Pfad 2: Implementierung hat Lücken offenbart** (fehlende Szenarien, technische Einschränkungen)
- Konzentriere dich auf Präzisierung der Spezifikation.
- Kläre: Welches Szenario hat gefehlt? Neues Akzeptanzkriterium oder Edge-Case? Ändert dies Bestehendes? Gibt es verwandte Lücken?

**Pfad 3: Grundlegende Infragestellung** (Feature-Richtung unsicher, Aufteilung nötig)
- Stelle die gesamte Spezifikation von Grund auf infrage.
- Kläre: Welche Annahme wird angezweifelt? Sollte das Feature aufgeteilt oder zusammengeführt werden? Wie sieht die minimale Version (MVP) aus?

### Nach dem Interview: Spezifikation aktualisieren
- Nimm Änderungen in der Spezifikationsdatei vor.
- Lies die Datei nach dem Speichern erneut zur Verifikation.
- Pflege Decision-Log und Offene Fragen: Geklärte Fragen als erledigt markieren, neue Entscheidungen protokollieren, neue offene Fragen hinzufügen.

### Tracking-Dateien aktualisieren
- Aktualisiere `features/INDEX.md`, falls Status oder Abhängigkeiten geändert.
- Aktualisiere `docs/PRD.md`, falls die Roadmap betroffen ist.

## Regeln / Qualitätskriterien
- „Grill Me"-Prinzip wie bei vb-feature-spezifikation: immer nur eine Frage, Antwortempfehlung geben, dem Gespräch folgen.
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.
- Konkrete Produkte, Frameworks, Cloud-Dienste oder Toolketten aus dem Ursprungsskill gelten nur dann als verbindlich, wenn sie im Projektkontext bestätigt oder als VB-Rahmenbedingung aufgeführt sind.

## Ressourcen
- `features/PROJ-X-*.md` — bestehende Spezifikation
- `features/INDEX.md` — Feature-Map
- `docs/PRD.md` — Projektvision
