---
name: vb-release-finalization
description: Unterstützt die Finalisierung eines Releases der Java-Anwendungen im VSL-/mono-elsa-Kontext. Führt durch Vorbereitung, externe Abhängigkeiten, Endpoint-Anpassungen, Applications-Repository, Rechenkern-Finalisierung, Deployment und Monitoring.
---

# VB Release Finalization

## Ziel

Unterstützt die Finalisierung eines Releases der Java-Anwendungen im VSL-/mono-elsa-Kontext. Der Skill führt durch Vorbereitung, externe Projektabhängigkeiten, Endpoint-Anpassungen, Applications-Repository, Rechenkern-Finalisierung, mono-elsa-Finalisierung, Nachbereitung, Deployment, Rechenkernmigration, Lieferscheine und Monitoring nach Livegang.

Verwenden bei:
- Finalisierung einer Vollversion oder Beta der Java-Anwendungen
- Vorbereitung eines VSL-/mono-elsa-Releases
- Prüfung externer SNAPSHOT-/Beta-/Release-Abhängigkeiten
- Erstellung einer Release-Checkliste oder eines Ablaufplans
- Vorbereitung von Lieferscheinen und Deployment-Aufträgen
- Migration von Rechenkernen bzw. Cluster-/Vorversionswechsel

NICHT verwenden bei:
- Fachlicher BiPRO-Analyse; dafür `vb-bipro-analysis`
- Webservice-Fehlerdiagnose; dafür `vb-webservice-diagnostics`
- Allgemeiner Projektplanung ohne Release-Kontext

## Vorgehen

### 1. Release-Kontext klären
Erstelle einen Release-Steckbrief mit: Release-Typ, Zielversion, Vorgängerversion, betroffene Anwendungen (VBL/DOL/Webservice/WebUI/Rechenkern), Zielumgebungen, Cluster, Status externer Projekte, Freigaben, Deployment-/Lieferdatum

### 2. Externe Projekte prüfen
Prüfe SNAPSHOT-Abhängigkeiten, ob externe Projekte vorher released werden müssen, Beta-Versionen, finalisierte externe Versionen. Output: Abhängigkeitenliste mit Status

### 3. Frühe Vorbereitung durchführen
IT-Server/Cloud Infrastruktur informieren, Technisches Marketing informieren, BAV-Netto-Tool/externe Lieferungen prüfen

### 4. Einen Tag vor Finalisierung prüfen
`clean install` mit Tests, Release Notes vorbereiten, Vorgängerversionen und URLs dokumentieren, Freigaben prüfen (Rechenkern: Mathe-Abteilung, mono-elsa: Gesamtfreigabe Marketing), Deploymentfragen klären

### 5. Endpoints anpassen und testen
Postman Workspace, Environments, Health-Check-Monitors anpassen. Smoketest-Projekt: properties aktualisieren, taggen, neue Version in `.gitlab-ci.yml` eintragen

### 6. Applications-Repository prüfen
Richtiger Branch, betroffene Anwendungspfade, Stage-Verzeichnisse, Replicas, Memory-Limits

### 7. Rechenkernprojekt finalisieren
Freigabe Mathe-Abteilung abwarten, `rechenkern-win32-resources` finalisieren, Projekt `rechner` finalisieren (pom.xml, Tag, Pipeline, deployen, revert zu SNAPSHOT)

### 8. mono-elsa finalisieren
Gesamtfreigabe abwarten, Branch wählen, pom.xml Versionen anpassen, `ENABLE_INSTALLSHIELD_JOB` und `VBPP_MAIN_BUILD` setzen, `clean install -fn`, Push, Tag, Pipeline, deployen, revert

### 9. Nachbereitung durchführen
Cluster-ID tauschen, nächste WS-Version vorbereiten (CurrentVersion, Preversion)

### 10. Rechenkerne migrieren
Vorversions-Rechenkerne von AWS nach OpenShift migrieren, `RK_SERVICE` und `network-policy.yml` anpassen, MRs und Deployment-Jobs starten

### 11. Lieferscheine erstellen
Zeitpunkt mit zuständigen Personen klären, Anwendungen identifizieren, Felder pflegen (Version, Quelle, Ziel, Freigaben, Übernahmen), Erfassung abschließen, IT-Server informieren

### 12. Monitoring nach Livegang
Grafana DEV/QA/Integration/PROD, Tarifrechner-Dashboards, Health-Checks, Smoketest, Fehlerquoten, Rechenkern-Erreichbarkeit, alte Vorversion prüfen

## Regeln / Qualitätskriterien

- Keine Finalisierung ohne geprüfte externe Projekte und Applications-Repository
- Snapshots, Beta-Versionen und finalisierte externe Versionen werden bewusst behandelt
- Revert-Schritte sind explizit eingeplant
- Vorversion und neue Version werden nicht verwechselt
- Deployment, Lieferscheine und Monitoring sind Teil des Release-Prozesses, nicht Nachgedanke
- Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`

### Typische Fehler
- Testfehler erst am Finalisierungstag entdecken
- Smoketest-Version nicht in `.gitlab-ci.yml` nachziehen
- Falsche MRs im Applications-Repository mergen
- `main-SNAPSHOT` nach Finalisierung nicht wiederherstellen
- Vorversions-Rechenkerne/AWS/OpenShift-Links falsch setzen
- Lieferscheine ohne korrekte Quelle/MR/Dockerimage erstellen

## Ressourcen

- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf` (Primärreferenz)
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Gesamtdokumentation_v3.html`
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Einarbeitungsplan.html`
- `docs/referenzen/Webservices-Strategie/REFERENZEN.md`