---
name: vb-feature-spezifikation
description: Prozess-Skill zur Erstellung vollständiger, testbarer Feature-Spezifikationen mit User Stories, Akzeptanzkriterien, Edge Cases, Out-of-Scope und Decision Log.
---

# vb-feature-spezifikation

## Ziel
Erstellung vollständiger, testbarer Feature-Spezifikationen mit User Stories, Akzeptanzkriterien, Edge Cases, Out-of-Scope und Decision Log.

Dieser Skill ergänzt `vb-anforderungsmanager` und `vb-business-analyst`. Bei fachlichen Projekten müssen Fachbereich und Fachexperten eingebunden werden.

Verwenden, wenn eine Feature-Idee in eine vollständige, testbare Spezifikation verwandelt werden soll — mit User-Stories, Akzeptanzkriterien und Edge-Cases.

## Vorgehen

### Vor dem Start
- Lies `docs/PRD.md` — verstehe die Projektvision und die Zielgruppe.
- Lies `features/INDEX.md` — prüfe bestehende Features, finde die nächste freie ID, prüfe auf Duplikate.
- Prüfe bestehende Komponenten und APIs in der Codebasis.
- Falls das Projekt noch nicht initialisiert wurde: Brich ab und verweise auf die Projekt-Initialisierung.
- Falls kein Argument übergeben wurde: Frage, welches Feature spezifiziert werden soll.

### Interview-Phase („Grill Me"-Prinzip)
- Stelle immer nur eine Frage — niemals mehrere gleichzeitig.
- Gib immer eine Antwortempfehlung — der Nutzer bestätigt oder korrigiert.
- Folge dem Gesprächsverlauf — neue Zweige öffnen, Abhängigkeiten nacheinander klären.
- Erkunde zuerst die Codebasis, falls eine Frage dadurch beantwortet werden kann.
- Kein festes Fragenlimit — höre auf, wenn du das Feature wirklich verstehst.

Decke folgende Themen ab: Wer nutzt das Feature? Was ist die Kern-Aktion? Wie sieht Erfolg aus? Must-have Verhaltensweisen für MVP? Validierungsregeln und Einschränkungen? Fehlerzustände, Empty States, Edge-Cases? Abhängigkeiten? Performance- oder Sicherheitsanforderungen?

### Nach dem Interview: Spezifikation schreiben
- Verwende das Template unter [template.md](template.md).
- Befülle „Out of Scope", „Decision Log" und „Open Questions".
- Schreibe Akzeptanzkriterien im Angenommen/Wenn/Dann-Format.
- Präsentiere den Entwurf zur Prüfung, arbeite Feedback ein.

### Tracking-Dateien aktualisieren
- Aktualisiere `features/INDEX.md`: Status von „Roadmap" auf „Planned".
- Aktualisiere `docs/PRD.md`: Roadmap-Tabelle falls zutreffend.

## Regeln / Qualitätskriterien
- Schreibe NIEMALS Code — das ist Aufgabe der Umsetzungs-Skills.
- Triff NIEMALS technische Entscheidungen — das ist Aufgabe des Architektur-Skills.
- Fokus: WAS das Feature tut (nicht WIE).
- Jede Spezifikation = EINE testbare, bereitstellbare Einheit (Single Responsibility).
- Kombiniere niemals mehrere unabhängige Funktionalitäten, CRUD für verschiedene Entitäten, Nutzer- + Admin-Funktionen oder verschiedene UI-Masken.
- Teile auf, wenn: unabhängig testbar, unabhängig bereitstellbar, andere Nutzerrolle, separate UI-Maske.
- Abhängigkeiten zwischen Features dokumentieren.
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.
- Konkrete Produkte, Frameworks, Cloud-Dienste oder Toolketten aus dem Ursprungsskill gelten nur dann als verbindlich, wenn sie im Projektkontext bestätigt oder als VB-Rahmenbedingung aufgeführt sind.

## Ressourcen
- [template.md](template.md) — Spezifikations-Template
- `docs/PRD.md` — Projektvision
- `features/INDEX.md` — Feature-Map
- Verwandte Skills: vb-anforderungsmanager, vb-business-analyst
