---
title: Installation
weight: 30
---

# Installation

Die Dateien von OPUS 4 werden seit Version 4.5-RC1 mit Hilfe von Git 
Kommandos installiert und aktualisiert. Git ist ein Werkzeug, das in 
der Softwareentwicklung eingetzt wird, um unterschiedliche Versionen 
einer Software verwalten und synchronisieren zu können.

<p class="note">
Die folgende Anleitung bezieht sich auf ein Ubuntu System. Momentan ist 
Ubuntu auch das einzige Linux, das vom Installationsskript direkt 
unterstützt wird. OPUS 4 kann aber auch mit anderen Distributionen 
betrieben werden, indem die einzelne Schritte der Installation manuell 
ausgeführt werden.
</p>

## Voraussetzungen

Bevor OPUS 4 installiert werden kann, müssen einige Voraussetzungen 
erfüllt sein.

* [Git](requirements.html#git-installieren)
* [cURL](requirements.html#curl-installieren)
* [PHP](requirements.html#php-pakete-installieren)
* [Java](requirements.html#java-runtime) 
* [Apache 2](apache.html)
* [MySQL](database.html)
* [Apache Solr](solr.html)
* [Mailserver](requirements.html#mailserver)
* [Pandoc](requirements.html#pandoc)
{: class="navlist" }

## Git clone

Um mit Git eine neue OPUS 4 Instanz einzurichten, wird zuerst eine lokale Kopie der
Dateien ("Clone") angelegt.

{% highlight bash %}
$ git clone https://github.com/opus4/application opus4
$ cd opus4
{% endhighlight %}

Durch die Kommando wir das Verzeichnis `opus4` mit allen Dateien aus
dem Git-Repository von OPUS 4 angelegt. Nun kann das Installationsskript
ausgeführt werden.

<p class="info">
Das lokale Repository ist eine vollständige Kopie. Das heißt, die bisherigen
Änderungen und Branches sind ebenfalls lokal verfügbar.
</p>

## Installationsskript ausführen

Im `bin`-Verzeichnis liegt ein Installationsskript mit dem die nächsten Schritte
durchgeführt werden können.

{% highlight bash %}
$ sudo bin/install.sh
{% endhighlight %}

Während der Installation werden einige Informationen abgefragt. Das Skript
erzeugt auf dieser Basis die notwendigen Konfigurationsdateien für OPUS 4.

* [Installationsskript](installscript.html)
{: class="navlist" } 

## Webserver neustarten
 
Nach der Installation muss zum Schluss der Webserver neu gestartet 
werden. Das Installationsskript fordert dazu auf bzw. kann den Neustart
auch direkt ausführen.

Unter Ubuntu kann der Webserver z.B. mit folgendem Kommando neu gestartet 
werden:

{% highlight bash %}
$  sudo systemctl reload apache2
{% endhighlight %}

Anschließend sollte OPUS 4 lokal unter folgender URL verfügbar sein.

```
http://localhost/opus4
```

Die URL ist abhängig von der Webserver-Konfiguration und von den Werten, die 
bei der Installation angegeben wurden.





