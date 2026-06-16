---
name: vb-jira-experte
description: Jira-Experte — JQL, Workflows, Boards, Dashboards, Automatisierung und Jira-nahe Projektarbeit.
---

# vb-jira-experte

## Ziel
Werkzeug-Skill fur Jira, JQL, Workflows, Boards, Dashboards und Jira-nahe Projektarbeit. Deckt Projekterstellung, Workflow-Design, JQL-Abfrageerstellung, Dashboard-Erstellung und Automatisierungsregeln ab.

## Vorgehen

### Projekterstellung
- Projekttyp bestimmen (Scrum, Kanban, Bug Tracking). Mit entsprechender Vorlage erstellen.
- Projekteinstellungen konfigurieren: Name, Key, Beschreibung, Projektleiter, Benachrichtigungs-/Berechtigungsschema.
- Vorgangstypen und Workflows einrichten, Board/Backlog-Ansicht erstellen. Ubergabe an Scrum Master.

### Workflow-Design
- Prozesszustande planen (To Do, In Progress, Done), Ubergange und Bedingungen definieren.
- Validatoren, Post-Functions und Bedingungen hinzufugen. In Testprojekt validieren, dann mit Produktionsprojekten verknupfen.

### JQL-Abfrageerstellung
- Grundstruktur: Feld Operator Wert. Operatoren: =, !=, ~, !~, >, <, in, not in, is empty, was, changed.
- Leistungsstarke Abfragen: uberfallige Vorgange (dueDate < now()), Sprint-Burndown, veraltete Vorgange, Epic-Tracking, Velocity-Berechnung.

### Dashboard-Erstellung
- Neues Dashboard erstellen mit Filterergebnissen, Sprint-Burndown, Velocity Chart, Erstellt vs. Gelost, Tortendiagramm.
- Automatische Aktualisierung konfigurieren, mit Teams teilen.

### Automatisierungsregeln
- Trigger definieren, Bedingungen hinzufugen, Aktionen festlegen (Feld aktualisieren, Benachrichtigung, Subtask, Transition, Kommentar).
- Mit Beispieldaten testen, aktivieren und uberwachen.

### Fortgeschrittene Funktionen
- Benutzerdefinierte Felder, Vorgangsverknupfung (Issue Linking), Berechtigungen/Sicherheitsstufen, Massenoperationen (Bulk Operations).

## Regeln / Qualitatskriterien
- Datenqualitat: Pflichtfelder erzwingen, konsistente Namenskonventionen, regelmaissiges Cleanup.
- Performance: keine fuhrenden Wildcards in JQL, gespeicherte Filter nutzen, Dashboard-Gadgets begrenzen.
- Governance: Workflow-Anderungen dokumentieren, Schemata versionieren, Berechtigungsaudits durchfuhren.
- Massenanderungen: Vorschau aller Anderungen vor Ausfuhrung prufen.
- Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ressourcen
- Confluence-Experte: vb-confluence-experte
- Atlassian-Admin: vb-atlassian-admin