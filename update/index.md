---
title: Update
weight: 35
---

# Update

Ab der OPUS Version 4.5 wird `OPUS als Git-Version` angeboten und die Aktualisierung des OPUS-Codes erfolgt mit `Git-Kommandos` (ein Tarball steht nicht mehr zur Verfügung).
Die Aktualisierung der `Datenbank` erfolgt anschließend mit einem `Update-Script`.

<p class="note" markdown="1">
Um eine OPUS Instanz mit Git aktualisieren zu können, muss die [Instanz mit Git installiert][INSTALL] worden sein.
</p>

[INSTALL]: ../installation/index.md


## Aktualisierung des OPUS-Codes auf eine neue Version

**Vor Beginn eines jeden Updates sicherheitshalber ein Backup der Instanz inklusive Datenbank durchführen!**

1.) Git Status überprüfen und ggf. lokale Änderungen übernehmen und ausstehende Commits durchführen

{% highlight bash %}
git status
git add ...
git commit -m "<commit message>" <DATEI>
{% endhighlight %}

2.) Software von GitHub aktualisieren
{% highlight bash %}
git pull
{% endhighlight %}

3.)  Git Status überprüfen
{% highlight bash %}
git status
{% endhighlight %}

4.) Konflikte auflösen (mit `meld` oder ähnliches)
{% highlight bash %}
meld <DATEINAME>
git add <DATEINAME>
git commit -am "<commit message>"
{% endhighlight %}

5.) Update Composer-Pakete
{% highlight bash %}
php composer.phar update
{% endhighlight %}

6.) Aktualisierung der Datenbank und Anpassungen an den Daten
{% highlight bash %}
bin/update.sh
{% endhighlight %}


## Spezielle Hinweise zu den Versionen

* [OPUS 4.7 Update](update47.html)
* [OPUS 4.6 Update](update46.html)
* [OPUS 4.5 Update](update45.html)
* [Update von 4.4.5 auf Git-Version](from445.html)
* [Migration von OPUS 3](../migration.html)
{: class="navlist" }

## Update von OPUS 4 vor Version 4.4.5

OPUS 4 Repositorien, die eine ältere Version als 4.4.5 verwenden, sollten zuerst auf 4.4.5 aktualisiert werden. Dafür
kann der [4.4.5 Tarball][OPUS445] und die Anleitung in der [PDF Dokumentation][OPUS445DOC] verwendet werden. Dadurch
wird die Datenbank auf den neuesten Stand gebracht und der Umstieg auf die Installation mit Git wird einfacher.

[OPUS445]: http://www.kobv.de/entwicklung/software/opus-4/download/
[OPUS445DOC]: http://www.kobv.de/entwicklung/software/opus-4/dokumentation/







