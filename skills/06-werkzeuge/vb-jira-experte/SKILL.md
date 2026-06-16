---
name: "vb-jira-experte"
description: "VB-adaptierter Skill. Ursprung: skills/project-management/jira-expert/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-jira-experte

## VB-Einordnung

Werkzeug-Skill für Jira, JQL, Workflows, Boards, Dashboards und Jira-nahe Projektarbeit.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ursprüngliche Detailanweisung (Referenz)

---

# Atlassian Jira Experte

Experte auf Master-Niveau in der Jira-Konfiguration, im Projektmanagement, JQL, Workflows, Automatisierung und Reporting. Behandelt alle technischen und operativen Aspekte von Jira.

## Schnellstart — Häufigste Operationen

**Projekt erstellen**:
```
mcp jira create_project --name "Mein Projekt" --key "MEINPROJ" --type scrum --lead "user@example.com"
```

**JQL-Abfrage ausführen**:
```
mcp jira search_issues --jql "project = MEINPROJ AND status != Done AND dueDate < now()" --maxResults 50
```

Für die vollständige Befehlsreferenz siehe [Atlassian MCP Integration](#atlassian-mcp-integration). Für JQL-Funktionen siehe [JQL-Funktionsreferenz](#jql-funktionsreferenz). Für Berichtsvorlagen siehe [Berichtsvorlagen](#berichtsvorlagen).

---

## Workflows

### Projekterstellung
1. Projekttyp bestimmen (Scrum, Kanban, Bug Tracking, etc.).
2. Projekt mit entsprechender Vorlage erstellen.
3. Projekteinstellungen konfigurieren:
   - Name, Key (Schlüssel), Beschreibung.
   - Projektleiter und Standard-Bearbeiter.
   - Benachrichtigungsschema.
   - Berechtigungsschema.
4. Vorgangstypen und Workflows einrichten.
5. Benutzerdefinierte Felder bei Bedarf konfigurieren.
6. Initiales Board/Backlog-Ansicht erstellen.
7. **ÜBERGABE AN**: Scrum Master für das Team-Onboarding.

### Workflow-Design
1. Prozesszustände planen (To Do → In Progress → Done).
2. Übergänge (Transitions) und Bedingungen definieren.
3. Validatoren, Post-Functions und Bedingungen hinzufügen.
4. Workflow-Schema konfigurieren.
5. **Validieren**: Zuerst in einem Testprojekt bereitstellen; verifizieren, dass sich alle Übergänge, Bedingungen und Post-Functions wie erwartet verhalten, bevor sie mit Produktionsprojekten verknüpft werden.
6. Workflow mit Projekt verknüpfen.
7. Workflow mit Beispiel-Vorgängen testen.

### JQL-Abfrageerstellung
**Grundstruktur**: `Feld Operator Wert`

**Gängige Operatoren**:
- `=, !=` : Gleich, Ungleich.
- `~, !~` : Enthält, enthält nicht.
- `>, <, >=, <=` : Vergleich.
- `in, not in` : Listenmitgliedschaft.
- `is empty, is not empty` : Ist leer, ist nicht leer.
- `was, was in, was not` : Historische Abfrage.
- `changed` : Geändert.

**Leistungsstarke JQL-Beispiele**:

Überfällige Vorgänge finden:
```jql
dueDate < now() AND status != Done
```

Sprint-Burndown Vorgänge:
```jql
sprint = 23 AND status changed TO "Done" DURING (startOfSprint(), endOfSprint())
```

Veraltete Vorgänge finden:
```jql
updated < -30d AND status != Done
```

Projektübergreifendes Epic-Tracking:
```jql
"Epic Link" = PROJ-123 ORDER BY rank
```

Velocity-Berechnung:
```jql
sprint in closedSprints() AND resolution = Done
```

Teamkapazität:
```jql
assignee in (user1, user2) AND sprint in openSprints()
```

### Dashboard-Erstellung
1. Neues Dashboard erstellen (persönlich oder geteilt).
2. Relevante Gadgets hinzufügen:
   - Filterergebnisse (JQL-basiert).
   - Sprint-Burndown.
   - Velocity Chart (Geschwindigkeitsdiagramm).
   - Erstellt vs. Gelöst.
   - Tortendiagramm (Statusverteilung).
3. Layout für bessere Lesbarkeit anordnen.
4. Automatische Aktualisierung konfigurieren.
5. Mit entsprechenden Teams teilen.
6. **ÜBERGABE AN**: Senior PM oder Scrum Master zur Nutzung.

### Automatisierungsregeln
1. Trigger (Auslöser) definieren (Vorgang erstellt, Feld geändert, geplant).
2. Bedingungen hinzufügen (falls zutreffend).
3. Aktionen definieren:
   - Feld aktualisieren.
   - Benachrichtigung senden.
   - Subtask (Unteraufgabe) erstellen.
   - Vorgangsstatus ändern (Transition).
   - Kommentar posten.
4. Automatisierung mit Beispieldaten testen.
5. Aktivieren und überwachen.

## Fortgeschrittene Funktionen

### Benutzerdefinierte Felder (Custom Fields)
**Wann zu erstellen**:
- Daten verfolgen, die nicht in Standardfeldern enthalten sind.
- Prozessspezifische Informationen erfassen.
- Erweitertes Reporting ermöglichen.

**Feldtypen**: Text, Numerisch, Datum, Auswahl (einfach/mehrfach/kaskadierend), Benutzerauswahl.

**Konfiguration**:
1. Benutzerdefiniertes Feld erstellen.
2. Feldkontext konfigurieren (welche Projekte/Vorgangstypen).
3. Zu entsprechenden Bildschirmmasken (Screens) hinzufügen.
4. Suchvorlagen bei Bedarf aktualisieren.

### Vorgangsverknüpfung (Issue Linking)
**Verknüpfungstypen**:
- Blockiert / Wird blockiert durch.
- Bezieht sich auf.
- Dupliziert / Wird dupliziert durch.
- Klon / Wird geklont durch.
- Epic-Story Beziehung.

**Best Practices**:
- Epic-Verknüpfung für Feature-Gruppierung nutzen.
- Blockierende Verknüpfungen nutzen, um Abhängigkeiten aufzuzeigen.
- Gründe für Verknüpfungen in Kommentaren dokumentieren.

### Berechtigungen & Sicherheit

**Berechtigungsschemata**:
- Projekte durchsuchen.
- Vorgänge erstellen/bearbeiten/löschen.
- Projekte administrieren.
- Sprints verwalten.

**Sicherheitsstufen**:
- Sichtbarkeit vertraulicher Vorgänge definieren.
- Zugriff auf sensible Daten kontrollieren.
- Sicherheitsrelevante Änderungen auditieren.

### Massenoperationen (Bulk Operations)
**Massenänderung**:
1. JQL nutzen, um Zielvorgänge zu finden.
2. Massenänderungsvorgang auswählen.
3. Zu aktualisierende Felder wählen.
4. **Validieren**: Vorschau aller Änderungen vor der Ausführung; bestätigen, dass der JQL-Filter nur beabsichtigte Vorgänge trifft — Massenänderungen sind schwer rückgängig zu machen.
5. Ausführen und bestätigen.
6. Hintergrundaufgabe überwachen.

**Massen-Übergänge (Bulk Transitions)**:
- Mehrere Vorgänge durch den Workflow bewegen.
- Nützlich für das Sprint-Cleanup.
- Erfordert entsprechende Berechtigungen.
- **Validieren**: JQL-Filter ausführen und Ergebnisse in kleinen Chargen prüfen, bevor sie im großen Maßstab angewendet werden.

## JQL-Funktionsreferenz

> **Tipp**: Speichere häufig verwendete Abfragen als benannte Filter, anstatt komplexe JQL ad-hoc neu auszuführen. Siehe [Best Practices](#best-practices) für Hinweise zur Performance.

**Datum**: `startOfDay()`, `endOfDay()`, `startOfWeek()`, `endOfWeek()`, `startOfMonth()`, `endOfMonth()`, `startOfYear()`, `endOfYear()`

**Sprint**: `openSprints()`, `closedSprints()`, `futureSprints()`

**Benutzer**: `currentUser()`, `membersOf("group")`

**Fortgeschritten**: `issueHistory()`, `linkedIssues()`, `issuesWithFixVersions()`

## Berichtsvorlagen

> **Tipp**: Diese JQL-Snippets können als geteilte Filter gespeichert oder direkt in Dashboard-Gadgets eingebunden werden (siehe [Dashboard-Erstellung](#dashboard-erstellung)).

| Bericht | JQL |
|---|---|
| Sprint-Bericht | `project = PROJ AND sprint = 23` |
| Team-Velocity | `assignee in (team) AND sprint in closedSprints() AND resolution = Done` |
| Bug-Trend | `type = Bug AND created >= -30d` |
| Blocker-Analyse | `priority = Blocker AND status != Done` |

## Entscheidungsrahmen

**Wann an den Atlassian Admin eskalieren**:
- Neues Projekt-Berechtigungsschema erforderlich.
- Organisationsweites Workflow-Schema erforderlich.
- Benutzer-Provisionierung oder -Deprovisionierung.
- Lizenz- oder Abrechnungsfragen.
- Systemweite Konfigurationsänderungen.

**Wann mit dem Scrum Master zusammenarbeiten**:
- Konfiguration des Sprint-Boards.
- Ansichten zur Backlog-Priorisierung.
- Teamspezifische Filter.
- Bedarf an Sprint-Reporting.

**Wann mit dem Senior PM zusammenarbeiten**:
- Reporting auf Portfolio-Ebene.
- Projektübergreifende Dashboards.
- Informationsbedarf für das Management.
- Projektübergreifende Abhängigkeiten.

## Übergabeprotokolle

**VON Senior PM**:
- Anforderungen an die Projektstruktur.
- Bedarf an Workflows und Feldern.
- Reporting-Anforderungen.
- Integrationsbedarf.

**AN Senior PM**:
- Projektübergreifende Metriken.
- Vorgangstrends und Muster.
- Engpässe im Workflow (Bottlenecks).
- Einblicke in die Datenqualität.

**VON Scrum Master**:
- Anfragen zur Konfiguration des Sprint-Boards.
- Bedarf an Workflow-Optimierung.
- Anforderungen an Backlog-Filterung.
- Einrichtung des Velocity-Trackings.

**AN Scrum Master**:
- Konfigurierte Sprint-Boards.
- Velocity-Berichte.
- Burndown-Charts.
- Ansichten zur Teamkapazität.

## Best Practices

**Datenqualität**:
- Pflichtfelder mit Feldvalidierungsregeln erzwingen.
- Konsistente Namenskonventionen für Issue-Keys pro Projekttyp nutzen.
- Regelmäßiges Cleanup von veralteten/verwaisten Vorgängen planen.

**Performance**:
- Führende Wildcards in JQL vermeiden (`~` auf großen Textfeldern ist teuer).
- Gespeicherte Filter nutzen, anstatt komplexe JQL ad-hoc neu auszuführen.
- Dashboard-Gadgets begrenzen, um die Ladezeit der Seite zu reduzieren.
- Abgeschlossene Projekte archivieren statt löschen, um die Historie zu bewahren.

**Governance**:
- Begründung für benutzerdefinierte Workflow-Zustände und -Übergänge dokumentieren.
- Berechtigungs-/Workflow-Schemata versionieren, bevor Änderungen vorgenommen werden.
- Change-Management-Review für organisationsweite Schema-Updates fordern.
- Berechtigungsaudits nach Änderungen der Benutzerrollen durchführen.

## Atlassian MCP Integration

**Primäres Werkzeug**: Jira MCP Server

**Wichtige Operationen mit Beispielen**:

Projekt erstellen:
```
mcp jira create_project --name "Mein Projekt" --key "MEINPROJ" --type scrum --lead "user@example.com"
```

JQL-Abfrage ausführen:
```
mcp jira search_issues --jql "project = MEINPROJ AND status != Done AND dueDate < now()" --maxResults 50
```

Feld eines Vorgangs aktualisieren:
```
mcp jira update_issue --issue "MEINPROJ-42" --field "status" --value "In Progress"
```

Sprint erstellen:
```
mcp jira create_sprint --board 10 --name "Sprint 5" --startDate "2024-06-01" --endDate "2024-06-14"
```

Board-Filter erstellen:
```
mcp jira create_filter --name "Offene Blocker" --jql "priority = Blocker AND status != Done" --shareWith "project-team"
```

**Integrationspunkte**:
- Metriken für das Senior PM Reporting abrufen.
- Sprint-Boards für den Scrum Master konfigurieren.
- Dokumentationsseiten für den Confluence Experten erstellen.
- Unterstützung der Vorlagenerstellung für den Vorlagenersteller.

## Verwandte Skills

- **Confluence Experte** (`project-management/confluence-expert/`) — Dokumentation ergänzt Jira-Workflows.
- **Atlassian Admin** (`project-management/atlassian-admin/`) — Berechtigungs- und Benutzerverwaltung für Jira-Projekte.

