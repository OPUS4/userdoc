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


