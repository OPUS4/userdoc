---
title: Cronjob zur Cache-Revalidierung
weight: 650
---

# Cronjob zur Cache-Revalidierung

Zur Verbesserung der Performanz wurde in Opus 4.4 ein Caching-Mechanismus eingeführt, der
Dokumente im Opus-XML-Format zwischenspeichert und so schneller zur Verfügung stellen kann.

Wenn ein Dokument bearbeitet und gespeichert wird, dann wird der Cache für dieses Dokument
automatisch aktualisiert, so dass die folgenden Zugriffe auf das Dokument deutlich beschleunigt
werden.

Aufgrund des in Opus4 verwendeten Datenmodells findet die automatische Aktualisierung allerdings
nicht immer statt: Werden Daten geändert, die nicht unmittelbar zu einem Dokument gehören, aber
mit Dokumenten verknüpft sind, dann wird der Cache aus Gründen der Performanz nicht aktualisiert,
sondern stattdessen für diejenigen Dokumente gelöscht, die mit den geänderten Daten verknüpft
sind. Das trifft beispielsweise (aber nicht ausschließlich) auf Änderungen an Collections oder
Lizenzen zu. In diesem Fall wird der Cache für ein Dokument neu generiert, sobald das nächste Mal
auf dieses zugegriffen wird - der erste Zugriff ist also vergleichsweise langsam, alle folgenden jedoch
profitieren wieder von dem aktualisierten Cache. Das kann allerdings insbesondere dann zu
Performanzproblemen führen, wenn die mit Dokumenten verknüpften Daten vergleichsweise häufig
geändert werden müssen.

Um dieses Problem zu umgehen, kann die Wiederherstellung des Caches regelmäßig über einen
Cronjob erfolgen. Hierfür gibt es ein entsprechendes Skript, das unter

    $BASEDIR/scripts/cron/cron-update-document-cache.php

zu finden ist.

Der Aufruf des Skript erfolgt entsprechend der anderen [Opus-Cron-Skripte](../config/jobs.html) wie folgt:

    $ cd $BASEDIR/scripts/cron
    $ cron-php-runner.sh cron-update-document-cache.php
        /somepath/var/lock/
        /somepath/var/log/

Ein Cron-Job (hier als Beispiel für die Ausführung alle 5 Minuten) wird wie folgt angelegt:

    $ crontab –e
        5 * * * *
        $BASEDIR/scripts/cron/cron-php-runner.sh
        $BASEDIR/scripts/cron/cron-update-document-cache.php
        $BASEDIR/workspace/lock
        $BASEDIR/workspace/log > /dev/null 2> /dev/null

Mit der Cache-Revalidierung wird nun auch der Solr-Index aktualisiert. Bis zu dieser
Aktualisierung sind die betroffenen Dokumente nicht korrekt indexiert und werden über die Suche
nicht korrekt aufgefunden. Daher wird empfohlen, den cronjob auf jeden Fall einzurichten, um eine
möglichst zeitnahe Re-Indexierung zu gewährleisten.
