---
name: vb-architektur-randbedingungen
description: VB-Architektur Rand- und Rahmenbedingungen nach Confluence (v34, Maerz 2026). Vollstaendiger Katalog aller VB-Architekturvorgaben.
---

# VB-Architektur: Rand- und Rahmenbedingungen

Vollstaendiger Ueberblick ueber die aktuell beim Volkswohl Bund angewendeten Rand- und Rahmenbedingungen (Stand: Maerz 2026, v34).

## 1. Gesetze und Normen

### Gesetze
| Gesetz | Gueltigkeit | Beschreibung |
|---|---|---|
| DSGVO | EU | Regeln zur Verarbeitung personenbezogener Daten |
| DORA | EU | Digital Operational Resilience Act, ersetzt seit 17.1.2025 VAIT |

### Normen
| Norm | Kategorie | Beschreibung |
|---|---|---|
| ISO/IEC/IEEE 42010 | Architekturbeschreibung | Strukturierung und Kommunikation von Systemarchitekturen |
| ISO/IEC 25010 | Softwarequalitaet | Definition und Bewertung von Softwarequalitaetsanforderungen |
| ISO 12207 | Softwarelebenszyklus | Prozesse waehrend des gesamten Software-Lebenszyklus |

## 2. Projektteam und Organisation

### Projektteam
- Fachabteilung: Wechsel der Verantwortlichkeiten? Projektbeteiligte?
- Entwicklerteam: Wechsel voraussehbar (z.B. PASTA)? Abgaenge planbar (Renteneintritt)?
- Intern/extern: Wird das Projekt intern oder extern realisiert? Gemischte Teams?
- Projektsteuerung: Interne oder externe Projektleitung/Beratung?

### Organisatorische Randbedingungen
- **Trennung Entwicklung und Betrieb**: DevOps-Ansaeze nicht vollstaendig umsetzbar. Deployments, neue DBs erfordern Koordination mit IT-Betrieb
- **Vorgehensmodelle**: Wasserfall (Solo, Klassisch), Scrum, VBLife

### Ressourcen
- Aufwandsschaetzung, Fixer Endtermin, Termin vs. Funktionsumfang
- Release-Planung, Budget fuer Technik
- Team: Anzahl, Qualifikation, Motivation, Verfuegbarkeit

### Revision und Nachweispflichten
- Nachvollziehbarkeit: Wer hat einen Datensatz geaendert?
- Welcher Dienst hat auf welchen Dienst Zugriff?

## 3. Technik - Betrieb

### Authentifizierung & Autorisierung
| Implementierung | Beschreibung | Beispiel |
|---|---|---|
| CAS | Central Authentication Service (intern/extern) | — |
| Keycloak | Open-Source IAM | VBLife |
| ZBBV | Zentrale Benutzer- und Berechtigungsverwaltung | — |

### Datenbanken
| Datenbank | Hersteller | Beispiel |
|---|---|---|
| IBM DB2 | IBM | LOS |
| Microsoft SQL Server | Microsoft | VBLife |

### Kommunikation / Messaging
| Protokoll | Beispiel |
|---|---|
| MQSeries | Zusy |
| RabbitMQ | VBLife |

### Plattformen
| Plattform | Typ | Beispiel |
|---|---|---|
| Amazon Cloud | Cloud | VBON-Tarifrechner |
| JBoss (Jaas) | On-Premise | BiPRO-Auth |
| Jetty | On-Premise | Antragsvorerfassung VBS |
| Kubernetes (k8s) | On-Premise | AVIS Massenaenderungen |
| OpenShift | On-Premise | QR-Code-Webservice |
| IBM z/OS | On-Premise | ASS, VO, LOS |

### Protokolle
AMQP, FTP, HTTP, HTTPS, IMAP, LDAP, OAuth2/OpenID Connect, SFTP, SOAP

## 4. Technik - Entwicklung

### APIs
OAuth, OpenAPI, REST

### Backend-Bibliotheken
Apache Commons, ArchUnit, Feign, H2, Hibernate, Jackson, joda-time, JUnit, logback, logstash, micrometer, mockito, RabbitMQ, slf4j, Spring, Spring-Boot, Spring-Cloud, Spring/Rabbit AMQP, springdoc-openapi, swagger, TestNG, Zalando Problem, Hamcrest, db2jcc, HikariCP, AspectJ, JavaMail

### Frontend-Bibliotheken
JSF (Prokundo), Angular (VBLife), Primefaces (VBON), Vaadin (Sascha), OpenAPI-Generator (VBLife), jQuery

### Build-Server
GitLab

### Entwicklungsumgebungen / Editoren
| IDE | Hersteller | Beschreibung |
|---|---|---|
| IDz | IBM | IBM Developer for z/OS |
| IntelliJ | Jetbrains | Desktop-Entwicklungsumgebung |
| MPS | Jetbrains | DSL-Entwicklung |
| QUICK3270 | DN-Computing | Terminal-Emulation Grossrechner |
| Micro Focus Net-Express | OpenText | Cobol Runtimes (abgekuendigt) |
| VS Code | Microsoft | Desktop-Entwicklungsumgebung |
| Eclipse | Eclipse Foundation | Desktop-Entwicklungsumgebung |

### Programmiersprachen
Cobol, Java

### Programmierkonventionen
VB-Programmierrichtlinie

### Entwicklungswerkzeuge
RenovateBot, GitLab

## 5. Test-Management

### Testwerkzeuge
| Werkzeug | Beschreibung | Beispiel |
|---|---|---|
| JUnit | Test-Framework | Prokundo |
| ReadyAPI | API-Testing | VBLife |
| TestNG | Test-Framework | VBLife |
| Cypress | E2E-Test-Framework | Pasta |
| Playwright | E2E-Test-Framework | VBLife |

### Testprozesse
Blackbox-Test (VBON), Manueller Test (LOS), Massentest (Arbeitslauf 1), Regressionstest (Arbeitslauf 1), Unit-Test (VBLife), Paralleltest (VO)

---

*Quelle: Confluence - Rand- und Rahmenbedingungen einer VB-Software-Architektur (v34, Maerz 2026)*
*Letzte Autoren: Andreas Engelbert, Marc Weidensee, Christian Koppen, Kevin Schaefer, Georg Machner, Daniel Freudenreich*