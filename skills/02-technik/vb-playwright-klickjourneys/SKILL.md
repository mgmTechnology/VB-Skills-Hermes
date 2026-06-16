---
name: "vb-playwright-klickjourneys"
description: "Erstellt, stabilisiert, diagnostiziert und dokumentiert Playwright-Klickjourneys für Web-Applikationen. Für Entwickler in jedem Web-Projekt nutzbar."
---

# vb-playwright-klickjourneys

## VB-Einordnung

Dieser Skill ist ein zentraler Technik- und Testautomatisierungs-Skill für Web-Projekte.

Er soll von jedem Entwickler für das jeweilige Web-Projekt angewendet werden können, wenn Klickstrecken, Smoke Tests, Regressionstests, Login-Strecken, Navigationsstrecken oder fachliche End-to-End-Prozesse mit Playwright erstellt, ausgeführt oder stabilisiert werden sollen.

## Typische Nutzung im VB-Skill-System

Der Skill wird besonders häufig kombiniert mit:

- `vb-lotse`
- `vb-it-ae-entwickler`
- `vb-testautomatisierung`
- `vb-testmanager`
- `vb-code-review`
- `vb-anonymisierung`
- `vb-dsgvo-pruefung`
- `vb-dokumentation`

## Sicherheits- und Datenschutz-Hinweis

Bei Klickjourneys können sensible Daten in Testskripten, Screenshots, Videos, Traces, Reports, Storage-State-Dateien oder `.env`-Dateien landen.

Daher gilt:

- keine echten personenbezogenen Daten in Testskripten verwenden
- keine Passwörter oder Tokens in Git einchecken
- `auth.json`, `.env`, `playwright-report/` und `test-results/` prüfen bzw. ignorieren
- bei Testdaten zusätzlich `vb-anonymisierung` und `vb-testdaten-governance` verwenden
- produktive Systeme nicht ohne ausdrückliche Freigabe automatisiert anklicken

---

# Skill: Playwright Klickjourneys für Web-Applikationen erstellen

## Zweck

Dieser Skill unterstützt dabei, für Web-Applikationen automatisierte Klickjourneys mit Playwright zu erstellen, auszuführen und auszuwerten.

Er ist besonders geeignet für:

* Smoke Tests
* Regressionstests
* Login- und Navigationsstrecken
* fachliche End-to-End-Prozesse
* wiederholbare Tests nach Deployments
* Dokumentation von Benutzerabläufen
* technische Qualitätssicherung in Web-Projekten

Typische Zielsysteme sind interne oder externe Web-Anwendungen, z. B. Test-, Abnahme- oder Produktionsumgebungen.

---

## Wann dieser Skill verwendet werden soll

Verwende diesen Skill, wenn der Benutzer eine der folgenden Aufgaben beschreibt:

* „Ich möchte eine Klickjourney aufzeichnen.“
* „Ich möchte testen, ob eine Web-Anwendung noch funktioniert.“
* „Ich möchte mit Playwright einen Test erzeugen.“
* „Ich möchte eine Login-Strecke automatisieren.“
* „Ich möchte eine Web-Anwendung mit Browser-Klicks testen.“
* „Ich habe mit `npx playwright codegen` etwas aufgezeichnet.“
* „Playwright findet keine Tests.“
* „Der Playwright Report wird nicht erzeugt.“
* „Cannot find module '@playwright/test'“
* „No tests found“

---

## Grundprinzip

Playwright kann Benutzerinteraktionen im Browser aufzeichnen und daraus automatisierten Testcode erzeugen.

Der typische Ablauf ist:

1. Projektordner vorbereiten
2. Playwright installieren
3. Browser installieren
4. Klickjourney mit Codegen aufzeichnen
5. Testdatei speichern
6. Test ausführen
7. HTML-Report öffnen
8. Fehler analysieren und Test stabilisieren

---

## Voraussetzungen

Auf dem Rechner müssen installiert sein:

* Node.js
* npm
* Zugriff auf die Ziel-Webanwendung
* ein lokaler Projektordner
* optional Git

Prüfbefehle:

```bash
node --version
npm --version
```

Falls Node.js oder npm fehlen, müssen diese zuerst installiert werden.

---

## Empfohlene Projektstruktur

Beispiel:

```text
C:\Dev\Github\testVBON
├─ package.json
├─ package-lock.json
├─ node_modules
├─ playwright.config.ts
├─ tests
│  └─ klickjourney.spec.ts
├─ playwright-report
└─ test-results
```

Der Ordner `tests` enthält die eigentlichen Playwright-Testdateien.

---

## Initialisierung eines neuen Playwright-Projekts

Im Projektordner ausführen:

```bash
cd C:\Dev\Github\testVBON
npm init -y
npm install -D @playwright/test
npx playwright install
```

Alternativ kann Playwright vollständig initialisiert werden mit:

```bash
npm init playwright@latest
```

Diese Variante erzeugt zusätzlich eine Playwright-Konfiguration und Beispieltests.

---

## Klickjourney aufzeichnen

Allgemeines Muster:

```bash
npx playwright codegen https://zielsystem.example.org/ --output tests/klickjourney.spec.ts
```

Windows-cmd-Variante:

```bat
npx playwright codegen https://zielsystem.example.org/ --output tests\klickjourney.spec.ts
```

Beispiel für VBON-Testumgebung:

```bat
npx playwright codegen https://test.vbon.de/ --output tests\vbon-klickjourney.spec.ts
```

Während der Aufzeichnung:

1. Es öffnet sich ein Browser.
2. Die gewünschte Journey wird manuell durchgeklickt.
3. Playwright erzeugt parallel Testcode.
4. Die Datei wird unter dem angegebenen Pfad gespeichert.
5. Nach Abschluss das Codegen-Fenster sauber schließen.

Nicht sofort mit `Strg+C` abbrechen, da sonst eventuell keine vollständige Testdatei erzeugt wird.

---

## Prüfen, ob die Testdatei erzeugt wurde

Im Projektordner:

```bat
dir tests
```

Datei anzeigen:

```bat
type tests\vbon-klickjourney.spec.ts
```

Eine gültige Playwright-Testdatei enthält mindestens:

```ts
import { test, expect } from '@playwright/test';

test('test', async ({ page }) => {
  await page.goto('https://test.vbon.de/');
});
```

Wichtig ist insbesondere der `test(...)`-Block.

---

## Test ausführen

Aus dem Projektordner:

```bat
npx playwright test tests\vbon-klickjourney.spec.ts
```

Bei Shells wie Git Bash, Cmder oder ähnlichen Umgebungen besser mit Slash und Anführungszeichen:

```bash
npx playwright test "tests/vbon-klickjourney.spec.ts"
```

Alle Tests ausführen:

```bash
npx playwright test
```

---

## Report anzeigen

Nach einem Testlauf:

```bash
npx playwright show-report
```

Der Report liegt normalerweise unter:

```text
playwright-report/
```

Falls noch kein Test ausgeführt wurde, erscheint sinngemäß:

```text
No report found
```

Das ist normal, solange noch kein erfolgreicher oder fehlgeschlagener Testlauf stattgefunden hat.

---

## Typische Fehler und Lösungen

### Fehler: `No report found`

Ursache:

* Es wurde noch kein Test ausgeführt.
* Der vorherige Testlauf wurde abgebrochen.
* Es wurde kein Report erzeugt.

Lösung:

```bash
npx playwright test
npx playwright show-report
```

---

### Fehler: `No tests found`

Mögliche Ursachen:

* Der Pfad zur Testdatei ist falsch.
* Man befindet sich im falschen Ordner.
* Die Datei enthält keinen gültigen `test(...)`-Block.
* Die Datei liegt nicht unter dem erwarteten Testverzeichnis.
* Die Shell interpretiert Backslashes ungünstig.

Prüfen:

```bat
dir tests
type tests\vbon-klickjourney.spec.ts
findstr /n "test(" tests\vbon-klickjourney.spec.ts
```

Alternative Ausführung:

```bash
npx playwright test "tests/vbon-klickjourney.spec.ts"
```

---

### Fehler: `Cannot find module '@playwright/test'`

Ursache:

Das Paket `@playwright/test` ist im Projekt nicht installiert.

Lösung:

```bash
npm init -y
npm install -D @playwright/test
npx playwright install
```

Danach erneut:

```bash
npx playwright test "tests/vbon-klickjourney.spec.ts"
```

---

### Fehler durch falschen Arbeitsordner

Beispielproblem:

Man befindet sich bereits in:

```text
C:\Dev\Github\testVBON\tests
```

und startet dann:

```bat
npx playwright test tests\vbon-klickjourney.spec.ts
```

Dann wird effektiv nach folgendem Pfad gesucht:

```text
C:\Dev\Github\testVBON\tests\tests\vbon-klickjourney.spec.ts
```

Lösung:

Entweder eine Ebene zurück:

```bat
cd ..
npx playwright test tests\vbon-klickjourney.spec.ts
```

Oder direkt aus dem `tests`-Ordner:

```bat
npx playwright test vbon-klickjourney.spec.ts
```

---

## Empfohlene Playwright-Konfiguration

Eine typische `playwright.config.ts` kann so aussehen:

```ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
  testDir: './tests',
  timeout: 60_000,
  expect: {
    timeout: 10_000
  },
  fullyParallel: false,
  retries: 0,
  reporter: [
    ['html'],
    ['list']
  ],
  use: {
    baseURL: 'https://test.vbon.de/',
    trace: 'on-first-retry',
    screenshot: 'only-on-failure',
    video: 'retain-on-failure',
    ignoreHTTPSErrors: true
  },
  projects: [
    {
      name: 'chromium',
      use: { ...devices['Desktop Chrome'] }
    }
  ]
});
```

Für interne Testsysteme ist `ignoreHTTPSErrors: true` häufig hilfreich, wenn Zertifikate oder Testumgebungen nicht vollständig browservertrauenswürdig sind.

---

## Stabilisierung aufgezeichneter Tests

Aufgezeichnete Tests sind oft ein guter Start, aber nicht immer stabil.

Nach der Aufzeichnung sollten folgende Punkte geprüft werden:

* Werden robuste Selektoren verwendet?
* Gibt es dynamische IDs?
* Gibt es Wartezeiten, die besser durch Assertions ersetzt werden sollten?
* Sind Testdaten eindeutig?
* Gibt es Seiteneffekte durch bereits vorhandene Daten?
* Ist der Test unabhängig wiederholbar?
* Wird nach fachlichen Ergebnissen geprüft, nicht nur nach Klicks?

Schlechter Ansatz:

```ts
await page.waitForTimeout(5000);
```

Besserer Ansatz:

```ts
await expect(page.getByText('Angebot wurde gespeichert')).toBeVisible();
```

---

## Empfohlene Selektorstrategie

Bevorzugte Reihenfolge:

1. `getByRole`
2. `getByLabel`
3. `getByText`
4. `getByPlaceholder`
5. `getByTestId`
6. CSS-Selektoren nur bei Bedarf

Beispiele:

```ts
await page.getByRole('button', { name: 'Anmelden' }).click();
await page.getByLabel('Benutzername').fill('testuser');
await page.getByText('Angebot speichern').click();
await page.getByTestId('save-offer-button').click();
```

Für langlebige Tests sollten in der Anwendung gezielt `data-testid`-Attribute ergänzt werden.

Beispiel:

```html
<button data-testid="save-offer-button">Speichern</button>
```

Playwright:

```ts
await page.getByTestId('save-offer-button').click();
```

---

## Umgang mit Login, SSO und 2FA

Bei Anwendungen mit Login, CAS, SSO oder 2FA muss die Teststrategie bewusst festgelegt werden.

Mögliche Varianten:

### Variante 1: Login vollständig mit testen

Geeignet für Smoke Tests der gesamten Strecke.

Nachteil:

* anfällig bei 2FA
* langsamer
* abhängig vom Authentifizierungssystem

### Variante 2: Login einmalig vorbereiten und Session speichern

Playwright kann einen eingeloggten Zustand speichern:

```bash
npx playwright codegen https://test.vbon.de/ --save-storage=auth.json
```

Nutzung im Test:

```ts
test.use({ storageState: 'auth.json' });
```

Wichtig:

* `auth.json` enthält potentiell sensible Sitzungsinformationen.
* Nicht in Git einchecken.
* In `.gitignore` aufnehmen.

### Variante 3: Technischen Testbenutzer verwenden

Für CI/CD und regelmäßige Tests oft die beste Variante.

Voraussetzungen:

* dedizierter Testbenutzer
* klare Berechtigungen
* keine produktiven Daten
* keine personenbezogenen Echtdaten
* definierte Testdaten

---

## Datenschutz und Sicherheit

Bei internen Web-Anwendungen ist besonders zu beachten:

* Keine echten personenbezogenen Daten in Testskripten verwenden.
* Keine Passwörter im Code speichern.
* Keine Session-Dateien in Git einchecken.
* Testdaten müssen anonymisiert oder synthetisch sein.
* Screenshots und Videos können sensible Inhalte enthalten.
* Reports aus Testsystemen nicht unkontrolliert verteilen.
* Zugriff auf Reports und Artefakte einschränken.

Empfohlene `.gitignore`-Einträge:

```gitignore
node_modules/
playwright-report/
test-results/
auth.json
.env
```

---

## Verwendung von Umgebungsvariablen

Zugangsdaten und Zielsysteme sollten nicht hart im Test stehen.

Beispiel `.env`:

```env
BASE_URL=https://test.vbon.de/
TEST_USER=testuser
TEST_PASSWORD=geheim
```

Hinweis:

Die `.env`-Datei nicht einchecken.

Beispiel im Test:

```ts
const baseUrl = process.env.BASE_URL ?? 'https://test.vbon.de/';
```

---

## Sinnvolle Journey-Typen

Für Web-Applikationen sind besonders diese Journey-Typen geeignet:

### Smoke Journey

Prüft, ob die Anwendung grundsätzlich erreichbar und bedienbar ist.

Beispiel:

```text
Startseite öffnen
Login anzeigen
Hauptnavigation prüfen
Logout
```

### Fachliche Kernjourney

Prüft einen zentralen Geschäftsprozess.

Beispiel:

```text
Login
Kundendaten erfassen
Angebot berechnen
Ergebnis prüfen
Angebot speichern
Angebot erneut laden
```

### Regressionsjourney

Prüft bekannte kritische Stellen nach Änderungen.

Beispiel:

```text
Bestehenden Vorgang öffnen
Daten ändern
Speichern
Validierung prüfen
```

### Monitoring-Journey

Prüft regelmäßig, ob eine Anwendung oder ein Kernprozess technisch funktioniert.

Beispiel:

```text
Login
Dashboard öffnen
Backend-Status prüfen
Logout
```

---

## Vorgehen bei bestehenden Projekten

1. Projektordner öffnen
2. Prüfen, ob `package.json` existiert
3. Playwright installieren
4. `tests`-Ordner anlegen
5. Journey mit Codegen aufzeichnen
6. Test ausführen
7. Test stabilisieren
8. Test in Git aufnehmen
9. Optional in CI/CD integrieren

Befehle:

```bash
npm install -D @playwright/test
npx playwright install
mkdir tests
npx playwright codegen https://zielsystem.example.org/ --output tests/klickjourney.spec.ts
npx playwright test
npx playwright show-report
```

---

## Vorgehen bei neuen Projekten

1. Neuen Projektordner anlegen
2. npm initialisieren
3. Playwright initialisieren
4. Zielsystem festlegen
5. Erste Smoke Journey erstellen
6. Konfiguration prüfen
7. Testdatenstrategie festlegen
8. Repository vorbereiten

Befehle:

```bash
mkdir testprojekt
cd testprojekt
npm init -y
npm install -D @playwright/test
npx playwright install
mkdir tests
npx playwright codegen https://zielsystem.example.org/ --output tests/smoke.spec.ts
npx playwright test
```

---

## Minimale Beispiel-Testdatei

```ts
import { test, expect } from '@playwright/test';

test('smoke test', async ({ page }) => {
  await page.goto('https://test.vbon.de/');
  await expect(page).toHaveURL(/test\.vbon\.de/);
});
```

---

## Beispiel für VBON-Testumgebung

```ts
import { test, expect } from '@playwright/test';

test('VBON Startseite erreichbar', async ({ page }) => {
  await page.goto('https://test.vbon.de/');
  await expect(page).toHaveURL(/test\.vbon\.de/);
});
```

Aufruf:

```bash
npx playwright test "tests/vbon-klickjourney.spec.ts"
```

Report:

```bash
npx playwright show-report
```

---

## Qualitätsempfehlungen

Eine gute Klickjourney sollte:

* fachlich verständlich benannt sein
* nicht zu viele unterschiedliche Dinge gleichzeitig prüfen
* möglichst stabile Selektoren verwenden
* klare Assertions enthalten
* mit definierten Testdaten arbeiten
* unabhängig wiederholbar sein
* keine vertraulichen Daten im Code enthalten
* bei Fehlern aussagekräftige Reports erzeugen

Schlecht:

```text
Ein riesiger Test klickt durch die komplette Anwendung ohne klare Prüfungen.
```

Besser:

```text
Mehrere kleine Journeys prüfen jeweils einen klaren fachlichen Ablauf.
```

---

## Empfohlene Benennung

Dateien:

```text
smoke.spec.ts
login.spec.ts
angebot-anlegen.spec.ts
angebot-speichern.spec.ts
regression-finalisierung.spec.ts
```

Tests:

```ts
test('Benutzer kann sich anmelden', async ({ page }) => {
  // ...
});

test('Angebot kann berechnet und gespeichert werden', async ({ page }) => {
  // ...
});
```

---

## Checkliste für die KI

Wenn der Benutzer Unterstützung bei Playwright-Klickjourneys möchte, prüfe systematisch:

1. In welchem Projektordner befindet sich der Benutzer?
2. Gibt es eine `package.json`?
3. Ist `@playwright/test` installiert?
4. Sind die Playwright-Browser installiert?
5. Existiert ein `tests`-Ordner?
6. Existiert die angegebene `.spec.ts`-Datei?
7. Enthält die Datei einen `test(...)`-Block?
8. Wird der Test aus dem richtigen Ordner gestartet?
9. Wird bei gemischten Shells besser `/` statt `\` verwendet?
10. Gibt es einen Report erst nach einem Testlauf?
11. Sind Login, 2FA, SSO oder Zertifikate beteiligt?
12. Sind sensible Daten im Test oder Report enthalten?

---

## Diagnosebefehle

Projektinhalt anzeigen:

```bat
dir
```

Tests anzeigen:

```bat
dir tests
```

Dateiinhalt anzeigen:

```bat
type tests\vbon-klickjourney.spec.ts
```

Nach Testblöcken suchen:

```bat
findstr /n "test(" tests\vbon-klickjourney.spec.ts
```

Paket prüfen:

```bat
npm list @playwright/test
```

Playwright-Version prüfen:

```bat
npx playwright --version
```

Test mit Report ausführen:

```bat
npx playwright test
npx playwright show-report
```

---

## Standardantwort bei `Cannot find module '@playwright/test'`

Wenn diese Fehlermeldung erscheint:

```text
Error: Cannot find module '@playwright/test'
```

Dann antworte:

```text
Das Playwright-Testpaket ist im Projekt nicht installiert. Führe im Projektordner aus:

npm init -y
npm install -D @playwright/test
npx playwright install

Danach:

npx playwright test "tests/vbon-klickjourney.spec.ts"
```

---

## Standardantwort bei `No tests found`

Wenn diese Fehlermeldung erscheint:

```text
Error: No tests found.
```

Dann antworte:

```text
Playwright findet keine ausführbare Testdatei oder keinen gültigen test(...)-Block.

Prüfe:

dir tests
type tests\vbon-klickjourney.spec.ts
findstr /n "test(" tests\vbon-klickjourney.spec.ts

Starte den Test aus dem Projektordner mit:

npx playwright test "tests/vbon-klickjourney.spec.ts"
```

---

## Standardantwort bei `No report found`

Wenn diese Meldung erscheint:

```text
No report found
```

Dann antworte:

```text
Es wurde noch kein Playwright-Testlauf ausgeführt oder es wurde kein Report erzeugt.

Führe zuerst aus:

npx playwright test

Danach:

npx playwright show-report
```

---

## Zielbild

Am Ende soll der Benutzer eine versionierbare, wiederholbare und auswertbare Klickjourney besitzen.

Ergebnisartefakte:

```text
tests/*.spec.ts
playwright.config.ts
playwright-report/
test-results/
```

Der eigentliche Mehrwert entsteht nicht durch die reine Aufzeichnung, sondern durch die anschließende Stabilisierung:

* klare Testnamen
* robuste Selektoren
* fachliche Assertions
* saubere Testdaten
* sichere Behandlung von Zugangsdaten
* CI/CD-Fähigkeit
