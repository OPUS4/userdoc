---
title: Voraussetzungen
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
In der Entwicklung und im Hosting beim KOBV wird momentan [Ubuntu](http://www.ubuntu.com/) 20.04 LTS eingesetzt. Die
Informationen und Kommandos beziehen sich auf Ubuntu. OPUS sollte auch auf anderen gängigen Distribution funktionieren.
Dort sind aber unter Umständen andere Kommandos bzw. zusätzliche Installationsschritte notwendig.
</p>

* [Apache 2]({{ site.baseurl }}/installation/apache.html)
* [MySQL](https://www.mysql.com/) (mindestens Version 5.6)
* [PHP](http://php.net/) 7.1
* [Git](https://git-scm.com/)
* [cURL](https://curl.haxx.se/)
* [SOLR](https://solr.apache.org/) 7.x
* [Java Runtime](#java-runtime) (mindestens 1.8)
* [Mailserver](#mailserver)
* [Pandoc](#pandoc)

Es wird empfohlen, eine möglichst aktuelle Version von PHP zu verwenden, die immer noch gewartet und mit
Sicherheitsupdates versorgt wird. OPUS 4 funktioniert derzeit bis PHP Version 7.1 


### PHP Pakete installieren

<p class="warning" markdown="1">
Ubuntu 20 kommt standardmäßig mit PHP Version 7.2. OPUS 4 verwendet momentan noch Zend Framework 1 und ist damit leider nicht kompatibel zu PHP 7.2 und neuer.
Daher muss derzeit bei Verwendung von Ubuntu 20 ein Downgrade der PHP-Version auf die Version 7.1 erfolgen.
Die Pakete für PHP 7.1 sind unter dem Repository ppa:ondrej/php verfügbar (siehe weiteres Software-Repository einbinden).

Die PHP Version 7.2 für OPUS 4 kann nach dem Umbau des Zendframeworks genutzt werden.
Achten Sie dafür auf die aktuelle Entwicklung von OPUS 4.
</p>

Für den Betrieb von OPUS 4 sind einige zusätzliche PHP-Pakete notwendig. PHP und diese Pakete können unter Ubuntu
mit folgendem Kommando installiert werden.

{% highlight bash %}
$ sudo apt-get install
{% endhighlight %}

Das Kommando muss mit folgenden Paketen aufgerufen werden.

|---|---|
| Paket | Hinweis |
|---|---|
| `php` | |
| `php-cli` | |
| `php-common` | |
| `php-curl` | |
| `php-gd` | |
| `php-intl` | |
| `php-log` | |
| `php-mbstring` | |
| `php-mcrypt` | |
| `php-mysql` | |
| `php-xsl` bzw. php-xml | |
| `php-zip` | |
| `libapache2-mod-php` | |
| `libapache2-mod-xsendfile` | |
| `libxml2-utils` | 
|------|
| Für die Entwicklung: |
|------|
| `php-dev` | |
|---|---|

Weiteres Software-Repository einbinden

{% highlight bash %}
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository ppa:ondrej/php
$ sudo apt-get update
{% endhighlight %}

<p class="note" markdown="1">
Die Namen der Pakete sind mitunter mit einer Versionsnummer versehen. Für die PHP-Version 7.1 z.B. `php7.1-curl`. 
</p>

{% highlight bash %}
$ sudo apt-get install php7.1-curl
{% endhighlight %}

<p class="warning" markdown="1">
Damit OPUS 4 fehlerfrei funktioniert, muss der Parameter
[allow_url_fopen](http://php.net/manual/en/filesystem.configuration.php) in der
[php.ini](http://php.net/manual/en/configuration.file.php) auf `1` gesetzt, also eingeschaltet sein. Das
ist in aktuellen PHP Versionen normalerweise der Fall.
</p>

<p class="warning" markdown="1">
Das Modul `php-librdf` muss deaktiviert werden, da ansonsten der BibTeX-Export und die OAI-Schnittstelle nicht
funktionieren.
</p>

### Git installieren

Git wird für die Installation und später die Updates von OPUS 4 von GitHub benötigt. Es kann unter Ubuntu mit
folgendem Kommando installiert werden.

{% highlight bash %}
$ sudo apt-get install git
{% endhighlight %}

### cURL installieren

cURL wird unter anderem für die Installation zum Abruf verschiedener Pakete verwendet, wie z.b. composer.phar. Es kann unter Ubuntu mit
folgendem Kommando installiert werden.

{% highlight bash %}
$ sudo apt-get install curl
{% endhighlight %}

### Java Runtime

Um [Solr][SOLR] ausführen zu können, muss eine aktuelle Java Runtime Environment (JRE) installiert sein.
Unter Ubuntu kann z.B. [OpenJdk](http://openjdk.java.net/) verwendet werden.

{% highlight bash %}
$ sudo apt-get install openjdk-8-jdk
{% endhighlight %}

<p class="note" markdown="1">
Java wird für den Betrieb von [Apache Solr][SOLR] benötigt. Abhängig von der Solr Version kann es unterschiedliche
Mindestanforderungen an das verwendete Java Runtime Environment geben. Siehe z.B.
[System Requirements for Solr 7.7.2](https://solr.apache.org/docs/7_7_2/SYSTEM_REQUIREMENTS.html).
</p>

### Mailserver

Damit OPUS 4 Nachrichten an Autoren verschicken kann, z.B. wenn ihr Dokument freigeschaltet wird, ist ein ein Mailserver
(SMTP) notwendig, der eingehende Mails von `localhost` (`127.0.0.1`) annehmen und weiterleiten kann. In den meisten
Fällen sollte die sogenannte "smarthost"-Konfiguration ausreichen


### Pandoc

Zur Verarbeitung von Sonderzeichen beim BibTeX-Import wird vom OPUS 4 BibTeX-Parser das Tool `Pandoc` benötigt.
Es ist mindestens die Version 2.17. erforderlich. Es kann unter Ubuntu mit folgendem Kommando installiert werden.

{% highlight bash %}
$ sudo apt-get install pandoc
{% endhighlight %}

Installierte Version von Pandoc überprüfen:

{% highlight bash %}
$ pandoc -v
{% endhighlight %}

Die neueste Version von Pandoc ist unter `https://github.com/jgm/pandoc/releases` zu finden.



## Client (Browser)

OPUS 4 sollte mit allen aktuellen Browsern, wie z.B. Microsoft Edge, Firefox, Chrome und Opera, nutzbar sein.

### Cookies

<p class="warning">
OPUS 4 ist nur sinnvoll zu benutzen, wenn im Webbrowser Cookies eingeschaltet sind. Sind
Cookies nicht erlaubt, so funktioniert der Login in die Administration nicht und der normale Anwender
kann ohne Cookies keine Dokumente über das Veröffentlichungsformular einstellen.
</p>

### Javascript

Manche Funktionen von OPUS 4 benötigen Javascript, so zum Beispiel das Aus- und Einklappen der Zusammenfassungen in der
Frontdoor. Bisher ist Javascript für die Nutzung von OPUS 4 aber nicht zwingend notwendig.

<p class="note">
Die Abhängigkeit von Javascript in OPUS 4 wird zunehmen, da dadurch z.B. effizientere Eingabemethoden für Sammlungen
und andere Informationen umgesetzt werden können.
</p>
