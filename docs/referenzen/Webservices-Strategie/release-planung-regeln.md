---
Titel: Release-Planung – Regeln und Meilensteine (Webservices & Strategie)
Stand: 2026-06-03
Status: gültig
Quelle: interne Festlegung der Gruppe Webservices & Strategie
---

# Release-Planung – verbindliche Regeln

## Grundregeln
- Liveschaltung nur an Mittwoch oder Donnerstag.
- Kein Deployment an einem Freitag (IT-Verfügbarkeit für Troubleshooting
  vor dem Wochenende muss gewährleistet sein).
- Go-Live ist Tag 0; alle Meilensteine werden rückwärts berechnet.

## Meilensteinregeln (Abstand und fester Wochentag)
| Meilenstein | Regel (Abstand und Logik) | Fester Wochentag |
|---|---|---|
| Kick-off (optional) | ca. 133 Tage (19 Wochen) vor Go-Live | Mittwoch |
| Erste Fachkonzepte | ca. 89 Tage vor Go-Live | Freitag |
| Letzte Einreichung | ca. 75 Tage vor Go-Live | Freitag |
| Antrags-Einzelseiten an Vermarktung | 1 Woche nach Letzter Einreichung Fachkonzept | Freitag |
| Antrags-PDFs an IT-AE | 2 Wochen nach Letzter Einreichung Fachkonzept | Freitag |
| Letzte Änderungen | ca. 55 Tage vor Go-Live | Freitag |
| Tech. Änderungsdoku | ca. 51 Tage vor Go-Live (Montag vor Beta-Version) | Montag |
| Vorbereitung Beta | 1 Werktag vor Beta-Version | variabel |
| Beta-Version | ca. 48 Tage vor Go-Live | Donnerstag |
| Abschluss Programmierung | ca. 19 Tage vor Go-Live | variabel |
| Beginn Feldtest | identisch mit Abschluss Programmierung | variabel |
| Planung Deployment | 1 Woche nach Beginn Feldtest | Freitag |
| Feldtest-Abschluss | am selben Tag wie Vorbereitung Finalisierung | Donnerstag |
| MATHE Abschluss VLRE | am selben Tag wie Vorbereitung Finalisierung | Donnerstag |
| Vorbereitung Finalisierung | 3 Werktage vor Beginn der Finalisierung | Donnerstag |
| Freigabe an IT (Deadline) | am selben Tag wie Beginn der Finalisierung | Dienstag |
| Finalisierung (Beginn) | ca. 8 Tage vor Go-Live | Dienstag |
| Liveschaltung | Tag 0 | Mittwoch oder Donnerstag |

## Kritische Phasen (keine Urlaubsplanung)
- Beta-Woche: Montag bis Freitag der Woche der Beta-Version.
- Finalisierungs-Woche: Montag bis Freitag der Woche vor Go-Live.
- Tag der Liveschaltung.

## Verifiziertes Beispiel (Go-Live Do, 25.06.2026)
Vollständiges Beispiel unter: `examples/Gruppen/Webservices-Strategie/beispiel-release-planung.md`

| Meilenstein | Datum | Phase |
|---|---|---|
| Kick-off (optional) | Mi, 11.02.2026 | Planung |
| Erste Einreichung Fachkonzept | Fr, 27.03.2026 | Planung |
| Letzte Einreichung Fachkonzept | Fr, 10.04.2026 | Planung |
| Antrags-Einzelseiten an Vermarktung | Fr, 17.04.2026 | Planung |
| Antrags-PDFs an IT-AE | Fr, 24.04.2026 | Planung |
| Letzte Änderungen Fachkonzept | Fr, 01.05.2026 | Planung |
| Technische Änderungsdoku fertig | Mo, 04.05.2026 | Entwicklung |
| Vorbereitung Beta | Do, 07.05.2026 | Entwicklung |
| Beta-Version bereit | Do, 07.05.2026 | Beta & Tests |
| Abschluss Programmierung | Fr, 05.06.2026 | Entwicklung |
| Beginn Feldtest | Fr, 05.06.2026 | Entwicklung |
| Planung Deployment | Fr, 12.06.2026 | Entwicklung |
| Feldtest-Abschluss | Do, 11.06.2026 | Release-Woche |
| MATHE Abschluss VLRE | Do, 11.06.2026 | Release-Woche |
| Vorbereitung Finalisierung | Do, 11.06.2026 | Entwicklung |
| Freigabe an IT (Deadline) | Di, 16.06.2026 | Release-Woche |
| Finalisierung (Beginn) | Di, 16.06.2026 | Release-Woche |
| Liveschaltung | Do, 25.06.2026 | Release-Woche |

Kritische Phasen im Beispiel:
- Beta-Woche: Mo, 04.05.2026 bis Fr, 08.05.2026
- Finalisierungs-Woche: Mo, 15.06.2026 bis Fr, 19.06.2026
- Tag der Liveschaltung: Do, 25.06.2026

## Verifiziertes Beispiel: Weihnachtsmann-Release (Go-Live Do, 17.12.2026)

Dieses Beispiel wurde mit dem FB-Plan abgeglichen. Der FB-Plan hat Vorrang — Abweichungen von den
reinen Referenzregeln sind dokumentiert.

| Meilenstein | Datum | Tag | Quelle |
|---|---|---|---|
| Kick-off (optional) | Mi, 05.08.2026 | Mi | FB + Regel identisch |
| Erste Einreichung Fachkonzept | Fr, 18.09.2026 | Fr | FB + Regel identisch |
| Letzte Einreichung Fachkonzept | Do, 01.10.2026 | Do | FB (Regel: Fr, 02.10.) |
| Antrags-Einzelseiten an Vermarktung | Fr, 09.10.2026 | Fr | FB + Regel identisch |
| Antrags-PDFs an IT-AE | Fr, 16.10.2026 | Fr | FB + Regel identisch |
| Letzte Änderungen / PDFs, AVBs, VV | Fr, 23.10.2026 | Fr | FB + Regel identisch |
| Technische Änderungsdoku fertig | Mo, 26.10.2026 | Mo | Regel (nicht im FB-Plan) |
| Beta-Version bereit | Mi, 28.10.2026 | Mi | FB (Regel: Do, 29.10.) |
| Abschluss Programmierung / Beginn Feldtest | Fr, 27.11.2026 | Fr | FB + Regel identisch |
| Planung Deployment | Fr, 04.12.2026 | Fr | FB + Regel identisch |
| Feldtest-Abschluss / MATHE VLRE / Finalisierung | Di, 08.12.2026 (14:00) | Di | FB (Regel: Feldtest-Ende Do 03.12., Finalisierung Di 08.12.) |
| Deployment VB ON, DOL, TAA-WS + Mail | Mi, 16.12.2026 | Mi | FB |
| Liveschaltung | Do, 17.12.2026 | Do | FB + Regel identisch |

Kritische Phasen:
- Beta-Woche: Mo, 26.10.2026 bis Fr, 30.10.2026 (⚠️ NRW-Herbstferien)
- Finalisierungs-Woche: Mo, 07.12.2026 bis Fr, 11.12.2026
- Tag der Liveschaltung: Do, 17.12.2026 (1 Woche vor Weihnachten)

## Umgang mit FB-Plan-Abweichungen

Der FB-Plan (Schnittstelle Fachabteilungen, IT-AE und IT-Betrieb) ist der mit allen Stakeholdern
abgestimmte Plan. Bei Abweichungen zwischen FB-Plan und Referenzregeln gilt:

1. **FB-Plan hat Vorrang** — er ist das Ergebnis der Abstimmung zwischen Fachabteilung, Marketing,
   IT-AE und IT-Betrieb.
2. **Abweichungen dokumentieren**, nicht stillschweigend korrigieren.
3. **Fehlende Meilensteine** aus den Referenzregeln ergänzen (z. B. Technische Änderungsdoku,
   Urlaubssperren).
4. **Risiken markieren**, die aus Abweichungen entstehen (z. B. kein Puffer zwischen Feldtest-Ende
   und Finalisierung).

### Bekannte, akzeptierte Abweichungsmuster

| Muster | Referenzregel | FB-Plan | Akzeptiert weil |
|---|---|---|---|
| Letzte Einreichung | Freitag | Donnerstag | FB rechnet in Wochen vor BETA, nicht Tagen vor Go-Live |
| Beta-Wochentag | Donnerstag | Mittwoch | 1 Tag früher, unkritisch |
| Feldtest-Ende = Finalisierung | 3 Werktage Puffer | Gleicher Tag | FB kompaktiert die Schlussphase; Feldtest faktisch am Vortag abschließen |
| Deployment-Tag | Go-Live = Mi/Do | Deployment Mi, Go-Live Do | Deployment ≠ Liveschaltung |