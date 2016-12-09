---
title: Apache Solr
---

# Apache Solr installieren

Das Installationsskript für OPUS 4 kann Apache Solr 5.3.1 automatisch 
herunterladen und das Installationsskript von Solr aufrufen.

Solr kann aber auch manuell zum Beispiel auf einem anderen System 
installiert werden. Mehr Informationen zu Solr und seiner Installation
finden sich auf der Homepage von [APACHE Solr][SOLRHOME]. 

Für OPUS 4 ist es nur wichtig, dass die Verbindungsdaten für den Solr
Server und den Core, der verwendet werden soll, in die 
Konfigurationsdatei eingetragen werden.

    application/configs/config.ini  
    
[SOLRHOME]: http://lucene.apache.org/solr/    