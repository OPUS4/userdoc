---
title: SWORD
---


# SWORD 

SWORD (Simple Web-service Offering Repository Deposit) ist eine webbasierte
Standard-Schnittstelle für Importe. OPUS 4.6 implementiert die SWORD-Schnittstelle in
Version 1.3. Die Details der Spezifikation sind unter folgender Adresse verfügbar:

<http://swordapp.org/sword-v1/>

SWORD ist normalerweise darauf ausgelegt, mit jedem Request nur *ein* Dokument zu
verarbeiten. Die Antworten der Schnittstelle beziehen sich gemäß der Spezifikation auf
einzelne Dokumente. Die SWORD-Schnittstelle von OPUS 4 importiert darüber hinaus auch
Pakete mit **mehreren** Dokumenten.  

<p class="info">
Es gibt momentan keine Pläne, den Funktionsumfang höherer SWORD-Versionen für OPUS 4
umzusetzen. Die Import-Funktionen an sich werden weiter ausgebaut werden, um mehr
Metadaten einfacher verarbeiten zu können, zum Beispiel Verknüpfungen mit
Klassifikationssystemen usw.
</p>


## Datenstruktur und Pakete

OPUS 4 unterstützt den Import von Metadaten und Volltexten als **\*.zip**- oder
**\*.tar**-Paket. Ein ZIP-/TAR-Paket kann die Metadaten und Dateien für mehr als 
ein Dokument enthalten.

    import.zip
      |-opus.xml
      |-document1.pdf
      |-document1.doc
      |-fulltext2.pdf
      |-image3.png


### Metadaten

Die Metadaten müssen in OPUS-XML gemäß dem Import-Schema vorliegen
([s. Import](index.html)). Die Metadatendatei muss `opus.xml` heißen, ansonsten
wird sie vom System nicht erkannt und der Import schlägt fehlt. `opus.xml` kann
die Metadaten für ein oder mehrere Dokumente enthalten. 

### Volltexte

In den Metadaten müssen die Dokumente mit den Dateien über das *<files*>-Element
explizit verknüpft werden. Es findet keine automatische Zuordnung anhand der
Namen statt. 

``` xml
<files>
    <file name="document1.pdf" />
    <file name="document1.doc" />
</files>
```

Enthält die Datei `opus.xml` nur die Metadaten für ein einziges Dokument, werden 
automatisch alle anderen Dateien diesem Dokument hinzugefügt, unabhängig davon, 
ob sie im `files`-Element deklariert wurden.

### Unterverzeichnisse 

Der Import unterstützt auch eine Paketstruktur, bei der die Dateien der Dokumente in 
separaten Verzeichnissen gespeichert werden, um Konflikte durch identische Dateinamen 
zu vermeiden.

    import.tar
      |-opus.xml
      |-doc1
      |   |-article.pdf
      |   |-image.png
      |-doc2
          |-article.pdf
          |-article.doc
          
In diesem Fall müssen die Dateien in den Metadaten explizit deklariert werden. Es reicht 
nicht, das Verzeichnis mit den Dateien für ein Dokument anzugeben.

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


## Konfiguration

Die importierten Dokumente werden mit einer konfigurierbaren Sammlung verknüpft, um sie 
zusätzlich zu markieren. Die Sammlung heißt normalerweise "Import" und ist Teil der 
CollectionRole "Import". Beide werden bei der Installation bzw. beim Update von OPUS 4 
automatisch angelegt. Die Sammlung ist in der `application.ini` über den Parameter

sword.collection.default.number = 'import'

definiert und kann in der `configuration.ini` auf eine andere Sammlung innerhalb der 
CollectionRole "Import" umgestellt werden. Es ist die *Nummer* der gewünschten
Sammlung anzugeben (nicht der Name).

Ob die Konfiguration der Sammlung richtig ist, lässt sich im SWORD-Servicedokument
feststellen. Es kann unter der URL

    https://user:password@[OPUS4-Servername]/[OPUS4-Instanz]/sword/servicedocument

aufgerufen werden. 

Auf eine korrekte Konfiguration weist insbesondere das *href*-Attribut im
Collection-Tag mit der URL der Sammlung hin:

``` xml
<service>
    …
    <workspace>
        …
        <collection href="https:// [OPUS4-Servername]/[OPUS4-Instanz]/sword/index/index/Import/[Collection-Nummer]">
            <atom:title>sword</atom:title>
            …
```

Ist die Konfiguration falsch, fehlen das *href*-Attribut sowie das folgende 
*<atom:title>*-Tag:

``` xml
<service>
    …
    <workspace>
        …
        <collection>
            …
```
    
Die Angabe der Sammlung unter `<collection href="...">` ist insofern falsch, als dass
hier gemäß SWORD-Spezifikation eigentlich die Deposit-Adresse stehen müsse. In 
OPUS 4 ist die Deposit-URL:
`https://user:password@[OPUS4-Servername]/[OPUS4-Instanz]/sword/deposit`

Die weiteren Parameter zur SWORD-Schnittstelle in den Konfigurationsdateien sind weniger
relevant. Sie dienen überwiegend dazu, beschreibende Angaben zu machen, die dann z.B.
im Servicedokument angezeigt werden. Diese Angaben sind hilfreich, wenn die Schnittstelle
nach außen geöffnet ist und Externe Inhalte in das Repositorium einbringen.





## Beispiel-Skripte

Ein Beispiel für ein Bash-Skript mit eingebetteten XSLT-Skripten für das Format NISO
JATS findet sich [hier](nisojats.html).
