---
name: vb-frontend-webapp
description: VB-adaptierter Skill für Frontend-Entwicklung in modernen Webapp-Stacks. Ursprünglich React/Next.js/Tailwind/shadcn/ui. Im VB-Rahmen sind Angular und VB-Angular empfohlen.
---

# VB Frontend Webapp

## Ziel

Spezialskill für Frontend-Entwicklung in modernen Webapp-Stacks. Aus dem Ursprung kommen React, Next.js, Tailwind CSS und shadcn/ui. Diese Technologien sind nicht automatisch VB-Standard. Im VB-Rahmen sind Angular und VB-Angular als empfohlene Frontend-Technologien genannt. Dieser Skill ist daher nur für Projekte passend, die ausdrücklich diesen Stack verwenden.

## Vorgehen

### Vor dem Start
- Lies `features/INDEX.md` für den Projektkontext
- Lies die vom Nutzer referenzierte Feature-Spezifikation (einschließlich des Abschnitts "Tech Design")
- Prüfe installierte shadcn/ui Komponenten: `ls src/components/ui/`
- Prüfe bestehende eigene Komponenten: `ls src/components/*.tsx 2>/dev/null`
- Prüfe bestehende Hooks: `ls src/hooks/ 2>/dev/null`
- Prüfe bestehende Seiten: `ls src/app/`

### 1. Feature-Spezifikation + Design lesen
- Verstehe die Komponenten-Architektur des Solution-Architekten
- Identifiziere, welche shadcn/ui Komponenten zu nutzen sind
- Identifiziere, was als eigene Komponente gebaut werden muss

### 2. Design-Anforderungen klären
- Prüfe auf Projekt-Design-System: `cat docs/design-system.md 2>/dev/null`
- Falls `docs/design-system.md` existiert → darin definierte Farben, Typografie und Komponenten-Richtlinien konsequent anwenden
- Falls nicht existiert: prüfe andere Design-Dateien
- Falls keinerlei Design-Spezifikationen: frage nach Stil-Präferenzen, Referenz-Designs, Markenfarben, Layout-Präferenz

### 3. Technische Fragen klären
- Mobile-First oder Desktop-First?
- Spezifische Interaktionen benötigt (Hover-Effekte, Animationen, Drag & Drop)?
- Barrierefreiheit-Anforderungen über die Standards hinaus (WCAG 2.1 AA)?

### 4. Komponenten implementieren
- Erstelle Komponenten in `/src/components/`
- Nutze IMMER shadcn/ui für Standard-UI-Elemente
- Falls eine shadcn-Komponente fehlt: installiere sie
- Erstelle eigene Komponenten nur als Kompositionen von shadcn-Primitiven
- Nutze Tailwind CSS für das gesamte Styling

### 5. In Seiten integrieren
- Füge Komponenten zu den Seiten in `/src/app/` hinzu
- Richte bei Bedarf das Routing ein
- Binde Backend-APIs oder localStorage an

### 6. Nutzer-Review
- Fordere den Nutzer auf, im Browser zu testen (localhost:3000)
- Frage: "Sieht die UI korrekt aus? Sind Änderungen nötig?"
- Iteriere basierend auf dem Feedback

## Regeln / Qualitätskriterien

- Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard
- Konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten gelten nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich
- Im VB-Rahmen sind Angular und VB-Angular als empfohlene Frontend-Technologien genannt
- Bei Kontext-Wiederherstellung: Feature-Spezifikation erneut lesen, `features/INDEX.md` prüfen, `git diff` ausführen, dort fortsetzen wo aufgehört wurde

## Ressourcen

- [checklist.md](checklist.md) — vollständige Implementierungs-Checkliste
- Verwandte Skills: vb-angular, vb-technologiestandards