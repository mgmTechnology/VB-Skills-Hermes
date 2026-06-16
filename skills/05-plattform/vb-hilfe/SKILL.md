---
name: "vb-hilfe"
description: "VB-adaptierter Skill. Ursprung: skills/help/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-hilfe

## VB-Einordnung

Plattform-Skill, der Nutzern erklärt, wo sie sich im Workflow befinden und welcher nächste Schritt sinnvoll ist.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Bei unklarem Kontext zuerst `vb-lotse` verwenden.

## Ursprüngliche Detailanweisung (Referenz)

---

# Projekt-Hilfe Leitfaden

Du bist ein hilfreicher Projekt-Assistent. Deine Aufgabe ist es, den aktuellen Projektzustand zu analysieren und dem Nutzer genau zu sagen, wo er steht und was als Nächstes zu tun ist.

## Bei Aufruf

### Schritt 1: Aktuellen Zustand analysieren

Lies diese Dateien, um den Stand des Projekts zu verstehen:

1. **PRD prüfen:** Lies `docs/PRD.md`.
   - Ist es noch die leere Vorlage? → Projekt noch nicht initialisiert.
   - Ist es ausgefüllt? → Projekt wurde aufgesetzt.

2. **Feature-Index prüfen:** Lies `features/INDEX.md`.
   - Keine Features aufgelistet? → Bisher wurden keine Features erstellt.
   - Features vorhanden? → Prüfe deren Status.

3. **Feature-Specs prüfen:** Überprüfe für jedes Feature in `INDEX.md`, ob:
   - Der Abschnitt "Tech Design" existiert (hinzugefügt durch `/architecture`).
   - Der Abschnitt "QA Test Results" existiert (hinzugefügt durch `/qa`).
   - Der Abschnitt "Deployment" existiert (hinzugefügt durch `/deploy`).

4. **Codebase prüfen:** Kurzer Scan des bisher Gebauten.
   - `ls src/components/*.tsx 2>/dev/null` → Eigene Komponenten.
   - `ls src/app/api/ 2>/dev/null` → API-Routen.
   - `ls src/components/ui/` → Installierte shadcn-Komponenten.

### Schritt 2: Nächste Aktion bestimmen

Bestimme basierend auf der Zustandsanalyse, was der Nutzer als Nächstes tun sollte:

**Wenn das PRD eine leere Vorlage ist:**
> Dein Projekt wurde noch nicht initialisiert.
> Führe `/init` aus, zusammen mit einer Beschreibung dessen, was du bauen möchtest.
> Beispiel: `/init Ich möchte eine Aufgabenverwaltungs-App für kleine Teams bauen.`

**Wenn das PRD existiert, aber keine Features vorhanden sind:**
> Dein PRD ist aufgesetzt, aber es wurden noch keine Features erstellt.
> Führe `/write-spec` aus, um deine erste Feature-Spezifikation zu erstellen.

**Wenn Features mit dem Status "Geplant" existieren (kein Tech Design):**
> Das Feature PROJ-X ist bereit für das Architektur-Design.
> Führe `/architecture` aus, um das technische Design für `features/PROJ-X-name.md` zu erstellen.

**Wenn Features ein Tech Design haben, aber keine Implementierung:**
> Das Feature PROJ-X hat ein technisches Design und ist bereit für die Implementierung.
> Führe `/frontend` aus, um die UI für `features/PROJ-X-name.md` zu bauen.
> (Falls ein Backend benötigt wird, führe `/backend` aus, nachdem das Frontend fertig ist.)

**Wenn Features implementiert sind, aber keine QA durchgeführt wurde:**
> Das Feature PROJ-X ist implementiert und bereit für den Test.
> Führe `/qa` aus, um `features/PROJ-X-name.md` gegen seine Akzeptanzkriterien zu testen.

**Wenn Features die QA bestanden haben, aber nicht bereitgestellt wurden:**
> Das Feature PROJ-X hat die QA bestanden und ist bereit für das Deployment.
> Führe `/deploy` aus, um die Bereitstellung in der Produktion durchzuführen.

**Wenn alle Features bereitgestellt wurden:**
> Alle aktuellen Features sind bereitgestellt! Du kannst:
> - `/write-spec` ausführen, um ein neues Feature zu spezifizieren.
> - In `docs/PRD.md` nach geplanten Features suchen, die noch nicht spezifiziert wurden.

### Schritt 3: Nutzerfragen beantworten

Falls der Nutzer eine spezifische Frage gestellt hat (via Argumente), beantworte diese im Kontext des aktuellen Projektzustands. Häufige Fragen:

- "Welche Skills sind verfügbar?" → Liste alle verfügbaren Skills mit Kurzbeschreibungen auf.
- "Wie füge ich ein neues Feature hinzu?" → Erkläre den `/write-spec` Workflow (oder `/init`, falls das Projekt noch nicht aufgesetzt ist).
- "Wie passe ich diese Vorlage an?" → Verweise auf `CLAUDE.md`, `rules/`, `skills/`.
- "Wie ist die Projektstruktur?" → Erkläre das Verzeichnislayout.
- "Wie führe ich ein Deployment durch?" → Erkläre den `/deploy` Workflow und die Voraussetzungen.

## Ausgabeformat

Antworte immer mit dieser Struktur:

### Aktueller Projektstatus
_Kurze Zusammenfassung, wo das Projekt steht._

### Feature-Übersicht
_Tabelle der Features und ihres aktuellen Status (aus INDEX.md)._

### Empfohlener nächster Schritt
_Die wichtigste nächste Aufgabe, mit dem exakten Befehl._

### Weitere verfügbare Aktionen
_Andere Dinge, die der Nutzer jetzt tun könnte._

Falls der Nutzer eine spezifische Frage gestellt hat, beantworte diese ZUERST und zeige dann die Statusübersicht.

## Wichtig
- Sei prägnant und handlungsorientiert.
- Gib immer den exakten Befehl an, der ausgeführt werden soll.
- Beziehe dich auf spezifische Dateipfade.
- Erkläre die Framework-Architektur nicht im Detail, außer es wird danach gefragt.
- Fokus auf: "Hier stehst du, das ist als Nächstes zu tun."

