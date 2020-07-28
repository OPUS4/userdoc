---
title: Suche
--- 

# Solr-Verbindung

OPUS4 benutzt für die Suche und das Browsing Apache Solr, das lokal installiert sein muss. Die
Standardwerte der Solr-Parameter für den Index (`searchengine.index`) und für die Textextraktion
(`searchengine.extract`) werden im Kapitel 'Installation und Konfiguration des Solr-Servers<!--TODO-->'
erläutert. Wird für Index und Textextraktion der gleiche Solr-Server benutzt, müssen auch für beide
Bereiche die gleichen Parameter eingetragen werden.

{% highlight ini %}
; OPUS4 uses a solr server for search and browsing.
; the solr server can be run on the same system or on a different host.
; Please enter the credentials to connect to your solr server.
; SEARCH ENGINE SETTINGS
searchengine.index.host =
searchengine.index.port =
searchengine.index.app =

; The text extraction can be run on a different solr server than the metadata indexer.
; You can also use the same solr server, in this case you have to enter
; the same credetials as above.
searchengine.extract.host =
searchengine.extract.port =
searchengine.extract.app =
{% endhighlight %}

<p class="warning" markdown="1">
Die alten Konfigurationsparameter funktionierten weiterhin, so daß existierdene `config.ini` Dateien auch mit
OPUS 4.5 verwendet werden können. Die Kompatibilität zu den alten Parametern könnte in Zukunft abgeschaltet werden.
Bei der Installation einer neuen Instanz werden die neuen Parameter verwendet.
</p>

## Neue Konfigurationsparameter

Die folgenden Parameter ersetzen die alten bekannten Parameter beschrieben oben. Der Service **default** setzt
dabei die Parameter für alle Verbindungen, sofern nichts für die anderen Services angegeben ist. Der Service
**extract** wird definiert die Verbindung für die Extraktion von Volltexten.

{% highlight ini %}
; Default connection parameters for indexing and searching
searchengine.solr.default.service.default.endpoint.localhost.host =
searchengine.solr.default.service.default.endpoint.localhost.port =
searchengine.solr.default.service.default.endpoint.localhost.path =

; Connection parameters used for extraction (if different from default)
searchengine.solr.default.service.extract.endpoint.localhost.host =
searchengine.solr.default.service.extract.endpoint.localhost.port =
searchengine.solr.default.service.extract.endpoint.localhost.path =
{% endhighlight %}

Die Verbindungen für die Suche bzw. die Indizierung können auch explizit gesetzt werden.

{% highlight ini %}
searchengine.solr.default.service.index.endpoint.localhost.host =
searchengine.solr.default.service.index.endpoint.localhost.port =
searchengine.solr.default.service.index.endpoint.localhost.path =

searchengine.solr.default.service.search.endpoint.localhost.host =
searchengine.solr.default.service.search.endpoint.localhost.port =
searchengine.solr.default.service.search.endpoint.localhost.path =
{% endhighlight %}

### Unterstützte Services

|Service | Beschreibung |
|--------|------|
| default | Standardverbindung für alle Services |
| index | Verbindung für Indizierung |
| extract | Verbindung für die Extraktion von Volltexten |
| search | Verbindung für die Suchfunktionen |

# Solr-Schema

Für einige Änderungen im Verhalten von OPUS 4 müssen Anpassungen in der
Datei `schema.xml` vorgenommen werden, die Teil der Solr-Konfiguration 
für den Suchindex einer Instanz ist.

## Anzeige von Dokumenten ohne Titel in Suchergebnissen

Mit dem ausgelieferten Solr-Schema für OPUS 4 werden Dokumente ohne 
Titel immer am Ende der Suchergebnisse angezeigt, wenn nach Titel 
sortiert wird. 

Um das Verhalten zu ändern, so dass Dokumente ohne Titel am Anfang bzw. am Ende 
angezeigt werden, je nach Sortierrichtung, muss im Schema für den 
Feldtypen (fieldType) `alphaOnlySort` der Wert von `sortMissingLast` 
auf `false` gesetzt werden. 

{% highlight xml %}
<fieldType name="alphaOnlySort" class="solr.TextField" 
    sortMissingLast="false" omitNorms="true">
{% endhighlight %}

Der Feldtyp wird für die Titel und die Autoren verwendet.

## Anpassung des XSLT für die Indizierung

Mit OPUS 4.7 liegt die Datei `solr.xslt` im Composer-Package `opus4-repo/search`. 

    vendor/opus4-repo/search/src/Solr/Document/solr.xslt

Um Anpassungen an der Indizierung vorzunehmen, sollte die Datei and folgende Stelle kopiert werden.

    $BASEDIR/application/configs/solr/solr.xslt
    
Die Kopie der Datei kann dann angepasst werden. Nach einem Update müssen in diesem Fall Änderungen an der Defaultdatei
manuell übernommen werden. Damit die angepasst Datei verwendet wird muss folgender Eintrag zur `config.ini` hinzugefügt 
werden. 

    searchengine.solr.default.service.default.xsltfile = APPLICATION_PATH "/application/configs/solr/solr.xslt"
    
<p class="warning">
Anpassungen am XSLTs sollten mit Bedacht vorgenommen werden. Es ist möglich, dass die Indizierung mit kommenden 
Releases verändert wird und lokale Anpassungen müssen beim Update dann mit der Standardversion immer wieder in 
Einklang gebracht werden. Es sollte überlegt werden, ob die lokalen Anpassungen von Interesse für die OPUS 4 
Community sein könnten und in den Standard aufgenommen werden sollten. Dazu können auf GitHub Pull Requests und
Issues angelegt werden.  
</p>


