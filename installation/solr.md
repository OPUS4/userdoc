---
title: Apache Solr
---

# Apache Solr installieren

Das Installationsskript für OPUS 4 kann Apache Solr 7.7.1 automatisch 
herunterladen und das Installationsskript von Solr aufrufen.

Solr kann aber auch manuell zum Beispiel auf einem anderen System 
installiert werden. Mehr Informationen zu Solr und seiner Installation
finden sich auf der Homepage von [APACHE Solr][SOLRHOME]. 

Für OPUS 4 ist es nur wichtig, dass die Verbindungsdaten für den Solr
Server und den Core, der verwendet werden soll, in die 
Konfigurationsdatei eingetragen werden.

    application/configs/config.ini
    
# Apache Solr konfigurieren

Für den Betrieb von OPUS 4 wird ein Solr Core benötigt. Es gibt mehrere
Wege Solr für OPUS 4 vorzubereiten. In der Entwicklerdokumentation für
OPUS 4 wird eine Variante für Ubuntu 16 und Solr 7.7.1 beschrieben.

* [APACHE Solr manuell vorbereiten][SOLRSETUP]
{: class="navlist" }   
    
[SOLRHOME]: http://lucene.apache.org/solr/
[SOLRSETUP]: http://www.opus-repository.org/devdoc/installation/solrsetupmanuell.html
                 
     