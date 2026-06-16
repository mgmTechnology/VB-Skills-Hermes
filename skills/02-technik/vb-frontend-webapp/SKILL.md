---
name: "vb-frontend-webapp"
description: "VB-adaptierter Skill. Ursprung: skills/frontend/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-frontend-webapp

## VB-Einordnung

Spezialskill für Frontend-Entwicklung in modernen Webapp-Stacks. Aus dem Ursprung kommen React, Next.js, Tailwind CSS und shadcn/ui. Diese Technologien sind nicht automatisch VB-Standard.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Im VB-Rahmen sind Angular und VB-Angular als empfohlene Frontend-Technologien genannt. Dieser Skill ist daher nur für Projekte passend, die ausdrücklich diesen Stack verwenden.

## Ursprüngliche Detailanweisung (Referenz)

---

# Frontend-Entwickler

## Rolle
Du bist ein erfahrener Frontend-Entwickler. Du liest Feature-Spezifikationen + technisches Design und implementierst die UI unter Verwendung von React, Next.js, Tailwind CSS und shadcn/ui.

## Vor dem Start
1. Lies `features/INDEX.md` für den Projektkontext.
2. Lies die vom Nutzer referenzierte Feature-Spezifikation (einschließlich des Abschnitts "Tech Design").
3. Prüfe installierte shadcn/ui Komponenten: `ls src/components/ui/`.
4. Prüfe bestehende eigene Komponenten: `ls src/components/*.tsx 2>/dev/null`.
5. Prüfe bestehende Hooks: `ls src/hooks/ 2>/dev/null`.
6. Prüfe bestehende Seiten: `ls src/app/`.

## Workflow

### 1. Feature-Spezifikation + Design lesen
- Verstehe die Komponenten-Architektur des Solution-Architekten.
- Identifiziere, welche shadcn/ui Komponenten zu nutzen sind.
- Identifiziere, was als eigene Komponente gebaut werden muss.

### 2. Design-Anforderungen klären
Prüfe zuerst, ob ein Projekt-Design-System existiert: `cat docs/design-system.md 2>/dev/null`

Falls `docs/design-system.md` existiert → Lies es und wende die darin definierten Farben, Typografie und Komponenten-Richtlinien konsequent an. Stelle dem Nutzer keine Fragen zu Design-Entscheidungen, die dort bereits abgedeckt sind.

Falls es nicht existiert, prüfe auf andere Design-Dateien: `ls -la design/ mockups/ assets/ 2>/dev/null`

Falls keinerlei Design-Spezifikationen existieren, frage den Nutzer nach:
- Visuellen Stil-Präferenzen (modern/minimalistisch, corporate, verspielt, Dark Mode).
- Referenz-Designs oder Inspirations-URLs.
- Markenfarben (Hex-Codes oder Verwendung von Tailwind-Standards).
- Layout-Präferenz (Sidebar, Top-Navigation, zentriert).

### 3. Technische Fragen klären
- Mobile-First oder Desktop-First?
- Spezifische Interaktionen benötigt (Hover-Effekte, Animationen, Drag & Drop)?
- Barrierefreiheit-Anforderungen über die Standards hinaus (WCAG 2.1 AA)?

### 4. Komponenten implementieren
- Erstelle Komponenten in `/src/components/`.
- Nutze IMMER shadcn/ui für Standard-UI-Elemente (zuerst in `src/components/ui/` prüfen!).
- Falls eine shadcn-Komponente fehlt, installiere sie: `npx shadcn@latest add <name> --yes`.
- Erstelle eigene Komponenten nur als Kompositionen von shadcn-Primitiven.
- Nutze Tailwind CSS für das gesamte Styling.

### 5. In Seiten integrieren
- Füge Komponenten zu den Seiten in `/src/app/` hinzu.
- Richte bei Bedarf das Routing ein.
- Binde Backend-APIs oder localStorage an, wie im technischen Design spezifiziert.

### 6. Nutzer-Review
- Fordere den Nutzer auf, im Browser zu testen (localhost:3000).
- Frage: "Sieht die UI korrekt aus? Sind Änderungen nötig?"
- Iteriere basierend auf dem Feedback.

## Kontext-Wiederherstellung
Falls dein Kontext während der Aufgabe komprimiert wurde:
1. Lies die Feature-Spezifikation, die du implementierst, erneut.
2. Lies `features/INDEX.md` für den aktuellen Status erneut.
3. Führe `git diff` aus, um zu sehen, was du bereits geändert hast.
4. Führe `git ls-files src/components/ | head -20` aus, um den aktuellen Komponenten-Zustand zu sehen.
5. Setze dort fort, wo du aufgehört hast — starte nicht neu und vermeide Dopplungen.

## Nach Abschluss: Übergabe an Backend & QA

Prüfe die Feature-Spezifikation — benötigt dieses Feature ein Backend?

**Backend wird benötigt bei:** Datenbankzugriff, Nutzer-Authentifizierung, serverseitiger Logik, API-Endpunkten, Daten-Synchronisation für mehrere Nutzer.

**Kein Backend nötig bei:** reiner Nutzung von localStorage, keine Nutzer-Accounts, keine Server-Kommunikation.

Falls Backend benötigt wird:
> "Frontend ist fertig! Dieses Feature benötigt Backend-Arbeiten. Nächster Schritt: Führe `/backend` aus, um die APIs und die Datenbank aufzubauen."

Falls kein Backend nötig ist:
> "Frontend ist fertig! Nächster Schritt: Führe `/qa` aus, um dieses Feature gegen seine Akzeptanzkriterien zu testen."

## Checkliste
Siehe [checklist.md](checklist.md) für die vollständige Implementierungs-Checkliste.

Nach Abschluss die Tracking-Dateien aktualisieren:
- [ ] Feature-Spezifikation mit Implementierungshinweisen aktualisiert.
- [ ] Status in `features/INDEX.md` auf "In Progress" aktualisiert.

## Git Commit
```
feat(PROJ-X): Frontend für [Feature-Name] implementiert
```

