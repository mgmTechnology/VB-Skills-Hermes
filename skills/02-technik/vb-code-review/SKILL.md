---
name: vb-code-review
description: VB-adaptierter Skill für strukturierte Code Reviews mit starkem Dokumentationsfokus (JavaDoc/JSDoc) und klaren Reviewphasen.
---

# VB Code Review

## Ziel

Technik-Skill für strukturierte Code Reviews. Der importierte Skill ergänzt die bestehende VB-Struktur um einen starken Dokumentationsfokus mit JavaDoc/JSDoc sowie klare Reviewphasen für Qualität, Architektur, Security und Performance. Liefere ein vollständiges, produktionsnahes Code-Review mit konkreten, direkt umsetzbaren Hinweisen.

## Vorgehen

### Phase 1 — Kontextanalyse
- Kläre: Welche Sprache(n)/Framework(s)? Einzelner Snippet, Klasse, Modul, mehrere Dateien?
- Erkennbaren Nutzungskontext bestimmen (API, Service, Frontend, Utility)
- Falls unklar und review-relevant: beim User nachfragen

### Phase 2 — Dokumentations-Review (JavaDoc / JSDoc)
- **Dieser Schritt ist nicht optional.** Fehlende oder unvollständige Dokumentation ist ein gleichrangiger Befund wie ein funktionaler Bug.
- Java: JavaDoc für alle public/protected Klassen, Interfaces, Enums, Records, Methoden und Konstruktoren
- Java: Alle @throws/@exception deklarieren, @param, @return, @since, @deprecated
- JavaScript/TypeScript: JSDoc für alle exportierten Funktionen, Klassen, Methoden, Typen/Interfaces
- JavaScript/TypeScript: @param {Typ}, @returns, @throws, @example, @deprecated

### Phase 3 — Code-Qualitäts-Review
Prüfe systematisch:
- **Korrektheit & Logik**: Off-by-one, Null/undefined-Handling, Fehlerbehandlung, Rückgabewerte
- **Lesbarkeit & Maintainability**: Naming, Magic Numbers, Methodenlänge, Komplexität, DRY
- **Architektur & Design**: Layering, Abhängigkeiten (Coupling/Cohesion), Interfaces, Open/Closed
- **Performance**: N+1 Queries, unnötige Objekterzeugungen, Stream-Missbrauch, Caching
- **Security**: Input-Validierung, SQL-Injection/XSS/CSRF, sensible Daten, Fehlermeldungen, Auth
- **Fehlerbehandlung**: Kein leeres catch, Checked vs Unchecked, Logging-Level, try-with-resources
- **Tests**: Testabdeckung kritischer Pfade, Verhalten vs Implementierung, Edge Cases, Isolation

### Phase 4 — Priorisiertes Befund-Summary
- 🔴 KRITISCH: Funktionaler Bug, Security-Lücke, Datenverlust-Risiko
- 🟠 WICHTIG: Wartbarkeitsproblem, Performance-Issue, fehlende Fehlerbehandlung
- 🟡 VERBESSERUNG: Clean-Code-Verletzung, unvollständige Doku, Naming
- 🟢 OPTIONAL: Stilfrage, Alternative mit geringem Impact

### Phase 5 — Dokumentations-Ergänzungen
- Liefere fertige Dokumentationsblöcke (JavaDoc/JSDoc) zum direkten Einfügen

### Phase 6 — Gesamtbewertung
- Kurzes Fazit (3–6 Sätze): Gesamteindruck, Stärken, wichtigste Baustellen, Merge-Empfehlung

## Regeln / Qualitätskriterien

- Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard
- Konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten gelten nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich
- Bei Java/Spring-Boot-Projekten zusätzlich vb-java-springboot, vb-technologiestandards und ggf. vb-sicherheitspruefung berücksichtigen
- Bei mehreren Dateien: jede Datei mit eigenem Header, übergreifende Architektur-Befunde separat, Priorisierungstabelle am Ende zusammengeführt
- Jeder Befund enthält: Ort, Problem, Begründung, Fix (ggf. mit Code)

## Ressourcen

- Verwandte Skills: vb-java-springboot, vb-technologiestandards, vb-sicherheitspruefung