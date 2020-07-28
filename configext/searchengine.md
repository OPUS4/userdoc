---
title: Solr-Schema
--- 

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


