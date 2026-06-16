# VB Skill-Plattform — Gesamtdokumentation

**Stand:** 15.06.2026  
**Verantwortlich:** Marc, Webservices & Strategie, IT-AE Lebensversicherungen

---

## 1. Architektur

### Drei-Schichten-Modell

```
┌─────────────────────────────────────────────┐
│  SCHICHT 1: Memory (immer aktiv, 0 Token)    │
│  Wer bist du, Tech-Stack, Projekt-Pfade      │
├─────────────────────────────────────────────┤
│  SCHICHT 2: vb-lotse (~3 KB)                 │
│  Router: kennt alle Skills, lädt keinen       │
├─────────────────────────────────────────────┤
│  SCHICHT 3: Fach-Skills (bei Bedarf)          │
│  Nur 1-3 Skills geladen, ~5-30 KB            │
└─────────────────────────────────────────────┘
```

### Token-Strategie

| Ansatz | Token |
|---|---|
| Alle 76 Skills laden | ~360 KB (unmöglich) |
| Lotse + 1-3 Fach-Skills | ~8-35 KB (produktiv) |
| **Ersparnis** | **90-95%** |

---

## 2. Skill-Katalog (76 Skills)

### 00-prozess — Prozess-Steuerung (14 Skills)

Diese Skills steuern den VB-Entwicklungsprozess von der Idee bis zur Abnahme.

| Skill | Größe | Funktion |
|---|---|---|
| `vb-lotse` | 6 KB | Zentraler Router, empfiehlt Skill-Kette |
| `vb-analyse` | 1.5 KB | Fachliche Analyse eines Systems |
| `vb-anforderungen` | 1.3 KB | User Stories und Anforderungsspezifikation |
| `vb-architektur` | 0.2 KB | Architekturentscheidungen treffen |
| `vb-architekturprozess` | 1.3 KB | Architekturprozess nach VB-Standard |
| `vb-dokumentation` | 1.3 KB | Technische Dokumentation erstellen |
| `vb-feature-spezifikation` | 9.9 KB | Feature-Spec mit API-Verträgen |
| `vb-klickjourney-test` | 0.4 KB | Playwright-UI-Tests |
| `vb-projekt-initialisierung` | 8.2 KB | Neues Projekt strukturiert aufsetzen |
| `vb-qualitaetspruefung` | 0.2 KB | Qualitätsprüfung nach VB-Standards |
| `vb-review` | 1.2 KB | Code- und Dokumenten-Review |
| `vb-spezifikation-verfeinern` | 6.9 KB | Spezifikation präzisieren |
| `vb-test` | 1.3 KB | Teststrategie definieren |
| `vb-umsetzung` | 1.2 KB | Implementierung nach VB-Standards |

### 01-rollen — VB Projektmanagement-Handbuch (17 Rollen)

Alle Rollen aus dem offiziellen VB PM-Handbuch. Jeder Skill ~1.5 KB.

| Skill | Rolle |
|---|---|
| `vb-projektleitung` | Projektleitung |
| `vb-fachbereichskoordinator` | Fachbereichskoordinator |
| `vb-anforderungsmanager` | Anforderungsmanager |
| `vb-fachexperte` | Fachexperte |
| `vb-business-analyst` | Business Analyst |
| `vb-it-ae-koordinator` | IT-AE Koordinator |
| `vb-it-ae-architekt` | IT-AE Architekt |
| `vb-it-ae-entwickler` | IT-AE Entwickler |
| `vb-it-ae-testautomatisierer` | IT-AE Testautomatisierer |
| `vb-testmanager` | Testmanager |
| `vb-fehlermanager` | Fehlermanager |
| `vb-testdatenmanager` | Testdatenmanager |
| `vb-tester-fachabteilung` | Tester Fachabteilung |
| `vb-tester-it-betrieb` | Tester IT-Betrieb |
| `vb-mpm` | Multi-Projekt-Management |
| `vb-sonderfunktion` | Sonderfunktion |
| `vb-priorunde-vorbereitung` | Priorunde |
| `vb-lenkungsausschuss-vorbereitung` | Lenkungsausschuss |

### 02-technik — Webservices & Strategie (6 Skills)

Fachspezifische Skills für die Gruppe Webservices & Strategie.

| Skill | Größe | Funktion |
|---|---|---|
| `vb-bipro-analysis` | 6.3 KB | BiPRO fachlich-technisch analysieren |
| `vb-onboarding-webservices` | 5.4 KB | Einarbeitungsplan neue Entwickler |
| `vb-release-finalization` | 12.6 KB | Release-Finalisierung VSL/mono-elsa |
| `vb-release-planning` | 20.2 KB | Release-Planung mit NRW-Kalenderlogik |
| `vb-webservice-diagnostics` | 5.6 KB | Produktionsfehler VBL/DOL diagnostizieren |
| `vb-webservice-documentation` | 5.0 KB | Technische Webservice-Dokumentation |

### 02-technik — Allgemein (11 Skills)

| Skill | Größe | Funktion |
|---|---|---|
| `vb-api-design` | 1.3 KB | REST-API-Design |
| `vb-backend-webapp` | 5.8 KB | Backend-Webanwendung |
| `vb-code-review` | 8.9 KB | Code-Review nach VB-Standards |
| `vb-datenmodell` | 1.3 KB | Datenmodellierung |
| `vb-deployment` | 6.3 KB | Deployment nach VB-Prozess |
| `vb-devops` | 1.3 KB | DevOps-Praktiken |
| `vb-frontend-webapp` | 5.6 KB | Frontend-Webanwendung |
| `vb-java-springboot` | 1.3 KB | Java/Spring Boot |
| `vb-playwright-klickjourneys` | 18.0 KB | Playwright E2E-Tests |
| `vb-qa-engineering` | 8.9 KB | Qualitätssicherung |
| `vb-solution-architecture` | 6.4 KB | Lösungsarchitektur |
| `vb-testautomatisierung` | 1.3 KB | Testautomatisierung |
| `vb-webservices` | 1.3 KB | Webservice-Entwicklung |

### 03-governance (6 Skills)

| Skill | Größe | Funktion |
|---|---|---|
| `vb-anonymisierung` | 16.9 KB | Personenbezogene Daten anonymisieren |
| `vb-dsgvo-pruefung` | 1.3 KB | DSGVO-Prüfung |
| `vb-revision` | 1.3 KB | Revisionsanforderungen |
| `vb-security-standards-import` | 15.0 KB | Sicherheitsstandards importieren |
| `vb-sicherheitspruefung` | 1.3 KB | Sicherheitsprüfung |
| `vb-testdaten-governance` | 1.3 KB | Testdaten-Governance |

### 04-standards (4 Skills)

| Skill | Größe | Funktion |
|---|---|---|
| `vb-architekturleitlinien` | 1.4 KB | VB-Architekturleitlinien |
| `vb-loesungscheck` | 1.4 KB | Lösung gegen VB-Standards prüfen |
| `vb-technologiestandards` | 1.4 KB | VB-Technologiestandards |
| `vb-teststandards` | 1.4 KB | VB-Teststandards |

### 05-plattform (6 Skills)

| Skill | Größe | Funktion |
|---|---|---|
| `vb-devscouts-evaluation` | 5.1 KB | KI-Tool-Evaluation |
| `vb-hilfe` | 5.7 KB | Hilfe zur Skill-Plattform |
| `vb-skill-entwickler` | 1.1 KB | Neue Skills entwickeln |
| `vb-skill-finder` | 7.0 KB | Passenden Skill finden |
| `vb-skill-katalog` | 1.0 KB | Skill-Katalog pflegen |
| `vb-skill-review` | 1.1 KB | Skill-Review |

### 06-werkzeuge (9 Skills)

| Skill | Größe | Funktion |
|---|---|---|
| `vb-atlassian-admin` | 15.2 KB | Atlassian-Administration |
| `vb-atlassian-templates` | 12.5 KB | Atlassian-Vorlagen |
| `vb-confluence-experte` | 11.7 KB | Confluence-Dokumentation |
| `vb-jira-experte` | 11.6 KB | Jira (JQL, Workflows, Dashboards) |
| `vb-lean-six-sigma-black-belt` | 7.3 KB | Lean Six Sigma (DMAIC) |
| `vb-meeting-analyzer` | 14.5 KB | Meeting-Analyse |
| `vb-scrum-master` | 11.3 KB | Scrum Master |
| `vb-senior-pm` | 19.3 KB | Senior Projektmanagement |
| `vb-team-kommunikation` | 5.1 KB | Team-Kommunikation |

---

## 3. Erweiterte Skills (Hermes-eigene)

Diese Skills sind in Hermes installiert, nicht im ZIP enthalten:

| Skill | Größe | Funktion |
|---|---|---|
| `marc-vb-profile` | ~3 KB | Persönliches Profil (automatisch per Memory) |
| `bipro-taa-leben-webservice` | ~8 KB | Konsolidierte BiPRO TAA Leben Referenz |
| `bipro-taa-leben-einarbeitung` | ~5 KB | 6-Wochen Einarbeitungsplan (detailliert) |
| `vb-skill-befueller` | ~4 KB | Hilft Fachabteilungen beim Befüllen von Skills |

---

## 4. Nutzung

### Täglicher Workflow

```
Nutzer: "Ich muss einen Release planen"
    ↓
Hermes lädt vb-lotse (~3 KB)
    ↓
Lotse: "Empfehle vb-release-planning (NRW-Kalenderlogik)"
    ↓
Nutzer: "Ja, laden"
    ↓
Hermes lädt vb-release-planning (~20 KB)
    ↓
Nutzer bekommt Release-Plan mit Feiertagsprüfung
```

**Token-Verbrauch: ~23 KB von ~360 KB möglichen.**

### Für Fachabteilungen: Skills befüllen

```
Nutzer: "Hilf mir, den Testprozess zu dokumentieren"
    ↓
Hermes lädt vb-skill-befueller (~4 KB)
    ↓
Befüller: Strukturiertes Interview (9 Fragen)
    ↓
SKILL.md-Entwurf mit VB-Verfahrensanweisungen
    ↓
Review durch Wissensträger
    ↓
Fertiger Skill im Katalog
```

### Hermes-Integration

```
# Lotse laden
skill_view(name='vb-lotse')

# Fach-Skill laden (nach Lotse-Empfehlung)
skill_view(name='vb-release-planning')

# Skill-Befüller für Fachabteilungen
skill_view(name='vb-skill-befueller')
```

---

## 5. Erstellungsprozess

Diese Plattform wurde am 15.06.2026 in einer Hermes-Session mit Marc aufgebaut:

1. **Analyse:** Alle *.md Dateien in `C:\Dev\Github\biprototal` gelesen
2. **Profil:** `marc-vb-profile` mit persönlichem Kontext, Tech-Stack, Arbeitsweise
3. **Fach-Skills:** `bipro-taa-leben-webservice` und `bipro-taa-leben-einarbeitung` aus Gesamtdokumentation v3
4. **Methodik:** `vb-lean-six-sigma-black-belt` und `vb-jira-experte` installiert
5. **Plattform:** `vb-lotse` (Router) und `vb-skill-befueller` (für Fachabteilungen)
6. **ZIP-Extraktion:** 70 Skills aus dem ursprünglichen skills.zip
7. **Live-Test:** Lotse → Einarbeitungsplan erfolgreich geroutet

---

## 6. Verzeichnisstruktur

```
C:\Dev\Github\VB Lotse\
├── README.md                    ← Kurzübersicht
├── DOKUMENTATION.md             ← diese Datei (vollständig)
├── vb-lotse\
│   └── SKILL.md                 ← Der Router
├── vb-skill-befueller\
│   └── SKILL.md                 ← Skill-Befüller für Fachabteilungen
└── skills\                      ← 70 Skills aus ZIP
    ├── 00-prozess\              (14 Skills)
    ├── 01-rollen\               (17 Skills)
    ├── 02-technik\              (17 Skills)
    ├── 03-governance\           (6 Skills)
    ├── 04-standards\            (4 Skills)
    ├── 05-plattform\            (6 Skills)
    └── 06-werkzeuge\            (9 Skills)
```

### Zusätzlich in Hermes installiert

```
C:\Users\Marc\AppData\Local\hermes\skills\
├── vb-lotse\
├── vb-skill-befueller\
├── user-profile\marc-vb-profile\
├── bipro\bipro-taa-leben-webservice\
├── bipro\bipro-taa-leben-einarbeitung\
├── methodology\vb-lean-six-sigma-black-belt\
└── project-management\vb-jira-experte\
```

---

## 7. Referenzdokumente (im biprototal-Repo)

Diese Dokumente bilden die fachliche Grundlage vieler Skills:

| Dokument | Pfad |
|---|---|
| Entwicklerhandbuch (33 Kap.) | `C:\Dev\Github\biprototal\docs\entwicklerhandbuch.md` |
| Umsetzungsplan (Phasen 1-5) | `C:\Dev\Github\biprototal\docs\process.md` |
| Skill-Generator Spezifikation | `C:\Dev\Github\biprototal\docs\spezifikation_skillgenerator_v1.0.md` |
| Skill-Generator Architektur | `C:\Dev\Github\biprototal\docs\architektur_skillgenerator_v1.0.md` |
| Feature-Spec WS-Doku MVP | `C:\Dev\Github\biprototal\docs\featurespec_skillgenerator_wsdoku_mvp_v1.0.md` |
| Anonymisierungs-Spec | `C:\Dev\Github\biprototal\docs\anonymisierung_skillgenerator_wsdoku_v1.0.md` |
| BiPRO Gesamtdokumentation v3 | `C:\Dev\Github\biprototal\docs\Webservice-Dokumentation\v3\` |
| VB-Technologiestandards | `C:\Dev\Github\biprototal\reference\standards-mapping.md` |
| VB-Rollen-Mapping | `C:\Dev\Github\biprototal\reference\rollen-mapping.md` |

---

## 8. Nächste Schritte

1. [ ] **Skill-Generator MVP** aus biprototal umsetzen (WS-Doku → "Als Skill sichern")
2. [ ] **Ersten Fachbereich-Skill befüllen** mit vb-skill-befueller (z.B. Testmanager)
3. [ ] **Lotse erweitern** wenn neue Skills entstehen
4. [ ] **Hermes cronjob** für regelmäßige Skill-Aktualisierung prüfen
5. [ ] **Playwright-Klickjourneys** für BiPRO Total UI-Tests

---

*Erstellt mit Hermes Agent am 15.06.2026*
*Modell: deepseek-v4-pro · Host: Windows 10 · Projekt: VB Lotse*
