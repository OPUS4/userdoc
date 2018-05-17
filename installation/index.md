---
title: Installation
weight: 30
---

# Installation

Die Dateien von OPUS 4 werden seit Version 4.5-RC1 mit Hilfe von Git 
Kommandos installiert und aktualisiert. Git ist ein Werkzeug, dass in 
der Softwareentwicklung eingetzt wird, um unterschiedliche Versionen 
einer Software verwalten und synchronisieren zu können.

<p class="note">
Die folgende Anleitung bezieht sich auf ein Ubuntu System. Momentan ist 
Ubuntu auch das einzige Linux, das vom Installationsskript direkt 
unterstützt wird. OPUS 4.5 kann aber auch mit anderen Distributionen 
betrieben werden, indem die einzelne Schritte der Installation manuell 
ausgeführt werden.
</p>

## Voraussetzungen

Bevor OPUS 4 installiert werden kann müssen einige Voraussetzungen 
erfüllt sein.

* [Git](requirements.html#git-installieren)
* [cURL](requirements.html#curl-installieren)
* [PHP](requirements.html#php-pakete-installieren)
* [Java](requirements.html#java-runtime) 
* [Apache 2](apache.html)
* [MySQL](database.html)
* [Apache Solr](solr.html)
{: class="navlist" }

## Git clone

Um mit Git eine neue OPUS 4 Instanz einzurichten muss zuerst eine lokale Kopie der
Dateien, ein Klone, angelegt werden.

    $ git clone https://github.com/opus4/application opus4
    $ cd opus4
    
Durch die Kommando wir das Verzeichnis `opus4` mit allen Dateien aus
dem Git-Repository von OPUS 4 angelegt. Nun kann das Installationsskript
ausgeführt werden.

<p class="info">
Das lokale Repository ist eine vollständige Kopie. Das heißt die bisherigen
Änderungen und Branches sind ebenfalls lokal verfügbar.
</p>

## Installationsskript ausführen

Im `bin`-Verzeichnis liegt ein Installationsskript mit dem die nächsten Schritte
durchgeführt werden können.

    $ sudo bin/install.sh

Während der Installation werden einige Informationen abgefragt. Optional wird ein
Apache Solr Server installiert. Falls aber Solr bereits vorhanden ist können auch
einfach nur die entsprechenden Verbinungsparameter angegeben werden. Das Skript
erzeugt dann die notwendigen Konfigurationsdateien für OPUS 4.

* [Installationsskript](installscript.html)
{: class="navlist" } 

## Webserver neustarten
 
Nach der Installation muss zum Schluss der Webserver neu gestartet 
werden. Das Installationsskript fordert dazu auf bzw. kann den Neustart
auch direkt ausführen.
 
Unter Ubuntu kann der Webserver mit folgendem Kommando neu gestartet 
werden.

    $ sudo service apache2 restart
    
Anschließend sollte OPUS 4 lokal unter folgender URL verfügbar sein.

    http://localhost/opus4

Die URL kann anders sein, wenn während der Installation die 
Standardwerte modifiziert wurden.





