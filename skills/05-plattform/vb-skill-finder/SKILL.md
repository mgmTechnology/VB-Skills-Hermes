---
name: "vb-skill-finder"
description: "VB-adaptierter Skill. Ursprung: skills/find-skills/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-skill-finder

## VB-Einordnung

Plattform-Skill zur Suche und Bewertung weiterer Skills. Nützlich, wenn die vorhandene VB-Skill-Plattform erweitert werden soll.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Externe Skills dürfen erst nach Prüfung und Einordnung übernommen werden. Sie sind nicht automatisch VB-konform.

## Ursprüngliche Detailanweisung (Referenz)

Dieser Abschnitt enthält die ursprüngliche Anweisung, auf der dieser VB-Skill basiert.

---

# Skills finden

Dieser Skill hilft dir dabei, Skills aus dem offenen Agent-Skill-Ökosystem zu entdecken und zu installieren.

## Wann dieser Skill zu nutzen ist

Nutze diesen Skill, wenn der Nutzer:

- Fragt "Wie mache ich X", wobei X eine häufige Aufgabe sein könnte, für die ein Skill existiert.
- Sagt "Finde einen Skill für X" oder "Gibt es einen Skill für X?".
- Fragt "Kannst du X", wobei X eine spezialisierte Fähigkeit ist.
- Interesse daran zeigt, die Fähigkeiten des Agenten zu erweitern.
- Nach Werkzeugen, Vorlagen oder Workflows suchen möchte.
- Erwähnt, dass er Hilfe in einem spezifischen Bereich wünscht (Design, Testing, Deployment, etc.).

## Was ist das Skills CLI?

Das Skills CLI (`npx skills`) ist der Paketmanager für das offene Agent-Skill-Ökosystem. Skills sind modulare Pakete, die die Fähigkeiten von Agenten durch spezialisiertes Wissen, Workflows und Werkzeuge erweitern.

**Wichtige Befehle:**

- `npx skills find [Suchbegriff]` - Interaktive Suche nach Skills oder per Schlagwort.
- `npx skills add <Paket>` - Installiert einen Skill von GitHub oder anderen Quellen.
- `npx skills check` - Prüft auf Skill-Updates.
- `npx skills update` - Aktualisiert alle installierten Skills.

**Skills durchsuchen unter:** https://skills.sh/

## Wie man Nutzern hilft, Skills zu finden

### Schritt 1: Bedarf verstehen

Wenn ein Nutzer um Hilfe bittet, identifiziere:

1. Den Bereich (z.B. React, Testing, Design, Deployment).
2. Die spezifische Aufgabe (z.B. Tests schreiben, Animationen erstellen, PRs reviewen).
3. Ob dies eine so häufige Aufgabe ist, dass wahrscheinlich ein Skill existiert.

### Schritt 2: Zuerst das Leaderboard prüfen

Bevor du eine CLI-Suche startest, prüfe das [skills.sh Leaderboard](https://skills.sh/), um zu sehen, ob bereits ein bekannter Skill für den Bereich existiert. Das Leaderboard rankt Skills nach Gesamtzahl der Installationen und zeigt die beliebtesten Optionen an.

Zum Beispiel gehören zu den Top-Skills für Webentwicklung:
- `vercel-labs/agent-skills` — React, Next.js, Webdesign (jeweils 100K+ Installationen).
- `anthropics/skills` — Frontend-Design, Dokumentenverarbeitung (100K+ Installationen).

### Schritt 3: Nach Skills suchen

Wenn das Leaderboard den Bedarf des Nutzers nicht abdeckt, führe den Find-Befehl aus:

```bash
npx skills find [Suchbegriff]
```

Beispiele:

- Nutzer fragt "Wie mache ich meine React-App schneller?" → `npx skills find react performance`
- Nutzer fragt "Kannst du mir bei PR-Reviews helfen?" → `npx skills find pr review`
- Nutzer fragt "Ich muss ein Changelog erstellen" → `npx skills find changelog`

### Schritt 4: Qualität vor der Empfehlung prüfen

**Empfiehl keinen Skill allein basierend auf den Suchergebnissen.** Überprüfe immer:

1. **Installationszahlen** — Bevorzuge Skills mit 1K+ Installationen. Sei vorsichtig bei allem unter 100.
2. **Reputation der Quelle** — Offizielle Quellen (`vercel-labs`, `anthropics`, `microsoft`) sind vertrauenswürdiger als unbekannte Autoren.
3. **GitHub Stars** — Prüfe das Quell-Repository. Ein Skill aus einem Repo mit <100 Stars sollte mit Skepsis betrachtet werden.

### Schritt 5: Optionen dem Nutzer präsentieren

Wenn du relevante Skills findest, präsentiere sie dem Nutzer mit:

1. Dem Skill-Namen und dessen Funktion.
2. Der Anzahl der Installationen und der Quelle.
3. Dem Installationsbefehl, den er ausführen kann.
4. Einem Link zu skills.sh für weitere Informationen.

Beispiel-Antwort:

```
Ich habe einen Skill gefunden, der helfen könnte! Der "react-best-practices" Skill bietet
Richtlinien zur Performance-Optimierung für React und Next.js von Vercel Engineering.
(185K Installationen)

Zur Installation:
npx skills add vercel-labs/agent-skills@react-best-practices

Mehr erfahren: https://skills.sh/vercel-labs/agent-skills/react-best-practices
```

### Schritt 6: Installation anbieten

Wenn der Nutzer fortfahren möchte, kannst du den Skill für ihn installieren:

```bash
npx skills add <owner/repo@skill> -g -y
```

Das Flag `-g` installiert global (Benutzerebene) und `-y` überspringt Bestätigungsaufforderungen.

## Gängige Skill-Kategorien

Berücksichtige bei der Suche diese gängigen Kategorien:

| Kategorie       | Beispiel-Abfragen                         |
| --------------- | ----------------------------------------- |
| Webentwicklung  | react, nextjs, typescript, css, tailwind  |
| Testing         | testing, jest, playwright, e2e            |
| DevOps          | deploy, docker, kubernetes, ci-cd         |
| Dokumentation   | docs, readme, changelog, api-docs         |
| Code-Qualität   | review, lint, refactor, best-practices    |
| Design          | ui, ux, design-system, accessibility      |
| Produktivität   | workflow, automation, git                 |

## Tipps für effektive Suchen

1. **Nutze spezifische Schlagworte**: "react testing" ist besser als nur "testing".
2. **Probiere alternative Begriffe**: Wenn "deploy" nicht funktioniert, versuche "deployment" oder "ci-cd".
3. **Prüfe populäre Quellen**: Viele Skills stammen von `vercel-labs/agent-skills` oder `ComposioHQ/awesome-claude-skills`.

## Wenn keine Skills gefunden werden

Wenn keine relevanten Skills existieren:

1. Bestätige, dass kein passender Skill gefunden wurde.
2. Biete an, bei der Aufgabe direkt mit deinen allgemeinen Fähigkeiten zu helfen.
3. Schlage vor, dass der Nutzer mit `npx skills init` einen eigenen Skill erstellen kann.

Beispiel:

```
Ich habe nach Skills für "xyz" gesucht, aber keine Treffer gefunden.
Ich kann dir dennoch direkt bei dieser Aufgabe helfen! Soll ich fortfahren?

Falls du dies öfter tust, könntest du einen eigenen Skill erstellen:
npx skills init mein-xyz-skill
```

