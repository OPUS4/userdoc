---
title: Apache Webserver
weight: 100
---

# Apache Webserver

Es wird empfohlen Apache 2.4 oder neuer zu verwenden.

## Installation

Mit folgendem Kommando kann Apache 2 auf einem Ubuntu System installiert werden.

{% highlight bash %}
$ sudo apt-get install apache2
{% endhighlight %}

## Konfiguration

Ein Konfigurationdatei, z.B. `opus4.conf`, könnte wie folgt
aussehen.

{% highlight bash %}
AllowEncodedSlashes On

Alias /opus4 "/var/local/opus4/public"

<Directory "/var/local/opus4/public">
  Options FollowSymLinks
  AllowOverride All
  Require local
  RewriteEngine on
  LogLevel rewrite:info
</Directory>
{% endhighlight %}

Diese Datei kann in das Verzeichnis `/etc/apache2/sites-available` kopiert und mit folgendem Kommando aktiviert werden.

{% highlight bash %}
$ sudo a2ensite opus4
{% endhighlight %}

Anschließend muss Apache neu gestartet werden.

{% highlight bash %}
$ sudo service apache2 restart
{% endhighlight %}
