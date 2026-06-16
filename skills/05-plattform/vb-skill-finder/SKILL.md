---
name: vb-skill-finder
description: Sucht und bewertet Skills aus dem offenen Agent-Skill-Ökosystem — Entdecken und Installieren über das Skills CLI.
---

# vb-skill-finder

## Ziel
Plattform-Skill zur Suche und Bewertung weiterer Skills aus dem offenen Agent-Skill-Ökosystem. Nützlich, wenn die vorhandene VB-Skill-Plattform erweitert werden soll. Externe Skills dürfen erst nach Prüfung und Einordnung übernommen werden — sie sind nicht automatisch VB-konform.

## Vorgehen

### Schritt 1: Bedarf verstehen
- Identifiziere Bereich (z. B. React, Testing, Design, Deployment), spezifische Aufgabe und ob ein Skill wahrscheinlich existiert.

### Schritt 2: Leaderboard prüfen
- Prüfe [skills.sh Leaderboard](https://skills.sh/) auf bereits bekannte Skills für den Bereich.

### Schritt 3: Skills CLI verwenden
- Suche mit `npx skills find [Suchbegriff]`.
- Installiere mit `npx skills add <Paket> -g -y`.
- Prüfe Updates mit `npx skills check` und `npx skills update`.

### Schritt 4: Qualität vor Empfehlung prüfen
- Bevorzuge Skills mit 1K+ Installationen.
- Bevorzuge offizielle Quellen (`vercel-labs`, `anthropics`, `microsoft`).
- Prüfe GitHub Stars des Quell-Repositories (<100 Stars skeptisch sein).

### Schritt 5: Optionen präsentieren
- Skill-Name mit Funktion, Installationszahlen, Quelle, Installationsbefehl und Link zu skills.sh.

### Schritt 6: Installation anbieten
- `npx skills add <owner/repo@skill> -g -y` für globale Installation.

## Regeln / Qualitätskriterien
- Keinen Skill allein basierend auf Suchergebnissen empfehlen — immer Qualitätsprüfung.
- Installationszahlen und Reputation der Quelle einbeziehen.
- Bei keinen Treffern: bestätigen, direkte Hilfe anbieten, auf `npx skills init` zur Skill-Erstellung verweisen.
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen explizite Nutzerbestätigung einholen.
- Externe Skills erst nach Prüfung und Einordnung übernehmen.

## Ressourcen
- Skill-Entwickler: vb-skill-entwickler
- Skill-Katalog: vb-skill-katalog
- Skill-Review: vb-skill-review