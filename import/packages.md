---
title: OPUS 4 Pakete
---

# OPUS 4 Pakete

OPUS 4 unterstützt den Import von Metadaten und Volltexten als **\*.zip** oder **\*.tar** Paket.
Diese Pakete müssen die Datei `opus.xml` mit den Metadaten enthalten.

    import.zip
      |-opus.xml
      |-document1.pdf
      |-document1.doc
      |-fulltext2.pdf
      |-image3.png

## Metadaten

Die Metadaten müssen dem Import Schema entsprechen. Die Datei `opus.xml` kann die Metadaten für mehrere
Dokumente enthalten.

<http://www.opus-repository.org/schema/opus-import.xsd>

OPUS 4 Import XML sieht wie folgt aus.

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
Das Import XML wird noch weiter entwickelt, um die Verwendung zu vereinfachen. Es können zum Beispiel bereits 
Verknüpfungen zu Sammlungen importiert werden, aber dafür ist die interne Datenbank-ID der Sammlung notwendig. 
Klassifikationen werden in OPUS 4 zum Beispiel als Sammlungen verwaltet. Um das Dokument mit einem Eintrag der
DDC zu verknüpfen benötigt man eine Nummer wie **16728** und diese kann in jedem Repository unterschiedlich
sein.
<br />
Es ist geplant zum Beispiel für Klassifikationen allgemeinverständliche Angaben zu unterstützen, wo dann
zum Beispiel der Typ **DDC** und der Identifier **345** angegeben werden können.
</p>

## Volltexte importieren

In den Metadaten müssen die Dokumente mit den Dateien verknüpft werden. Es findet keine automatische Zuordnung
anhand der Namen statt.

``` xml
<files>
    <file name="document1.pdf" />
    <file name="document1.doc" />
</files>
```

Enthält die Datei `opus.xml` nur die Metadaten für ein einziges Dokument, werden automatisch alle anderen Dateien
zu diesem Dokument hinzugefügt, unabhängig davon ob sie im `files`-Element deklariert wurden.

Der Import unterstützt auch eine Paketstruktur bei der die Dateien der Dokumente in separaten Verzeichnissen
gespeichert werden, um Konflikte durch identische Dateinamen zu vermeiden.

    import.tar
      |-opus.xml
      |-doc1
      |   |-article.pdf
      |   |-image.png
      |-doc2
          |-article.pdf
          |-article.doc
          
In diesem Fall müssen die Dateien in den Metadaten explizit deklariert werden. Es reicht nicht das Verzeichnis mit
den Dateien für ein Dokument anzugeben.

``` xml
<files>
    <!-- Datei wird mit Namen 'article.pdf' hinzufügen -->
    <file path="doc1/article.pdf" />
</files>
```

oder

``` xml
<files basedir="doc1">
    <!-- Datei wird mit Namen 'article.pdf' hinzufügen -->
    <file path="article.pdf" />
</files>
```

oder

``` xml
<files>
    <!-- Datei wird mit Namen 'article-original.doc' hinzufügen -->
    <file path="doc1/article.doc" name="article-original.doc" />
</files>
```
