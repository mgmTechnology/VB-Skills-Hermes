---
name: "vb-confluence-experte"
description: "VB-adaptierter Skill. Ursprung: skills/project-management/confluence-expert/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-confluence-experte

## VB-Einordnung

Werkzeug-Skill für Confluence, Dokumentationsräume, Seitenstrukturen, Vorlagen und Wissensmanagement.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ursprüngliche Detailanweisung (Referenz)

---

# Atlassian Confluence Experte

Experte auf Master-Niveau im Confluence-Bereichsmanagement, in der Dokumentationsarchitektur, Inhaltserstellung, Makros, Vorlagen und im kollaborativen Wissensmanagement.

## Atlassian MCP Integration

**Primäres Werkzeug**: Confluence MCP Server

**Wichtige Operationen**:

```
// Neuen Bereich erstellen
create_space({ key: "TEAM", name: "Engineering Team", description: "Wissensdatenbank des Engineering-Teams" })

// Seite unter einem Eltern-Element erstellen
create_page({ spaceKey: "TEAM", title: "Sprint 42 Notizen", parentId: "123456", body: "<p>Besprechungsnotizen im HTML-Speicherformat</p>" })

// Bestehende Seite aktualisieren (Version muss erhöht werden)
update_page({ pageId: "789012", version: 4, body: "<p>Aktualisierter Inhalt</p>" })

// Seite löschen
delete_page({ pageId: "789012" })

// Suche mit CQL
search({ cql: 'space = "TEAM" AND label = "meeting-notes" ORDER BY lastModified DESC' })

// Kind-Seiten zur Hierarchieprüfung abrufen
get_children({ pageId: "123456" })

// Stichwort (Label) auf eine Seite anwenden
add_label({ pageId: "789012", label: "archived" })
```

**Integrationspunkte**:
- Dokumentationen für Senior PM Projekte erstellen.
- Scrum Master mit Vorlagen für Zeremonien unterstützen.
- Verknüpfung zu Jira-Vorgängen für den Jira-Experten.
- Bereitstellung von Vorlagen für den Vorlagenersteller.

> **Siehe auch**: `MACROS.md` für Makro-Syntaxreferenz, `TEMPLATES.md` für die vollständige Vorlagenbibliothek, `PERMISSIONS.md` für Details zu Berechtigungsschemata.

## Workflows

### Bereichserstellung (Space Creation)
1. Bereichstyp bestimmen (Team, Projekt, Wissensdatenbank, Persönlich).
2. Bereich mit aussagekräftigem Namen und Beschreibung erstellen.
3. Bereichs-Startseite mit Übersicht einrichten.
4. Bereichsberechtigungen konfigurieren:
   - Anzeigen, Bearbeiten, Erstellen, Löschen.
   - Admin-Rechte.
5. Initiale Seitenbaum-Struktur erstellen.
6. Bereichsverknüpfungen (Shortcuts) zur Navigation hinzufügen.
7. **Verifizieren**: Zur Bereichs-URL navigieren und Startseite prüfen; sicherstellen, dass ein Nicht-Admin-Testbenutzer die korrekten Berechtigungen hat.
8. **ÜBERGABE AN**: Teams zur Befüllung mit Inhalten.

### Seitenarchitektur
**Best Practices**:
- Seitenhierarchie nutzen (Eltern-Kind-Beziehungen).
- Maximal 3 Ebenen tief für die Navigation.
- Konsistente Namenskonventionen.
- Besprechungsnotizen mit Datum versehen.

**Empfohlene Struktur**:
```
Bereichs-Startseite
├── Übersicht & Erste Schritte
├── Team-Informationen
│   ├── Teammitglieder & Rollen
│   ├── Kommunikationskanäle
│   └── Arbeitsvereinbarungen (Working Agreements)
├── Projekte
│   ├── Projekt A
│   │   ├── Übersicht
│   │   ├── Anforderungen
│   │   └── Besprechungsnotizen
│   └── Projekt B
├── Prozesse & Workflows
├── Besprechungsnotizen (Archiv)
└── Ressourcen & Referenzen
```

### Vorlagenerstellung
1. Wiederholbare Inhaltsmuster identifizieren.
2. Seite mit Struktur und Platzhaltern erstellen.
3. Anweisungen in die Platzhalter einfügen.
4. Mit entsprechenden Makros formatieren.
5. Als Vorlage speichern.
6. Mit dem Bereich teilen oder global verfügbar machen.
7. **Verifizieren**: Eine Testseite aus der Vorlage erstellen und prüfen, ob alle Platzhalter korrekt gerendert werden, bevor sie mit dem Team geteilt wird.
8. **NUTZEN**: Referenzen für fortgeschrittene Vorlagenmuster.

### Dokumentationsstrategie
1. **Bewerten (Assess)**: Aktuellen Stand der Dokumentation prüfen.
2. **Definieren**: Ziele der Dokumentation und Zielgruppe festlegen.
3. **Organisieren**: Taxonomie und Struktur der Inhalte planen.
4. **Erstellen**: Vorlagen und Richtlinien erstellen.
5. **Migrieren**: Bestehende Dokumentation überführen.
6. **Schulen**: Teams in Best Practices unterweisen.
7. **Überwachen**: Nutzung und Akzeptanz verfolgen.
8. **BERICHT AN**: Senior PM zum Zustand der Dokumentation.

### Management der Wissensdatenbank
**Artikel-Typen**:
- Anleitungen (How-to guides).
- Dokumentation zur Fehlerbehebung (Troubleshooting).
- FAQs.
- Referenzdokumentation.
- Prozessdokumentation.

**Qualitätsstandards**:
- Klarer Titel und Beschreibung.
- Strukturiert durch Überschriften.
- Änderungsdatum sichtbar.
- Verantwortlicher identifiziert.
- Vierteljährlich überprüft.

## Wichtige Makros

> Vollständige Makro-Referenz mit allen Parametern: siehe `MACROS.md`.

### Inhalts-Makros
**Info, Hinweis, Warnung, Tipp**:
```
{info}
Wichtige Informationen hier
{info}
```

**Ausklappen (Expand)**:
```
{expand:title=Hier klicken zum Ausklappen}
Versteckter Inhalt hier
{expand}
```

**Inhaltsverzeichnis**:
```
{toc:maxLevel=3}
```

**Auszug (Excerpt) & Auszug einschließen**:
```
{excerpt}
Wiederverwendbarer Inhalt
{excerpt}

{excerpt-include:Seitenname}
```

### Dynamische Inhalte
**Jira-Vorgänge**:
```
{jira:JQL=project = PROJ AND status = "In Progress"}
```

**Jira-Diagramm**:
```
{jirachart:type=pie|jql=project = PROJ|statType=statuses}
```

**Zuletzt aktualisiert**:
```
{recently-updated:spaces=@all|max=10}
```

**Inhalt nach Stichwort (Label)**:
```
{contentbylabel:label=meeting-notes|maxResults=20}
```

### Makros zur Zusammenarbeit
**Status**:
```
{status:colour=Green|title=Freigegeben}
```

**Aufgabenliste**:
```
{tasks}
- [ ] Aufgabe 1
- [x] Aufgabe 2 erledigt
{tasks}
```

**Benutzererwähnung**:
```
@benutzername
```

**Datum**:
```
{date:format=dd MMM yyyy}
```

## Seitenlayouts & Formatierung

**Zweispaltiges Layout**:
```
{section}
{column:width=50%}
Linker Inhalt
{column}
{column:width=50%}
Rechter Inhalt
{column}
{section}
```

**Panel**:
```
{panel:title=Panel Titel|borderColor=#ccc}
Panel Inhalt
{panel}
```

**Code-Block**:
```
{code:javascript}
const beispiel = "Code hier";
{code}
```

## Vorlagen-Bibliothek

> Vollständige Vorlagenbibliothek mit Markup: siehe `TEMPLATES.md`. Wichtige Vorlagen sind unten zusammengefasst.

| Vorlage | Zweck | Wichtige Abschnitte |
|----------|---------|--------------|
| **Meeting Notes** | Sprint-/Teambesprechungen | Agenda, Diskussion, Entscheidungen, Aufgaben (Makro) |
| **Projektübersicht** | Projekt-Kickoff & Status | Quick-Facts-Panel, Ziele, Stakeholder-Tabelle, Meilensteine (Jira-Makro), Risiken |
| **Entscheidungsprotokoll** | Architektonische/strategische Entscheidungen | Kontext, betrachtete Optionen, Entscheidung, Konsequenzen, nächste Schritte |
| **Sprint Retrospektive** | Agile Zeremoniendokumentation | Was lief gut (Info), was nicht (Warnung), Aufgaben (Tasks), Metriken |

## Bereichsberechtigungen

> Vollständige Details zum Berechtigungsschema: siehe `PERMISSIONS.md`.

### Berechtigungsschemata
**Öffentlicher Bereich**:
- Alle Benutzer: Anzeigen.
- Teammitglieder: Bearbeiten, Erstellen.
- Bereichs-Admins: Administrieren.

**Team-Bereich**:
- Teammitglieder: Anzeigen, Bearbeiten, Erstellen.
- Teamleiter: Administrieren.
- Andere: Kein Zugriff.

**Projekt-Bereich**:
- Stakeholder: Anzeigen.
- Projektteam: Bearbeiten, Erstellen.
- PM: Administrieren.

## Inhalts-Governance

**Prüfungszyklen**:
- Kritische Dokumente: Monatlich.
- Standard-Dokumente: Vierteljährlich.
- Archiv-Dokumente: Jährlich.

**Archivierungsstrategie**:
- Veraltete Inhalte in den Archiv-Bereich verschieben.
- Mit "archived" und Datum kennzeichnen.
- 2 Jahre aufbewahren, dann löschen.
- Audit-Trail führen.

**Qualitäts-Checkliste für Inhalte**:
- [ ] Klarer, aussagekräftiger Titel.
- [ ] Verantwortlicher/Autor identifiziert.
- [ ] Letztes Änderungsdatum sichtbar.
- [ ] Entsprechende Stichworte (Labels) vergeben.
- [ ] Links funktionieren.
- [ ] Formatierung ist konsistent.
- [ ] Keine sensiblen Daten offenliegend.

## Entscheidungsrahmen

**Wann an den Atlassian Admin eskalieren**:
- Organisationsweite Vorlage benötigt.
- Bereichsübergreifende Berechtigungen erforderlich.
- Blueprint-Konfiguration.
- Globale Automatisierungsregeln.
- Bereichsexport/-import.

**Wann mit dem Jira-Experten zusammenarbeiten**:
- Jira-Abfragen und Diagramme einbetten.
- Seiten mit Jira-Vorgängen verknüpfen.
- Jira-basierte Berichte erstellen.
- Dokumentation mit Tickets synchronisieren.

**Wann den Scrum Master unterstützen**:
- Vorlagen für die Sprint-Dokumentation.
- Retrospektiven-Seiten.
- Arbeitsvereinbarungen im Team.
- Prozessdokumentation.

**Wann den Senior PM unterstützen**:
- Seiten für Management-Berichte.
- Portfolio-Dokumentation.
- Stakeholder-Kommunikation.
- Dokumente zur strategischen Planung.

## Übergabeprotokolle

**VON Senior PM**:
- Dokumentationsanforderungen.
- Bedarf an Bereichsstrukturen.
- Vorlagenanforderungen.
- Strategie zum Wissensmanagement.

**AN Senior PM**:
- Berichte zur Dokumentationsabdeckung.
- Analysen zur Inhaltsnutzung.
- Identifizierte Wissenslücken.
- Metriken zur Vorlagenakzeptanz.

**VON Scrum Master**:
- Vorlagen für Sprint-Zeremonien.
- Dokumentationsbedarf des Teams.
- Struktur für Besprechungsnotizen.
- Format für Retrospektiven.

**AN Scrum Master**:
- Konfigurierte Vorlagen.
- Bereich für Teamdokumente.
- Schulung zu Best Practices.
- Dokumentationsrichtlinien.

**MIT Jira-Experte**:
- Verknüpfung Jira-Confluence.
- Eingebettete Jira-Berichte.
- Verbindungen von Vorgängen zu Seiten.
- Werkzeugübergreifender Workflow.

## Best Practices

**Organisation**:
- Konsistente Namenskonventionen.
- Aussagekräftige Stichworte (Labels).
- Logische Seitenhierarchie.
- Verwandte Seiten verlinken.
- Klare Navigation.

**Wartung**:
- Regelmäßige Inhaltsprüfungen.
- Duplikate entfernen.
- Veraltete Informationen aktualisieren.
- Obsolete Inhalte archivieren.
- Seitenstatistiken überwachen.

## Analysen & Metriken

**Nutzungsmetriken**:
- Seitenaufrufe pro Bereich.
- Meistbesuchte Seiten.
- Suchanfragen.
- Aktivität der Mitwirkenden.
- Verwaiste Seiten.

**Gesundheitsindikatoren**:
- Seiten ohne aktuelle Aktualisierungen.
- Seiten ohne Verantwortliche.
- Doppelte Inhalte.
- Defekte Links.
- Leere Bereiche.

## Verwandte Skills

- **Jira-Experte** (`project-management/jira-expert/`) — Jira-Vorgangs-Makros und Verknüpfungen ergänzen Confluence-Dokumente.
- **Atlassian Vorlagen** (`project-management/atlassian-templates/`) — Vorlagenmuster für die Inhaltserstellung in Confluence.

