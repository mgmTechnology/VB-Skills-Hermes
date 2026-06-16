---
name: vb-atlassian-admin
description: Atlassian-Administration — Benutzerverwaltung, Gruppen, SSO, Marketplace-Apps, System-Performance und Disaster Recovery.
---

# vb-atlassian-admin

## Ziel
Werkzeug-Skill für Atlassian-Administration. Deckt Benutzer-Bereitstellung und -Abmeldung, Gruppenverwaltung, Berechtigungsschemata, SSO-Konfiguration, Marketplace-App-Verwaltung, System-Performance-Optimierung, Integrationen und Disaster Recovery ab. Administrative Aktionen nur nach expliziter Bestätigung und nur mit berechtigtem Nutzerkontext.

## Vorgehen

### Benutzer-Bereitstellung
- Benutzerkonto uber admin.atlassian.com erstellen oder per REST API POST /rest/api/3/user.
- Zu entsprechenden Gruppen hinzufugen und Produktzugriff zuweisen. Verifizieren: Benutzer ist aktiv und kann sich anmelden.

### Benutzer-Abmeldung
- KRITISCH: Audit der Inhalte und Tickets des Benutzers durchfuhren. Offene Vorgange und eigene Bereiche/Seiten neu zuweisen.
- Aus allen Gruppen entfernen, Produktzugriff entziehen, Konto deaktivieren. Verifizieren per REST API.

### Gruppenverwaltung
- Gruppen nach Teams, Rollen und Projekten strukturieren. Vierteljahrlich uberprufen und bereinigen.

### Berechtigungsschemata
- Jira und Confluence: Offentliches Projekt/Team-Projekt/Eingeschranktes Projekt/Admin-Projekt.
- Best Practices: Gruppen statt Einzelberechtigungen, Least Privilege, regelmassige Audits.

### SSO-Konfiguration
- SAML-Einstellungen konfigurieren, mit Admin- und regularem Benutzer testen, SSO erzwingen, SCIM aktivieren.

### Marketplace-App-Verwaltung
- Bedarf und Sicherheit bewerten, in Sandbox testen, installieren, Benutzer schulen. Verifizieren per Health-Check.

### System-Performance
- Alte Projekte/Bereiche archivieren, Reindizierung, ungenutzte Workflows bereinigen. Tagliche Health-Checks, wochentliche Reports.

### Disaster Recovery
- Tagliche automatisierte Backups, wochentliche Verifizierung, 30 Tage Aufbewahrung. Vierteljahrliche Wiederherstellungsubungen.

## Regeln / Qualitatskriterien
- Administrative Aktionen nur nach expliziter Bestatigung und mit berechtigtem Nutzerkontext.
- Prinzip der geringsten Rechte anwenden. MFA fur alle Admins erzwingen.
- Audit-Logs mindestens 7 Jahre aufbewahren. Namenskonventionen einhalten.
- Change Management: grosse Anderungen 2 Wochen vorher ankundigen, in Sandbox testen.
- Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ressourcen
- Confluence-Experte: vb-confluence-experte
- Jira-Experte: vb-jira-experte
- Scrum-Master: vb-scrum-master
- Senior-PM: vb-senior-pm
