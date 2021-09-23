---
title: OAI Export
---

# OAI Export

Über die OAI-Schnittstelle (Open Archives Initiative) können Metadaten sowie Volltexte aus dem Repositorium von externen Harvestern abgerufen werden, wie z.B. durch die DNB oder von der Suchmaschine BASE.
OPUS 4 unterstützt die Formate EPICUR, XMetaDissPlus, OAI-DC und MARC-21.

Die Parameter für die OAI-Schnittstelle werden in der `config.ini`-Datei im Abschnitt `OAI Settings` eingetragen.


{% highlight ini %}
; OAI SETTINGS
oai.baseurl =
oai.repository.name = Opus4 Demo Instance
oai.repository.identifier = opus4.demo
oai.sample.identifier = oai:opus4.demo:90
{% endhighlight %}

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

## OAI-Formate
Die Daten aus OPUS 4 können in unterschiedlichen Formaten mithilfe eines Arguments – dem Metadatenpräfix – in der Protokollanforderung `GetRecord` oder `ListRecords` abgerufen werden.
Die Formatvorlagen für die spezifischen Präfixe liegen im Verzeichnis `$BASEDIR/modules/oai/views/scripts/index/prefixes/`.
Als Administrator haben Sie unter dem Menüpunkt `Administration > Systeminformationen > OAI-Links` die Möglichkeit zu überprüfen,
wie die Daten in den einzelnen Formaten übergeben werden.

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

{% highlight ini %}
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
{% endhighlight %}

<p class="note" markdown="1">
In manchen Kulturkreisen kann die Namensbezeichnung für Personen auch nur aus einem Namen bestehen.
Ebenso bei Künstlernamen oder Persönlichkeiten aus anderen Epochen (z.B. bei Digitalisaten) kann es vorkommen, dass der Name nur aus einem s.g. "Givenname" besteht.
Wenn kein Vorname zur Namensbezeichnung zugehörig ist, dann muss der Eintrag ins Metadatenfeld "Nachname" erfolgen, damit dies mit XMetaDissPlus korrekt übergeben wird.
</p>

{% highlight ini %}
z.B.
<dc:creator xsi:type="pc:MetaPers">
<pc:person>
<pc:name type="otherName">
<pc:personEnteredUnderGivenName>Origenes
</pc:personEnteredUnderGivenName>
</pc:name>
</pc:person>
</dc:creator>
{% endhighlight %}

`<dcterms:isPartOf>` - Pflichtelement für alle periodischen Veröffentlichungen, wie z.B. Jahrbücher, Amtsblätter etc. Dieses Element erwartet als Attribute die Angabe einer Schriftenreihe und einer Bandnummer,
die dann als `<ZSTitelID>` und als `<ZS-Ausgabe>` übergeben werden.
{% highlight ini %}
z.B.
<dcterms:isPartOf xsi:type="ddb:ZSTitelID" >250</dcterms:isPartOf>
<dcterms:isPartOf xsi:type="ddb:ZS-Ausgabe" >2020</dcterms:isPartOf> 
{% endhighlight %}

### Format MARC21
`MARC21` ist eine Version von MARC (MAchine-Readable Cataloging) und wird vor allem in Bibliothekskatalogen für Bibliografische Daten verwendet. Siehe "Deutsche Übersetzung des  MARC 21 Format for Bibliographic Data" <https://d-nb.info/996983511/34>.
Für den Abruf der Daten über die OAI-Schnittstelle mit dem Präfix `marc21` können noch zusätzliche Angaben in der `config.ini`-Datei konfiguriert werden, die noch nicht in der Datenbank stehen.
{% highlight ini %}
; MARC21 XML EXPORT
; used to set MARC field 003
marc21.isil= <ISIL der Bibliothek eingeben>
; default value used to set subfield a of MARC field 264
marc21.publisherCity= <Ist nur erforderlich, wenn kein DNB-Institut angelegt ist>
; default value used to set subfield b of MARC field 264
marc21.publisherName=
{% endhighlight %}