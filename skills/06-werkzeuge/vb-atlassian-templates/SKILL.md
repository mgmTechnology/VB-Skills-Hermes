---
name: "vb-atlassian-templates"
description: "VB-adaptierter Skill. Ursprung: skills/project-management/atlassian-templates/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-atlassian-templates

## VB-Einordnung

Werkzeug-Skill für Jira-/Confluence-Vorlagen, Blueprints und standardisierte Strukturen.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ursprüngliche Detailanweisung (Referenz)

---

# Atlassian Vorlagen- & Dateiersteller Experte

Spezialist für die Erstellung, Änderung und Verwaltung von wiederverwendbaren Vorlagen (Templates) und Dateien für Jira und Confluence. Stellt Konsistenz sicher, beschleunigt die Inhaltserstellung und pflegt organisationsweite Standards.

---

## Workflows

### Prozess zur Vorlagenerstellung
1. **Discover (Entdecken)**: Stakeholder interviewen, um den Bedarf zu verstehen.
2. **Analyze (Analysieren)**: Bestehende Inhaltsmuster prüfen.
3. **Design (Entwerfen)**: Vorlagenstruktur und Platzhalter erstellen.
4. **Implement (Implementieren)**: Vorlage mit Makros und Formatierung aufbauen.
5. **Test (Testen)**: Mit Beispieldaten validieren — bestätigen, dass die Vorlage in der Vorschau korrekt gerendert wird, bevor sie veröffentlicht wird.
6. **Document (Dokumentieren)**: Nutzungshinweise erstellen.
7. **Publish (Veröffentlichen)**: In den entsprechenden Bereich/Projekt via MCP bereitstellen (siehe MCP-Operationen unten).
8. **Verify (Verifizieren)**: Erfolg der Bereitstellung bestätigen; bei Fehlern auf die vorherige Version zurückrollen.
9. **Train (Schulen)**: Nutzer in der Verwendung der Vorlage schulen.
10. **Monitor (Überwachen)**: Akzeptanz verfolgen und Feedback sammeln.
11. **Iterate (Iterieren)**: Basierend auf der Nutzung verfeinern.

### Prozess zur Vorlagenänderung
1. **Assess (Bewerten)**: Änderungsanfrage und Auswirkungen prüfen.
2. **Version (Versionieren)**: Neue Version erstellen, alte verfügbar halten.
3. **Modify (Modifizieren)**: Vorlagenstruktur/-inhalt aktualisieren.
4. **Test (Testen)**: Validieren, dass Änderungen die bestehende Nutzung nicht beeinträchtigen; Vorschau der aktualisierten Vorlage vor der Veröffentlichung prüfen.
5. **Migrate (Migrieren)**: Migrationspfad für bestehende Inhalte anbieten.
6. **Communicate (Kommunizieren)**: Änderungen den Nutzern mitteilen.
7. **Support (Unterstützen)**: Nutzer bei der Migration unterstützen.
8. **Archive (Archivieren)**: Alte Version nach dem Übergang deponieren; bestätigen, dass die veraltete Vorlage als "nicht gelistet" markiert, aber nicht gelöscht wird.

### Blueprint-Entwicklung
1. Blueprint-Umfang und Zweck definieren.
2. Mehrseitige Struktur entwerfen.
3. Seitenvorlagen für jeden Abschnitt erstellen.
4. Regeln für die Seitenerstellung konfigurieren.
5. Dynamische Inhalte hinzufügen (Jira-Abfragen, Benutzerdaten).
6. Blueprint-Erstellungsflow end-to-end in einem Testbereich testen.
7. Verifizieren, dass alle Makro-Referenzen vor der Bereitstellung korrekt aufgelöst werden.
8. **ÜBERGABE AN**: Atlassian Admin für die globale Bereitstellung.

---

## Confluence Vorlagen-Bibliothek

Siehe **TEMPLATES.md** für vollständige Referenztabellen und kopierbereite Vorlagenstrukturen. Die folgende Tabelle fasst die Standardtypen zusammen, die dieser Skill erstellt und verwaltet.

### Confluence Vorlagentypen
| Vorlage | Zweck | Wichtige genutzte Makros |
|----------|---------|-----------------|
| **Meeting Notes** | Strukturierte Besprechungsprotokolle mit Agenda, Entscheidungen und Aufgaben | `{date}`, `{tasks}`, `{panel}`, `{info}`, `{note}` |
| **Project Charter** | Projektumfang auf Organisationsebene, Stakeholder-RACI, Zeitplan und Budget | `{panel}`, `{status}`, `{timeline}`, `{info}` |
| **Sprint Retrospective** | Agile Zeremonien-Vorlage (Was lief gut / Was lief nicht gut / Maßnahmen) | `{panel}`, `{expand}`, `{tasks}`, `{status}` |
| **PRD** | Feature-Definition mit Zielen, User Stories, funktionalen/nicht-funktionalen Anforderungen und Release-Plan | `{panel}`, `{status}`, `{jira}`, `{warning}` |
| **Decision Log** | Strukturierte Analyse von Optionen mit Entscheidungsmatrix und Umsetzungsverfolgung | `{panel}`, `{status}`, `{info}`, `{tasks}` |

**Standard-Abschnitte**, die in allen Confluence-Vorlagen enthalten sind:
- Header-Panel mit Metadaten (Owner, Datum, Status).
- Klar beschriftete Inhaltsbereiche mit Inline-Platzhalteranweisungen.
- Aufgabenblock (Action Items) unter Verwendung des `{tasks}` Makros.
- Verwandte Links und Referenzen.

### Vollständiges Beispiel: Meeting Notes Vorlage

Das Folgende ist eine kopierbereite Meeting Notes Vorlage im Confluence-Speicherformat (Wiki Markup):

```
{panel:title=Besprechungs-Metadaten|borderColor=#0052CC|titleBGColor=#0052CC|titleColor=#FFFFFF}
*Datum:* {date}
*Besprechungsleiter:* @[Name]
*Teilnehmer:* @[Name], @[Name]
*Status:* {status:colour=Yellow|title=In Bearbeitung}
{panel}

h2. Agenda
# [Tagesordnungspunkt 1]
# [Tagesordnungspunkt 2]
# [Tagesordnungspunkt 3]

h2. Diskussion & Entscheidungen
{panel:title=Wichtige Entscheidungen|borderColor=#36B37E|titleBGColor=#36B37E|titleColor=#FFFFFF}
* *Entscheidung 1:* [Was wurde entschieden und warum]
* *Entscheidung 2:* [Was wurde entschieden und warum]
{panel}

{info:title=Notizen}
[Detaillierte Diskussionsnotizen, Kontext oder Hintergrund hier]
{info}

h2. Aufgaben (Action Items)
{tasks}
* [ ] [Aufgabe] — Verantwortlich: @[Name] — Fällig am: {date}
* [ ] [Aufgabe] — Verantwortlich: @[Name] — Fällig am: {date}
{tasks}

h2. Nächste Schritte & Verwandte Links
* Nächste Besprechung: {date}
* Verwandte Seiten: [Link]
* Verwandte Jira-Vorgänge: {jira:key=PROJ-123}
```

> Vollständige Beispiele für alle anderen Vorlagentypen (Project Charter, Sprint Retrospective, PRD, Decision Log) und alle Jira-Vorlagen können auf Anfrage generiert werden oder sind in **TEMPLATES.md** zu finden.

---

## Jira Vorlagen-Bibliothek

### Jira Vorlagentypen
| Vorlage | Zweck | Wichtige Abschnitte |
|----------|---------|--------------|
| **User Story** | Feature-Anfragen im "Als ein / möchte ich / so dass" Format | Akzeptanzkriterien (Gegeben/Wenn/Dann), Design-Links, Technische Notizen, Definition of Done |
| **Bug Report** | Fehlererfassung mit Schritten zur Reproduktion | Umgebung, Schritte zur Reproduktion, Erwartetes vs. Tatsächliches Verhalten, Schweregrad, Workaround |
| **Epic** | Umfang einer übergeordneten Initiative | Vision, Ziele, Erfolgsmetriken, Story-Breakdown, Abhängigkeiten, Zeitplan |

**Standard-Abschnitte**, die in allen Jira-Vorlagen enthalten sind:
- Klare Zusammenfassungszeile.
- Akzeptanz- oder Erfolgskriterien als Checkboxen.
- Block für verwandte Vorgänge und Abhängigkeiten.
- Definition of Done (für Stories).

---

## Makro-Nutzungsrichtlinien

**Dynamische Inhalte**: Makros für automatisch aktualisierte Inhalte nutzen (Daten, Erwähnungen, Jira-Abfragen).
**Visuelle Hierarchie**: `{panel}`, `{info}` und `{note}` zur visuellen Unterscheidung nutzen.
**Interaktivität**: `{expand}` für ausklappbare Bereiche in langen Vorlagen nutzen.
**Integration**: Jira-Diagramme und -Tabellen via `{jira}` Makro für Live-Daten einbetten.

---

## Atlassian MCP Integration

**Primäre Werkzeuge**: Confluence MCP, Jira MCP

### Vorlagen-Operationen via MCP

Alle untenstehenden MCP-Aufrufe verwenden die exakten Parameternamen, die vom Atlassian MCP Server erwartet werden. Ersetze die Platzhalter in spitzen Klammern durch reale Werte vor der Ausführung.

**Seitenvorlage in Confluence erstellen:**
```json
{
  "tool": "confluence_create_page",
  "parameters": {
    "space_key": "PROJ",
    "title": "Vorlage: Meeting Notes",
    "body": "<Vorlage Inhalt im Storage-Format>",
    "labels": ["template", "meeting-notes"],
    "parent_id": "<optionale ID der übergeordneten Seite>"
  }
}
```

**Bestehende Vorlage aktualisieren:**
```json
{
  "tool": "confluence_update_page",
  "parameters": {
    "page_id": "<bestehende Page-ID>",
    "version": "<aktuelle_version + 1>",
    "title": "Vorlage: Meeting Notes",
    "body": "<aktualisierter Inhalt im Storage-Format>",
    "version_comment": "v2 — Status-Makro im Header hinzugefügt"
  }
}
```

**Jira Vorgangsbeschreibungs-Vorlage erstellen (via Feldkonfiguration):**
```json
{
  "tool": "jira_update_field_configuration",
  "parameters": {
    "project_key": "PROJ",
    "field_id": "description",
    "default_value": "<Vorlage in Markdown oder Atlassian Document Format JSON>"
  }
}
```

**Vorlage in mehreren Bereichen bereitstellen (Batch):**
```json
// Für jeden Zielbereich (Space Key) wiederholen
{
  "tool": "confluence_create_page",
  "parameters": {
    "space_key": "<SPACE_KEY>",
    "title": "Vorlage: Meeting Notes",
    "body": "<Vorlage Inhalt im Storage-Format>",
    "labels": ["template"]
  }
}
// Nach jeder Erstellung verifizieren:
{
  "tool": "confluence_get_page",
  "parameters": {
    "space_key": "<SPACE_KEY>",
    "title": "Vorlage: Meeting Notes"
  }
}
// Sicherstellen, dass Response-Status == 200 und Page-Body nicht leer ist, bevor mit dem nächsten Bereich fortgefahren wird.
```

**Validierungs-Checkpoint nach der Bereitstellung:**
- Die erstellte/aktualisierte Seite abrufen und sicherstellen, dass sie ohne Makro-Fehler gerendert wird.
- Prüfen, ob `{jira}` Einbettungen gegen das Ziel-Jira-Projekt aufgelöst werden.
- Bestätigen, dass `{tasks}` Blöcke in der veröffentlichten Ansicht interaktiv sind.
- Falls eine Prüfung fehlschlägt: Revert mittels `confluence_update_page` mit `version: <aktuelle + 1>` und dem Inhalt der vorherigen Version.

---

## Best Practices & Governance

**Organisationsspezifische Standards:**
- Vorlagenversionen mit Versionshinweisen im Seiten-Header verfolgen.
- Veraltete Vorlagen mit einem `{warning}` Banner markieren, bevor sie archiviert werden; archivieren (nicht löschen).
- Nutzungshandbücher pflegen, die von jeder Vorlage aus verlinkt sind.
- Feedback in einem vierteljährlichen Review-Zyklus sammeln; Nutzungsmetriken vor der Deprecating einbeziehen.

**Quality Gates (vor jeder Bereitstellung anwenden):**
- Beispielinhalte für jeden Abschnitt bereitgestellt.
- Mit Beispieldaten in der Vorschau getestet.
- Versionskommentar zum Änderungsprotokoll hinzugefügt.
- Feedback-Mechanismus vorhanden (Kommentare aktiviert oder verlinkte Umfrage).

**Governance-Prozess**:
1. Anfrage und Begründung.
2. Design und Review.
3. Test mit Pilot-Nutzern.
4. Dokumentation.
5. Genehmigung.
6. Bereitstellung (via MCP oder manuell).
7. Schulung.
8. Überwachung.

---

## Übergabeprotokolle

Siehe **HANDOFFS.md** für die vollständige Übergabematrix. Zusammenfassung:

| Partner | Erhält VON | Sendet AN |
|---------|--------------|---------|
| **Senior PM** | Vorlagenanforderungen, Berichtsvorlagen, Managementformate | Fertiggestellte Vorlagen, Nutzungsanalysen, Optimierungsvorschläge |
| **Scrum Master** | Bedarf für Sprint-Zeremonien, teamspezifische Anfragen, Retro-Format-Präferenzen | Sprint-bereite Vorlagen, agile Zeremonienstrukturen, Velocity-Tracking-Vorlagen |
| **Jira Experte** | Anforderungen an Vorgangsvorlagen, Anzeige-Bedarf für benutzerdefinierte Felder | Vorgangsbeschreibungs-Vorlagen, Feldkonfigurations-Vorlagen, JQL-Abfragevorlagen |
| **Confluence Experte** | Bereichsspezifischer Bedarf, globale Vorlagenanfragen, Blueprint-Anforderungen | Konfigurierte Seitenvorlagen, Blueprint-Strukturen, Bereitstellungspläne |
| **Atlassian Admin** | Organisationsweite Standards, globale Bereitstellungsanforderungen, Compliance-Vorlagen | Globale Vorlagen zur Genehmigung, Nutzungsberichte, Compliance-Status |

