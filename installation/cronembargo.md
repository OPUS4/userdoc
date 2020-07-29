---
title: Cronjob für Embargo-Updates
weight: 660
---

# Cronjob für Embargo-Updates

Wenn für ein Dokument ein Embargo-Datum gesetzt wurde und dieses abläuft, ändert sich an dem Dokument 
nichts. Das Datum wird beim Zugriff auf Dateien für die Bestimmung der Berechtigungen verwendet.
 
Damit ein Dokument, bei dem das Embargo abgelaufen ist, z.B. beim Harvesting durch die DNB auftaucht,
muss ServerDateModified des Dokuments aktualisiert werden. Beim Harvesting werden in der Regel alle die
Dokumente abgeholt, die sich seit der letzten Abfrage verändert haben.

Für die notwendige Aktualisierung der Dokumente gibt es ein Script, das mithilfe von Cron, z.B. einmal
jede Nacht ausgeführt werden kann.

    $BASEDIR/scripts/cron/cron-embargo-update.php
    
Der Aufruf des Script wie bei den anderen [Skripten](../config/jobs.html) wie folgt:

    $ cd $BASEDIR/scripts/cron
    $ cron-php-runner.sh cron-embargo-update.php
        /somepath/var/lock/
        /somepath/var/log/

Ein Cron-Job (hier als Beispiel für die Ausführung jeden Tag um 1 Uhr) wird wie folgt angelegt:

    $ crontab –e
        * 1 * * *
        $BASEDIR/scripts/cron/cron-php-runner.sh
        $BASEDIR/scripts/cron/cron-embarbo-update.php
        $BASEDIR/workspace/lock
        $BASEDIR/workspace/log > /dev/null 2> /dev/null
