---
title: Enrichments
weight: 40
---

# Enrichment als Facette

Enrichments werden automatisch indiziert (seit OPUS 4.7). Sie werden nicht für die einfache Suche verwendet. Um 
ein Enrichment als Facette in der Suchanzeige verwenden zu können, muss es in der Konfiguration (`config.ini`)
als Facette konfiguriert werden.

Der Name einer Enrichment-Facette entspricht dem Namen des Enrichments mit dem Präfix `enrichment_`, also z.B.
`enrichment_Event` für das Enrichment `Event` oder `enrichment_open.source` für `opus.source`. 

{% highlight ini %}
searchengine.solr.facets = author_facet,year,doctype,language,enrichment_opus.source,enrichment_Event
{% endhighlight %}

Als Überschrift für die Facette wird automatisch die Übersetzung des Enrichments verwendet. Um die Übersetzung
anzupassen kann die Option __heading__ für die Facette konfiguriert werden. Im folgenden Beispiel wird der 
Übersetzungsschlüssel `EnrichmentOpusSource` für die Überschrift der `opus.source`-Facette verwendet.
 
{% highlight ini %}
search.facet.enrichment_opus-source.heading = 'EnrichmentOpusSource'
{% endhighlight %}

## Enrichments mit Punkt im Namen

Die Namen von Enrichments erlauben Punkte ("."), z.B. in `opus.source`. Das führt aktuell zu Problemen bei der 
Verwendung des Names in der `config.ini`-Datei. Für die Konfiguration einer Enrichment-Facette, muss deshalb der 
Punkt (".") durch einen Bindestrich ("-") ersetzt werden. 

In der Liste der anzuzeigenden Facetten (`searchengine.solr.facets`) muss der normale Name verwendet werden.



