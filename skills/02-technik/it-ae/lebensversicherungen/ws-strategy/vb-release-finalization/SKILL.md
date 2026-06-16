# vb-release-finalization

## Zweck
Unterstützt die Finalisierung eines Releases der Java-Anwendungen im VSL-/mono-elsa-Kontext. Der Skill führt durch Vorbereitung, externe Projektabhängigkeiten, Endpoint-Anpassungen, Applications-Repository, Rechenkern-Finalisierung, mono-elsa-Finalisierung, Nachbereitung, Deployment, Rechenkernmigration, Lieferscheine und Monitoring nach Livegang.

## Wann verwenden
- Finalisierung einer Vollversion oder Beta der Java-Anwendungen.
- Vorbereitung eines VSL-/mono-elsa-Releases.
- Prüfung externer SNAPSHOT-/Beta-/Release-Abhängigkeiten.
- Erstellung einer Release-Checkliste oder eines Ablaufplans.
- Vorbereitung von Lieferscheinen und Deployment-Aufträgen.
- Migration von Rechenkernen bzw. Cluster-/Vorversionswechsel.

## Wann NICHT verwenden
- Fachliche BiPRO-Analyse; dafür `vb-bipro-analysis`.
- Webservice-Fehlerdiagnose; dafür `vb-webservice-diagnostics`.
- Allgemeine Projektplanung ohne Release-Kontext.


## Verbindliche Referenzen
Nutze bei Bedarf diese lokalen Referenzen im Repository:

- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Gesamtdokumentation_v3.html`
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Einarbeitungsplan.html`
- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf`
- `docs/referenzen/Webservices-Strategie/REFERENZEN.md`

Regel: Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`. Erfinde keine VB-Standards.


## Primärreferenz
- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf`

## Grundannahmen aus der Referenz
- Java-Anwendungen werden über GitLab CI/CD gebaut und deployed.
- Aktuell werden `vsl-ws`, `vsl-webui` und `vsl-rk` nach OpenShift deployed.
- Der produktive Rechenkern wird zusätzlich in AWS deployed, um Kapazität und Skalierung zu nutzen.
- Relevante Vertriebsanwendungen: Webservices, Weboberflächen und historisch VBOFF.
- Die Anleitung unterscheidet Vollversion und Beta; Unterschiede sind zu prüfen.

## Benötigte Eingaben
- Release-Typ: Beta, Vollversion, Hotfix, Testversion.
- Zielversion und Vorgängerversion.
- betroffene Anwendungen: VBL, DOL, Webservice, WebUI, Rechenkern.
- Zielumgebungen: DEV, QA, Integration, PROD.
- Cluster: `a`/`b`, Vorversion/neue Version, OpenShift/AWS.
- Status externer Projekte und SNAPSHOTs.
- Freigaben: Mathe-Abteilung, Marketing/Gesamtfreigabe, IT-Server/Cloud Infrastruktur.
- gewünschtes Deployment-/Lieferdatum.

## Vorgehen

### 1. Release-Kontext klären
Erstelle einen Release-Steckbrief:

| Feld | Wert |
|---|---|
| Release-Typ | Beta / Vollversion / Hotfix |
| Zielversion |  |
| Vorgängerversion |  |
| VBL betroffen | ja/nein |
| DOL betroffen | ja/nein |
| Webservices | ja/nein |
| WebUIs | ja/nein |
| Rechenkern | ja/nein |
| Zielcluster |  |
| Deploymentdatum |  |
| Freigabenstatus |  |

### 2. Externe Projekte prüfen
Vor Finalisierung müssen relevante externe Projekte und das Applications-Repository geprüft sein.

Prüfe insbesondere:

- Gibt es SNAPSHOT-Abhängigkeiten?
- Muss ein externes Projekt vorher released werden?
- Gibt es Beta-Versionen, die bewusst verwendet werden?
- Sind externe Projekte bereits endgültig finalisiert und direkt in `mono-elsa` einzutragen?
- Sind Ansprechpartner und Erledigt-Status klar?

Output: Abhängigkeitenliste mit Status `offen`, `bereit`, `zu klären`, `blockierend`.

### 3. Frühe Vorbereitung durchführen
Frühzeitig klären:

- IT-Server/Cloud Infrastruktur informieren, wann Lieferscheine und Deployment geplant sind.
- Technisches Marketing informieren, dass Makler rechtzeitig über mögliche Session-Ausfälle informiert werden.
- BAV-Netto-Tool bzw. externe Lieferungen prüfen, falls relevant.

### 4. Einen Tag vor Finalisierung prüfen
Pflichtprüfungen:

- `clean install` mit Tests einen Tag vorher ausführen.
- Bei Testfehlern für Durchlauf ggf. `clean install -fn` nutzen, aber Fehler nicht ignorieren.
- Release Notes / Dokumentation vorbereiten.
- Vorgängerversionen und URLs von Webservices/WebUIs dokumentieren.
- Freigaben prüfen:
  - Rechenkern: Freigabe Mathe-Abteilung.
  - mono-elsa: Gesamtfreigabe Marketing / Frank Bohlmann bzw. Ticketstatus.
- Deploymentfragen klären:
  - Was deployen wir?
  - Wird DOL deployed?
  - Ändern sich Versionsnummern?
  - Wird der Rechenkern deployed?
  - Auf welchem Cluster wird deployed?

### 5. Endpoints anpassen und testen
Prüfe und aktualisiere:

#### Postman
- Workspace `VB Leben`.
- `Environments` anpassen.
- Bei Beta beachten: häufig Webservices/Rechenkerne, nicht Weboberflächen.
- Health-Check-Monitore unter `Monitors` anpassen.

#### Smoketest
- Projekt `Smoketest`.
- `properties_Template.yaml` mit Endpunkten/Umgebungen aktualisieren.
- Smoketest-Projekt taggen.
- Neue Smoketest-Version in `.gitlab-ci.yml` von `mono-elsa` eintragen, z. B. `smoke-tester-1.0.5` statt `1.0.4`.

### 6. Applications-Repository prüfen
Im Applications-Repository werden OpenShift-Deskriptoren und Konfigurationen verwaltet.

Prüfe:

- richtiger Branch.
- betroffene Anwendungspfade, z. B.:
  - `app/vertriebssoftware/leben/mono-elsa/vsl_ws_vbl_a`
  - `app/vertriebssoftware/leben/core/vsl_rk_vbl_a`
- Stage-Verzeichnisse, z. B. `production/patches/deployment.yml`.
- `spec.replicas`.
- `limits.memory` und `requests.memory`.

Hinweise:
- Testversion/Hotfix: Replicas meist nicht anzupassen.
- PROD-Webservices: typischerweise 4 Replicas.
- ITN: häufig 2–4 Replicas.
- DEV/QA: häufig 1 Replica.
- Rechenkerne: häufig deutlich mehr Replicas, etwa 7–20.
- Werte sind keine feste Vorgabe; sie müssen releasebezogen geklärt werden.

### 7. Rechenkernprojekt finalisieren
Ablauf:

1. Freigabe der Mathe-Abteilung abwarten.
2. `rechenkern-win32-resources` finalisieren.
   - GitLab `Run Pipeline`, nicht taggen.
   - Variable `MAVEN_NEW_VERSION` setzen, z. B. `49.0.0-beta1` ohne `vb-release/`.
   - optional `SOURCE_VERSION` setzen.
3. Projekt `rechner` finalisieren.
   - in IntelliJ auschecken, main-Branch, pull.
   - in `rechner/pom.xml` `rechenkern-win32-resources.version` von `main-SNAPSHOT` auf neue Version setzen.
   - Maven Reimport und `clean install`.
   - Push.
   - Tag `vb-release/xx.x.x` erstellen.
   - Pipeline abwarten.
   - DEV/QA deployen.
   - Bei Finalisierung auch Integration/Production deployen.
   - Applications-MRs nur gezielt mergen; andere MRs nicht versehentlich mergen.
   - für Integration/Production Lieferscheine erstellen.
   - lokalen letzten Commit reverten und wieder `main-SNAPSHOT` herstellen.

### 8. mono-elsa finalisieren
Ablauf:

1. Gesamtfreigabe abwarten.
2. Projekt in IntelliJ auschecken.
3. Branch wählen:
   - Finalisierung: meist `main`.
   - Hotfix: eigener Hotfix-Branch.
4. pull.
5. In `mono-elsa/pom.xml` Versionen externer Projekte anpassen.
   - komplette Liste prüfen, auch wenn meist nur hervorgehobene Versionen geändert werden.
   - im Zweifel Ansprechpartner fragen.
6. In `mono-elsa/gitlab-ci-cd/variables.yml` setzen:
   - `ENABLE_INSTALLSHIELD_JOB=true`
   - `VBPP_MAIN_BUILD=true`
7. Maven Reimport und `clean install -fn`.
8. Push.
9. GitLab Tag `vb-release/xx.x.x` erstellen.
10. Pipeline abwarten.
11. DEV/QA deployen.
12. Nach `Deploy-Clients` warten, bis Artefakte im Artifactory angekommen sind.
13. `Starte-Installshield` erst danach starten.
14. Im Finalisierungsthread zum Testen aufrufen.
15. letzten Commit reverten und Snapshot-/Git-Variablen wieder zurückstellen.

### 9. Nachbereitung durchführen
Nach mono-elsa-Finalisierung, unabhängig vom Deployment:

- Cluster-ID für VBL/DOL CurrentVersion ggf. `a`/`b` tauschen.
- Nicht manuell anpassen: `VSL_CLUSTERID_*_PREVERSION`, falls automatisch gesetzt.
- Im Rechenkern `VBL_CLUSTER` und `DOL_CLUSTER` prüfen/anpassen.
- nächste WS-Version vorbereiten:
  - `VSL_WS_CURRENTVERSION`
  - `VSL_WS_PREVERSION`

### 10. Rechenkerne migrieren
Bei Releasewechsel:

- neue Webservices/Weboberflächen ersetzen alte.
- alte Webservices bleiben als Vorversion verfügbar.
- Vorversions-Rechenkerne werden ggf. von AWS nach OpenShift migriert, damit AWS-Kapazität für neue Version frei wird.

Prüfe:

- Cluster der Webservices ermitteln.
- PROD-Rechenkerne der Vorversion in OpenShift hochfahren.
- `RK_SERVICE` in `config.yml` anpassen:
  - Vorversion OpenShift: `http://vsl-rk-vbl-a/api/rechner/quote`.
  - neue Version AWS: `https://rechenkern-ws-vbl-prod.../api/rechner/quote`.
- `network-policy.yml` anpassen:
  - OpenShift: `policy.net.k8s/allow-to-vsl-rk-vbl-a: "true"`.
  - AWS: `policy.net.k8s/allow-to-openshift-aws-production-ingress: "true"`.
- für `vsl_ws_dol_b`, `vsl_ws_vbl_b`, `vsl_ws_dol_a` wiederholen.
- MRs erstellen und Deployment-Jobs aus Tag-Pipeline starten.

### 11. Lieferscheine erstellen
Vorher mit zuständigen Personen Zeitpunkt klären.

Prüfe:

- Welche Anwendungen werden ausgeliefert?
- DOL ja/nein?
- Versionsnummern geändert?
- Rechenkern ja/nein?
- Cluster?
- Vorversion der Web-Applikationen verfügbar und URL-Doku aktualisiert?

Für jeden Lieferschein:

- Programm/System aus Vorlage suchen.
- Pipeline/Tag und Merge-Request bzw. Dockerimage ermitteln.
- Felder pflegen:
  - Änderungsdatum/Version (SCM): `xx.x.x`.
  - vorherige Version: unmittelbar vorherige Version, mit Smoketest/Postman verifiziert.
  - Lieferdatum.
  - Auslieferung Quelle: MR-Link oder Dockerimage.
  - Ziel: bei Rechenkern ggf. Clusterumstellung.
  - Anlagen: Mantis/Jira Ticket technisches Marketing.
  - benötigte Freigaben.
  - benötigte Übernahmen: IT-Containerplattform.
  - Bemerkungen inkl. Produktionsabhängigkeiten/Rechenserver-Version.
- Sonderfall AWS Cloud: passender Cloud-Lieferschein und Dockerimage aus Artifactory.
- Erfassung abschließen.
- Freigaben abwarten.
- Übergabe an Betrieb klicken.
- IT-Server/Cloud Infrastruktur informieren.
- Icinga-/Healthcheck-Verantwortliche informieren, wenn neue WS Service-URL relevant ist.

### 12. Monitoring nach Livegang
Prüfe in den folgenden Tagen:

- Grafana DEV/QA/Integration/PROD.
- Tarifrechner-Dashboards.
- Health-Checks.
- Smoketest mit korrekten `endpoints.json`.
- Fehlerquoten und auffällige Operations-/Consumer-Verteilung.
- Rechenkern-Erreichbarkeit und Latenzen.
- alte Vorversion weiterhin erreichbar.

## Output-Format

```markdown
# Release-Finalisierung

## 1. Release-Steckbrief
## 2. Externe Projekte / Abhängigkeiten
## 3. Freigaben
## 4. Vorbereitung T-1
## 5. Endpoint- und Smoketest-Änderungen
## 6. Applications-Repository
## 7. Rechenkern-Finalisierung
## 8. mono-elsa-Finalisierung
## 9. Nachbereitung / Cluster / Versionen
## 10. Deployment / Lieferscheine
## 11. Monitoring nach Livegang
## 12. Risiken / offene Punkte
## 13. Go/No-Go-Checkliste
```

## Go/No-Go-Checkliste

- [ ] Externe Projekte geprüft, keine ungewollten SNAPSHOTs.
- [ ] Applications-Repository geprüft.
- [ ] `clean install` vor Finalisierung gelaufen.
- [ ] Release Notes / Dokumentation vorbereitet.
- [ ] Freigabe Mathe für Rechenkern vorhanden oder nicht relevant.
- [ ] Gesamtfreigabe mono-elsa vorhanden.
- [ ] Endpoints in Postman angepasst.
- [ ] Health-Checks/Monitors angepasst.
- [ ] Smoketest aktualisiert, getaggt und in mono-elsa referenziert.
- [ ] Replicas/Memory geprüft.
- [ ] Rechenkern finalisiert/deployed/reverted.
- [ ] mono-elsa finalisiert/deployed/reverted.
- [ ] Cluster-/Vorversionsvariablen nachgezogen.
- [ ] Lieferscheine erstellt und übergeben.
- [ ] Monitoring nach Livegang geplant.

## Qualitätskriterien
- Keine Finalisierung ohne geprüfte externe Projekte und Applications-Repository.
- Snapshots, Beta-Versionen und finalisierte externe Versionen werden bewusst behandelt.
- Revert-Schritte sind explizit eingeplant.
- Vorversion und neue Version werden nicht verwechselt.
- Deployment, Lieferscheine und Monitoring sind Teil des Release-Prozesses, nicht Nachgedanke.

## Typische Fehler
- Testfehler erst am Finalisierungstag entdecken.
- Smoketest-Version nicht in `.gitlab-ci.yml` nachziehen.
- Falsche MRs im Applications-Repository mergen.
- `main-SNAPSHOT` nach Finalisierung nicht wiederherstellen.
- Vorversions-Rechenkerne/AWS/OpenShift-Links falsch setzen.
- Lieferscheine ohne korrekte Quelle/MR/Dockerimage erstellen.
