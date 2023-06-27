--- 
title: Benutzerdefinierte Felder (Enrichments)
weight: 95
---

# Benutzerdefinierte Felder (Enrichments)

Es gibt in OPUS4 die Möglichkeit, benutzerdefinierte Felder (EnrichmentKeys) anzulegen, um
Informationen zu Dokumenten zu erfassen, die nicht durch Standardfelder abgedeckt sind. Hierzu
werden die benutzerdefinierten Felder zunächst in der Administration (Administration >
Oberflächenanpassungen > Benutzerdefinierte Felder (Enrichments)) angelegt, indem nach einem
Klick auf "Neuer EnrichmentKey" der gewünschte Feldname eingetragen wird (z.B. "Lom_Wert")."
Das so angelegte benutzerdefinierte Feld kann nun in den gewünschten Dokumenttypen verwendet
werden. Wie diese Felder in den Dokumenttyp aufgenommen werden ist in der Konfiguration
beschrieben.

* [Einfache Textfelder neu anlegen](../translation/fields.html#einfache-textfelder-neu-anlegen)
* [Select-Felder neu anlegen](../translation/fields.html#select-felder-neu-anlegen)

Es werden ab der Version 4.2 auch einige EnrichmentKeys mitausgeliefert:

Die folgenden Felder sind nur systemintern von Bedeutung und können daher ignoriert werden:

    submitter.user_id
    reviewer.user_id
    review.rejected_by
    review.accepted_by

## Enrichment-Typen

Enrichments kann ein Typ zugewiesen werden. Der Typ erlaubt es ein für Eingabe passendes  
Formularelement zu verwenden und eine Validierung der Werte durchzuführen.

| Typ | Beschreibung |
|-----+--------------|    
| `Boolean`  | Ja/Nein-Feld, das als Checkbox angezeigt wird. |
| `RegEx`    | Eingabefeld, dessen Wert mit einem regulären Ausdruck validiert wird. |
| `Select`   | Liste von vorgegebenen Werten. |
| `Text`     | Einfaches Eingabefeld. (__default__) |
| `TextArea` | Mehrzeiliges Eingabefeld. | 

<p class="info">
Die Verwendung des Enrichment-Typ ist bisher nur in der Administration umgesetzt. Im 
Publish-Modul wird diese Information bisher nicht verwendet.
</p>

### Validierung von Enrichments

Die Validierung von Eingaben betrifft in erster Linie die Typen `RegEx` und `Select`. In der Konfiguration eines
Enrichment kann ausgewählt werden, ob die Validierung strikt erfolgen soll. Das heißt, ob bereits in der Datenbank
gespeicherte Werte auch validiert werden sollen. In diesem Fall werden keine ungültigen Werte beim Speichern 
eines Dokuments akzeptiert. Diese Funktionalität ist notwendig, um zum Beispiel nach einer Änderung der Liste für 
ein Select-Feld entscheiden zu können, ob alte, nicht mehr gültige Werte weiterhin gespeichert bleiben dürfen oder 
ob sie beim Editieren eines Dokuments aktualisiert werden müssen. 

### __RegEx__-Enrichments

Enrichments vom Typ `RegEx` sind Eingabefelder dessen Werte anhand eines regulären Ausdrucks geprüft werden. Der
Ausdruck folgt den Regeln für [PCRE Patterns](https://www.php.net/manual/en/pcre.pattern.php) und kann konfiguriert
werden. Neu eingegebene Werte müssen dem Pattern entsprechen. 

### __Select__-Enrichments

Enrichments vom Typ `Select` werden als Select-Feld angezeigt. Die möglichen Werte können in der Konfiguration des
Enrichments definiert werden.
    
## Felder für die Migration von OPUS 3    

Darüber hinaus werden bei der Migration von OPUS 3 auf OPUS 4 bereits benutzerdefinierte Felder
angelegt, die bestimmte individuelle Inhalte aus OPUS 3 erfassen:

| Key | Beschreibung |
|-----+--------------|
| BemerkungExtern | Hierhin werden Bemerkungen aus OPUS3 migriert, die eine Darstellung von HTML-Code auf der Frontdoor benötigen (OPUS4 erlaubt aus Sicherheitsgründen kein HTML in den Eingabefeldern) |
| ClassRvk | Opus4 enthält keine RVK-Klassifikation, die Opus3-RVK-Klasse wird in dieses Feld migriert |
| ContributorsName | In Opus3 befinden sich bei Abschlussarbeiten die Namen sämtlicher Betreuer in einem Feld. Es existieren keine einheitlichen Separatoren zwischen den Namen, was beim Aufsplitten zu Fehlern führen kann. Aus dem Grund werden die Betreuer nochmal als Ganzes eingelesen, umsie später korrigieren zu können. |
| InvalidVerification | Dieser Schlüssel wird bei der Migration angelegt, wenn die E-Mail-Adresse des Submitters nicht Zend-Valide ist |
| SourceTitle | Enthält die komplette bibliografische Angaben zur Zweitpublikationen eines Opus3-Dokuments |
| SourceSwb | Die SWB-Ident-Nummer wird in dieses Feld eingetragen, da sie in Opus4 nicht geführt wird. |
| SubjectUncontrolledGerman, SubjectUncontrolledEnglish, SubjectSwd | Diese Felder sind der Tatsache geschuldet, dass die Schlagwörter teilweise gemischte Syntax haben und in OPUS3 nur ein Feld ausgegeben wird. Bei der Migration werden die Schlagwörter in separate Felder aufgesplittet, was mitunter zu falschen Konstellationen führt. Aus dem Grund werden die Schlagwörter |

Diese benutzerdefinierten Felder sind geschützt und nur für die Instanzen verwendbar, die von
OPUS3 migriert wurden. In neu installierten OPUS4 Instanzen können diese Felder nicht verwendet
werden.

## Felder für die Funktion "DOI-Import"

Für den "DOI-Import" (ab Version 4.8.1) werden einige Enrichment-Felder benötigt. Diese werden bei Neuinstallationen automatisch angelegt. 

`ConferencePlace` und `ConferenceTitle` Enthalten "Ort der Konferenz" und "Name der Konferenz"; v.a. für den Dokumenttyp conferenceobject relevant.

`opus_crossrefLicence` Enthält die Lizenz, die in Crossref angegeben ist (User-relevant, da die OPUS-Lizenz u.U. entsprechend einzutragen ist).

`opus_crossrefDocumentType` Enthält nach dem Import den Dokumenttyp, der in Crossref angegeben ist (kann User-relevant sein, zwecks Nachvollziehbarkeit des Mappings).

`opus_import_origin`  Enthält die Quelle des DOI-Imports, z.Zt. immer "crossref" (evtl. User-relevant, z.B. als Facette)

### Weitere Felder, die nur systemintern von Bedeutung sind:

`opus_import_data` Enthält nach dem DOI-Import die kompletten Metadaten des Dokuments von Crossref.

`opus_doiImportPopulated` Enthält eine Liste der Felder, die mittels DOI-Import befüllt wurden (kommasepariert).

`opus_doi_flag` Enthält 'true', wenn ein DOI-Import erfolgreich durchgeführt wurde, d.h. alle verfügbaren Metadaten ins Formular eingetragen wurden.

 
