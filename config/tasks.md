---
title: Tasks
---

# Hintergrundverarbeitung mit Crunz

Mit OPUS 4.9 wurde ein neues System für die Verarbeitung von Jobs eingeführt, das
[Crunz](https://github.com/lavary/crunz) verwendet, um die separaten Cron-Jobs durch einen einzigen zu ersetzen.

Mit Crunz muss nur noch ein Cron-Job angelegt werden, der dann jede Minute aufgerufen wird, um zu
prüfen, ob ein OPUS 4 Task ausgeführt werden muss. Die Konfiguration der einzelnen Tasks erfolgt
dann innerhalb von OPUS 4. 

## Voraussetzungen

Um die neue Hintergrundverarbeitung zu nutzen, muss für die OPUS 4 Instanz folgendes Crontab 
eingerichtet werden. `PATH_TO_OPUS4` sollte dabei der Pfad in das Hauptverzeichnis der Instanz
sein.

    * * * * * cd PATH_TO_OPUS4 && vendor/bin/crunz schedule:run 

Die Konfiguration für Crunz befindet sich im Hauptverzeichnis, in der Datei `crunz.yml`.
Normalerweise ist es nicht notwendig in dieser Datei Änderungen vorzunehmen.

## Allgemeine Konfiguration

In der OPUS 4 Konfiguration, `application/configs/application.ini`, gibt es einige neue Optionen, 
die in den meisten Fällen nicht verändert werden müssen.

    ; CRON TASK SETTINGS
    ; Enable/disable the usage of the task scheduler: true or false
    cron.enabled = true
    ; The path to the script to run a task required by the task scheduler
    cron.taskRunner = APPLICATION_PATH "/scripts/tasks/task-runner.php"
    ; Path to a custom cron task configuration
    cron.configFile = APPLICATION_PATH "/application/configs/tasks.ini"

Die Konfiguration der eigentlichen Hintergrundaufgaben erfolgt in einer separaten Datei, `tasks.ini`.

    application/config/tasks.ini

## Tasks konfigurieren

Die Datei `tasks.ini` enthält die für OPUS 4 implementieren Standard-Tasks. Momentan sind im Standard
alle deaktiviert und müssen lokal, bei Bedarf aktiviert werden. 

[!NOTE]
Bislang wurden für diese Aufgaben separate Skripte und Crontabs verwendet. Diese Skripte existieren
weiterhin, damit ein schrittweiser Umstieg auf das neue System möglich ist. Später werden diese 
Skripte voraussichtlich verschwinden, um die Verwaltung der Hintergrundprozesse zu vereinheitlichen. 

Jede Aufgabe hat einen beliebigen Namen und mindestens die folgenden drei Parameter.

``` ini
NAME.enabled = true
NAME.class = "IMPLEMENTIERENDE_KLASSE"
NAME.schedule = "0 0 * * *" 
```
Beispielsweise: 

``` ini
embargoUpdateTask.enabled = true
embargoUpdateTask.class = "Application_Job_EmbargoUpdateJob"
embargoUpdateTask.schedule = "0 2 * * *"
```

Darüber hinaus kann es für einzelne Job-Klassen spezifische Optionen geben. 

``` ini
cleanTemporariesTask.enabled = false
cleanTemporariesTask.class = "Application_Job_CleanTemporariesJob"
cleanTemporariesTask.schedule = "0 0 * * *"
; Duration e.g., P2D, P4M
cleanTemporariesTask.options.duration = "P2D";
``` 

## Debugging

Die Ausführung von Tasks wird in der Datei `tasks.log` geloggt.

    workspace/log/tasks.log

Bei Fehler, die in Crunz auftreten werden in die Datei `crunz-error.log` geschrieben.

    workspace/log/crunz-error.log

Einzelne Tasks erzeugen unter Umständen weitere spezifische Log-Dateien. Der Aufruf von
Crunz, jede Minute, wird normalerweise nicht geloggt. 

Crunz hat weitere Kommandos, die zum Debugging verwendet werden können. Mit `schedule:list`
können alle aktivierten Tasks angezeigt werden. Dabei wird jeder Task mit einer Nummer gelistet. 

    $ vendor/bin/crunz schedule:list 

Mit der `task:debug` und der Nummer eines Tasks können weitere Informationen abgerufen werden.

    $ vendor/bin/crunz task:debug TASK_NUMBER_FROM_LIST

Mit den OPUS 4 Kommandos `task:list` und `task:info` lassen sich Informationen über die in 
der Datei `tasks.ini` konfigurierten Tasks abrufen.

    $ bin/opus4 task:list

    $ bin/opus4 task:info NAME_OF_TASK
