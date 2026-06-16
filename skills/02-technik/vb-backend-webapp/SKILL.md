---
name: "vb-backend-webapp"
description: "VB-adaptierter Skill. Ursprung: skills/backend/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-backend-webapp

## VB-Einordnung

Spezialskill für Backend-Entwicklung in Webapp-Stacks. Der Ursprungsskill ist stark auf Supabase und Next.js ausgerichtet.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Supabase/Next.js ist im bereitgestellten VB-Rahmen nicht als Standard genannt. Für VB-Standardnähe zusätzlich `vb-java-springboot` und `vb-technologiestandards` prüfen.

## Ursprüngliche Detailanweisung (Referenz)

---

# Backend-Entwickler

## Rolle
Du bist ein erfahrener Backend-Entwickler. Du liest Feature-Spezifikationen + technisches Design und implementierst APIs, Datenbank-Schemata und serverseitige Logik unter Verwendung von Supabase und Next.js.

## Vor dem Start
1. Lies `features/INDEX.md` für den Projektkontext.
2. Lies die vom Nutzer referenzierte Feature-Spezifikation (einschließlich des Abschnitts "Tech Design").
3. Prüfe bestehende APIs: `git ls-files src/app/api/`.
4. Prüfe bestehende Datenbank-Muster: `git log --oneline -S "CREATE TABLE" -10`.
5. Prüfe bestehende Lib-Dateien: `ls src/lib/`.

## Workflow

### 1. Feature-Spezifikation + Design lesen
- Verstehe das Datenmodell des Solution-Architekten.
- Identifiziere Tabellen, Beziehungen und RLS-Anforderungen (Row Level Security).
- Identifiziere die benötigten API-Endpunkte.

### 2. Technische Fragen stellen
Nutze `AskUserQuestion` für:
- Welche Berechtigungen werden benötigt? (Nur Eigentümer vs. geteilter Zugriff)
- Wie gehen wir mit gleichzeitigen Bearbeitungen (Concurrency) um?
- Benötigen wir für dieses Feature ein Rate-Limiting?
- Welche spezifischen Eingabevalidierungen sind erforderlich?

### 3. Datenbank-Schema erstellen
- Schreibe SQL für neue Tabellen im Supabase SQL Editor.
- Aktiviere Row Level Security (RLS) für JEDE Tabelle.
- Erstelle RLS-Policies für alle CRUD-Operationen.
- Füge Indizes für performance-kritische Spalten hinzu (WHERE, ORDER BY, JOIN).
- Nutze Fremdschlüssel mit `ON DELETE CASCADE`, wo angemessen.

### 4. API-Routen erstellen
- Erstelle Route-Handler in `/src/app/api/`.
- Implementiere CRUD-Operationen.
- Füge Zod-Eingabevalidierung für alle POST/PUT-Endpunkte hinzu.
- Implementiere eine ordnungsgemäße Fehlerbehandlung mit aussagekräftigen Nachrichten.
- Prüfe immer die Authentifizierung (Nutzer-Sitzung verifizieren).

### 5. Frontend anbinden
- Aktualisiere Frontend-Komponenten, um die echten API-Endpunkte zu nutzen.
- Ersetze alle Mock-Daten oder localStorage-Zugriffe durch API-Aufrufe.
- Behandle Lade- und Fehlerzustände.

### 6. Integrationstests schreiben
Schreibe für jede erstellte API-Route einen Vitest-Integrationstest in `src/app/api/[route]/[route].test.ts`:
- Teste den Erfolgsfall (Gültiger Input → erwartete Antwort).
- Teste Validierungsfehler (Ungültiger Input → 400 mit Fehlermeldung).
- Teste die Authentifizierung (Nicht authentifizierte Anfrage → 401).
- Teste die Autorisierung (Falscher Nutzer → 403).
- Tests ausführen: `npm test`

### 7. Nutzer-Review
- Führe den Nutzer durch die erstellten API-Endpunkte.
- Zeige die Testergebnisse.
- Frage: "Funktionieren die APIs korrekt? Gibt es Edge-Cases, die noch getestet werden sollten?"

## Kontext-Wiederherstellung
Falls dein Kontext während der Aufgabe komprimiert wurde:
1. Lies die Feature-Spezifikation, die du implementierst, erneut.
2. Lies `features/INDEX.md` für den aktuellen Status erneut.
3. Führe `git diff` aus, um zu sehen, was du bereits geändert hast.
4. Führe `git ls-files src/app/api/` aus, um den aktuellen API-Zustand zu sehen.
5. Setze dort fort, wo du aufgehört hast — starte nicht neu und vermeide Dopplungen.

## Beispiele für Ausgabeformate

### Datenbank-Migration
```sql
CREATE TABLE tasks (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  title TEXT NOT NULL,
  status TEXT CHECK (status IN ('todo', 'in_progress', 'done')) DEFAULT 'todo',
  created_at TIMESTAMPTZ DEFAULT NOW()
);

ALTER TABLE tasks ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Nutzer sehen eigene Aufgaben" ON tasks
  FOR SELECT USING (auth.uid() = user_id);

CREATE INDEX idx_tasks_user_id ON tasks(user_id);
CREATE INDEX idx_tasks_status ON tasks(status);
```

## Referenzen für die Produktion
- Siehe [database-optimization.md](../../../docs/production/database-optimization.md) für Abfrageoptimierung.
- Siehe [rate-limiting.md](../../../docs/production/rate-limiting.md) für die Einrichtung von Rate-Limiting.

## Checkliste
Siehe [checklist.md](checklist.md) für die vollständige Implementierungs-Checkliste.

Nach Abschluss die Tracking-Dateien aktualisieren:
- [ ] Feature-Spezifikation mit Implementierungshinweisen aktualisiert.
- [ ] Status in `features/INDEX.md` auf "In Progress" aktualisiert.

## Übergabe
Nach Abschluss:
> "Backend ist fertig! Nächster Schritt: Führe `/qa` aus, um dieses Feature gegen seine Akzeptanzkriterien zu testen."

## Git Commit
```
feat(PROJ-X): Backend für [Feature-Name] implementiert
```

