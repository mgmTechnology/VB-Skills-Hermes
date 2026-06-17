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