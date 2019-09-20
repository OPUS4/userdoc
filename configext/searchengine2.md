---
title: Solr-Anpassung für Facette Jahr
--- 

# Solr-Anpassung für Facette Jahr

Mit OPUS 4.7 liegt die Datei `solr.xslt` im Composer-Package `opus4-repo/search`. 

    vendor/opus4-repo/search/src/Solr/Document/solr.xslt

Um Anpassungen an der Indizierung vorzunehmen, sollte die Datei and folgende Stelle kopiert werden.

    $BASEDIR/application/configs/solr/solr.xslt
    
Die Kopie der Datei kann dann angepasst werden. Nach einem Update müssen in diesem Fall Änderungen an der Defaultdatei
manuell übernommen werden. Damit die angepasst Datei verwendet wird muss folgender Eintrag zur `config.ini` hinzugefügt 
werden. 

    ; searchengine.solr.default.service.default.xsltfile = APPLICATION_PATH "/application/configs/solr/solr.xslt"

## Datumsfelder für die Facette Erscheinungsjahr

Für die Facette "Erscheinungsjahr" (year) wird die Jahresangabe im Feld "Datum der Erstveröffentlichung" (PublishedDate)
verwendet. Wenn dieses nicht vorhanden ist, kommt das Feld "Jahr der Erstveröffentlichung" (PublishedYear) zum Einsatz.
Alternativ dazu besteht die Möglichkeit, die Indexierung der Jahresfacette individuell zu konfigurieren und dafür z.B. 
das Datumsfeld "Jahr der Fertigstellung" (CompletedDate) zu verwenden.

{% highlight xml %}
<!-- year -->
<xsl:variable name="year">
    <xsl:attribute name="name">year</xsl:attribute>
    <xsl:value-of select="/Opus/Opus_Document/@CompletedYear" />
</xsl:variable>
{% endhighlight %}
                


