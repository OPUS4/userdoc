---
title: Vorausetzungen
weight: 10
---

# Voraussetzungen

Hier sind die grundlegenden Voraussetzungen für einen OPUS 4 Server und die Client-System beschrieben.

* [Server](#server)
* [Client](#client-browser)
{: class="navlist" }

## Server

Vor der Installation und den Betrieb von OPUS 4 muss das System einige Grundvoraussetzungen erfüllen.

<p class="note" markdown="1">
In der Entwicklung und im Hosting beim KOBV wird momentan [Ubuntu](http://www.ubuntu.com/) 14.04 LTS eingesetzt. Die
Informationen und Kommandos beziehen sich auf Ubuntu. OPUS sollte auch auf anderen gängigen Distribution funktionieren.
Dort sind aber unter Umständen andere Kommandos bzw. zusätzliche Installationsschritte notwendig.
</p>

* [Apache 2]({{ site.baseurl }}/installation/apache.html)
* [MySQL](https://www.mysql.com/) (mindestens Version 5.1)
* [PHP](http://php.net/) 5.5 (oder neuer)
* [Git](https://git-scm.com/)
* [cURL](https://curl.haxx.se/)
* [Solr][SOLR] 5.x
* [Java Runtime](#java-runtime) (mindestens 1.6)
* [Mailserver](#mailserver)

OPUS 4 funktioniert im allgemeinen auch mit älteren PHP Versionen ab 5.3 (mit "Multibyte-String"-Unterstützung). Es
wird aber empfohlen eine möglichst aktuelle Version von PHP zu verwenden, die immer noch gewartet und mit
Sicherheitsupdates versorgt wird. OPUS 4 funktioniert mit PHP 7. 

### PHP Pakete installieren

Für den Betrieb von OPUS sind einige zusätzliche PHP-Pakete notwendige. PHP und diese Pakete können unter Ubuntu
mit folgendem Kommando installiert werden.

    sudo apt-get install

Das Kommando muss mit folgenden Paketen aufgerufen werden.

|---|---|
| Paket | Hinweis |
|---|---|
| `php` | |
| `php-cli` | |
| `php-common` | |
| `php-curl` | |
| `php-gd` | |
| `php-log` | |
| `php-mbstring` | |
| `php-mcrypt` | |
| `php-mysql` | |
| `php-xsl` | |
| `php-zip` | |
| `libapache2-mod-php` | |
|------|
| Für die Entwicklung: |
|------|
| `php-dev` | |
|---|---|

<p class="note" markdown="1">
Die Namen der Pakete sind manchmal mit einer Versionsnummer versehen, 
z.B. `php7.0-xsl`. Unter Ubuntu 16 lässt sich z.B. PHP 7 oder PHP 5 
verwenden.
</p>

    $ sudo apt-get install php

<p class="warning" markdown="1">
Damit OPUS 4 fehlerfrei funktioniert, muss der Parameter
[allow_url_fopen](http://php.net/manual/en/filesystem.configuration.php) in der
[php.ini](http://php.net/manual/en/configuration.file.php) auf `1` gesetzt, also eingeschaltet sein. Das
ist in aktuellen PHP Versionen normalerweise der Fall.
</p>

<p class="warning" markdown="1">
Das Modul `php5-librdf` muss deaktiviert werden, da ansonsten der BibTeX-Export und die OAI-Schnittstelle nicht
funktionieren.
</p>

### Git installieren

Git wird für die Installation und später die Updates von OPUS 4 von GitHub benötigt. Es kann unter Ubuntu mit
folgendem Kommando installiert werden.

{% highlight bash %}
$ sudo apt-get install git
{% endhighlight %}

### cURL installieren

cURL wird unter anderem für die Installation zum Abruf verschiedener Pakete, wie z.b. composer.phar verwendet. Es kann unter Ubuntu mit
folgendem Kommando installiert werden.

{% highlight bash %}
$ sudo apt-get install curl
{% endhighlight %}

### Java Runtime

Um [Solr][SOLR] ausführen zu können, muss eine aktuelle Java Runtime Environment (JRE) installiert sein.
Unter Ubuntu kann z.B. [OpenJdk](http://openjdk.java.net/) verwendet werden.

    $ sudo apt-get install openjdk-7-jdk

<p class="note" markdown="1">
Java wird für den Betrieb von [Apache Solr][SOLR] benötigt. Abhängig von der Solr Version kann es unterschiedliche
Mindestanforderungen an das verwendete Java Runtime Environment geben. Siehe z.B.
[System Requirements for Solr 5.3.1](http://lucene.apache.org/solr/5_3_1/SYSTEM_REQUIREMENTS.html).
</p>

### Mailserver

Damit OPUS 4 Nachrichten an Autoren verschicken kann, z.B. wenn ihr Dokument freigeschaltet wird ist ein ein Mailserver
(SMTP) notwendig, der eingehende Mails von `localhost` (`127.0.0.1`) annehmen und weiterleiten kann. In den meisten
Fällen sollte die sogenannte "smarthost"-Konfiguration ausreichen

## Client (Browser)

OPUS 4 sollte mit allen aktuellen Browsern, wie z.B. Internet Explorer, Firefox, Chrome, und Opera, nutzbar sein.

### Cookies

<p class="warning">
OPUS ist nur sinnvoll zu benutzen, wenn im Webbrowser Cookies eingeschaltet sind. Sind
Cookies nicht erlaubt, so funktioniert der Login in die Administration nicht und der normale Anwender
kann ohne Cookies keine Dokumente über das Veröffentlichungsformular einstellen.
</p>

### Javascript

Manche Funktionen von OPUS benötigen Javascript, so zum Beispiel das Aus- und Einklappen der Zusammenfassungen in der
Frontdoor. Bisher ist Javascript für die Nutzung von OPUS 4 aber nicht zwingend notwendig.

<p class="note">
Die Abhängigkeit von Javascript in OPUS 4 wird zunehmen, da dadurch z.B. effizientere Eingabemethoden für Sammlungen
und andere Informationen umgesetzt werden können.
</p>

[SOLR]: http://lucene.apache.org/solr
