---
name: vb-projekt-initialisierung
description: Prozess-Skill für den Start eines neuen Software- oder Produktvorhabens. Produktvision, MVP-Abgrenzung und erste Feature-Landkarte.
---

# vb-projekt-initialisierung

## Ziel
Start eines neuen Software- oder Produktvorhabens. Nützlich für frühe Projektideen, Produktvision, MVP-Abgrenzung und erste Feature-Landkarte. Dieser Skill ergänzt `vb-projektleitung` und `vb-analyse`, ersetzt aber keine Projektgenehmigung.

## Vorgehen

### Vor dem Start
- Lies `docs/PRD.md` — prüfe, ob das Projekt bereits initialisiert wurde.
- Lies `features/INDEX.md` — prüfe, ob bereits Features existieren.
- Falls das Projekt bereits initialisiert ist: Brich ab und verweise auf vb-feature-spezifikation oder vb-spezifikation-verfeinern.

### Interview-Phase („Grill Me"-Prinzip)
- Stelle immer nur eine Frage — niemals mehrere gleichzeitig.
- Gib immer eine Antwortempfehlung.
- Folge dem Gesprächsverlauf.
- Erkunde vorhandene Dateien, bevor du fragst.
- Kein festes Fragenlimit — aufhören, wenn volles Verständnis erreicht ist.

Decke folgende Themen ab: Kernproblem, primäre Zielnutzer und Pain Points, Must-have Features für MVP vs. Nice-to-have, existierende Alternativen/Wettbewerber, Constraints (Timeline, Budget, Team), Erfolgskriterien, explizite Non-Goals.

### Obligatorisch: Backend-Entscheidung
- Kläre, ob die App Daten persistent speichern oder zwischen Nutzern/Geräten synchronisieren muss.
- Bei Backend-Bedarf: Infrastruktur-Setup als erstes Feature mit höchster Priorität einplanen.

### Obligatorisch: Design System
- Kläre, ob ein bestehendes Design System, Brand Guidelines oder UI-Referenzen existieren.
- Falls vorhanden: In `docs/design-system.md` speichern und im PRD referenzieren.

### Nach dem Interview: PRD erstellen
- Schreibe `docs/PRD.md` mit: Vision, Target Users, Core Features (priorisiert), Success Metrics, Constraints, Non-Goals.
- Präsentiere den Entwurf zur Prüfung, arbeite Feedback ein.

### Feature-Map erstellen
- Wende Single Responsibility an: Jedes Feature = EINE testbare, bereitstellbare Einheit.
- Identifiziere Abhängigkeiten zwischen Features.
- Weise Prioritäten zu: P0 = MVP, P1 = nächste, P2 = später.
- Erstelle `features/INDEX.md` mit Feature ID, Name, Beschreibung, Priorität, Abhängigkeiten, Status.
- Präsentiere die Feature-Map, arbeite Feedback ein.

## Regeln / Qualitätskriterien
- Erstelle KEINE individuellen Feature-Spezifikationsdateien — das ist Aufgabe von vb-feature-spezifikation.
- Schreibe KEINEN Code und triff KEINE technischen Entscheidungen.
- Stelle immer nur eine Frage auf einmal.
- Höre nicht frühzeitig auf — arbeite bis zur vollständigen Klarheit.
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.
- Konkrete Produkte, Frameworks, Cloud-Dienste oder Toolketten aus dem Ursprungsskill gelten nur dann als verbindlich, wenn sie im Projektkontext bestätigt oder als VB-Rahmenbedingung aufgeführt sind.

## Ressourcen
- `docs/PRD.md` — Produktvision
- `features/INDEX.md` — Feature-Map
- `docs/design-system.md` — Design System (optional)
- Verwandte Skills: vb-projektleitung, vb-analyse, vb-feature-spezifikation
