---
name: vb-architektur-randbedingungen
description: VB-Architektur Rand- und Rahmenbedingungen nach Confluence (v34, März 2026). Vollständiger Katalog aller VB-Architekturvorgaben.
---

# VB-Architektur: Rand- und Rahmenbedingungen

## Ziel
Vollständiger Überblick über die aktuell beim Volkswohl Bund angewendeten Rand- und Rahmenbedingungen für Software-Architekturen. Verwenden, wenn Architekturentscheidungen getroffen oder Architekturdokumentationen erstellt werden.

## Vorgehen
- Vor jeder Architekturarbeit diese Randbedingungen laden und prüfen.
- Bei Architekturentscheidungen die relevanten Kategorien aus diesem Katalog berücksichtigen.

### Zu prüfende Kategorien

**Gesetze und Normen:** DSGVO (EU), DORA (EU), ISO/IEC/IEEE 42010, ISO/IEC 25010, ISO 12207.

**Projektteam und Organisation:**
- Fachabteilung: Verantwortlichkeiten, Projektbeteiligte.
- Entwicklerteam: Wechsel voraussehbar? Abgänge planbar? Intern/extern? Gemischte Teams?
- Projektsteuerung: Interne oder externe Projektleitung/Beratung?
- Trennung Entwicklung und Betrieb: DevOps-Ansätze nicht vollständig umsetzbar.
- Vorgehensmodelle: Wasserfall (Solo, Klassisch), Scrum, VBLife.
- Revision und Nachweispflichten: Wer hat Datensatz geändert? Welcher Dienst hat Zugriff?

**Technik — Betrieb:**
- Authentifizierung: CAS, Keycloak, ZBBV.
- Datenbanken: IBM DB2 (LOS), Microsoft SQL Server (VBLife).
- Messaging: MQSeries, RabbitMQ.
- Plattformen: Amazon Cloud, JBoss, Jetty, Kubernetes, OpenShift, IBM z/OS.
- Protokolle: AMQP, FTP, HTTP, HTTPS, IMAP, LDAP, OAuth2/OpenID Connect, SFTP, SOAP.

**Technik — Entwicklung:**
- APIs: OAuth, OpenAPI, REST.
- Backend: Spring, Spring-Boot, Spring-Cloud, Hibernate, JUnit, TestNG u.a.
- Frontend: JSF (Prokundo), Angular (VBLife), Primefaces (VBON), Vaadin (Sascha).
- Build-Server: GitLab.
- Entwicklungsumgebungen: IDz, IntelliJ, VS Code, Eclipse u.a.
- Programmiersprachen: Cobol, Java.

**Test-Management:** JUnit, ReadyAPI, TestNG, Cypress, Playwright; Blackbox-Test, Manueller Test, Massentest, Regressionstest, Unit-Test, Paralleltest.

## Regeln / Qualitätskriterien
- Keine Architekturentscheidung ohne Prüfung dieser Randbedingungen.
- Immer die aktuellste Version (v34, März 2026) verwenden.
- Bei Abweichungen: Begründung dokumentieren.

## Ressourcen
- Confluence — Rand- und Rahmenbedingungen einer VB-Software-Architektur (v34, März 2026)

*Quelle: Confluence · Autoren: Andreas Engelbert, Marc Weidensee, Christian Koppen, Kevin Schaefer, Georg Machner, Daniel Freudenreich*