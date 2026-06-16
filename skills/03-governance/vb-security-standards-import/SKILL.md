---
name: vb-security-standards-import
description: Importierte Sicherheitsstandards als Checkliste — Secret-Erkennung, Dependency-Security, Eingabevalidierung, Datenschutz, Incident Response.
---

# vb-security-standards-import

## Ziel
Dient als zusätzliche Sicherheits-Checkliste für Code-Reviews und Entwicklungsprozesse. Behandelt zentrale Sicherheitsprinzipien: Keine Geheimnisse im Code, Sicherheit von Abhängigkeiten, Eingabevalidierung und Datenschutz. Nur anwenden, sofern mit VB-Randbedingungen und Projektvorgaben vereinbar. Der Inhalt ist nicht automatisch ein VB-Standard.

## Vorgehen

### Zentrale Sicherheitsprinzipien prüfen
- **Keine Geheimnisse im Code**: API-Schlüssel, Passwörter oder Token niemals fest im Code hinterlegen. Umgebungsvariablen für sensible Daten nutzen. Sensible Dateien von Git ausschließen (.env, credentials.json). Vor dem Commit auf Secrets scannen.
- **Sicherheit von Abhängigkeiten**: Wenn möglich, Standardbibliothek nutzen. Externe Abhängigkeiten minimieren und aktuell halten. Auf Sicherheitslücken prüfen (pip-audit, safety).
- **Eingabevalidierung**: Alle Benutzereingaben validieren. Dateipfade bereinigen. Command Injection verhindern. Edge-Cases sicher behandeln.
- **Datenschutz**: Keine unnötigen sensiblen Daten speichern. Daten bei Übertragung verschlüsseln. DSGVO-Compliance sicherstellen.

### Pre-Commit Secret Scanning
- Nach gängigen Geheimnismustern suchen: `api_key`, `secret`, `password`, `token`, `Bearer`, OpenAI-Keys (`sk-...`), GitHub-Tokens (`ghp_...`), AWS-Keys (`AKIA...`).
- Git-Ignore-Muster für .env, .pem, credentials.json, secrets.yaml und IDE-Dateien konfigurieren.

### Python Sicherheits-Best-Practices anwenden
- Sichere Dateipfade mit `pathlib.Path.resolve()` und `is_relative_to()`.
- Sichere Befehlsausführung mit `subprocess.run(args, shell=False, timeout=30)`.
- Eingabevalidierung per Regex (E-Mail-Format, Dateinamenbereinigung).
- Keine sensiblen Infos in Fehlermeldungen preisgeben.

### Dependency-Management
- Genaue Versionen in requirements.txt festlegen (`pip freeze > requirements.txt`).
- Regelmäßig `pip-audit` oder `safety check` ausführen.
- Dependabot-Warnungen überwachen, gefährdete Pakete umgehend aktualisieren.
- Paketlizenzen prüfen und dokumentieren.

### Sicherheitsprüfung vor Commit
- Checkliste durchgehen: Geheimnisse, Eingabevalidierung, Dependency-Security, Fehlerbehandlung, Datenschutz.
- Bei Verstößen sofort korrigieren.

### Incident Response (bei offengelegten Secrets)
- Zugangsdaten SOFORT rotieren.
- Aus Git-Historie entfernen (`git filter-branch`).
- Sicherheitsteam benachrichtigen und Vorfall dokumentieren.

### Regelmäßige Sicherheitswartung
- **Wöchentlich**: Dependabot-Warnungen prüfen, auf Geheimnisse scannen.
- **Monatlich**: Vollständiges Sicherheitsaudit, Abhängigkeiten aktualisieren.
- **Vierteljährlich**: Sicherheitsstandards prüfen, Werkzeuge aktualisieren.
- **Jährlich**: Umfassende Sicherheitsbewertung.

## Regeln / Qualitätskriterien
- Dieser Inhalt ist nicht automatisch ein VB-Standard — nur anwenden, wenn mit VB-Randbedingungen vereinbar.
- Sicherheitslücken KEINE öffentlichen Issues erstellen — vertraulich melden.
- Stack-Traces in Produktion bereinigen, Logging ohne Geheimnisse.
- Empfohlene Sicherheits-Tools: gitleaks, trufflehog, pip-audit, safety, bandit, semgrep.
- Vor schreibenden, löschenden, produktiven oder administrativen Aktionen explizite Nutzerbestätigung einholen.

## Ressourcen
Keine
