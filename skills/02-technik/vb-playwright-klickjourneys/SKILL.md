---
name: vb-playwright-klickjourneys
description: Erstellt, stabilisiert, diagnostiziert und dokumentiert Playwright-Klickjourneys für Web-Applikationen. Für Entwickler in jedem Web-Projekt nutzbar.
---

# VB Playwright Klickjourneys

## Ziel

Zentraler Technik- und Testautomatisierungs-Skill für Web-Projekte. Erstellen, Ausführen, Stabilisieren und Dokumentieren von Klickjourneys mit Playwright. Geeignet für Smoke Tests, Regressionstests, Login- und Navigationsstrecken, fachliche End-to-End-Prozesse, wiederholbare Tests nach Deployments und Dokumentation von Benutzerabläufen.

Typische Zielsysteme: interne oder externe Web-Anwendungen (Test-, Abnahme- oder Produktionsumgebungen).

## Vorgehen

### Projekt initialisieren
- Node.js und npm müssen installiert sein (prüfen: `node --version`, `npm --version`)
- Im Projektordner: `npm init -y`, `npm install -D @playwright/test`, `npx playwright install`

### Klickjourney aufzeichnen
- Allgemein: `npx playwright codegen https://zielsystem.example.org/ --output tests/klickjourney.spec.ts`
- Während der Aufzeichnung öffnet sich ein Browser; Journey manuell durchklicken
- Nach Abschluss das Codegen-Fenster sauber schließen (nicht mit Strg+C abbrechen)
- Prüfen ob Testdatei erzeugt wurde: `dir tests`
- Eine gültige Playwright-Testdatei enthält mindestens `import { test, expect } from '@playwright/test'` und einen `test(...)`-Block

### Test ausführen
- `npx playwright test tests\klickjourney.spec.ts`
- Bei Shells wie Git Bash: `npx playwright test "tests/klickjourney.spec.ts"`
- Alle Tests: `npx playwright test`

### Report anzeigen
- `npx playwright show-report` (Report liegt unter `playwright-report/`)

### Stabilisierung aufgezeichneter Tests
- Robuste Selektoren verwenden (keine dynamischen IDs)
- Wartezeiten durch Assertions ersetzen: `await expect(page.getByText('Angebot wurde gespeichert')).toBeVisible()` statt `await page.waitForTimeout(5000)`
- Testdaten auf Eindeutigkeit prüfen
- Seiteneffekte durch bereits vorhandene Daten vermeiden
- Test muss unabhängig wiederholbar sein

### Selektorstrategie (bevorzugte Reihenfolge)
1. `getByRole`
2. `getByLabel`
3. `getByText`
4. `getByPlaceholder`
5. `getByTestId`
6. CSS-Selektoren nur bei Bedarf

### Umgang mit Login, SSO und 2FA
- Login vollständig mit testen (anfällig bei 2FA, langsamer)
- ODER: Session speichern: `npx playwright codegen https://test.vbon.de/ --save-storage=auth.json`, dann im Test `test.use({ storageState: 'auth.json' })`

### Playwright-Konfiguration
- Typische `playwright.config.ts` mit `testDir: './tests'`, `timeout: 60_000`, `reporter: [['html'], ['list']]`, `trace: 'on-first-retry'`, `screenshot: 'only-on-failure'`, `video: 'retain-on-failure'`
- Für interne Testsysteme: `ignoreHTTPSErrors: true`

## Regeln / Qualitätskriterien

### Sicherheits- und Datenschutz
- Keine echten personenbezogenen Daten in Testskripten verwenden
- Keine Passwörter oder Tokens in Git einchecken
- `auth.json`, `.env`, `playwright-report/` und `test-results/` prüfen bzw. ignorieren
- Bei Testdaten zusätzlich `vb-anonymisierung` und `vb-testdaten-governance` verwenden
- Produktive Systeme nicht ohne ausdrückliche Freigabe automatisiert anklicken

### Typische Fehler und Lösungen
- **No report found**: Noch kein Test ausgeführt oder vorheriger Testlauf abgebrochen → `npx playwright test` + `npx playwright show-report`
- **No tests found**: Pfad falsch, falscher Ordner, kein gültiger `test(...)`-Block, Datei nicht unter Testverzeichnis, Shell interpretiert Backslashes ungünstig → Pfad und Ordner prüfen, mit Anführungszeichen und Slash ausführen
- **Cannot find module '@playwright/test'**: Paket nicht installiert → `npm init -y && npm install -D @playwright/test && npx playwright install`
- **Falscher Arbeitsordner**: Doppelte Pfade vermeiden (nicht aus `tests/` Ordner `tests/datei.spec.ts` aufrufen)

## Ressourcen

- Häufig kombiniert mit: vb-lotse, vb-it-ae-entwickler, vb-testautomatisierung, vb-testmanager, vb-code-review, vb-anonymisierung, vb-dsgvo-pruefung, vb-dokumentation
- Empfohlene Projektstruktur: `package.json`, `playwright.config.ts`, `tests/`, `playwright-report/`, `test-results/`
