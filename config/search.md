---
title: Search
---

# Search Engine

OPUS4 benutzt für die Suche und das Browsing Apache Solr, das lokal installiert sein muss. Die
Standardwerte der Solr-Parameter für den Index ( searchengine.index ) und für die Textextraktion
( searchengine.extract ) werden im Kapitel 'Installation und Konfiguration des Solr-Servers 44 '
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


