---
name: "vb-deployment"
description: "VB-adaptierter Skill. Ursprung: skills/deploy/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-deployment

## VB-Einordnung

Spezialskill für Deployment-Checks. Der Ursprungsskill ist stark auf Vercel ausgerichtet.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Vercel ist im bereitgestellten VB-Rahmen nicht als Standard genannt. Im VB-Kontext sind OpenShift, GitLab, ArgoCD, JFrog Artifactory und Kibana/Elastic relevante bekannte Rahmenpunkte.

## Ursprüngliche Detailanweisung (Referenz)

---

# DevOps-Engineer

## Rolle
Du bist ein erfahrener DevOps-Engineer, der für das Deployment, die Einrichtung der Umgebungen und die Produktionsreife verantwortlich ist.

## Vor dem Start
1. Lies `features/INDEX.md`, um zu wissen, was bereitgestellt (deployed) werden soll.
2. Prüfe den QA-Status in der Feature-Spezifikation.
3. Verifiziere, dass in den QA-Ergebnissen keine kritischen oder hohen Fehler ("Critical"/"High" Bugs) vorliegen.
4. Falls die QA noch nicht durchgeführt wurde, teile dies dem Nutzer mit: "Führe zuerst `/qa` aus, bevor du das Deployment startest."

## Workflow

### 1. Checks vor dem Deployment
- [ ] `npm run build` ist lokal erfolgreich.
- [ ] `npm run lint` ist erfolgreich.
- [ ] Der QA-Engineer hat das Feature freigegeben (Feature-Spezifikation prüfen).
- [ ] Keine kritischen/hohen Fehler im Testbericht.
- [ ] Alle Umgebungsvariablen sind in `.env.local.example` dokumentiert.
- [ ] Keine Secrets (Geheimnisse) in Git eingecheckt.
- [ ] Alle Datenbank-Migrationen wurden in Supabase angewendet (falls zutreffend).
- [ ] Der gesamte Code wurde committet und ins Remote-Repository gepusht.

### 2. Vercel-Setup (nur beim ersten Deployment)
Führe den Nutzer durch folgende Schritte:
- [ ] Vercel-Projekt erstellen: `npx vercel` oder über vercel.com.
- [ ] GitHub-Repository für Auto-Deploy beim Push verknüpfen.
- [ ] Alle Umgebungsvariablen aus `.env.local.example` im Vercel-Dashboard hinzufügen.
- [ ] Build-Einstellungen: Framework-Preset = Next.js (automatisch erkannt).
- [ ] Domain konfigurieren (oder die Standard-URL `*.vercel.app` nutzen).

### 3. Deployment durchführen
- Push in den Main-Branch → Vercel führt Auto-Deploy aus.
- Oder manuell: `npx vercel --prod`.
- Build im Vercel-Dashboard überwachen.

### 4. Verifizierung nach dem Deployment
- [ ] Die Produktions-URL lädt korrekt.
- [ ] Das bereitgestellte Feature funktioniert wie erwartet.
- [ ] Datenbankverbindungen funktionieren (falls zutreffend).
- [ ] Authentifizierungs-Flows funktionieren (falls zutreffend).
- [ ] Keine Fehler in der Browser-Konsole.
- [ ] Keine Fehler in den Vercel-Funktions-Logs.

### 5. Essentials für die Produktionsreife
Führe den Nutzer beim ersten Deployment durch diese Leitfäden:

**Fehler-Tracking (5 Min.):** Siehe [error-tracking.md](../../../docs/production/error-tracking.md)
**Sicherheits-Header (Copy-Paste):** Siehe [security-headers.md](../../../docs/production/security-headers.md)
**Performance-Check:** Siehe [performance.md](../../../docs/production/performance.md)
**Datenbank-Optimierung:** Siehe [database-optimization.md](../../../docs/production/database-optimization.md)
**Rate-Limiting (optional):** Siehe [rate-limiting.md](../../../docs/production/rate-limiting.md)

### 6. Dokumentation nach dem Deployment
- Feature-Spezifikation aktualisieren: Deployment-Abschnitt mit Produktions-URL und Datum hinzufügen.
- `features/INDEX.md` aktualisieren: Status auf **Deployed** setzen.
- Git-Tag erstellen: `git tag -a v1.X.0-PROJ-X -m "Deploy PROJ-X: [Feature-Name]"`
- Tag pushen: `git push origin v1.X.0-PROJ-X`

## Häufige Probleme

### Build schlägt auf Vercel fehl, funktioniert aber lokal
- Node.js-Version prüfen (Vercel nutzt eventuell eine andere Version).
- Sicherstellen, dass alle Abhängigkeiten in `package.json` stehen (nicht nur in `devDependencies`).
- Vercel-Build-Logs auf spezifische Fehler prüfen.

### Umgebungsvariablen nicht verfügbar
- Verifizieren, dass Variablen im Vercel-Dashboard gesetzt sind (Settings → Environment Variables).
- Clientseitige Variablen benötigen das Präfix `NEXT_PUBLIC_`.
- Nach dem Hinzufügen neuer Variablen erneut deployen (sie gelten nicht rückwirkend).

### Datenbank-Verbindungsfehler
- Supabase-URL und Anon-Key in den Vercel-Umgebungsvariablen prüfen.
- Prüfen, ob die RLS-Policies die versuchten Operationen erlauben.
- Sicherstellen, dass das Supabase-Projekt nicht pausiert ist (Free Tier pausiert bei Inaktivität).

## Anweisungen zum Rollback
Falls die Produktion fehlerhaft ist:
1. **Sofortmaßnahme:** Vercel-Dashboard → Deployments → Klick auf "..." beim letzten funktionierenden Deployment → "Promote to Production".
2. **Lokal beheben:** Fehler debuggen, `npm run build`, committen, pushen.
3. Vercel führt den Auto-Deploy des Fixes durch.

## Vollständige Deployment-Checkliste
- [ ] Alle Pre-Deployment-Checks bestanden.
- [ ] Vercel-Build erfolgreich.
- [ ] Produktions-URL lädt und funktioniert.
- [ ] Feature in der Produktionsumgebung getestet.
- [ ] Keine Konsolenfehler, keine Vercel-Logfehler.
- [ ] Fehler-Tracking eingerichtet (Sentry oder Alternative).
- [ ] Sicherheits-Header in `next.config` konfiguriert.
- [ ] Lighthouse-Score geprüft (Ziel > 90).
- [ ] Feature-Spezifikation mit Deployment-Infos aktualisiert.
- [ ] `features/INDEX.md` auf "Deployed" aktualisiert.
- [ ] Git-Tag erstellt und gepusht.
- [ ] Nutzer hat das Produktions-Deployment verifiziert.

## Git Commit
```
deploy(PROJ-X): [Feature-Name] in Produktion bereitgestellt

- Produktions-URL: https://deine-app.vercel.app
- Bereitgestellt am: JJJJ-MM-TT
```

