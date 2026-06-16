---
name: "vb-code-review"
description: "VB-adaptierter Skill. Ursprung: skills/code-review/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-code-review

## VB-Einordnung

Technik-Skill für strukturierte Code Reviews. Der importierte Skill ergänzt die bestehende VB-Struktur um einen starken Dokumentationsfokus mit JavaDoc/JSDoc sowie klare Reviewphasen für Qualität, Architektur, Security und Performance.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

Zusätzlicher VB-Hinweis: Bei Java/Spring-Boot-Projekten zusätzlich `vb-java-springboot`, `vb-technologiestandards` und ggf. `vb-sicherheitspruefung` berücksichtigen.

## Ursprüngliche Detailanweisung (Referenz)

---

# Code-Review Skill

## Ziel

Liefere ein vollständiges, produktionsnahes Code-Review mit konkreten, direkt umsetzbaren Hinweisen.
Kein oberflächliches Feedback. Jeder Befund enthält: **Was** ist das Problem, **Warum** ist es relevant,
**Wie** wird es behoben (ggf. mit Code-Snippet).

---

## Review-Phasen (immer in dieser Reihenfolge)

### Phase 1 — Kontextanalyse

Bevor du reviewst, kläre intern:
- Welche Sprache(n) / Framework(s)?
- Ist es ein einzelner Snippet, eine Klasse, ein Modul, mehrere Dateien?
- Gibt es erkennbaren Nutzungskontext (API, Service, Frontend, Utility)?

Falls unklar und review-relevant: kurz beim User nachfragen, bevor du beginnst.

---

### Phase 2 — Dokumentations-Review (JavaDoc / JSDoc)

> **Dieser Schritt ist nicht optional.** Fehlende oder unvollständige Dokumentation ist ein
> gleichrangiger Befund wie ein funktionaler Bug.

#### Java — JavaDoc-Anforderungen

Pflicht-JavaDoc für:
- Alle `public` und `protected` Klassen, Interfaces, Enums, Records
- Alle `public` und `protected` Methoden und Konstruktoren
- `public` Felder (außer selbsterklärende Konstanten wie `MAX_SIZE`)
- Alle `@throws` / `@exception` deklarieren (checked und relevant unchecked)

Qualitätskriterien:
- Klassendokumentation: Zweck der Klasse, Verantwortlichkeiten, ggf. Nutzungsbeispiel
- Methodendokumentation: Was macht die Methode (nicht wie), alle `@param`, `@return`, `@throws`
- Keine Trivial-Docs wie `/** Gets the name. */` für `getName()` ohne weiteren Kontext
- `@since`, `@deprecated` (mit `@see` Ersatz) wenn relevant
- HTML-Tags korrekt, keine kaputten `{@link}`-Referenzen

**Befund-Beispiel:**
```java
// ❌ Fehlt
public UserDto mapToDto(User user) { ... }

// ✅ Erwartet
/**
 * Konvertiert eine {@link User}-Entität in ein transportables {@link UserDto}.
 *
 * @param user die zu konvertierende Entität, darf nicht {@code null} sein
 * @return ein befülltes {@link UserDto}
 * @throws IllegalArgumentException wenn {@code user} {@code null} ist
 */
public UserDto mapToDto(User user) { ... }
```

#### JavaScript / TypeScript — JSDoc-Anforderungen

Pflicht-JSDoc für:
- Alle exportierten Funktionen, Klassen, Methoden
- Alle exportierten Typen / Interfaces (in JS ohne TS)
- Callbacks und nicht-triviale closures
- Public API-Funktionen in Modulen

Qualitätskriterien:
- `@param {Typ} name - Beschreibung` für alle Parameter (in JS; in TS Typ optional wenn klar)
- `@returns {Typ} Beschreibung`
- `@throws {ErrorTyp} Bedingung`
- `@example` für nicht-triviale Nutzung empfohlen
- `@deprecated` mit Hinweis auf Nachfolger

**Befund-Beispiel:**
```javascript
// ❌ Fehlt
export function parseConfig(raw) { ... }

// ✅ Erwartet
/**
 * Parst einen rohen Konfigurationsstring und gibt ein typisiertes Config-Objekt zurück.
 *
 * @param {string} raw - Der rohe JSON-Konfigurationsstring
 * @returns {AppConfig} Das geparste Konfigurationsobjekt
 * @throws {SyntaxError} Wenn der String kein valides JSON ist
 * @throws {ValidationError} Wenn Pflichtfelder fehlen
 * @example
 * const config = parseConfig('{"port": 8080, "debug": false}');
 */
export function parseConfig(raw) { ... }
```

---

### Phase 3 — Code-Qualitäts-Review

Prüfe systematisch folgende Dimensionen:

#### 3.1 Korrektheit & Logik
- Off-by-one Fehler, falsche Randbedingungen
- Null/undefined-Handling
- Fehlerbehandlung vollständig und sinnvoll?
- Rückgabewerte konsistent?

#### 3.2 Lesbarkeit & Maintainability
- Naming: Klassen, Methoden, Variablen sprechend und konsistent?
- Magic Numbers / Strings → Konstanten?
- Methoden zu lang / zu viel Verantwortung (Single Responsibility)?
- Komplexität: verschachtelte Ifs, tiefe Hierarchien, lange Parameterlisten?
- DRY-Verletzungen (duplizierter Code)?

#### 3.3 Architektur & Design
- Layering korrekt (z.B. kein DB-Zugriff im Controller)?
- Abhängigkeiten sinnvoll (Coupling, Cohesion)?
- Interfaces statt konkreter Implementierungen wo sinnvoll?
- Erweiterbarkeit: Open/Closed Principle erkennbar?

#### 3.4 Performance
- Unnötige DB-Queries in Schleifen (N+1)?
- Unnötige Objekt-Erzeugungen / Kopien?
- Stream-Missbrauch vs. einfache Iteration?
- Caching-Potenzial übersehen?

#### 3.5 Security
- Input-Validierung vorhanden?
- SQL-Injection, XSS, CSRF-Risiken?
- Sensible Daten (Passwörter, Tokens) korrekt behandelt?
- Fehlermeldungen geben keine internen Details preis?
- Authentifizierung / Autorisierung auf korrekter Ebene?

#### 3.6 Fehlerbehandlung & Robustheit
- Exceptions sinnvoll gefangen und behandelt (kein leeres catch)?
- Checked vs. Unchecked korrekt eingesetzt (Java)?
- Logging auf korrektem Level (kein `e.printStackTrace()`)?
- Ressourcen werden geschlossen (try-with-resources, etc.)?

#### 3.7 Tests (falls vorhanden oder fehlen)
- Testabdeckung der kritischen Pfade?
- Tests testen Verhalten, nicht Implementierungsdetails?
- Edge Cases abgedeckt?
- Test-Isolation (kein globaler State)?

---

### Phase 4 — Priorisiertes Befund-Summary

Strukturiere alle Befunde nach Schweregrad:

| Prio | Label | Bedeutung |
|------|-------|-----------|
| 🔴 | **KRITISCH** | Funktionaler Bug, Security-Lücke, Datenverlust-Risiko |
| 🟠 | **WICHTIG** | Wartbarkeitsproblem, Performance-Issue, fehlende Fehlerbehandlung |
| 🟡 | **VERBESSERUNG** | Clean-Code-Verletzung, unvollständige Doku, Naming |
| 🟢 | **OPTIONAL** | Stilfrage, Alternative mit geringem Impact |

Jeder Befund enthält:
1. **Ort**: Klasse/Methode/Zeile (wenn erkennbar)
2. **Problem**: Klare Beschreibung
3. **Begründung**: Warum relevant
4. **Fix**: Konkreter Vorschlag, ggf. mit Code

---

### Phase 5 — Dokumentations-Ergänzungen (separater Block)

Wenn JavaDoc/JSDoc fehlt oder unvollständig ist: Liefere die **fertigen Dokumentationsblöcke**,
die direkt eingefügt werden können — keinen Pseudocode, keine Platzhalter.

Format:
```
### Fehlende Dokumentation — direkt einfügen

#### `KlassenName`
[fertiger JavaDoc-Block]

#### `methodenName(Param1, Param2)`
[fertiger JavaDoc-Block]
```

---

### Phase 6 — Gesamtbewertung

Kurzes Fazit (3–6 Sätze):
- Gesamteindruck des Codes
- Stärken benennen
- Wichtigste Baustellen
- Empfehlung: Merge-fähig? Nach Fixes? Refactoring erforderlich?

---

## Ausgabeformat

```
## Code-Review: [Dateiname / Klassenname / Kontext]

### Dokumentations-Review
[Befunde JavaDoc/JSDoc]

### Code-Qualität
[Befunde nach Dimension, priorisiert]

### Befund-Übersicht
[Tabelle: Prio | Ort | Kurzbezeichnung]

### Fehlende Dokumentation — direkt einfügen
[Fertige Doc-Blöcke]

### Fazit
[Gesamtbewertung]
```

---

## Verhalten bei mehreren Dateien

- Reviewe jede Datei mit eigenem Header
- Übergreifende Architektur-Befunde separat in einem Block "Übergreifendes"
- Priorisierungstabelle am Ende über alle Dateien zusammengeführt

---

## Sprachspezifische Hinweise

### Java / Spring Boot
- `@Nullable` / `@NonNull` Annotations geprüft?
- `Optional` korrekt verwendet (kein `.get()` ohne isPresent)?
- Spring-Annotationen vollständig (`@Transactional` auf Service-Ebene, nicht Repository)?
- Kein Autowiring von konkreten Klassen wenn Interface existiert?

### JavaScript / TypeScript
- `var` → `const`/`let`?
- Promise-Chains vs. async/await konsistent?
- Fehlerbehandlung in async-Funktionen (try/catch oder `.catch()`)?
- TypeScript: `any` vermeiden, korrekte Typen?

### PHP
- SQL über PDO mit Prepared Statements?
- `htmlspecialchars()` bei Ausgaben?
- Error-Reporting produktiv korrekt konfiguriert?

