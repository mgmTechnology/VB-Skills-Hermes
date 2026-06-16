---
name: vb-solution-architecture
description: VB-adaptierter Skill für PM-freundliche technische Designs. Übersetzt Feature-Spezifikationen in verständliche Architekturpläne für nicht-technische Stakeholder.
---

# VB Solution Architecture

## Ziel

Technik-/Architektur-Skill für PM-freundliche technische Designs. Der Skill ist nützlich, wenn Architekturentscheidungen verständlich für Projektleitung, Fachbereich oder Management erklärt werden sollen. Übersetzt Feature-Spezifikationen in verständliche Architekturpläne. Zielgruppe sind Produktmanager und nicht-technische Stakeholder.

## Vorgehen

### Vor dem Start
- Lies `features/INDEX.md`, um den Projektkontext zu verstehen
- Verifiziere, dass das Feature eine vollständige Spezifikation hat (Status "Planned", Spezifikationsdatei existiert)
- Prüfe bestehende Komponenten: `git ls-files src/components/`
- Prüfe bestehende APIs: `git ls-files src/app/api/`
- Lies die Feature-Spezifikation

### 1. Feature-Spezifikation lesen
- Verstehe User-Stories + Akzeptanzkriterien
- Bestimme: Benötigen wir ein Backend? Oder ist es rein Frontend-basiert?

### 2. Klärende Fragen stellen (falls nötig)
- Benötigen wir Login/Nutzer-Accounts?
- Sollen die Daten über Geräte hinweg synchronisiert werden?
- Gibt es verschiedene Nutzerrollen?
- Gibt es Integrationen von Drittanbietern?

### 3. High-Level Design erstellen
A) Komponentenstruktur (Visueller Baum) — zeige welche UI-Teile benötigt werden
B) Datenmodell (einfache Sprache) — beschreibe welche Informationen gespeichert werden
C) Technische Entscheidungen (begründet für PM) — erkläre WARUM in einfacher Sprache
D) Abhängigkeiten (zu installierende Pakete) — liste Paketnamen mit kurzem Zweck

### 4. Design zur Feature-Spezifikation hinzufügen
- Füge Abschnitt "Tech Design (Solution Architect)" zur Feature-Spezifikation hinzu

### 5. Technische Entscheidungen protokollieren
- Protokolliere jede bedeutsame technische Entscheidung im Decision-Log der Spezifikation

### 6. Nutzer-Review
- Präsentiere das Design zur Prüfung
- Frage: "Ist dieses Design verständlich? Gibt es Fragen?"
- Warte auf die Freigabe

## Regeln / Qualitätskriterien

- KRITISCH: Schreibe NIEMALS Code und zeige keine Implementierungsdetails
- Keine SQL-Abfragen, kein TypeScript/JavaScript Code, keine Schnipsel von API-Implementierungen
- Fokus: WAS wird gebaut und WARUM, nicht das detaillierte WIE
- Dieser Skill schreibt bewusst keine Implementierungsdetails
- Für VB-Architekturprüfung zusätzlich vb-architekturleitlinien und vb-loesungscheck nutzen
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich

## Ressourcen

- Verwandte Skills: vb-architekturleitlinien, vb-loesungscheck