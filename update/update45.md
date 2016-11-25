---
title: OPUS 4.5 Update
---

# OPUS 4.5 Update

Wie bei allen Updates müssen zuerst die OPUS 4 Dateien mit Git auf den
neuesten Stand gebracht werden. Danach kann das Updateskript verwendet
werden um weitere Schritte auszuführen.

Das Update auf OPUS 4.5 setzt mindestens OPUS 4.5-RC1 voraus. Falls es
sich bei dem Repository noch um OPUS 4.4.5 handelt, kann mit der folgenden
Anleitung direkt auf OPUS 4.5 umgestiegen werden. 

* [Update von 4.4.5 auf Git-Version](from445.html)
{: class="navlist" }

Anschließend muss die Datenbank aktualisiert werden. Dafür das Skript

    bin/update.sh

ausführen.

## Was passiert beim Update?

### Neue Konfigurationsdatei anlegen

Wenn die Datei `console.ini` noch nicht existiert wird sie angelegt und
in Ihr die Zugangsdaten für den OPUS 4 Admin Account für die Datenbank
gespeichert. 

    application/configs/console.ini
    
Wenn die Zugangsdaten nicht in der Datei `db/createdb.sh` gefunden
werden können, werden sie auf der Konsole abgefragt.
 
### Datenbankschema aktualisieren

Für die Aktualisierung der Datenbank wird das folgende SQL Skript auf
die Datenbank angewendet. Die Datenbank muss auf dem Stand von OPUS 4.4.5 
sein.

    db/schema/update/update-4.5.sql

