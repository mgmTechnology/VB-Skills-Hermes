---
name: vb-deployment
description: VB-adaptierter Skill für Deployment-Checks. Ursprünglich auf Vercel ausgerichtet, im VB-Kontext sind OpenShift, GitLab, ArgoCD, JFrog Artifactory und Kibana/Elastic relevant.
---

# VB Deployment

## Ziel

Spezialskill für Deployment-Checks. Der Ursprungsskill ist stark auf Vercel ausgerichtet, was nicht automatisch VB-Standard ist. Im VB-Kontext sind OpenShift, GitLab, ArgoCD, JFrog Artifactory und Kibana/Elastic relevante bekannte Rahmenpunkte. Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

## Vorgehen

### Vor dem Start
- Lies `features/INDEX.md`, um zu wissen, was bereitgestellt (deployed) werden soll
- Prüfe den QA-Status in der Feature-Spezifikation
- Verifiziere, dass in den QA-Ergebnissen keine kritischen oder hohen Fehler vorliegen
- Falls QA noch nicht durchgeführt wurde: "Führe zuerst `/qa` aus, bevor du das Deployment startest."

### 1. Checks vor dem Deployment
- `npm run build` ist lokal erfolgreich
- `npm run lint` ist erfolgreich
- Der QA-Engineer hat das Feature freigegeben
- Keine kritischen/hohen Fehler im Testbericht
- Alle Umgebungsvariablen sind in `.env.local.example` dokumentiert
- Keine Secrets in Git eingecheckt
- Alle Datenbank-Migrationen wurden angewendet (falls zutreffend)
- Der gesamte Code wurde committet und ins Remote-Repository gepusht

### 2. Vercel-Setup (nur beim ersten Deployment)
- Vercel-Projekt erstellen: `npx vercel` oder über vercel.com
- GitHub-Repository für Auto-Deploy beim Push verknüpfen
- Alle Umgebungsvariablen im Vercel-Dashboard hinzufügen
- Build-Einstellungen: Framework-Preset = Next.js
- Domain konfigurieren

### 3. Deployment durchführen
- Push in den Main-Branch → Vercel führt Auto-Deploy aus
- Oder manuell: `npx vercel --prod`
- Build im Vercel-Dashboard überwachen

### 4. Verifizierung nach dem Deployment
- Produktions-URL lädt korrekt
- Das bereitgestellte Feature funktioniert wie erwartet
- Datenbankverbindungen funktionieren (falls zutreffend)
- Authentifizierungs-Flows funktionieren
- Keine Fehler in der Browser-Konsole
- Keine Fehler in den Vercel-Funktions-Logs

### 5. Essentials für die Produktionsreife
- Fehler-Tracking einrichten
- Sicherheits-Header konfigurieren
- Performance-Check durchführen
- Datenbank-Optimierung prüfen
- Rate-Limiting (optional) einrichten

### 6. Dokumentation nach dem Deployment
- Feature-Spezifikation aktualisieren: Deployment-Abschnitt mit URL und Datum
- `features/INDEX.md` aktualisieren: Status auf Deployed setzen
- Git-Tag erstellen und pushen

## Regeln / Qualitätskriterien

- Kein Deployment ohne bestandene QA
- Keine kritischen/hohen Fehler vor Deployment
- Umgebungsvariablen nie in Git
- Vercel ist im VB-Rahmen nicht als Standard genannt
- Für VB-Standardnähe OpenShift, GitLab, ArgoCD, JFrog und Kibana/Elastic beachten
- Bei Build-Fehlern: Node.js-Version prüfen, Abhängigkeiten in package.json vs devDependencies

## Ressourcen

- [error-tracking.md](../../../docs/production/error-tracking.md)
- [security-headers.md](../../../docs/production/security-headers.md)
- [performance.md](../../../docs/production/performance.md)
- [database-optimization.md](../../../docs/production/database-optimization.md)
- [rate-limiting.md](../../../docs/production/rate-limiting.md)