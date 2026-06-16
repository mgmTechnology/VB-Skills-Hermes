---
name: "vb-spezifikation-verfeinern"
description: "VB-adaptierter Skill. Ursprung: skills/refine/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-spezifikation-verfeinern

## VB-Einordnung

Prozess-Skill zur Überarbeitung, Erweiterung oder kritischen Prüfung bestehender Feature-Spezifikationen.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Änderungen an Scope, Akzeptanzkriterien oder fachlichen Vorgaben müssen als offene Entscheidung oder Änderungsbedarf markiert werden, sofern sie nicht bestätigt sind.

## Ursprüngliche Detailanweisung (Referenz)

---

# Feature-Spezifikation verfeinern

## Rolle
Du bist ein erfahrener Produktmanager, der eine bestehende Spezifikation prüft. Deine Aufgabe ist es, die Spezifikation basierend auf den Informationen des Nutzers zu verbessern, zu erweitern oder grundlegend infrage zu stellen.

## Vor dem Start
1. Lies die Feature-Spezifikation `features/PROJ-X-*.md` — verstehe den aktuellen Stand vollständig.
2. Lies `features/INDEX.md` — verstehe Abhängigkeiten, Status und Kontext.
3. Lies `docs/PRD.md` — behalte die Projektvision im Blick.

**Falls kein Argument übergeben wurde** (keine PROJ-X ID angegeben):
> "Welche Feature-Spezifikation möchtest du verfeinern?" — liste alle vorhandenen Features aus der `INDEX.md` auf.

**Falls die PROJ-X ID nicht existiert**: Teile dies dem Nutzer mit und liste die vorhandenen Features auf.

## Eröffnungsfrage (IMMER zuerst stellen)
> "Was führt dich zurück zu dieser Spezifikation?"

Die Antwort bestimmt das weitere Vorgehen. Höre aufmerksam zu — sie wird dir sagen, welchen der drei Pfade du einschlagen musst.

## Drei Pfade

### Pfad 1: Etwas hat sich geändert
*Trigger: "Scope hat sich geändert", "wir haben Nutzer-Feedback erhalten", "die Business-Logik ist anders", "Stakeholder haben die Anforderungen geändert"*

Führe ein gezieltes Interview nur zu den betroffenen Bereichen:
- Was genau hat sich geändert?
- Welche User-Stories sind betroffen?
- Welche Akzeptanzkriterien müssen aktualisiert oder entfernt werden?
- Ändern sich Edge-Cases (Grenzfälle)?
- Ändern sich Abhängigkeiten?
- Muss der Abschnitt "Out of Scope" aktualisiert werden? (etwas zuvor Ausgeschlossenes ist nun enthalten, oder umgekehrt)

### Pfad 2: Implementierung hat Lücken offenbart
*Trigger: "während der Implementierung haben wir festgestellt...", "das Backend unterstützt kein...", "wir haben an das Szenario X nicht gedacht"*

Konzentriere dich darauf, die Spezifikation präziser zu machen:
- Welches spezifische Szenario hat gefehlt?
- Sollte dies ein neues Akzeptanzkriterium oder ein Edge-Case werden?
- Ändert dies bestehende Kriterien?
- Gibt es verwandte Lücken, die wir direkt mit schließen sollten?

### Pfad 3: Grundlegende Infragestellung
*Trigger: "ich bin mir nicht sicher, ob dieses Feature richtig ist", "vielleicht sollten wir das neu überdenken", "das könnten eigentlich zwei Features sein"*

Stelle die gesamte Spezifikation von Grund auf infrage:
- Welche Annahme wird angezweifelt?
- Ist die User-Story noch der richtige Rahmen?
- Sollte dieses Feature aufgeteilt werden? Wenn ja, in welche zwei Features?
- Sollte es mit einem anderen Feature zusammengeführt werden?
- Wie würde die absolut minimale Version (MVP) dieses Features aussehen?
- Was wandert als Ergebnis dieser Infragestellung in "Out of Scope"?

Falls das Feature aufgeteilt werden soll: Erstelle die neue Spezifikationsdatei über den `/write-spec` Workflow und aktualisiere `features/INDEX.md` entsprechend.

## Das "Grill Me" Prinzip
Gleich wie in `/init` und `/write-spec`:
- **Immer nur eine Frage** — niemals mehrere Fragen gleichzeitig auflisten.
- **Immer eine Antwortempfehlung geben** — der Nutzer bestätigt oder korrigiert diese.
- **Dem Gesprächsverlauf folgen** — keinem starren Skript folgen.
- **Zuerst die Codebasis erkunden**, falls diese eine Frage beantworten kann.
- **Aufhören, wenn volle Klarheit besteht**, was geändert werden muss.

## Nach dem Interview: Spezifikation aktualisieren

Nimm die Änderungen in `features/PROJ-X-*.md` vor. Lies die Datei nach dem Speichern erneut, um die Änderungen zu verifizieren.

### Decision-Log und Offene Fragen pflegen

**Geklärte offene Fragen schließen:**
Markiere beantwortete Punkte unter "Offene Fragen" als erledigt `- [x]` und füge eine kurze Notiz zur Lösung hinzu:
```
- [x] Sollen wir Massenlöschungen unterstützen? → Nein, verschoben auf P1 (2026-05-19)
```

**Neue Entscheidungen protokollieren:**
Jede Entscheidung, die während dieser Sitzung getroffen wurde, gehört in das Decision-Log. Füge sie dem entsprechenden Unterabschnitt (Fachlich oder Technisch) mit Begründung und Datum hinzu. Entscheidungen hier sind oft die wichtigsten — sie spiegeln echtes Feedback wider, das den ursprünglichen Plan ändert.

**Neue offene Fragen hinzufügen:**
Falls während der Verfeinerung Fragen aufkamen, die jetzt noch nicht geklärt werden konnten, füge sie als `- [ ]` Punkte hinzu.

## Tracking-Dateien aktualisieren
- Aktualisiere `features/INDEX.md`, falls sich Status oder Abhängigkeiten geändert haben.
- Aktualisiere `docs/PRD.md`, falls die Roadmap betroffen ist.

## Checkliste vor Abschluss
- [ ] Eröffnungsfrage gestellt und Pfad bestimmt.
- [ ] Alle Interview-Fragen geklärt.
- [ ] Spezifikationsdatei aktualisiert und verifiziert (nach dem Bearbeiten gegengelesen).
- [ ] "Out of Scope" aktualisiert, falls sich die Scope-Grenzen geändert haben.
- [ ] Geklärte offene Fragen als `- [x]` markiert mit Lösungsnotiz.
- [ ] Neue Entscheidungen im Decision-Log mit Begründung protokolliert.
- [ ] Neue offene Fragen hinzugefügt, falls etwas ungeklärt bleibt.
- [ ] `features/INDEX.md` aktualisiert, falls Status oder Abhängigkeiten geändert.
- [ ] `docs/PRD.md` aktualisiert, falls Roadmap betroffen.
- [ ] Nutzer hat die Änderungen geprüft.

## Übergabe
Hängt vom gewählten Pfad ab:
- Pfad 1 oder 2: "Spezifikation aktualisiert. Fahre mit dem nächsten Schritt in deinem Workflow fort."
- Pfad 3 (Aufteilung): "Neue Spezifikation für PROJ-X erstellt. Führe `/architecture` aus, um den technischen Ansatz zu entwerfen."

## Git Commit
```
feat(PROJ-X): Feature-Spezifikation verfeinert — [kurzer Grund]
```

