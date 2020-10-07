---
title: Solr-Verbindung
weight: 10
--- 

# Solr-Verbindung

OPUS4 benutzt für die Suche und das Browsing Apache Solr, das lokal installiert sein muss. Die
Standardwerte der Solr-Parameter für den Index (`searchengine.index`) und für die Textextraktion
(`searchengine.extract`) werden auf der Seite [Apache Solr installieren](../installation/solr.html)
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
Die alten Konfigurationsparameter funktionierten weiterhin, so daß existierende `config.ini` Dateien auch mit
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

### Timeouts bei der Extraction/Indexierung

Bei sehr grossen Dateien kann es bei der Volltextextraktion zu Timeouts kommen. Die Timeouts
lassen sich konfigurieren. 

{% highlight ini %}
searchengine.solr.default.service.default.endpoint.localhost.timeout = 10
searchengine.solr.default.service.extract.endpoint.localhost.timeout = 10
{% endhighlight %}

Die Extraktion dauert wesentlich länger als die Indexierung. Daher wird ein Volltextcache
verwendet, der verhindert, dass die Dateien bei jeder Indexierung erneut extrahiert werden müssen.
Das hilft natürlich nicht bei der Indexierung von neu hinzugefügten Dokumenten, z.B. im 
Publish-Modul.

Um bei einer Neuindexierung mit `SolrIndexBuilder.php` keine Probleme mit Timeouts zu haben, 
können dieser für die Skripte auch komplett abgeschaltet werden in dem man die entsprechenden
Einträge zur Datei {{console.ini}} hinzufügt. Für den normalen Betrieb gelten dann immer noch
die Einstellungen aus der {{config.ini}} bzw. 5 Sekunden als Defaultwert.

{% highlight ini %}
searchengine.solr.default.service.default.endpoint.localhost.timeout = 0
searchengine.solr.default.service.extract.endpoint.localhost.timeout = 0
{% endhighlight %}

Um Problem mit Timeouts im Betrieb, bei der Anzeige von Webseiten nach der Indexierung eines
Dokuments zu vermeiden, kann die [asynchrone Indexierung](../config/jobs.html) verwendet werden.

