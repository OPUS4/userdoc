---
title: Apache Solr
weight: 120
---

# Apache Solr

<p class="note">
Für die Installation und den Betrieb von OPUS 4 wird Apache Solr benötigt!
</p>

Weitere Hinweise zum Apache Solr siehe unter: 
[Voraussetzungen]({{ site.baseurl }}/installation/requirements.html)

Die Verbindungsdaten des Solr Servers und der Core, der für OPUS 4 verwendet werden soll, müssen in der 
Konfigurationsdatei hinterlegt werden.

```
application/configs/config.ini
```
Dieses kann mit Hilfe des Installationsskriptes erfolgen:

[Installationsskript]({{ site.baseurl }}/installation/installscript.html)

In der Entwicklerdokumentation für OPUS 4 wird eine Variante für Ubuntu 16 
und Solr 7.7.1 beschrieben, um Apache Solr für OPUS 4 einzurichten.

* [APACHE Solr manuell vorbereiten][SOLRSETUP]
{: class="navlist" }   
    
[SOLRHOME]: http://lucene.apache.org/solr/
[SOLRSETUP]: http://www.opus-repository.org/devdoc/installation/solrsetupmanuell.html
