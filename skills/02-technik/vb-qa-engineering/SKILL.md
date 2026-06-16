---
name: vb-qa-engineering
description: VB-adaptierter Skill für Tests gegen Akzeptanzkriterien, Bug-Finding und Security-nahe Prüfung nach Implementierung.
---

# VB QA Engineering

## Ziel

Technik-/Qualitätsskill für Tests gegen Akzeptanzkriterien, Bug-Finding und Security-nahe Prüfung nach Implementierung. Ergänzt vb-testmanager, vb-tester-fachabteilung, vb-tester-it-betrieb, vb-testautomatisierung und vb-sicherheitspruefung.

## Vorgehen

### Vor dem Start
- Lies `features/INDEX.md` für den Projektkontext
- Lies die vom Nutzer referenzierte Feature-Spezifikation
- Prüfe kürzlich implementierte Features: `git log --oneline --grep="PROJ-" -10`
- Prüfe kürzliche Fehlerbehebungen: `git log --oneline --grep="fix" -10`
- Prüfe Playwright-Browser-Installation: `npx playwright install --dry-run 2>&1 | head -5`

### 1. Feature-Spezifikation lesen
- Verstehe ALLE Akzeptanzkriterien
- Verstehe ALLE dokumentierten Edge-Cases
- Verstehe die technischen Design-Entscheidungen
- Notiere alle Abhängigkeiten zu anderen Features

### 2. Manuelle Tests
- Teste JEDES Akzeptanzkriterium (Erfolg/Fehlschlag markieren)
- Teste ALLE dokumentierten Edge-Cases
- Teste undokumentierte Edge-Cases
- Browserübergreifend: Chrome, Firefox, Safari
- Responsiv: Mobil (375px), Tablet (768px), Desktop (1440px)

### 3. Sicherheitsaudit (Red Team)
- Teste Versuche zur Umgehung der Authentifizierung
- Teste die Autorisierung (Kann Nutzer X auf Daten von Nutzer Y zugreifen?)
- Teste Input-Injection (XSS, SQL-Injection über UI-Eingaben)
- Teste Rate-Limiting
- Prüfe auf offenliegende Secrets
- Prüfe auf sensible Daten in API-Antworten

### 4. Regressionstests
- Verifiziere bestehende Features mit Status "Deployed"
- Teste Kern-Flows verwandter Features
- Verifiziere keine visuellen Regressionen

### 5. Automatisierte Tests ausführen
- `npm test` (Vitest: Integrationstests)
- `npm run test:e2e` (Playwright: E2E-Tests)

### 6. Unit-Tests schreiben
- Teste Custom-Hooks mit nicht-trivialer Logik, Utility-Funktionen, Formular-Validierungslogik
- Nicht testen: reine Darstellungskomponenten, bereits durch E2E abgedeckte Logik
- Für jeden Test: Happy Path, Fehlerpfade, Edge-Cases
- Ausführen: `npm test`

### 7. E2E-Tests schreiben
- Schreibe für jedes bestandene Akzeptanzkriterium einen Playwright-Test
- Ein `test()` pro Akzeptanzkriterium
- Ausführen: `npm run test:e2e`

### 8. Ergebnisse dokumentieren
- Füge den Abschnitt "QA Test Results" zur Feature-Spezifikationsdatei hinzu

### 9. Nutzer-Review
- Präsentiere Testergebnisse mit Zusammenfassung
- Frage: "Welche Fehler sollten zuerst behoben werden?"

## Regeln / Qualitätskriterien

- Behebe Fehler NIEMALS selbst — das ist Aufgabe der Frontend-/Backend-Skills
- Fokus: Finden, Dokumentieren, Priorisieren
- Sei gründlich und objektiv: Berichte auch kleine Fehler
- Kritisch (Critical): Sicherheitslücken, Datenverlust, vollständiger Ausfall
- Hoch (High): Kernfunktionalität defekt, blockierende Probleme
- Mittel (Medium): Nicht-kritische Funktionsfehler, Workarounds existieren
- Niedrig (Low): UX-Themen, kosmetische Probleme
- BEREIT (READY): Keine verbleibenden kritischen oder hohen Fehler
- NICHT BEREIT (NOT READY): Kritische oder hohe Fehler vorhanden
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich

## Ressourcen

- [test-template.md](test-template.md) — Vorlage für QA Test Results
- Verwandte Skills: vb-testmanager, vb-tester-fachabteilung, vb-tester-it-betrieb, vb-testautomatisierung, vb-sicherheitspruefung