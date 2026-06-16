---
name: vb-atlassian-templates
description: Jira-/Confluence-Vorlagen, Blueprints und standardisierte Strukturen fur die Inhaltserstellung.
---

# vb-atlassian-templates

## Ziel
Werkzeug-Skill fur Jira-/Confluence-Vorlagen, Blueprints und standardisierte Strukturen. Erstellt und verwaltet wiederverwendbare Vorlagen fur Meeting Notes, Project Charter, Sprint Retrospective, PRD, Decision Log (Confluence) sowie User Story, Bug Report, Epic (Jira). Beschleunigt die Inhaltserstellung und pflegt organisationsweite Standards.

## Vorgehen

### Vorlagenerstellung
- Stakeholder interviewen, bestehende Inhaltsmuster prufen, Vorlagenstruktur und Platzhalter entwerfen.
- Mit Makros und Formatierung aufbauen, mit Beispieldaten testen, Nutzungshinweise dokumentieren.
- In den entsprechenden Bereich/das Projekt via MCP bereitstellen. Nutzer schulen und Akzeptanz verfolgen.

### Vorlagenanderung
- Anderungsanfrage und Auswirkungen prufen, neue Version erstellen, alte verfugbar halten.
- Migrationspfad fur bestehende Inhalte anbieten, Anderungen kommunizieren, Nutzer unterstutzen.
- Alte Version nach Ubergang archivieren (nicht loschen).

### Blueprint-Entwicklung
- Umfang definieren, mehrseitige Struktur entwerfen, Seitenvorlagen fur jeden Abschnitt erstellen.
- Regeln fur Seitenerstellung konfigurieren, dynamische Inhalte hinzufugen, end-to-end testen.
- Ubergabe an Atlassian Admin fur globale Bereitstellung.

### MCP-Operationen
- Seitenvorlage in Confluence erstellen: confluence_create_page mit space_key, title, body, labels.
- Bestehende Vorlage aktualisieren: confluence_update_page mit page_id, version, title, body.
- Jira Vorgangsbeschreibungs-Vorlage: jira_update_field_configuration mit project_key, field_id, default_value.

## Regeln / Qualitatskriterien
- Vorlagenversionen mit Versionshinweisen im Seiten-Header verfolgen.
- Veraltete Vorlagen mit Warnhinweis markieren, archivieren (nicht loschen).
- Quality Gates vor Bereitstellung: Beispielinhalte vorhanden, mit Beispieldaten getestet, Versionskommentar gepflegt, Feedback-Mechanismus.
- Standard-Abschnitte: Header-Panel mit Metadaten, klar beschriftete Inhaltsbereiche, Aufgabenblock, verwandte Links.
- Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ressourcen
- Confluence-Experte: vb-confluence-experte
- Jira-Experte: vb-jira-experte
- Senior-PM: vb-senior-pm
