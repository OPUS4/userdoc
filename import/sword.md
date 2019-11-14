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

In den Metadaten müssen die Dokumente mit den Dateien über das `<files>`-Element
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
ob sie im `<files>`-Element deklariert wurden.

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
    <!-- Datei wird unter dem Namen 'article.pdf' importiert -->
    <file path="doc1/article.pdf" />
</files>
```

oder

``` xml
<files basedir="doc1">
    <!-- Datei wird unter dem Namen 'article.pdf' importiert -->
    <file path="article.pdf" />
</files>
```

oder

``` xml
<files>
    <!-- Datei wird unter dem Namen 'article-original.doc' importiert -->
    <file path="doc1/article.doc" name="article-original.doc" />
</files>
```


## Zugriffssteuerung

Man benötigt einen Nutzer in OPUS, der berechtigt ist, auf das Modul "sword" 
zuzugreifen. Aus Sicherheitsgründen sollte man ein separates Nutzerkonto anlegen,
das nur Zugriff auf das SWORD-Modul hat. Username und Passwort dieses Accounts 
werden dann für das Login gebraucht. Der Zugriff auf die SWORD-Schnittstelle erfolgt
über HTTP Basic Authentication, d.h. konkret, dass man Username und Passwort auch
an Externe geben können muss, wenn Datenlieferanten wie z.B. das
[DeepGreen-Projekt](https://deepgreen.kobv.de) Dokumente nach OPUS importieren
sollen.

Es ist es sinnvoll, für jeden Datenlieferanten einen eigenen Account einzurichten.
Dies ist nicht nur sicherer, sondern erleichtert es später auch festzustellen, woher
ein Dokument gekommen ist. 

<p class="warning">
Der Verbindung zum Server sollte über HTTPS erfolgen, damit der Nutzername und das 
Passwort nicht unverschlüsselt übertragen werden. 
</p> 


## Konfiguration

Die importierten Dokumente werden mit einer konfigurierbaren Sammlung verknüpft, um sie 
zusätzlich zu markieren. Die Sammlung heißt normalerweise "Import" und ist Teil der 
CollectionRole "Import". Beide werden bei der Installation bzw. beim Update von OPUS 4 
automatisch angelegt. Die Sammlung ist in der `application.ini` über den Parameter

sword.collection.default.number = 'import'

definiert und kann in der `config.ini` auf eine andere Sammlung innerhalb der 
CollectionRole "Import" umgestellt werden. Es ist die *Nummer* der gewünschten
Sammlung anzugeben (nicht der Name).

Ob die Konfiguration der Sammlung richtig ist, lässt sich im SWORD-Servicedokument
feststellen. Es kann mit dem Login des SWORD-Accounts (s. vorherigen Abschnitt) unter
der URL

    https://user:password@[OPUS4-Servername]/[OPUS4-Instanz]/sword/servicedocument

aufgerufen werden. 

Auf eine korrekte Konfiguration weist insbesondere das `href`-Attribut im
Collection-Tag mit der URL der Sammlung[^1] hin:

``` xml
<service>
    …
    <workspace>
        …
        <collection href="https:// [OPUS4-Servername]/[OPUS4-Instanz]/sword/index/index/Import/[Collection-Nummer]">
            <atom:title>sword</atom:title>
            …
```
*[^1]: Bitte beachten Sie, dass dies nicht die Deposit-Adresse ist. Diese lautet in OPUS 4:  
    `https://user:password@[OPUS4-Servername]/[OPUS4-Instanz]/sword/deposit`*

Ist die Konfiguration falsch, fehlen das `href`-Attribut sowie das folgende 
`<atom:title>`-Tag:

``` xml
<service>
    …
    <workspace>
        …
        <collection>
            …
```
    
Die weiteren Parameter zur SWORD-Schnittstelle in den Konfigurationsdateien dienen
überwiegend dazu, beschreibende Angaben zu machen, die dann z.B.im Servicedokument
angezeigt werden. Diese Angaben können hilfreich sein, um externen Datenlieferanten
Informationen zur Konfiguration der Schnittstelle mitzuteilen. Die Bedeutung
der beschreibenden Angaben ist in der Spezifikation von SWORD 1.3 erläutert
(s. Link oben auf dieser Seite).


## SWORD-Import mit cURL

Es gibt keinen Standard-Client für den Zugriff auf die SWORD-Schnittstelle. Ohne zusätzlichen Aufwand lässt sie sich auf Kommandozeilenebene mit dem Tool cURL ansprechen, das sowohl unter Linux als auch Windows 10 standardmäßig vorhanden ist. Auch andere Tools wie z.B. die API-Entwicklungsplattform Postman eignen sich gut.
 
Beim Aufruf von cURL sind mindestens diese Parameter anzugeben:
* MIME-Type der zu importierenden Paket-Datei (`application/tar` oder `application/zip`)
* Pfad zur Paket-Datei (mit führendem `@`-Zeichen)
* Username und Passwort des SWORD-Accounts in OPUS
* Deposit-URL der SWORD-Schnittstelle

Darüber hinaus empfiehlt es sich, auch den Parameter `--verbose` zu setzen, um aussagekräftigere Rückmeldungen der Schnittstelle in der Kommandozeile und im Logfile zu erhalten. Die Protokollierung erfolgt im Standard-OPUS-Logfile.

Die Syntax lautet:

`curl --verbose --header "Content-Type: [MIME-Type]" --data-binary "@[Pfad zur Paket-Datei]" -u "[Username]:[Passwort]" "https:// [OPUS4-Servername]/[OPUS4-Instanz]/sword/deposit"`

Also z.B.:

`curl --verbose --header "Content-Type: application/zip" --data-binary "@/verzeichnis/sword-import-paket.zip" -u "username:passwort" "https://meinbeipielserver.de/opus-instanz/sword/deposit"`

Der Import hat funktioniert, wenn auf der Kommandozeile keine Fehlermeldung zurückgeliefert wird. Im OPUS-Logfile findet sich für jedes erfolgreich importierte Dokument der Eintrag `... OK` sowie abschließend eine zusammenfassende Meldung in der Form `Import finished successfully.` *N* `documents were imported.`

In den über SWORD importierten Dokumenten werden Informationen in folgenden Enrichment-Feldern abgelegt:
- opus.import.user : [user]
- opus.import.date : [import date]
- opus.import.file : [name of package]

Es ist darauf zu achten, dass diese EnrichmentKeys existieren.


## Beispiel-Skripte für NISO JATS

Ein Beispiel für ein Bash-Skript mit eingebetteten XSLT-Skripten zur Konversion und zum Import von Daten für das Format NISO JATS findet sich [hier](jats.html).
