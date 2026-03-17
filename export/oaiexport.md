---
title: OAI Export
weight: 40
---

# OAI Export

Über die OAI-Schnittstelle (Open Archives Initiative) können Metadaten sowie Volltexte aus dem Repositorium von externen Harvestern abgerufen werden, wie z.B. durch die DNB oder von der Suchmaschine BASE.
OPUS 4 unterstützt die Formate EPICUR, XMetaDissPlus, OAI-DC und MARC-21.

Die Parameter für die OAI-Schnittstelle werden in der `config.ini`-Datei im Abschnitt `OAI Settings` eingetragen.

~~~ ini
; OAI SETTINGS
oai.baseurl =
oai.repository.name = Opus4 Demo Instance
oai.repository.identifier = opus4.demo
oai.sample.identifier = oai:opus4.demo:90
~~~

Bei dem Parameter `oai.baseurl` wird die URL eingetragen, unter der die OAI-Schnittstelle
erreichbar ist. Diese wird in der Schnittstelle unter `<baseURL>` angezeigt und normalerweise
automatisch auf den Hostnamen der Opus-Instanz gesetzt. Sie sollte daher nur geändert werden,
falls eine abweichende URL Verwendung findet (z.B. bei Rechnern, die mehrere DNS-Einträge
besitzen). Der Parameter `oai.repository.name` wird in der OAI-Schnittstelle unter
`<repositoryName>` und der Parameter `oai.repository.identifier` unter `<repositoryIdentifier>` angezeigt. Bei
`oai.sample.identifier` kann ein existierendes Dokument eingetragen werden, das in der
Schnittstelle unter `<sampleIdentifier>` (d.h. Beispiel-Dokument) angezeigt wird.

Darüber hinaus existieren in der `application.ini`-Datei weitere OAI-Parameter, die bei der Installation
teilweise mit Standardwerten befüllt werden und nur in Ausnahmefällen anzupassen sind. Beispiele dafür
sind die Parameter `oai.max.listrecords` (Anzahl der Einträge für das Kommando `ListRecords`) und 
`oai.max.listidentifiers` (Anzahl der Einträge für das Kommando `ListIdentifiers`).

## Konfiguration der OAI-Formate

Die Daten aus OPUS 4 können in unterschiedlichen Formaten mithilfe eines Arguments – dem Metadatenpräfix – in der 
Protokollanforderung `GetRecord` oder `ListRecords` abgerufen werden.

Die Formatvorlagen für die spezifischen Präfixe liegen im 
Verzeichnis `$BASEDIR/modules/oai/views/scripts/index/prefixes/`.
Als Administrator haben Sie unter dem Menüpunkt `Administration > Systeminformationen > OAI-Links` die Möglichkeit zu 
überprüfen, wie die Daten in den einzelnen Formaten übergeben werden.

Welche Formate verfügbar sind, wird in der Konfiguration definiert. Momentan befindet sich diese Konfiguration in
`application/configs/application.ini`.

~~~ ini
oai.format.default.class = Oai_Model_DefaultServer
oai.format.default.viewHelper = optionValue, fileUrl, frontdoorUrl, transferUrl, dcmiType, dcType, openAireType

oai.format.copy_xml.xsltFile = copy_xml.xslt

oai.format.epicur.class = Oai_Model_Prefix_EpicurServer
oai.format.marc21.class = Oai_Model_Prefix_MarcXmlServer
oai.format.oai_dc.class = Oai_Model_Prefix_OaiDcServer
oai.format.oai_pp.class = Oai_Model_Prefix_OaiPpServer
oai.format.xmetadissplus.class = Oai_Model_Prefix_XmetaDissPlusServer
~~~

Einzelne Formate können auskommentiert werden, um sie aus der Schnittstelle zu entfernen. Sie tauchen dann auch 
nicht mehr unter `ListMetadataFormats` auf. 

Der Metädatenpräfix wird vom Namen für ein Format in der Konfiguration bestimmt, es sei denn ein `prefixLabel`
wird definiert.

    oai.format.NAME.class =
    oai.format.NAME.prefixLabel = 

    oai.format.xmetadissplus.class = Oai_Model_Prefix_XmetaDissPlusServer
    oai.format.xmetadissplus.prefixLabel = xMetaDissPlus 

Um die Defaultkonfiguration eines Formats zu verändern, können weitere Optionen angegeben werden.

### Allgemeine Optionen für OAI-Format-Klassen

| Option                | Beschreibung                                                                                     |
|-----------------------|--------------------------------------------------------------------------------------------------|
| class                 | PHP Klasse für Handling Requests                                                                 |
| prefixLabel           | Metadata-Präfix (z.B. `xMetaDissPlus`)                                                           |
| xsltFile              | Pfad zu XSLT-Datei für Format                                                                    |
| schemaUrl             | XSD-Schema URL für Format (z.B. `http://files.dnb.de/standards/xmetadissplus/xmetadissplus.xsd`) |
| metadataNamespaceUrl  | Namespace-URl für Format (z.B. `http://www.d-nb.de/standards/xmetadissplus/`)                    |
| visible               | Sichtbarkeit in OAI-Schnittstelle                                                                |
| hasFilesVisibleInOai  | Berücksichtige nur Dokumente mit Volltext, wenn TRUE                                             |
| checkEmbargo          | Berücksichtige Embargo-Datum, wenn TRUE                                                          |
| notEmbargoedOn        | Berücksichtige Embarg-Datum, wenn TRUE (Momentan redundant zu checkEmbargo)                      |
| identifierExists      | Identifier-Typ, der vorhanden sein muss, damit eine Dokument berücksichtig wird (z.B. `urn`)     |

Mit der `xsltFile` Option lässt sich ein eigenes angepasstes Stylesheet konfigurieren. Momentan kann natürlich auch 
direkt die eigentliche XSLT Datei editiert werden. In zukünftigen Version von OPUS 4 könnte die Datei aber in ein 
separates Composer-Paket **opus4-marcxml** ausgelagert werden. Es ist das Ziel der Entwicklung die einzelnen Formate
völlig unabhängig voneinander zu machen und das Hinzufügen neuer Formate durch installierbare Pakete zu ermöglichen.  

~~~ ini
oai.format.marc21.class = Oai_Model_Prefix_MarcXmlServer
oai.format.marc21.xsltFile = APPLICATION_PATH "/application/configs/oai/mymarc21.xslt"
~~~

## Standard-Formate

### Format EPICUR

Das Format `EPICUR` beinhaltet die Transfersyntax, um einen Metadatensatz mit der URN und der entsprechenden URL zu harvesten.
Durch den Abruf der Daten mit dem Präfix `EPICUR` holt sich die DNB die Informationen zu den vergegeben URNs und registriert diese bei sich.

### Format OAI-DC

Das Format `oai_dc` ist das simpelste Format für den Abruf der Daten über die OAI-Schnittstelle. Für den Austausch von Daten wurde das Format Dublin Core mit einem Kernsatz von Metadaten geschaffen.
Siehe <https://de.wikipedia.org/wiki/Dublin_Core>.
Die Suchmaschine BASE und auch OpenAIRE verwenden diesen Präfix.

### Format XMetaDissPlus

`XMetaDissPlus (XMDP)` ist ein Metadatenstandard zur Beschreibung von Online-Hochschulschriften sowie weiteren Publikationstypen.
Mit dem Format XMetaDissPlus holt sich die DNB die Metadaten sowie die Volltexte aus dem Repositorium und speichert diese als Kopie in ihrer Datenbank.
Folgende zwei Vorteile bietet die Ablieferung mit XMetadissPlus:
1. Die Pflichtexemplare werden an die DNB automatisch auf elektronischem Wege geliefert und
2. die Dokumente gelangen in die Langzeitarchivierung der DNB.

Die Repositorien, die ihre Daten auf diesem Wege an die DNB liefern möchten, müssen bestimmte Pflichtmetadaten erfassen und sich an die entsprechenden Konventionen halten.

Alle Elemente von XMetaDissPlus finden Sie unter
<https://www.dnb.de/SharedDocs/Downloads/DE/Professionell/Standardisierung/xmdpSchema24.zip?__blob=publicationFile&v=5>

Wichtige Elemente von XMetaDissPlus sind:

`<dc:publisher>` - Pflichtelement bei allen Publikationstypen und wird vom Metadatenfeld "Titel veröffentlichende Institution" gespeist.

`<thesis:grantor>` - Pflichtelement bei allen Hochschulschriften und wird vom Metadatenfeld "Titel verleihende Institution" gespeist.

`<dc:creator>` - In der Regel ist dies der Autor bzw. die Autorin. Bei der Erfassung sollte der Vor- und Nachname angegeben werden.

~~~ xml
z.B.
<dc:creator xsi:type="pc:MetaPers" >
<pc:person>
<pc:name type="nameUsedByThePerson" >
<pc:foreName>Max H.</pc:foreName>
<pc:surName>Mustermann</pc:surName>
</pc:name>
<pc:academicTitle>Dipl.-Ing</pc:academicTitle>
</pc:person>
</dc:creator>
~~~

<p class="note" markdown="1">
In manchen Kulturkreisen kann die Namensbezeichnung für Personen auch nur aus einem Namen bestehen.
Ebenso bei Künstlernamen oder Persönlichkeiten aus anderen Epochen (z.B. bei Digitalisaten) kann es vorkommen, dass der Name nur aus einem s.g. "Givenname" besteht.
Wenn kein Vorname zur Namensbezeichnung zugehörig ist, dann muss der Eintrag ins Metadatenfeld "Nachname" erfolgen, damit dies mit XMetaDissPlus korrekt übergeben wird.
</p>

~~~ xml
z.B.
<dc:creator xsi:type="pc:MetaPers">
<pc:person>
<pc:name type="otherName">
<pc:personEnteredUnderGivenName>Origenes
</pc:personEnteredUnderGivenName>
</pc:name>
</pc:person>
</dc:creator>
~~~

`<dcterms:isPartOf>` - Pflichtelement für alle periodischen Veröffentlichungen beim Dokumenttyp "PeriodicalPart", wie z.B. Jahrbücher, Amtsblätter etc. Dieses Element erwartet als Attribute `<ZSTitelID>` und `<ZS-Ausgabe>`. In der OPUS-Standardauslieferung können diese Angaben mit der Zuordnung zu einer Schriftenreihe und einer Bandnummer 
übergeben werden. Im Attribut "ddb:ZSTitelID" erscheint dann die ID der Schriftenreihe, über welche die DNB den Bezug zum Dokument herstellt.

~~~ xml
z.B.
<dcterms:isPartOf xsi:type="ddb:ZSTitelID" >250</dcterms:isPartOf>
<dcterms:isPartOf xsi:type="ddb:ZS-Ausgabe" >2020</dcterms:isPartOf> 
~~~

### Format MARC21

`MARC21` ist eine Version von MARC (MAchine-Readable Cataloging) und wird vor allem in Bibliothekskatalogen für Bibliografische Daten verwendet. Siehe "Deutsche Übersetzung des  MARC 21 Format for Bibliographic Data" <https://d-nb.info/996983511/34>.
Für den Abruf der Daten über die OAI-Schnittstelle mit dem Präfix `marc21` können noch zusätzliche Angaben in der `config.ini`-Datei konfiguriert werden, die noch nicht in der Datenbank stehen.

~~~ ini
; MARC21 XML EXPORT
; used to set MARC field 003
marc21.isil= <ISIL der Bibliothek eingeben>
; default value used to set subfield a of MARC field 264
marc21.publisherCity= <Ist nur erforderlich, wenn kein DNB-Institut angelegt ist>
; default value used to set subfield b of MARC field 264
marc21.publisherName= <Ist nur erforderlich, wenn kein DNB-Institut angelegt ist>
~~~

## OAI-Sets

Die verfügbaren OAI-Sets werden von mehreren Klassen generiert.

~~~ ini
oai.set.bibliography.class = Oai_Model_Set_BibliographySets
oai.set.doc-type.class = Oai_Model_Set_DocumentTypeSets
oai.set.publicationState.class = Oai_Model_Set_PublicationStateSets
oai.set.openaccess.class = Oai_Model_Set_CollectionRoleSingleSet
oai.set.openaccess.roleOaiName = open_access
oai.set.openaccess.requireOaiSubset = 0

; The order is important, the collection set type must come last.
oai.set.collection.class = Oai_Model_Set_CollectionSets
; TODO Excluding subsets is currently not supported.
oai.set.collection.exclude = open_access
~~~

In der Konfiguration wird ein Name für jeden Set-Typ verwendet, der beliebig gewählt werden kann.

    oai.set.NAME.class = KLASSE_DIE_SETS_IMPLEMENTIERT

### Oai_Model_Set_CollectionRoleSingleSet

Die Klasse `Oai_Model_Set_CollectionRoleSingleSet` erlaubt es alle verknüpften Dokumente einer CollectionRole
in einem einzigen Set auszugeben, egal mit welcher Sammlung in der CollectionRole die Dokumente verknüpft sind.
Das ist nützlich, wenn z.B. für verschiedene Open Access-Typen separate Sammlungen angelegt wurden. 

Eine CollectionRole, die **CollectionRoleSingleSet** verwendet, muss von der normalen Behandlung von Sammlung mit
`Oai_Model_Set_CollectionSets` ausgeschlossen werden. 
