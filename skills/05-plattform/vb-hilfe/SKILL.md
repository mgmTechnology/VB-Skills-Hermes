---
name: vb-hilfe
description: Erklärt Nutzern, wo sie sich im Workflow befinden und welcher nächste Schritt sinnvoll ist.
---

# vb-hilfe

## Ziel
Plattform-Skill, der Nutzern erklärt, wo sie sich im Workflow befinden und welcher nächste Schritt sinnvoll ist. Analysiert den aktuellen Projektzustand (PRD, Feature-Index, Feature-Specs, Codebase) und empfiehlt den passenden nächsten Befehl. Bei unklarem Kontext zuerst `vb-lotse` verwenden.

## Vorgehen

### Schritt 1: Aktuellen Zustand analysieren
- **PRD prüfen**: Lies `docs/PRD.md` — ist es noch die leere Vorlage oder ausgefüllt?
- **Feature-Index prüfen**: Lies `features/INDEX.md` — keine Features vorhanden oder welche mit Status?
- **Feature-Specs prüfen**: Für jedes Feature prüfen ob Tech Design, QA Test Results oder Deployment existieren.
- **Codebase scannen**: Prüfe vorhandene Komponenten (`src/components/`), API-Routen (`src/app/api/`) und shadcn-Komponenten (`src/components/ui/`).

### Schritt 2: Nächste Aktion bestimmen
- PRD leer → `/init` mit Projektbeschreibung ausführen.
- PRD existiert, keine Features → `/write-spec` für erste Feature-Spezifikation.
- Features mit Status "Geplant" → `/architecture` für Tech Design.
- Features mit Tech Design, keine Implementierung → `/frontend` (und ggf. `/backend`).
- Features implementiert, keine QA → `/qa` ausführen.
- Features mit QA, nicht deployed → `/deploy` ausführen.
- Alle Features deployed → `/write-spec` für neues Feature oder PRD prüfen.

### Schritt 3: Nutzerfragen beantworten
- "Welche Skills sind verfügbar?" → Liste aller Skills mit Kurzbeschreibungen.
- "Wie füge ich ein neues Feature hinzu?" → `/write-spec` Workflow erklären.
- "Wie passe ich diese Vorlage an?" → Auf `CLAUDE.md`, `rules/`, `skills/` verweisen.
- "Wie ist die Projektstruktur?" → Verzeichnislayout erklären.
- "Wie führe ich ein Deployment durch?" → `/deploy` Workflow und Voraussetzungen.

### Ausgabeformat
- Aktueller Projektstatus (kurze Zusammenfassung)
- Feature-Übersicht (Tabelle aus INDEX.md)
- Empfohlener nächster Schritt (exakter Befehl)
- Weitere verfügbare Aktionen
- Bei spezifischer Nutzerfrage: diese ZUERST beantworten, dann Statusübersicht.

## Regeln / Qualitätskriterien
- Sei prägnant und handlungsorientiert.
- Gib immer den exakten Befehl an.
- Beziehe dich auf spezifische Dateipfade.
- Erkläre Framework-Architektur nicht im Detail, außer es wird danach gefragt.
- Fokus auf: "Hier stehst du, das ist als Nächstes zu tun."
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen explizite Nutzerbestätigung einholen.

## Ressourcen
- Skill-Finder: vb-skill-finder
- Skill-Katalog: vb-skill-katalog