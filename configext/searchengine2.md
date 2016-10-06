---
title: Solr-Anpassung für Facette Jahr
--- 

# Solr-Anpassung für Facette Jahr

Für einige Änderungen im Verhalten von OPUS 4 müssen Anpassungen in der
Datei `$BASEDIR/application/configs/solr/solr.xslt` vorgenommen werden, die Teil der Solr-Konfiguration 
für den Suchindex einer Instanz ist.

## Datumsfelder für die Facette Erscheinungsjahr

Für die Facette "Erscheinungsjahr" (year) wird die Jahresangabe im Feld "Datum der Erstveröffentlichung" (PublishedDate) verwendet. 
Wenn dieses nicht vorhanden ist, kommt das Feld "Jahr der Erstveröffentlichung" (PublishedYear) zum Einsatz. Alternativ dazu besteht die 
Möglichkeit, die Indexierung der Jahresfacette individuell zu konfigurieren und dafür z.B. das Datumsfeld "Jahr der Fertigstellung" 
(CompletedDate) zu verwenden.

{% highlight xml %}
<!-- year -->
<xsl:variable name="year">
    <xsl:attribute name="name">year</xsl:attribute>
    <xsl:value-of select="/Opus/Opus_Document/@CompletedYear" />
</xsl:variable>
{% endhighlight %}
                


