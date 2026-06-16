# vb-security-standards-import

## VB-Einordnung

Importierter Security-Standard-Text aus dem Junie-Skillpaket.

## Abgrenzung

Dieser Inhalt ist nicht automatisch ein VB-Standard. Er dient als zusätzliche Sicherheits-Checkliste, sofern er mit den VB-Randbedingungen und Projektvorgaben vereinbar ist.

## Inhalt

# Sicherheits-Standards

## Zentrale Sicherheitsprinzipien

### **1. Keine Geheimnisse im Code**
- API-Schlüssel, Passwörter oder Token niemals fest im Code hinterlegen.
- Umgebungsvariablen für sensible Daten nutzen.
- Sensible Dateien von Git ausschließen (.env, credentials.json).
- Vor dem Commit auf Geheimnisse (Secrets) scannen.

### **2. Sicherheit von Abhängigkeiten (Dependencies)**
- Wenn möglich, die Standardbibliothek nutzen.
- Externe Abhängigkeiten minimieren.
- Abhängigkeiten aktuell halten.
- Abhängigkeiten auf Sicherheitslücken prüfen (Audit).

### **3. Eingabevalidierung**
- Alle Benutzereingaben validieren.
- Dateipfade bereinigen (Sanitize).
- Befehlsinjektionen (Command Injection) verhindern.
- Edge-Cases sicher behandeln.

### **4. Datenschutz**
- Keine unnötigen sensiblen Nutzerdaten speichern.
- Daten bei der Übertragung verschlüsseln.
- Best Practices zum Datenschutz befolgen.
- Einhaltung der DSGVO sicherstellen.

## Erkennung von Geheimnissen (Secrets)

### **Pre-Commit Secret Scanning**

```bash
# Vor dem Commit nach gängigen Geheimnissen suchen
git diff --cached | grep -iE 'api[_-]?key|secret|password|token|Bearer|Authorization'

# Spezifische Muster zur Erkennung
patterns=(
  "api[_-]?key.*=.*['\"][^x']+"
  "secret.*=.*['\"][^x']+"
  "password.*=.*['\"][^x']+"
  "token.*=.*['\"][^x']+"
  "Bearer\s+[A-Za-z0-9\-._~+/]+"
  "sk-[A-Za-z0-9]{20,}"  # OpenAI API keys
  "ghp_[A-Za-z0-9]{36}"  # GitHub Personal Access Tokens
  "AKIA[A-Z0-9]{16}"     # AWS Access Keys
)
```

### **Verbotene Muster**

```python
# ❌ Schlecht - Fest im Code hinterlegtes Geheimnis
API_KEY = "sk-1234567890abcdef"
password = "meinpasswort123"

# ✅ Gut - Umgebungsvariable
import os
API_KEY = os.getenv("API_KEY")
if not API_KEY:
    raise ValueError("API_KEY Umgebungsvariable nicht gesetzt")
```

### **Git Ignore Muster**

```gitignore
# Geheimnisse und Zugangsdaten
.env
.env.*
*.key
*.pem
credentials.json
secrets.yaml
config/local.py

# Python-Cache (kann sensible Daten enthalten)
__pycache__/
*.pyc
*.pyo

# OS-Dateien
.DS_Store
Thumbs.db

# IDE-Dateien
.vscode/settings.json
.idea/
```

## Python Sicherheits-Best-Practices

### **1. Sicherer Umgang mit Dateien**

```python
# ✅ Gut - Sicherer Umgang mit Pfaden
import os
from pathlib import Path

def read_user_file(filename: str) -> str:
    """Liest sicher eine vom Nutzer bereitgestellte Datei."""
    # Dateiname validieren
    if not filename or '..' in filename or filename.startswith('/'):
        raise ValueError("Ungültiger Dateiname")

    # Path für sichere Pfadmanipulation nutzen
    base_dir = Path(__file__).parent
    file_path = (base_dir / filename).resolve()

    # Sicherstellen, dass die Datei im erlaubten Verzeichnis liegt
    if not file_path.is_relative_to(base_dir):
        raise ValueError("Dateipfad außerhalb des erlaubten Verzeichnisses")

    # Sicher lesen
    with open(file_path, 'r') as f:
        return f.read()

# ❌ Schlecht - Unsicherer Umgang mit Pfaden
def read_file_unsafe(filename: str) -> str:
    # Anfällig für Directory Traversal (Pfad-Überschreitung)
    with open(filename, 'r') as f:
        return f.read()
```

### **2. Sicherheit bei der Befehlsausführung**

```python
# ✅ Gut - Sichere Befehlsausführung
import subprocess
from typing import List

def run_safe_command(args: List[str]) -> str:
    """Führt Befehle sicher mit einer Argumentliste aus."""
    # Argumentliste nutzen, nicht shell=True
    result = subprocess.run(
        args,
        capture_output=True,
        text=True,
        check=True,
        timeout=30  # Hängenbleiben verhindern
    )
    return result.stdout

# Beispiel
output = run_safe_command(['python', 'script.py', '--input', 'datei.txt'])

# ❌ Schlecht - Anfälligkeit für Shell-Injection
def run_command_unsafe(command: str) -> str:
    # Anfällig für Command Injection
    result = subprocess.run(
        command,
        shell=True,  # GEFÄHRLICH!
        capture_output=True
    )
    return result.stdout.decode()
```

### **3. Eingabevalidierung**

```python
# ✅ Gut - Eingaben validieren und bereinigen
def validate_email(email: str) -> bool:
    """Validiert das E-Mail-Format."""
    import re
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email) is not None

def sanitize_filename(filename: str) -> str:
    """Entfernt unsichere Zeichen aus dem Dateinamen."""
    import re
    # Trennzeichen und Null-Bytes entfernen
    safe = re.sub(r'[/\\:\0]', '', filename)
    # Führende Punkte entfernen (versteckte Dateien)
    safe = safe.lstrip('.')
    # Länge begrenzen
    return safe[:255]

# ❌ Schlecht - Keine Validierung
def process_input_unsafe(user_input: str):
    # Direkte Nutzung unvalidierter Eingaben
    exec(user_input)  # EXTREM GEFÄHRLICH!
```

### **4. Fehlerbehandlung**

```python
# ✅ Gut - Keine sensiblen Infos in Fehlermeldungen preisgeben
def connect_to_api(api_key: str):
    try:
        # Verbindungslogik
        pass
    except Exception as e:
        # API-Key nicht loggen!
        print("API-Verbindung fehlgeschlagen. Prüfen Sie Ihre Zugangsdaten.")
        raise ValueError("Authentifizierung fehlgeschlagen") from None

# ❌ Schlecht - Geheimnisse in Fehlermeldungen offenlegen
def connect_unsafe(api_key: str):
    try:
        pass
    except Exception as e:
        # Leakt den API-Key in die Logs!
        print(f"Verbindung fehlgeschlagen mit Key: {api_key}")
        raise
```

## Verwaltung von Abhängigkeiten (Dependencies)

### **Sicherheits-Checkliste für Abhängigkeiten**

```yaml
dependency_security:
  minimierung_der_abhaengigkeiten:
    - [ ] Wenn möglich, die Python-Standardbibliothek nutzen
    - [ ] Jede externe Abhängigkeit begründen
    - [ ] Gut gepflegte Pakete bevorzugen
    - [ ] Reputation des Pakets prüfen (Downloads, Sterne, Pflege)

  versions_festschreibung (Pinning):
    - [ ] Genaue Versionen in requirements.txt festlegen
    - [ ] Versionsbeschränkungen nutzen (>=, <)
    - [ ] Dokumentieren, warum spezifische Versionen benötigt werden
    - [ ] Upgrades vor dem Deployment testen

  vulnerabilitaets_scan:
    - [ ] Regelmäßig `pip-audit` oder `safety check` ausführen
    - [ ] Sicherheitshinweise (Advisories) prüfen
    - [ ] Gefährdete Pakete umgehend aktualisieren
    - [ ] Dependabot-Warnungen (GitHub) überwachen

  lizenz_compliance:
    - [ ] Paketlizenzen prüfen
    - [ ] GPL in kommerziellem Code vermeiden (falls zutreffend)
    - [ ] Alle Lizenzen dokumentieren
    - [ ] Anforderungen an die Nennung (Attribution) erfüllen
```

### **Befehle für Sicherheits-Scans**

```bash
# Auf bekannte Sicherheitslücken in Abhängigkeiten prüfen
pip install pip-audit
pip-audit

# Oder safety nutzen
pip install safety
safety check

# Auf veraltete Pakete prüfen
pip list --outdated

# requirements.txt mit Versions-Pinning generieren
pip freeze > requirements.txt
```

### **Sichere Requirements.txt**

```txt
# Genaue Versionen für Reproduzierbarkeit festlegen
requests==2.31.0
pyyaml==6.0.1

# Versionsbeschränkungen für Flexibilität nutzen
click>=8.0.0,<9.0.0
python-dateutil>=2.8.0

# Dokumentieren, warum spezifische Versionen genutzt werden
# numpy==1.24.0  # Erforderlich für Python 3.11 Kompatibilität
```

## Datenschutz

### **1. Umgang mit Nutzerdaten**

```python
# ✅ Gut - Minimale Datenerhebung
def analyze_text(text: str) -> dict:
    """Analysiert Text, ohne ihn zu speichern."""
    # Lokal verarbeiten, nicht an externe Dienste senden
    score = calculate_score(text)
    return {"score": score}

# ❌ Schlecht - Unnötige Datenspeicherung
def analyze_text_unsafe(text: str, user_id: str) -> dict:
    # Speichert Nutzerdaten unnötigerweise
    save_to_database(user_id, text)
    return analyze(text)
```

### **2. Best Practices zum Datenschutz**

```yaml
privacy_guidelines:
  datenminimierung:
    - Nur unbedingt notwendige Daten erheben
    - Daten nach Möglichkeit lokal verarbeiten
    - Daten nach der Verarbeitung löschen
    - Keine sensiblen Informationen loggen

  transparenz:
    - Dokumentieren, welche Daten erhoben werden
    - Erklären, wie Daten genutzt werden
    - Opt-out-Mechanismen bereitstellen
    - Datenexport und -löschung ermöglichen

  compliance:
    - DSGVO bei EU-Nutzern befolgen
    - Einwilligung zur Datenerhebung einholen
    - Datenschutzerklärung bereitstellen
```

## Sicherheits-Checkliste für Code-Reviews

### **Sicherheitsprüfung vor dem Commit**

```yaml
security_review:
  geheimnisse_und_zugangsdaten:
    - [ ] Keine fest hinterlegten API-Schlüssel
    - [ ] Keine fest hinterlegten Passwörter
    - [ ] Keine fest hinterlegten Token
    - [ ] Keine privaten Schlüssel committet
    - [ ] .env Dateien in .gitignore

  eingabevalidierung:
    - [ ] Alle Benutzereingaben validiert
    - [ ] Dateipfade bereinigt
    - [ ] SQL-Abfragen parametrisiert (falls zutreffend)
    - [ ] Command Injection verhindert
    - [ ] XSS-Prävention (bei Web-Apps)

  sicherheit_der_abhaengigkeiten:
    - [ ] Keine bekannten verwundbaren Abhängigkeiten
    - [ ] Abhängigkeiten minimiert
    - [ ] Versionen in requirements.txt fixiert
    - [ ] Lizenzen geprüft und kompatibel

  fehlerbehandlung:
    - [ ] Fehler legen keine sensiblen Daten offen
    - [ ] Stack-Traces in Produktion bereinigt
    - [ ] Logging enthält keine Geheimnisse
    - [ ] Fehlermeldungen sind nutzerfreundlich

  datenschutz:
    - [ ] Keine sensiblen Daten geloggt
    - [ ] Personenbezogene Daten ordnungsgemäß behandelt
    - [ ] Verschlüsselung wo nötig eingesetzt
    - [ ] Datenschutzerklärung aktualisiert (falls nötig)
```

## Reaktion auf Vorfälle (Incident Response)

### **Schweregrad von Sicherheitsproblemen**

```yaml
severity_levels:
  P0_kritisch:
    beschreibung: "Offengelegte Geheimnisse, aktive Exploits, Datenleck"
    reaktionszeit: "< 1 Stunde"
    massnahmen:
      - Offengelegte Zugangsdaten sofort sperren/rotieren
      - Kompromittierte Konten deaktivieren
      - Betroffene Nutzer benachrichtigen
      - Sicherheitslücke schließen (Patch)
      - Vorfall dokumentieren

  P1_hoch:
    beschreibung: "Verwundbare Abhängigkeiten, potenzielle Exploits"
    reaktionszeit: "< 24 Stunden"
    massnahmen:
      - Verwundbare Pakete aktualisieren
      - Fixes gründlich testen
      - Sicherheits-Patches einspielen
      - Auf Ausnutzung überwachen

  P2_mittel:
    beschreibung: "Verletzung von Sicherheits-Best-Practices"
    reaktionszeit: "< 1 Woche"
    massnahmen:
      - Probleme prüfen und beheben
      - Sicherheitsdokumentation aktualisieren
      - Team schulen

  P3_niedrig:
    beschreibung: "Geringfügige Sicherheitsverbesserungen"
    reaktionszeit: "< 1 Monat"
    massnahmen:
      - Korrekturen im Backlog einplanen
      - Standards aktualisieren
```

### **Reaktion auf offengelegte Geheimnisse**

```bash
# Wenn Sie versehentlich ein Geheimnis committet haben:

# 1. Zugangsdaten SOFORT rotieren
# (Passwort ändern, API-Key neu generieren etc.)

# 2. Aus der Git-Historie entfernen
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch pfad/zur/datei" \
  --prune-empty --tag-name-filter cat -- --all

# 3. Force-Push (nur wenn nicht auf Main/Produktion!)
git push origin --force --all

# 4. Sicherheitsteam benachrichtigen
# Vorfall dokumentieren
```

## Sicherheits-Werkzeuge

### **Empfohlene Sicherheits-Tools**

```yaml
security_tools:
  secret_erkennung:
    - gitleaks: "Scannt Git-Repos nach Geheimnissen"
    - trufflehog: "Findet Geheimnisse in der Git-Historie"
    - detect-secrets: "Verhindert neue Geheimnisse"

  abhaengigkeits_scan:
    - pip-audit: "Scannt Python-Abhängigkeiten"
    - safety: "Prüft auf bekannte Sicherheitslücken"
    - dependabot: "Automatisierte Updates (GitHub)"

  code_analyse:
    - bandit: "Sicherheits-Linter für Python"
    - pylint: "Allgemeiner Python-Linter mit Sicherheitsprüfungen"
    - semgrep: "Statische Analyse für Sicherheitsmuster"

  laufzeitschutz:
    - fail2ban: "Verhindert Brute-Force-Angriffe (falls zutreffend)"
    - rate limiting: "Verhindert Missbrauch"
    - monitoring: "Erkennt anomales Verhalten"
```

### **Skript für Sicherheits-Scans**

```bash
#!/bin/bash
# security-scan.sh - Alle Sicherheitsprüfungen ausführen

echo "🔒 Starte Sicherheits-Scans..."

# Secret-Erkennung
echo "Scanne nach Geheimnissen..."
gitleaks detect --verbose --redact || echo "⚠️  Potenzielle Geheimnisse gefunden"

# Verwundbare Abhängigkeiten
echo "Prüfe Abhängigkeiten..."
pip-audit || echo "⚠️  Verwundbare Abhängigkeiten gefunden"

# Python-Sicherheits-Linter
echo "Starte Bandit Sicherheits-Linter..."
bandit -r . -f screen || echo "⚠️  Sicherheitsprobleme gefunden"

# Suche nach gängigen Problemen
echo "Prüfe auf fest hinterlegte Passwörter..."
grep -r "password\s*=" --include="*.py" . && echo "⚠️  Potenzielle fest hinterlegte Passwörter"

echo "✅ Sicherheits-Scan abgeschlossen"
```

## Prozess für Sicherheits-Updates

### **Regelmäßige Sicherheitswartung**

- **Wöchentlich:** Dependabot-Warnungen prüfen, auf Geheimnisse scannen.
- **Monatlich:** Vollständiges Sicherheitsaudit, Abhängigkeiten aktualisieren.
- **Vierteljährlich:** Sicherheitsstandards prüfen, Werkzeuge aktualisieren.
- **Jährlich:** Umfassende Sicherheitsbewertung.

### **Sicherheits-Dokumentation**

```markdown
## Sicherheitsrichtlinie (Security Policy)

### Melden von Sicherheitsproblemen

**Erstellen Sie KEINE öffentlichen Issues für Sicherheitslücken!**

E-Mail: security@example.com
PGP-Key: [Link zum öffentlichen Schlüssel]

Erwartete Reaktionszeit: 24 Stunden

### Offenlegungsprozess (Disclosure Process)

1. Meldung empfangen und bestätigt.
2. Problem verifiziert und bewertet.
3. Fix entwickelt und getestet.
4. Sicherheitshinweis veröffentlicht.
5. Anerkennung für den Melder.
```

---

**Fokus**: Python-Sicherheit, Secret-Erkennung, Abhängigkeitsmanagement
**Aktualisiert**: November 2025
**Prüfung**: Monatliche Sicherheitsbewertung
**Compliance**: OWASP Top 10, Python Security Best Practices
