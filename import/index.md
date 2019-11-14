---
title: Import
weight: 65
---

# Import

OPUS unterstützt folgende Import-Verfahren:

* Import von Metadaten auf Kommandozeilenebene
* Import von Metadaten und Volltextdateien in gepackter Form über eine SWORD-Schnittstelle (Simple Webservice Offering Repository Deposit).

Für beide Verfahren gilt, dass die Metadaten in OPUS-XML gemäß dem Import-Schema vorliegen müssen:
<br />
<http://www.opus-repository.org/schema/opus-import.xsd>

Metadaten in OPUS 4-Import-XML haben folgende Struktur:

``` xml
<import>
    <opusDocument language="deu" type="article">
        <titlesMain>
            <titleMain language="deu">Beispiel Titel</titleMain>
        </titlesMain>
        <persons>
            <person role="author" firstName="Erika" lastName="Musterfrau">
                <identifiers>
                    <identifier type="orcid">0000:...</identifier>
                </identifiers>
            </person>
        </persons>
    </opusDocument>
</import>
```

<p class="note" markdown="1">
Das Import-XML wird noch weiter entwickelt, um die Verwendung zu vereinfachen. Es können 
zum Beispiel bereits Verknüpfungen zu Sammlungen importiert werden, aber dafür ist die 
interne Datenbank-ID der Sammlung notwendig. Klassifikationen werden in OPUS 4 zum Beispiel 
als Sammlungen verwaltet. Um das Dokument mit einem Eintrag der DDC zu verknüpfen, benötigt 
man eine Nummer wie **16728** und diese kann in jedem Repository unterschiedlich sein. 
<br />
Es ist geplant, für Klassifikationen allgemeinverständliche Angaben zu unterstützen, mit 
denen dann zum Beispiel der Typ **DDC** und der Identifier **345** angegeben werden können. 
</p>
