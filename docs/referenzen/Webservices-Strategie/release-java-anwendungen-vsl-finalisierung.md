# Release der Java-Anwendungen (VSL) - Finalisierung

Diese Dokumentation beschreibt den Prozess zur Finalisierung von Releases und Betas der VSL-Anwendungen. Sie ersetzt die PDF-Version und dient als kanonische Referenz.

## Inhaltsverzeichnis
1. [Vorwort](#vorwort)
2. [Abhängigkeiten](#abhängigkeiten)
3. [Relevante externe Projekte](#relevante-externe-projekte)
4. [Vorbereitung](#vorbereitung)
    - [Frühe Vorbereitung](#frühe-vorbereitung)
    - [Einen Tag vor Finalisierung](#einen-tag-vor-finalisierung)
    - [Endpoints anpassen](#endpoints-anpassen)
5. [Finalisierung](#finalisierung)
    - [Konfiguration im Applications-Repository](#konfiguration-im-applications-repository)
    - [Rechenkernprojekt](#rechenkernprojekt)
    - [Mono-Elsa](#mono-elsa)
6. [Nachbereitung](#nachbereitung)
7. [Deployment](#deployment)
8. [Rechenkerne migrieren](#rechenkerne-migrieren)
9. [Lieferscheine](#lieferscheine)
10. [Monitoring nach dem Livegang](#monitoring-nach-dem-livegang)
11. [Hinweise und Links](#hinweise-und-links)

---

## Vorwort
Unsere Java-Anwendungen werden über GitLab-CI/CD gebaut und deployed. Aktuell werden alle Anwendungen nach OpenShift deployed (vsl-ws, vsl-webui und vsl-rk). Der aktuelle produktive Rechenkern wird zusätzlich in die AWS-Cloud deployed, da wir dort mehr Kapazitäten haben und besser skalieren können.

Wir liefern drei Vertriebsanwendungen und eine Rechenkernanwendung aus:
*   **Weboberflächen:** VBON & DOL
*   **Webservices:** VBL & DOL
*   **Rechenkern:** Rechnerkernservices

*Hinweis: VBOFF wurde im Juni 2025 abgeschafft und dient nur noch Testzwecken.*

---

## Abhängigkeiten
Die korrekte Reihenfolge der Tätigkeiten ist aufgrund der Modulabhängigkeiten innerhalb des Multimodulprojekts "mono-elsa" und zum externen "rechner"-Projekt zwingend einzuhalten.

### Hierarchie der Anwendungen
1.  **Rechenkernanwendung (RK):** Basis für die Berechnungen.
2.  **Webservices (WS):** Nutzen den Rechenkern.
3.  **Weboberflächen (UI):** Nutzen die Webservices.

---

## Relevante externe Projekte
Sollten Bibliotheken in einer SNAPSHOT-Version eingebunden sein, muss zunächst ein Release durch den jeweiligen Ansprechpartner erstellt werden.

    | Projekt | Maven-Projekt | Git-Repository | Abhängigkeit in |
| :--- | :--- | :--- | :--- |
| rechenkern-win32-resources | de.vb.elsa.rechner:rechenkern-win32-resources | core/rechenkern-win32-resources | rechner, mono-elsa |
| rechner | de.vb.elsa.rechner:rechner | core/rechner | mono-elsa |
| avb-pro | de.vb.elsa.avb:avbpro | vbon/avbpro | avb-artifacts |
| avb-artifacts | de.vb.elsa.avb:avb-artifacts | avb-artifacts | mono-elsa |
| berufe-service | de.vb.elsa.db.berufe:berufe-service | core/berufskatalog/berufe-service | mono-elsa |
| berufe | de.vb.elsa.db.berufe:berufe | core/berufskatalog/berufe | mono-elsa |
| bewertungsmodul-funktionen | de.vb.pvbl:bewertungsmodul-funktionen | bewertungsmodul-funktionen | mono-elsa |
| db-bankverzeichnis | de.vb.db:db-bankverzeichnis | Artifactory | mono-elsa |
| dienst-framework | de.vb.commons:dienst-framework | core/dienst-framework | mono-elsa |
| dws.portfolio.info | de.vb.dws.portfolio.info | dws/portfolio-info-service | mono-elsa |
| eantrag-pdf-client | de.vb.eantrag:eantrag-pdf-client | eantrag-pdf-client | mono-elsa |
| elsa-db-elsa2-resources | de.vb.elsa.db:elsa-db-elsa2-resources | core/elsa-db-elsa2-resources | mono-elsa |
| elsa-db-zertifizierung | de.vb.elsa.db:elsa-db-zertifizierung | core/elsa-db-zertifizierung | mono-elsa |
| eunterschrift-wsclient | de.vb.eunterschrift:eunterschrift-wsclient | eunterschrift-wsclient | mono-elsa |
| ibanrechner | de.vb.sepa.iban:ibanrechner | iban-rechner | mono-elsa |
| outputserver | de.vb.commons:outputserver | libraries/outputserver | mono-elsa |
| printpdf | de.vb.commons:printpdf | libraries/printpdf | mono-elsa |
| priip-kid-generator | de.vb.idd.priip-kid:priip-kid-generator | priip-kid-generator | priip-kid-dokumente |
| priip-kid-dokumente-dws | de.vb.idd.priip-kid:priip-kid-dokumente-dws | priip-kid-dokumente-dws | mono-elsa |
| priip-kid-dokumente | de.vb.idd.priip-kid:priip-kid-dokumente | priip-kid-dokumente | mono-elsa |
| vsl-cos | de.vb.vsl:vsl-cos-ui-element | services/vsl-cos | mono-elsa |
| zuers-client / dto | de.vb.elsa.zuers | - | mono-elsa |

---

## Vorbereitung

### Frühe Vorbereitung
1.  **IT-Server/Cloud Infrastruktur:** Frühzeitig informieren (Schlegel, Raik oder Martin, Timo) über Lieferscheine und Deployment-Termin.
2.  **Technisches Marketing:** Info an Makler über mögliche Session-Ausfälle vorbereiten.
3.  **BAV-Netto-Tool:** Neue Version von teckpro prüfen und Deployment planen.

### Einen Tag vor Finalisierung
1.  **Vollständiger Testdurchlauf:** `clean install` mit Tests ausführen. Bei Fehlern ggf. `-fn` nutzen, aber Fehler analysieren.
2.  **Dokumentation:** Release Notes (VBL/DOL) vorbereiten und Deep Links auf Projektseiten setzen.
3.  **Freigaben einholen:**
    *   Rechenkern: Mathe-Abteilung.
    *   Mono-Elsa: Marketing / Frank Bohlmann.
4.  **Deployment-Checkliste:** Klären: Was wird deployed? (DOL? Rechenkern? Cluster?). Bei Beta werden oft nur RK und WS deployed.

### Endpoints anpassen
Die Endpunkte in Postman (Environments & Monitors/Health-Checks) und im Smoketest-Projekt anpassen.
*   **Smoketest:** `properties_Template.yaml` anpassen, Projekt taggen und Version in `.gitlab-ci.yml` von Mono-Elsa (Zeilen 101/103) sowie `smoketest_service_urls.yaml` aktualisieren.

---

## Finalisierung

### Konfiguration im Applications-Repository

Im Applications-Repository werden die Deskriptoren und Konfigurationen unserer Anwendungen für OpenShift verwaltet und angepasst. Vor jedem Deployment ist sicherzustellen, dass die Konfigurationen korrekt und aktuell sind.

#### Replicas und Speicherkapazität
*Hinweis: Bei einer Testversion oder Hotfix müssen in der Regel keine Replicas angepasst werden.*

Für jede Anwendung wird die Anzahl der "Replicas" (Instanzen/Pods) definiert. Zum Herunterfahren wird dieser Wert auf 0 gesetzt. Beim Deployment muss der gewünschte Wert geprüft und ggf. angepasst werden. Aktuelle Instanzen können über [Elastic](hier) eingesehen werden.

**Vorgehensweise:**
1.  **Applications-Repository** in IntelliJ öffnen und Branch auschecken.
    *   Beispiel Webservice: `app/vertriebssoftware/leben/mono-elsa/vsl_ws_vbl_a`
    *   Beispiel Rechenkern: `app/vertriebssoftware/leben/core/vsl_rk_vbl_a`
2.  Zu `patches/deployment.yml` für die entsprechende Stage navigieren.
    *   Pfad-Beispiel: `vertriebssoftware/leben/mono-elsa/vsl_ws_vbl_a/production/patches/deployment.yml`
3.  **Werte anpassen:**
    *   `spec.replicas`: PROD ca. 4, ITN 2-4, DEV/QA 1. Rechenkerne oft 7-20.
    *   `spec...limits.memory`: Default 2560Mi.
    *   `spec...requests.memory`: Default 2560Mi.

### Rechenkernprojekt
**WICHTIG:** Tabelle der relevanten externen Projekte und das Applications-Repository müssen vorher gecheckt worden sein! Erst starten, wenn Freigabe der Mathe-Abteilung (Sender, Heike, Phan, Linh, van de Velden, Gerrit) vorliegt.

1.  **Projekt "rechenkern-win32-resources"** finalisieren:
    *   Aufruf "Run Pipeline" in GitLab (**NICHT TAGGEN!**).
    *   Variable `MAVEN_NEW_VERSION` anlegen (z.B. `49.0.0-beta1`, NICHT `vb-release/...`).
    *   (Optional) `SOURCE_VERSION` angeben (Default: `main-SNAPSHOT`).
2.  **Projekt "rechner" (oder "rechenkern")** finalisieren:
    *   In IntelliJ auschecken, `main`-Branch, aktuellsten Stand pullen.
    *   In `rechner/pom.xml` nach `<rechenkern-win32-resources.version>` suchen.
    *   `main-SNAPSHOT` durch die oben erstellte Version (z.B. `49.0.0`) ersetzen.
    *   Lokal Maven Reimport & `clean install` ausführen.
    *   Pushen.
    *   In GitLab: **New Tag** mit `vb-release/xx.x.x` erstellen.
    *   Nach Pipeline: Deployment nach DEV und QA über GitLab Jobs (z.B. `cp:deploy-dev-vsl-rk-vbl`).
    *   **QA-Deployment:** Merge-Requests im Applications-Repository (OpenShift) auswählen und mergen. *Achtung: Nur die eigenen MRs mergen!*
    *   Integration und Production: MRs werden erstellt, hierfür Lieferscheine erstellen (siehe unten).
3.  **Rollback:** In IntelliJ den letzten Commit reverten (zurück auf `main-SNAPSHOT`) und pushen.

### Mono-Elsa
**WICHTIG:** Erst starten, wenn Gesamtfreigabe (Frank Bohlmann / Marketing) vorliegt (siehe Jira-Ticket).

1.  In IntelliJ auschecken und Branch wählen (`main` für Finalisierung, Hotfix-Branch für Hotfix).
2.  **Stamm-POM (mono-elsa/pom.xml):** Versionen aller eingebundenen externen Projekte prüfen und anpassen (siehe Liste oben). Jedes Projekt muss einzeln verifiziert werden!
3.  **Variablen anpassen in `mono-elsa/gitlab-ci-cd/variables.yml`:**
    *   `ENABLE_INSTALLSHIELD_JOB` auf `true` setzen.
    *   `VBPP_MAIN_BUILD` auf `true` setzen.
4.  Lokal Reimport & `clean install -fn` ausführen.
5.  Pushen.
6.  In GitLab: **New Tag** mit `vb-release/xx.x.x` erstellen.
7.  Nach Pipeline: Deployment nach DEV und QA.
8.  **Installshield:** Job `Starte-Installshield` erst starten, wenn Artefakte vollständig im Artifactory sind (nach `Deploy-Clients`).
9.  **Testen:** Im Finalisierungsthread (MS Teams) zum Testen aufrufen.
10. **Rollback:** Letzten Commit reverten (zurück auf `main-SNAPSHOT` / `latest-SNAPSHOT` und Variablen zurücksetzen) und pushen.

---

## Nachbereitung
Diese Schritte sollten nach der Finalisierung von mono-elsa durchgeführt werden. Es muss nicht auf das Deployment der Version gewartet werden.

1.  **Cluster-ID Switch:** Meist ist schon abzusehen, welcher Zweig (DOL/VBL) ausgeliefert wird. Cluster-ID (z.B. von "a" auf "b") tauschen.
    *   **Mono-Elsa:** In `mono-elsa/gitlab-ci-cd/variables.yml` die Werte für `VSL_CLUSTERID_VBL_CURRENTVERSION` und `VSL_CLUSTERID_DOL_CURRENTVERSION` entsprechend tauschen. (*Hinweis: PREVERSION-Variablen werden automatisch gesetzt.*)
    *   **Rechenkern:** In `rechner/gitlab-ci.yml` die Werte für `VBL_CLUSTER` und `DOL_CLUSTER` anpassen.
2.  **WS-Versionen:** Wenn die nächste Version bekannt ist, `VSL_WS_CURRENTVERSION` und `VSL_WS_PREVERSION` in `mono-elsa/gitlab-ci-cd/variables.yml` anpassen (Format: `Jahr-Monat`).
3.  **Anleitung Vorversion:** Eine ausführliche Anleitung zum Deployen einer [Vorversion](link) prüfen.

---

## Deployment
Lieferscheine in der Lieferschein-App erstellen. Dies gilt als offizieller Deployment-Auftrag an die IT-Infrastruktur.

---

## Rechenkerne migrieren
Bei Vollversionen (nicht Beta) werden alte Webservices als "Vorversion" weitergeführt. Die Rechenkerne der Vorversion müssen von AWS nach OpenShift migriert werden.

1.  **Cluster ermitteln** (VBL/DOL).
2.  **PROD-RK der Vorversion in OpenShift** hochfahren (Tag-Pipeline der Vorversion nutzen).
3.  **Applications-Repository:** In den Webservice-Branches (z.B. `vsl_ws_vbl_a`) `RK_SERVICE` und `network-policy.yml` anpassen (Umschalten zwischen AWS und OpenShift).
4.  **Webservice-Deployment:** Jobs der Vorversion starten, um Merge-Requests mit den angepassten Policies zu erzeugen.

---

## Lieferscheine
Erstellung über die Lieferschein-App (Basis: "vsl" Vorlagen).
*   **Quelle:** Link zum Merge-Request im Applications-Repository oder Docker-Image URL.
*   **Felder:** Version, Lieferdatum, Ziel (Cluster), Anlagen (Jira/Mantis), Freigaben.
*   **Sonderfall AWS Cloud:** Für RKs in der Cloud das Docker-Image aus Artifactory als Quelle angeben.
*   **Abschluss:** Übergabe an Betrieb nach allen Freigaben. Info an IT-Infrastruktur und Christian Torka (Icinga).

---

## Monitoring nach dem Livegang
*   Grafana-Dashboards prüfen (DEV/QA/INT und PROD).
*   Versionsnummern in der Dokumentation (Confluence) aktualisieren.
*   Smoketest durchführen.

---

## Hinweise und Links
*   **Encoding-Fehler:** In IntelliJ auf UTF-8 konvertieren.
*   **Mail-Vorlage:** `Z:\IT-AE\ELSA-Installation\NEUE_INSTALLATIONEN\Vorlagen\Vorlage Neue Testversion.oft`
*   **Wichtige Dashboards:**
    *   [Grafana PROD](https://vsl-dashboard.apps.ad.volkswohl-bund.de/)
    *   [Grafana DEV/QA/INT](https://vsl-dashboard.appsdev.ad.volkswohl-bund.de/)
