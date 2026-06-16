# vb-bipro-analysis

## Zweck
Analysiert einen BiPRO TAA Leben WebService oder eine konkrete Änderung an der Schnittstelle fachlich und technisch. Der Skill verbindet Operationen, WSDL/XSD, VU-Erweiterungen, Provider-Modell, DTO-Hierarchie, Phasenpipeline, Mapping, Konverter und Roundtrip-Tests zu einer prüfbaren Analyse.

## Wann verwenden
- Einstieg in einen bestehenden BiPRO-Service oder eine Operation (`getQuote`, `getOffer`, `getOrder`, `setOrder`, `setOrderQualified`, `getFile`, `getOfferQuestions`, `getOrderQuestions`).
- Analyse eines neuen oder geänderten extern befüllbaren Attributs.
- Vorbereitung einer Änderung an XSD, Mapping, Konverter, Modell oder Testressourcen.
- Prüfung, ob eine Änderung nur schema-valide ist oder fachlich tatsächlich verarbeitet wird.
- Vorbereitung eines Reviews für VBL/DOL Leben-Schnittstellen.

## Wann NICHT verwenden
- Reine REST-API ohne BiPRO-/SOAP-/TAA-Bezug.
- Reines Java-Refactoring ohne Schnittstellen-, Mapping- oder Phasenbezug.
- Release-Finalisierung; dafür `vb-release-finalization` verwenden.


## Verbindliche Referenzen
Nutze bei Bedarf diese lokalen Referenzen im Repository:

- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Gesamtdokumentation_v3.html`
- `docs/referenzen/Webservices-Strategie/BiPRO_TAA_Leben_Einarbeitungsplan.html`
- `docs/referenzen/Webservices-Strategie/release-java-anwendungen-vsl-finalisierung.pdf`
- `docs/referenzen/Webservices-Strategie/REFERENZEN.md`

Regel: Wenn eine Aussage nicht aus Eingabe, Code oder Referenzen ableitbar ist, kennzeichne sie als `offen`, `zu verifizieren` oder `Annahme`. Erfinde keine VB-Standards.


## Benötigte Eingaben
Mindestens eine der folgenden Informationen:

- betroffene Operation und Version, z. B. `VBLService_2.4.6.1.12`.
- XML-/SOAP-Request oder Response-Ausschnitt.
- XSD-/WSDL-Datei oder Name des betroffenen Schemaartefakts.
- betroffene Modellklasse, Mappingregel, Konverter oder Roundtrip-Test.
- fachliche Beschreibung der Änderung.

## Vorgehen

### 1. Analyseziel festlegen
Kläre zuerst:

- Geht es um Verstehen, Änderung, Fehleranalyse oder Dokumentation?
- Welche Marke ist betroffen: VBL, DOL oder gemeinsame Leben-Basis?
- Welche Operation ist betroffen?
- Welche Version ist relevant?

### 2. Fachliche Operation einordnen
Erstelle eine kurze Operationskarte:

| Aspekt | Ergebnis |
|---|---|
| Operation | z. B. `getOffer` |
| fachlicher Zweck | Angebot, Tarifierung, Antrag, Einreichung, Dateiabruf |
| Dokumentenbezug | PDF, Angebot, Antrag, Datei |
| Authentifizierungs-/Security-Bezug | STS, SCT, IAM, offen |
| betroffene Partnerjourney | z. B. `getOfferQuestions -> getOffer -> getFile` |

### 3. Provider-Modell prüfen
Prüfe ausdrücklich, ob der Nutzer fälschlich nach Java-Methoden wie `getOffer(...)` sucht. Die Webservices folgen dem JAX-WS-Provider-Modell:

- generischer Einstieg über `invoke(SOAPMessage)`.
- Request-Typ wird datengetrieben über DTO/Konstanten bestimmt.
- Verarbeitung läuft über Phasen, nicht über eine Methode pro Operation.

Output: kurze Erklärung, wo im Code die Analyse realistisch beginnen muss.

### 4. Datenfluss rekonstruieren
Erstelle eine textuelle Flow-Sicht:

```text
SOAP Request
 -> TarifrechnerService.invoke(SOAPMessage)
 -> Payload als Source
 -> TAALebenWebServiceTarifrechner.verarbeite(Source)
 -> LebenWSDTO initialisieren
 -> Prozessphasen
 -> Mapping / Import / Berechnung
 -> Export / SOAPVorbereitung
 -> SOAP Response
```

### 5. XSD und VU-Erweiterung prüfen
Prüfe:

- liegt das Feld in `vb-leben`, `vb-vbl` oder `vb-dol`?
- wird `basis:Erweiterung` mit korrektem `xsi:type` verwendet?
- stimmt die Reihenfolge aus `xsd:sequence`?
- ist das Element optional (`minOccurs`) oder mehrfach (`maxOccurs`)?
- ist die Änderung nur schema-valide oder auch fachlich verarbeitet?

### 6. Internes Modell und DTO-Hierarchie prüfen
Ordne betroffene Objekte ein:

```text
PhasenDTO -> BiPRODTO -> LebenDTO -> LebenWSDTO
```

Prüfe insbesondere:

- Wo liegt der Wert im XML?
- Wo soll er im ELSA-/VB-Modell landen?
- Ist `@Property` mit korrekter Kardinalität vorhanden?
- Wird der Security-/Web-Kontext benötigt (`SecurityContextData`, SCT, Remote-Adresse)?

### 7. Mapping und Konverter prüfen
Unterscheide sauber:

| Ebene | Zweck |
|---|---|
| Eingabe-Mapping | BiPRO/XML -> internes Modell |
| Ausgabe-Mapping | internes Modell -> BiPRO/XML |
| Konverter | Wert-/Typumsetzung, z. B. Code -> Enum |
| Transformer | technische XML-Dokumenttransformation, nicht fachliches Mapping |

Prüfe:

- gibt es eine Eingaberegel?
- gibt es eine Ausgaberegel?
- muss eine Erweiterungsstruktur erzeugt werden?
- ist ein Konverter erforderlich?
- ist der Konverter registriert?

### 8. Test- und Absicherungsanalyse
Bewerte die Testlage:

- Gibt es einen validen Beispielrequest?
- Gibt es einen Roundtrip-Test?
- Gibt es Assertions für Eingabe und Ausgabe?
- Gibt es Testfälle für `xsi:type`, Reihenfolge, Sonderzeichen, Encoding oder PDF-Auswirkungen?
- Ist bei neuen Tarifen ein fachlich gültiger Versicherungsbeginn gesetzt?

### 9. Risiken und offene Punkte klassifizieren
Kennzeichne jeden Befund als:

- `belegt`
- `plausibel`
- `zu verifizieren`
- `Diskrepanz`
- `Empfehlung`

## Output-Format

```markdown
# BiPRO-Analyse

## 1. Kurzfazit

## 2. Betroffene Operation / Marke / Version

## 3. Fachlicher Kontext

## 4. Technischer Datenfluss

## 5. XSD / VU-Erweiterung

## 6. Internes Modell / DTO / Phasen

## 7. Mapping / Konverter

## 8. Tests / Roundtrip

## 9. Risiken und offene Punkte

## 10. Konkrete nächste Schritte
```

## Qualitätskriterien
- Keine Behauptung ohne Eingabe-, Code- oder Referenzbasis.
- XSD, Mapping, Konverter und Test werden getrennt bewertet.
- Provider-Modell wird explizit berücksichtigt.
- Fachlichkeit und Technik werden nicht vermischt.
- Offene Punkte werden sichtbar gemacht.

## Typische Fehler
- XSD-Änderung als vollständige Implementierung bewerten.
- Nach `getOffer()` als Java-Methode suchen.
- Eingabe-Mapping ergänzen, aber Ausgabe-Mapping vergessen.
- Konverter implementieren, aber nicht registrieren.
- Marke VBL/DOL oder gemeinsame Leben-XSD verwechseln.
