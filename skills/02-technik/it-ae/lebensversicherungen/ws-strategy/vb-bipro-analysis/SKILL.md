---
name: vb-bipro-analysis
description: Analysiert einen BiPRO TAA Leben WebService oder eine konkrete Änderung an der Schnittstelle fachlich und technisch. Verbindet Operationen, WSDL/XSD, VU-Erweiterungen, Provider-Modell, DTO-Hierarchie, Phasenpipeline, Mapping, Konverter und Roundtrip-Tests.
---

# VB BiPRO Analysis

## Ziel

Analysiert einen BiPRO TAA Leben WebService oder eine konkrete Änderung an der Schnittstelle fachlich und technisch. Der Skill verbindet Operationen, WSDL/XSD, VU-Erweiterungen, Provider-Modell, DTO-Hierarchie, Phasenpipeline, Mapping, Konverter und Roundtrip-Tests zu einer prüfbaren Analyse.

Verwenden bei:
- Einstieg in einen bestehenden BiPRO-Service oder eine Operation
- Analyse eines neuen oder geänderten extern befüllbaren Attributs
- Vorbereitung einer Änderung an XSD, Mapping, Konverter, Modell oder Testressourcen
- Prüfung, ob eine Änderung nur schema-valide ist oder fachlich tatsächlich verarbeitet wird
- Vorbereitung eines Reviews für VBL/DOL Leben-Schnittstellen

NICHT verwenden bei:
- Reiner REST-API ohne BiPRO-/SOAP-/TAA-Bezug
- Reinem Java-Refactoring ohne Schnittstellen-, Mapping- oder Phasenbezug
- Release-Finalisierung; dafür `vb-release-finalization` verwenden

## Vorgehen

### 1. Analyseziel festlegen
- Geht es um Verstehen, Änderung, Fehleranalyse oder Dokumentation?
- Welche Marke ist betroffen: VBL, DOL oder gemeinsame Leben-Basis?
- Welche Operation und Version ist relevant?

### 2. Fachliche Operation einordnen
Erstelle eine Operationskarte mit: Operation, fachlicher Zweck, Dokumentenbezug, Authentifizierungs-/Security-Bezug, betroffene Partnerjourney

### 3. Provider-Modell prüfen
Prüfe, ob der Nutzer fälschlich nach Java-Methoden wie `getOffer(...)` sucht. Die Webservices folgen dem JAX-WS-Provider-Modell: generischer Einstieg über `invoke(SOAPMessage)`, Request-Typ datengetrieben über DTO/Konstanten, Verarbeitung über Phasen.

### 4. Datenfluss rekonstruieren
Erstelle eine textuelle Flow-Sicht: SOAP Request → Provider.invoke → DTO → Phasen → Mapping → Rechenkern → Export → Response

### 5. XSD und VU-Erweiterung prüfen
- Liegt das Feld in `vb-leben`, `vb-vbl` oder `vb-dol`?
- Wird `basis:Erweiterung` mit korrektem `xsi:type` verwendet?
- Stimmt die Reihenfolge aus `xsd:sequence`?
- Ist das Element optional (`minOccurs`) oder mehrfach (`maxOccurs`)?
- Ist die Änderung nur schema-valide oder auch fachlich verarbeitet?

### 6. Internes Modell und DTO-Hierarchie prüfen
Ordne betroffene Objekte ein: PhasenDTO → BiPRODTO → LebenDTO → LebenWSDTO. Prüfe: XML-Position, ELSA-/VB-Modell-Ziel, @Property-Kardinalität, Security-/Web-Kontext

### 7. Mapping und Konverter prüfen
Unterscheide: Eingabe-Mapping, Ausgabe-Mapping, Konverter, Transformer. Prüfe: Eingaberegel, Ausgaberegel, Erweiterungsstruktur, Konverter erforderlich/registriert

### 8. Test- und Absicherungsanalyse
Bewerte: valider Beispielrequest, Roundtrip-Test, Assertions für Eingabe/Ausgabe, Testfälle für `xsi:type`, Reihenfolge, Sonderzeichen, Encoding, PDF-Auswirkungen, fachlich gültiger Versicherungsbeginn

### 9. Risiken und offene Punkte klassifizieren
Kennzeichne jeden Befund als `belegt`, `plausibel`, `zu verifizieren`, `Diskrepanz` oder `Empfehlung`

## Regeln / Qualitätskriterien

- Keine Behauptung ohne Eingabe-, Code- oder Referenzbasis
- XSD, Mapping, Konverter und Test werden getrennt bewertet
- Provider-Modell wird explizit berücksichtigt
- Fachlichkeit und Technik werden nicht vermischt
- Offene Punkte werden sichtbar gemacht
- Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`
- Keine VB-Standards erfinden

### Typische Fehler
- XSD-Änderung als vollständige Implementierung bewerten
- Nach `getOffer()` als Java-Methode suchen
- Eingabe-Mapping ergänzen, aber Ausgabe-Mapping vergessen
- Konverter implementieren, aber nicht registrieren
- Marke VBL/DOL oder gemeinsame Leben-XSD verwechseln

## Ressourcen

- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Gesamtdokumentation_v3.html`
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Einarbeitungsplan.html`
- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf`
- `docs/referenzen/Webservices-Strategie/REFERENZEN.md`
