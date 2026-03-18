---
title: Tasks
---

# Hintergrundverarbeitung mit Crunz

Mit OPUS 4.9 wurde ein neues System für die Verarbeitung von Jobs eingeführt, das
[Crunz](https://github.com/lavary/crunz) verwendet, um die separaten Cron-Jobs durch einen einzigen zu ersetzen.

Mit Crunz muss nur noch ein Cron-Job angelegt werden, der dann jede Minute aufgerufen wird, um zu
prüfen, ob ein OPUS 4 Job ausgeführt werden muss. Die Konfiguration der einzelnen Jobs erfolgt
dann innerhalb von OPUS 4. 

## Voraussetzungen

Um die neue Hintergrundverarbeitung zu nutzen, muss für die OPUS 4 Instanz folgendes Crontab 
eingerichtet werden. `PATH_TO_OPUS4` sollte dabei der Pfad in das Hauptverzeichnis der Instanz
sein.

    * * * * * cd PATH_TO_OPUS4 && vendor/bin/crunz schedule:run 

Die Konfiguration für Crunz befindet sich im Hauptverzeichnis, in der Datei `crunz.yml`.
Normalerweise ist es nicht notwendig in dieser Datei Änderungen vorzunehmen.

## Allgemeine Konfiguration

In der OPUS 4 Konfiguration, `application/configs/application.ini`, gibt es einige Optionen, 
die in den meisten Fällen nicht verändert werden müssen.

    ; CRON TASK SETTINGS
    ; Enable/disable the usage of the task scheduler: true or false
    cron.enabled = true
    ; The path to the script to run a task required by the task scheduler
    cron.taskRunner = APPLICATION_PATH "/scripts/tasks/task-runner.php"
    ; Path to a custom cron task configuration
    cron.configFile = APPLICATION_PATH "/application/configs/tasks.ini"

Die Konfiguration der eigentlichen Hintergrundaufgaben erfolgt in einer separaten Datei.

    application/config/tasks.ini


## Tasks konfigurieren


cleanTemporariesTask.enabled = false
cleanTemporariesTask.class = "Application_Job_CleanTemporariesJob"
cleanTemporariesTask.schedule = "0 0 * * *"
; Duration e.g., P2D, P4M
cleanTemporariesTask.options.duration = "P2D";






https://github.com/crunzphp/crunz

## Debugging

tasks.log
crunz-error.log


Crunz hat weitere Kommandos, die zum Debugging verwendet werden können.

    $ vendor/bin/crunz schedule:list 

    $ vendor/bin/crunz task:debug TASK_NUMBER_FROM_LIST
