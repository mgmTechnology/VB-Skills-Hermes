---
name: "vb-atlassian-admin"
description: "VB-adaptierter Skill. Ursprung: skills/project-management/atlassian-admin/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-atlassian-admin

## VB-Einordnung

Werkzeug-Skill für Atlassian-Administration. Administrative Aktionen nur nach expliziter Bestätigung und nur mit berechtigtem Nutzerkontext.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ursprüngliche Detailanweisung (Referenz)

---

# Atlassian Administrator Experte

## Workflows

### Benutzer-Bereitstellung (User Provisioning)
1. Benutzerkonto erstellen: `admin.atlassian.com > User management > Invite users`.
   - REST API: `POST /rest/api/3/user` mit `{"emailAddress": "...", "displayName": "...","products": [...]}`.
2. Zu entsprechenden Gruppen hinzufügen: `admin.atlassian.com > User management > Groups > [Gruppe] > Add members`.
3. Produktzugriff zuweisen (Jira, Confluence) über `admin.atlassian.com > Products > [Produkt] > Access`.
4. Standardberechtigungen gemäß Gruppenschema konfigurieren.
5. Willkommens-E-Mail mit Onboarding-Informationen senden.
6. **BENACHRICHTIGEN**: Relevante Teamleiter über das neue Mitglied informieren.
7. **VERIFIZIEREN**: Bestätigen, dass der Benutzer unter `admin.atlassian.com/o/{orgId}/users` als aktiv erscheint und sich anmelden kann.

### Benutzer-Abmeldung (User Deprovisioning)
1. **KRITISCH**: Audit der Inhalte und Tickets im Besitz des Benutzers durchführen.
   - Jira: `GET /rest/api/3/search?jql=assignee={accountId}`, um offene Vorgänge zu finden.
   - Confluence: `GET /wiki/rest/api/user/{accountId}/property`, um eigene Bereiche/Seiten zu finden.
2. Eigentümerschaft neu zuweisen für:
   - Jira-Projekte: `Projekteinstellungen > Personen > Leiter ändern`.
   - Confluence-Bereiche: `Bereichseinstellungen > Übersicht > Bereichsdetails bearbeiten`.
   - Offene Vorgänge: Massenzuweisung über `Jira > Vorgänge > Massenänderung`.
   - Filter und Dashboards: Übertragen über `Benutzerverwaltung > [Benutzer] > Verwaltete Inhalte`.
3. Aus allen Gruppen entfernen: `admin.atlassian.com > User management > [Benutzer] > Groups`.
4. Produktzugriff entziehen.
5. Konto deaktivieren: `admin.atlassian.com > User management > [Benutzer] > Deactivate`.
   - REST API: `DELETE /rest/api/3/user?accountId={accountId}`.
6. **VERIFIZIEREN**: Bestätigen, dass `GET /rest/api/3/user?accountId={accountId}` den Wert `"active": false` zurückgibt.
7. Abmeldung im Audit-Log dokumentieren.
8. **NUTZEN**: Jira-Experte zur Neuzuweisung verbleibender Vorgänge einbinden.

### Gruppenverwaltung
1. Gruppen erstellen: `admin.atlassian.com > User management > Groups > Create group`.
   - REST API: `POST /rest/api/3/group` mit `{"name": "..."}`.
   - Strukturierung nach: Teams (Entwicklung, Produkt, Vertrieb), Rollen (Admins, Benutzer, Betrachter), Projekten (Projekt-Alpha-Team).
2. Gruppenzweck und Mitgliedschaftskriterien definieren (in Confluence dokumentieren).
3. Standardberechtigungen pro Gruppe zuweisen.
4. Benutzer zu entsprechenden Gruppen hinzufügen.
5. **VERIFIZIEREN**: Gruppenmitglieder über `GET /rest/api/3/group/member?groupName={Name}` prüfen.
6. Regelmäßige Überprüfung und Bereinigung (vierteljährlich).
7. **NUTZEN**: Confluence-Experte zur Dokumentation der Gruppenstruktur einbinden.

### Design von Berechtigungsschemata
**Jira-Berechtigungsschemata** (`Jira-Einstellungen > Vorgänge > Berechtigungsschemata`):
- **Öffentliches Projekt**: Alle Benutzer können sehen, Mitglieder können bearbeiten.
- **Team-Projekt**: Teammitglieder haben Vollzugriff, Stakeholder Lesezugriff.
- **Eingeschränktes Projekt**: Nur namentlich genannte Personen.
- **Admin-Projekt**: Nur Administratoren.

**Confluence-Berechtigungsschemata** (`Confluence-Admin > Bereichsberechtigungen`):
- **Öffentlicher Bereich**: Alle Benutzer können sehen, Bereichsmitglieder bearbeiten.
- **Team-Bereich**: Teamspezifischer Zugriff.
- **Persönlicher Bereich**: Nur für den einzelnen Benutzer.
- **Eingeschränkter Bereich**: Namentlich genannte Personen und Gruppen.

**Best Practices**:
- Gruppen statt Einzelberechtigungen nutzen.
- Prinzip der geringsten Rechte (Least Privilege).
- Regelmäßige Berechtigungsaudits.
- Begründung der Berechtigungen dokumentieren.

### SSO-Konfiguration
1. Identitätsanbieter (IdP) wählen (Okta, Azure AD, Google).
2. SAML-Einstellungen konfigurieren: `admin.atlassian.com > Security > SAML single sign-on > Add SAML configuration`.
   - Entity-ID, ACS-URL und X.509-Zertifikat vom IdP eintragen.
3. SSO mit Admin-Konto testen (Passwort-Login während des Tests aktiv lassen).
4. Mit regulärem Benutzerkonto testen.
5. SSO für die Organisation aktivieren.
6. SSO erzwingen: `admin.atlassian.com > Security > Authentication policies > Enforce SSO`.
7. SCIM für automatische Bereitstellung konfigurieren: `admin.atlassian.com > User provisioning > [IdP] > Enable SCIM`.
8. **VERIFIZIEREN**: Bestätigen, dass der SSO-Flow erfolgreich ist und die Audit-Logs `saml.login.success` Ereignisse zeigen.
9. SSO-Logs überwachen: `admin.atlassian.com > Security > Audit log > Filter: SSO`.

### Marketplace App-Verwaltung
1. Bedarf und Sicherheit der App bewerten: Sicherheits-Selbstauskunft des Herstellers unter `marketplace.atlassian.com` prüfen.
2. Sicherheitsdokumentation des Herstellers prüfen (Penetrationstests, SOC 2).
3. App in einer Sandbox-Umgebung testen.
4. Kauf oder Testphase anfordern: `admin.atlassian.com > Billing > Manage subscriptions`.
5. App installieren: `admin.atlassian.com > Products > [Produkt] > Apps > Find new apps`.
6. App-Einstellungen gemäß Herstellerdokumentation konfigurieren.
7. Benutzer in der Nutzung der App schulen.
8. **VERIFIZIEREN**: Bestätigen, dass die App in `GET /rest/plugins/1.0/` erscheint und der Health-Check erfolgreich ist.
9. Performance und Nutzung der App überwachen; jährlich den weiteren Bedarf prüfen.

### Optimierung der System-Performance
**Jira** (`Jira-Einstellungen > System`):
- Alte Projekte archivieren: `Projekteinstellungen > Projekt archivieren`.
- Reindizierung: `Jira-Einstellungen > System > Indizierung > Vollständige Reindizierung`.
- Nicht genutzte Workflows und Schemata bereinigen: `Jira-Einstellungen > Vorgänge > Workflows`.
- Warteschlangen/Threads überwachen: `Jira-Einstellungen > System > Systeminfo`.

**Confluence** (`Confluence-Admin > Konfiguration`):
- Inaktive Bereiche archivieren: `Bereichskonfiguration > Übersicht > Bereich archivieren`.
- Verwaiste Seiten entfernen: `Confluence-Admin > Verwaiste Seiten`.
- Index und Cache überwachen: `Confluence-Admin > Cache-Verwaltung`.

**Überwachungs-Rhythmus**:
- Tägliche Health-Checks: `admin.atlassian.com > Products > [Produkt] > Health`.
- Wöchentliche Performance-Berichte.
- Monatliche Kapazitätsplanung.
- Vierteljährliche Optimierungs-Reviews.

### Einrichten von Integrationen
**Gängige Integrationen**:
- **Slack**: `Jira-Einstellungen > Apps > Slack-Integration` — Benachrichtigungen für Jira und Confluence.
- **GitHub/Bitbucket**: `Jira-Einstellungen > Apps > DVCS-Konten` — Commits mit Vorgängen verknüpfen.
- **Microsoft Teams**: `admin.atlassian.com > Apps > Microsoft Teams`.
- **Zoom**: Verfügbar über Marketplace-App `zoom-for-jira`.
- **Salesforce**: Über Marketplace-App `salesforce-connector`.

**Konfigurationsschritte**:
1. Integrationsanforderungen und benötigte OAuth-Scopes prüfen.
2. OAuth- oder API-Authentifizierung konfigurieren (Token in sicherem Vault speichern, nicht im Klartext).
3. Felder und Datenflüsse mappen.
4. Integration gründlich mit Testdaten prüfen.
5. Konfiguration im Confluence Runbook dokumentieren.
6. Benutzer in den Integrationsfunktionen schulen.
7. **VERIFIZIEREN**: Webhook-Zustellung über `Jira-Einstellungen > System > WebHooks > [Webhook] > Test` bestätigen.
8. Integrität der Integration über app-spezifische Dashboards überwachen.

## Globale Konfiguration

### Globale Jira-Einstellungen (`Jira-Einstellungen > Vorgänge`)
**Vorgangstypen**: Organisationsweite Vorgangstypen erstellen und verwalten; Vorgangstyp-Schemata definieren; projektübergreifend standardisieren.
**Workflows**: Globale Workflow-Vorlagen über `Workflows > Workflow hinzufügen` erstellen; Workflow-Schemata verwalten.
**Benutzerdefinierte Felder**: Organisationsweite Felder unter `Benutzerdefinierte Felder > Benutzerdefiniertes Feld hinzufügen` erstellen; Feldkonfigurationen und Kontext verwalten.
**Benachrichtigungsschemata**: Standard-Regeln konfigurieren; eigene Schemata erstellen; E-Mail-Vorlagen verwalten.

### Globale Confluence-Einstellungen (`Confluence-Admin`)
**Blueprints & Vorlagen**: Organisationsweite Vorlagen unter `Konfiguration > Globale Vorlagen und Blueprints` erstellen; Verfügbarkeit von Blueprints verwalten.
**Themes & Erscheinungsbild**: Branding unter `Konfiguration > Themes` konfigurieren; Logos und Farben anpassen.
**Makros**: Makros unter `Konfiguration > Makro-Nutzung` aktivieren/deaktivieren; Berechtigungen konfigurieren.

### Sicherheitseinstellungen (`admin.atlassian.com > Security`)
**Authentifizierung**:
- Passwort-Richtlinien: `Security > Authentication policies > Edit`.
- Sitzungs-Timeout: `Security > Session duration`.
- API-Token Verwaltung: `Security > API token controls`.

**Datenresidenz**: Speicherort der Daten unter `admin.atlassian.com > Data residency > Pin products` konfigurieren.

**Audit-Logs**: `admin.atlassian.com > Security > Audit log`.
- Umfassende Protokollierung aktivieren; Export über `GET /admin/v1/orgs/{orgId}/audit-log`.
- Gemäß Richtlinie aufbewahren (mindestens 7 Jahre für SOC 2/DSGVO Compliance).

## Governance & Richtlinien

### Zugriffs-Governance
- Vierteljährlicher Review aller Benutzerzugriffe: `admin.atlassian.com > User management > Export users`.
- Benutzerrollen und Berechtigungen prüfen; inaktive Benutzer entfernen.
- Anzahl der Organisations-Admins auf 2–3 Personen begrenzen; Admin-Aktionen monatlich auditieren.
- MFA für alle Admins erzwingen: `Security > Authentication policies > Require 2FA`.

### Namenskonventionen
**Jira**: Projekt-Keys mit 3–4 Großbuchstaben (PROJ, WEB); Vorgangstypen in Title Case; benutzerdefinierte Felder mit Präfix (CF: Story Points).
**Confluence**: Bereiche mit Team/Projekt-Präfix (TEAM: Engineering); Seiten aussagekräftig und konsistent; Stichworte (Labels) in Kleinbuchstaben, mit Bindestrich getrennt.

### Change Management
**Große Änderungen**: 2 Wochen im Voraus ankündigen; in Sandbox testen; Rollback-Plan erstellen; außerhalb der Spitzenzeiten durchführen; Review nach der Implementierung.
**Kleine Änderungen**: 48 Stunden im Voraus ankündigen; im Änderungsprotokoll dokumentieren; auf Probleme überwachen.

## Disaster Recovery

### Backup-Strategie
**Jira & Confluence**: Tägliche automatisierte Backups; wöchentliche manuelle Verifizierung; 30 Tage Aufbewahrung; Offsite-Speicherung.
- Manuelles Backup auslösen: `Jira-Einstellungen > System > System-Backup` / `Confluence-Admin > Sichern und Wiederherstellen`.

**Wiederherstellungstests**: Vierteljährliche Wiederherstellungsübungen; Verfahren dokumentieren; RTO und RPO messen.

### Incident Response (Vorfallreaktion)
**Schweregrade**:
- **P1 (Kritisch)**: Systemausfall — Reaktion in 15 Min.
- **P2 (Hoch)**: Kernfunktion defekt — Reaktion in 1 Std.
- **P3 (Mittel)**: Kleineres Problem — Reaktion in 4 Std.
- **P4 (Niedrig)**: Verbesserungswunsch — Reaktion in 24 Std.

**Reaktionsschritte**:
1. Vorfall bestätigen und protokollieren.
2. Auswirkungen und Schweregrad bewerten.
3. Status an Stakeholder kommunizieren.
4. Ursachenanalyse (check `admin.atlassian.com > Products > [Produkt] > Health` und Atlassian Status Page).
5. Fix implementieren.
6. **VERIFIZIEREN**: Behebung durch Test mit betroffenen Benutzern und Health-Check bestätigen.
7. Post-Mortem und Lessons Learned.

## Metriken & Reporting

**Systemzustand**: Aktive Benutzer (täglich/wöchentlich/monatlich), Speicherauslastung, API-Rate-Limits, Integrität der Integrationen, Antwortzeiten.
- Export über: `GET /admin/v1/orgs/{orgId}/users` für Benutzerzahlen; produktspezifische Analytics-Dashboards.

**Nutzungsanalysen**: Aktivste Projekte/Bereiche, Trends der Inhaltserstellung, Benutzer-Engagement, Suchmuster.
**Compliance-Metriken**: Abschlussquote der Zugriffs-Reviews, Ergebnisse von Sicherheitsaudits, fehlgeschlagene Login-Versuche, Nutzung von API-Token.

## Entscheidungsrahmen & Übergabeprotokolle

**An den Atlassian Support eskalieren**: Systemausfall, organisationsweite Performance-Einbußen, Datenverlust/-korruption, Lizenz-/Abrechnungsprobleme, komplexe Migrationen.

**An Produktexperten delegieren**:
- Jira-Experte: Projektspezifische Konfiguration.
- Confluence-Experte: Bereichsspezifische Einstellungen.
- Scrum Master: Team-Workflows.
- Senior PM: Strategische Planung.

**Sicherheitsteam einbeziehen**: Sicherheitsvorfälle, ungewöhnliche Zugriffsmuster, Vorbereitung von Compliance-Audits, Sicherheitsprüfung neuer Integrationen.

**AN Jira-Experte**: Neue globale Workflows, benutzerdefinierte Felder, Berechtigungsschemata oder Automatisierungsfunktionen verfügbar.
**AN Confluence-Experte**: Neue globale Vorlagen, Bereichsberechtigungsschemata, Blueprints oder Makros konfiguriert.
**AN Senior PM**: Nutzungsanalysen, Einblicke in die Kapazitätsplanung, Kostenoptimierung, Status der Sicherheits-Compliance.
**AN Scrum Master**: Teamzugriff bereitgestellt, Board-Konfigurationsoptionen, Automatisierungsregeln, Integrationen aktiviert.
**VON allen Rollen**: Anträge auf Benutzerzugriff, Berechtigungsänderungen, App-Installationswünsche, Konfigurations-Support, Vorfallsmeldungen.

## Atlassian MCP Integration

**Primäre Werkzeuge**: Jira MCP, Confluence MCP

**Admin-Operationen**:
- Benutzer- und Gruppenverwaltung via API.
- Massen-Updates von Berechtigungen.
- Konfigurations-Audits.
- Nutzungsberichte.
- Überwachung des Systemzustands.
- Automatisierte Compliance-Checks.

**Integrationspunkte**:
- Unterstützung aller Rollen durch Admin-Fähigkeiten.
- Befähigung des Jira-Experten durch globale Konfigurationen.
- Bereitstellung der Vorlagenverwaltung für den Confluence-Experten.
- Sicherstellung der Sichtbarkeit des Systemzustands für den Senior PM.
- Unterstützung des Scrum Masters bei der Teambereitstellung.

