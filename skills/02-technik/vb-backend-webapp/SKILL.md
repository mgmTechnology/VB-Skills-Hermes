---
name: vb-backend-webapp
description: VB-adaptierter Skill für Backend-Entwicklung in Webapp-Stacks. Ursprünglich auf Supabase/Next.js ausgerichtet, im VB-Kontext mit vb-java-springboot und vb-technologiestandards kombinieren.
---

# VB Backend Webapp

## Ziel

Spezialskill für Backend-Entwicklung in Webapp-Stacks. Der Ursprungsskill ist stark auf Supabase und Next.js ausgerichtet, was nicht automatisch VB-Standard ist. Für VB-Standardnähe zusätzlich `vb-java-springboot` und `vb-technologiestandards` prüfen. Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

## Vorgehen

### Vor dem Start
- Lies `features/INDEX.md` für den Projektkontext
- Lies die vom Nutzer referenzierte Feature-Spezifikation (einschließlich des Abschnitts "Tech Design")
- Prüfe bestehende APIs: `git ls-files src/app/api/`
- Prüfe bestehende Datenbank-Muster: `git log --oneline -S "CREATE TABLE" -10`
- Prüfe bestehende Lib-Dateien: `ls src/lib/`

### 1. Feature-Spezifikation + Design lesen
- Verstehe das Datenmodell des Solution-Architekten
- Identifiziere Tabellen, Beziehungen und RLS-Anforderungen (Row Level Security)
- Identifiziere die benötigten API-Endpunkte

### 2. Technische Fragen stellen
- Welche Berechtigungen werden benötigt? (Nur Eigentümer vs. geteilter Zugriff)
- Wie gehen wir mit gleichzeitigen Bearbeitungen (Concurrency) um?
- Benötigen wir für dieses Feature ein Rate-Limiting?
- Welche spezifischen Eingabevalidierungen sind erforderlich?

### 3. Datenbank-Schema erstellen
- Schreibe SQL für neue Tabellen im Supabase SQL Editor
- Aktiviere Row Level Security (RLS) für JEDE Tabelle
- Erstelle RLS-Policies für alle CRUD-Operationen
- Füge Indizes für performance-kritische Spalten hinzu (WHERE, ORDER BY, JOIN)
- Nutze Fremdschlüssel mit `ON DELETE CASCADE`, wo angemessen

### 4. API-Routen erstellen
- Erstelle Route-Handler in `/src/app/api/`
- Implementiere CRUD-Operationen
- Füge Zod-Eingabevalidierung für alle POST/PUT-Endpunkte hinzu
- Implementiere eine ordnungsgemäße Fehlerbehandlung mit aussagekräftigen Nachrichten
- Prüfe immer die Authentifizierung (Nutzer-Sitzung verifizieren)

### 5. Frontend anbinden
- Aktualisiere Frontend-Komponenten, um die echten API-Endpunkte zu nutzen
- Ersetze alle Mock-Daten oder localStorage-Zugriffe durch API-Aufrufe
- Behandle Lade- und Fehlerzustände

### 6. Integrationstests schreiben
- Schreibe für jede erstellte API-Route einen Vitest-Integrationstest
- Teste den Erfolgsfall, Validierungsfehler, Authentifizierung und Autorisierung
- Tests ausführen: `npm test`

### 7. Nutzer-Review
- Führe den Nutzer durch die erstellten API-Endpunkte
- Zeige die Testergebnisse

## Regeln / Qualitätskriterien

- Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard
- Konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten gelten nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich
- VB-Hinweis: Supabase/Next.js ist im bereitgestellten VB-Rahmen nicht als Standard genannt
- Bei Kontext-Wiederherstellung: Feature-Spezifikation erneut lesen, `features/INDEX.md` prüfen, `git diff` ausführen, dort fortsetzen wo aufgehört wurde

## Ressourcen

- [checklist.md](checklist.md) — vollständige Implementierungs-Checkliste
- [database-optimization.md](../../../docs/production/database-optimization.md)
- [rate-limiting.md](../../../docs/production/rate-limiting.md)
- Verwandte Skills: vb-java-springboot, vb-technologiestandards