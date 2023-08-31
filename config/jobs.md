---
title: Job Ausführung
---

# Job Ausführung

Es ist möglich, in OPUS4 bestimmte lang laufende Jobs (z.B. die Indexierung großer Dokumente)
asynchron zu verarbeiten. Auf diese Weise können Timeouts (weiße Seite) vermieden werden. Die
asynchrone Verarbeitung nutzt den Mechanismus des Unix cron-Daemon, der die zeitbasierte
Ausführung von Prozessen und wiederkehrende Aufgaben in sogenannten Cron-Jobs automatisiert.
Die Aktivierung der asynchronen Jobverarbeitung wird im Folgenden beschrieben.

<p class="warning">
Beim Aktivieren der asynchronen Jobverarbeitung ist zu beachten, dass die Änderungen im
System immer mit einer Verzögerung eintreten. So werden beispielsweise Änderungen
an Dokumenten erst über die Suche auffindbar, wenn die Solr-Indexierung erfolgt ist. In der
Zwischenzeit befindet sich der Solr-Index in einem inkonsistenten Zustand.
</p>

<p class="warning">
Achtung: Die Aktivierung erfolgt global für alle asynchronen Jobs (derzeit Solr-Indexierung, Mail-
Versand und Löschen temporärer Dokumente).
</p>

<p class="info" markdown="1">
Für OPUS 4.8.1 und PHP 8.1 wurde ein neues System für die Verarbeitung von Jobs entwickelt, das
die Konfiguration und Entwicklung vereinfachen soll. [Mehr Informationen](#neue-jobverarbeitung-mit-crunz) 
dazu weiter unten. Die alten Skripte können vorerst unverändert weiter genutzt werden.
</p>

## Erstellen von Cron-Jobs auf dem Server

Im Verzeichnis `$BASEDIR/scripts/cron` existiert jeweils ein PHP-Skript für jeden Job. Diese
Skripte werden dem Shell-Skript `cron-php-runner.sh` als Argument übergeben. Als weiteres
Argument muss das Verzeichnis für die lock-Datei angegeben werden, mit der die mehrfache,
parallele Ausführung desselben Skripts verhindert wird. Als optionales Argument kann ein Log-
Verzeichnis angegeben werden. Wird es nicht angegeben, dann erfolgt die Ausgabe des Skripts
direkt auf der Kommandozeile. Für die Ausführung als Cron-Job wird die Angabe des Log-
Verzeichnisses empfohlen. Eine Information über fehlgeschlagene Jobs kann auch in der
Administration unter "System Informationen" eingesehen werden.

<p class="warning">
Wird für einen der implementierten Verarbeitungsmechanismen kein Cron-Job angelegt, führt
das zu einem fehlerhaften Verhalten des Systems, weil die entsprechenden Jobs dann nicht
verarbeitet werden.
</p>

Zur Zeit ist die asynchrone Verarbeitung der Solr-Indexierung, des Mail-Versands und für das
Löschen temporärer Dokumente implementiert. Sie können folgendermaßen aufgerufen werden:

### Solr-Indexierung

{% highlight shell %}
$ cd $BASEDIR/scripts/cron
$ cron-php-runner.sh cron-solr-update.php /somepath/lock/ /somepath/log/
{% endhighlight %}

Ein Cron-Job (hier als Beispiel für die Ausführung alle 5 Minuten) wird wie folgt angelegt:

{% highlight shell %}
$ crontab –e 5 * * * *
    $BASEDIR/scripts/cron/cron-php-runner.sh
    $BASEDIR/scripts/cron/cron-solr-update.php
    $BASEDIR/workspace/lock
    $BASEDIR/workspace/log > /dev/null 2> /dev/null
{% endhighlight %}

### Mailversand

{% highlight shell %}
$ cd $BASEDIR/scripts/cron
$ cron-php-runner.sh cron-send-notification.php /somepath/var/lock/ /somepath/var/log/
{% endhighlight %}

Ein Cron-Job (hier als Beispiel für die Ausführung alle 5 Minuten) wird wie folgt angelegt:

{% highlight shell %}
$ crontab –e 5 * * * *
    $BASEDIR/scripts/cron/cron-php-runner.sh
    $BASEDIR/scripts/cron/cron-send-notification.php
    $BASEDIR/workspace/lock
    $BASEDIR/workspace/log > /dev/null 2> /dev/null
{% endhighlight %}

### Löschen temporärer Dokumente

{% highlight shell %}
$ cd $BASEDIR/scripts/cron
$ cron-php-runner.sh cron-db-clean-temporary.php /somepath/var/lock/ /somepath/var/log/

$ crontab –e 0 0 * * *
    $BASEDIR/scripts/cron/cron-php-runner.sh
    $BASEDIR/scripts/cron/cron-send-notification.php
    $BASEDIR/workspace/lock
    $BASEDIR/workspace/log > /dev/null 2> /dev/null
{% endhighlight %}

Beim Erstellen von Dokumenten werden in der Datenbank temporäre Dokumente angelegt und
normalerweise wieder gelöscht, sobald das Dokument endgültig angelegt oder der Vorgang explizit
abgebrochen wurde. Geschieht das nicht (bspw. durch Schließen des Browsers), dann verbleiben die
temporären Dokumente in der Datenbank.

<p class="warning">
Bei der Definition des cronjobs ist zu beachten, dass das Skript nach temporären Dokumenten
sucht, die mindestens einen Tag alt sind. Das heißt, dass der cronjob sinnvoller Weise höchstens
einmal täglich ausgeführt werden sollte.
</p>

## Aktivieren der asynchronen Jobverarbeitung

Jobs werden im System nur generiert, wenn in der `config.ini` der Wert für `runjobs.asynchronous`
auf `1` gesetzt wird (Standard ist `0`):

{% highlight ini %}
; JOB EXECUTION SETTINGS
; To enable asynchronous job execution, set this to 1
; You will need to set up appropriate cron jobs for
; scripts/cron/cron-php-runner.sh
runjobs.asynchronous = 0
{% endhighlight %}

<p class="info" markdown="1">
Bei Bedarf: Einrichten des Monitoring (z.B. Nagios)
Die URL `$BASEDIR/admin/info/worker-monitor` gibt den Wert `1` zurück, wenn es Jobs gibt, die
nicht verarbeitet werden konnten. Ansonsten wird der Wert `0` zurückgeliefert. Es ist so möglich, die
erfolgreiche Jobverarbeitung mit Monitoring-Systemen zu überwachen. Dafür muss im Admin-
Bereich unter [Zugriffskontrolle der IP-Bereich](../admin/security.html#ip-adressbereiche)
für das Monitoring freigeschaltet werden,
ansonsten ist die URL von außen nicht erreichbar.
</p>

## Neue Jobverarbeitung mit Crunz

Mit OPUS 4.8.1 wurde ein neues System für die Verarbeitung von Jobs eingeführt, das 
[Crunz](https://github.com/lavary/crunz) verwendet, um die Anzahl der notwendigen 
Cron-Jobs aus einen zu reduzieren.

Mit Crunz muss nur noch ein Cron-Job angelegt werden, der dann jede Minute aufgerufen wird, um zu
prüfen, ob ein OPUS 4 Job ausgeführt werden muss. Die Konfiguration der einzelnen Jobs erfolgt 
dann innerhalb von OPUS 4. 

