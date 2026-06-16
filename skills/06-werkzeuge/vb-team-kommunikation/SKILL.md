---
name: "vb-team-kommunikation"
description: "VB-adaptierter Skill. Ursprung: skills/project-management/team-communications/SKILL.md. Siehe VB-Kontext und Abgrenzung."
---

# vb-team-kommunikation

## VB-Einordnung

Methoden-Skill für interne Kommunikation, Statusberichte, Updates und FAQ-Texte.

## Abgrenzung

Dieser Skill ist in die VB-Skill-Struktur übernommen, aber nicht jede Aussage aus dem Ursprungsskill ist automatisch ein VB-Standard.

Wenn der Ursprungsskill konkrete Produkte, Frameworks, Cloud-Dienste, Kommandos oder Toolketten nennt, gelten diese nur dann als verbindlich, wenn sie im Projektkontext bestätigt sind oder in `docs/referenzen/standards-mapping.md` als VB-Rahmenbedingung aufgeführt sind.

Vor schreibenden, löschenden, produktiven oder administrativen Aktionen ist eine explizite Bestätigung des Nutzers erforderlich.

VB-Hinweis: Dieser Skill ist als Methoden-/Werkzeugskill eingeordnet und keine neue VB-Projektrolle.

## Ursprüngliche Detailanweisung (Referenz)

---

# Interne Kommunikation

Erstellt professionelle interne Kommunikation durch Laden der richtigen Referenzdatei, Sammeln von Kontext und Ausgabe im exakten Format des Unternehmens.

## Routing

Identifiziere den Kommunikationstyp aus der Anfrage des Nutzers und lies die passende Referenzdatei, bevor du etwas schreibst:

| Typ | Trigger-Phrasen | Referenzdatei |
|---|---|---|
| **3P-Update** | "3P", "progress plans problems", "wöchentliches Team-Update", "was haben wir geliefert" | `references/3p-updates.md` |
| **Newsletter** | "Newsletter", "Unternehmens-Update", "wöchentlicher/monatlicher Rückblick", "Zusammenfassung All-Hands" | `references/company-newsletter.md` |
| **FAQ** | "FAQ", "häufige Fragen", "was Leute fragen", "Unklarheiten bei" | `references/faq-answers.md` |
| **Allgemein** | alles Interne, was oben nicht passt | `references/general-comms.md` |

Falls der Typ unklar ist, stelle eine klärende Rückfrage — rate nicht.

## Workflow

1. **Referenzdatei lesen** für den ermittelten Typ. Halte dich exakt an deren Formatierung.
2. **Inputs sammeln.** Nutze verfügbare MCP-Werkzeuge (Slack, Gmail, Google Drive, Kalender), um echte Daten abzurufen. Falls keine Werkzeuge verbunden sind, bitte den Nutzer um Stichpunkte oder Roh-Kontext.
3. **Umfang klären.** Bestätige: Teamname (für 3Ps), Zeitraum, Zielgruppe und spezifische Punkte, die ein- oder ausgeschlossen werden sollen.
4. **Entwurf erstellen.** Folge präzise dem Format, Tonfall und den Längenbeschränkungen der Referenzdatei. Erfinde kein neues Format.
5. **Entwurf präsentieren** und fragen, ob etwas hinzugefügt, entfernt oder umformuliert werden muss.

## Tonfall & Stil (gilt für alle Typen)

- Nutze "wir" — du bist Teil des Unternehmens.
- Aktiv formulieren: Präsens für Fortschritt, Futur für Pläne.
- Prägnant. Jeder Satz sollte Informationen enthalten. Füllwörter streichen.
- Metriken und Links einbeziehen, wo immer möglich.
- Professionell, aber nahbar — kein unverständliches "Corporate Speak".
- Die wichtigsten Informationen zuerst.

## Wenn Werkzeuge nicht verfügbar sind

Falls der Nutzer Slack, Gmail, Drive oder Kalender nicht verbunden hat, halte den Prozess nicht auf. Bitte ihn, die Inhalte einzufügen oder zu beschreiben. Deine Aufgabe ist das Formatieren und Schärfen — das ist bereits wertvoll. Erwähne, welche Werkzeuge künftige Entwürfe verbessern würden, damit er sie später verbinden kann.

---

## Anti-Muster

| Anti-Muster | Warum es scheitert | Besserer Ansatz |
|---|---|---|
| Updates schreiben, ohne zuerst die Vorlage zu lesen | Ausgabe passt nicht zum Format des Unternehmens — Nutzer muss nacharbeit | Immer die passende Referenzdatei vor dem Entwurf laden |
| Metriken oder Erfolge erfinden | Interne Kommunikation muss faktisch sein — Erfindungen zerstören Vertrauen | Nur Daten einbeziehen, die der Nutzer geliefert oder die MCP-Tools abgerufen haben |
| Passiv für Erfolge nutzen | "Das Feature wurde geliefert" verbirgt, wer die Arbeit gemacht hat | "Team X hat das Feature geliefert" — Aktiv schreibt dem Team den Erfolg zu |
| Textwüsten für Status-Updates schreiben | Management scannt Texte nur, liest sie nicht — Kerninfos gehen verloren | Mit der Schlagzeile beginnen, gefolgt von 3–5 Stichpunkten |
| Senden, ohne die Zielgruppe zu bestätigen | Ein Team-Update liest sich anders als ein unternehmensweiter Newsletter | Immer bestätigen: Wer wird das lesen? |

---

## Verwandte Skills

| Skill | Beziehung |
|-------|-------------|
| `project-management/senior-pm` | Breiterer PM-Fokus — Statusberichte fließen in das PM-Reporting ein |
| `project-management/meeting-analyzer` | Meeting-Erkenntnisse können in 3P-Updates und Statusberichte einfließen |
| `project-management/confluence-expert` | Veröffentlicht Kommunikation als Confluence-Seiten für die dauerhafte Ablage |
| `marketing-skill/content-production` | Externe Kommunikation — für öffentliche Inhalte nutzen, nicht intern |

