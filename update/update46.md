---
title: OPUS 4.6 Update
---

# OPUS 4.6 Update

Wie bei allen Updates müssen zuerst die OPUS 4 Dateien mit Git auf den
neuesten Stand gebracht werden. Danach kann das Updateskript verwendet
werden um weitere Schritte auszuführen.

Das Update auf OPUS 4.6 setzt mindestens OPUS 4.5-RC1 voraus. Falls es
sich bei dem Repository noch um OPUS 4.4.5 handelt, kann mit der folgenden
Anleitung direkt auf OPUS 4.6 umgestiegen werden. 

* [Update von 4.4.5 auf Git-Version](from445.html)
{: class="navlist" }

Anschließend muss die Datenbank aktualisiert und Anpassungen an den Daten 
vorgenommen werden. Dafür muss das Skript

    bin/update.sh

ausgeführt werden.

Weitere Informationen zu den Neuheiten in OPUS 4.6 und zum Update finden
sich in den Release Notes.

* [OPUS 4.6 Release Notes](https://github.com/OPUS4/application/blob/4.6/RELEASE_NOTES.md)
{: class="navlist" }

## Was passiert beim Update?

### Neue Konfigurationsdatei anlegen

Wenn die Datei `console.ini` noch nicht existiert wird sie angelegt und
in Ihr die Zugangsdaten für den OPUS 4 Admin Account für die Datenbank
gespeichert. 

    application/configs/console.ini
    
Wenn die Zugangsdaten nicht in der Datei `db/createdb.sh` gefunden
werden können, werden sie auf der Konsole abgefragt.
 
### Datenbankschema aktualisieren

Beim Update von OPUS 4.5 auf die aktuelle Version 4.6 werden folgende 
Änderungen am Datenbankschema vorgenommen.

* Tabelle 'schema_version' wird vereinfacht
* Tabelle 'opus_version' wird hinzugefügt
* Lizenzen bekommen die neue Spalte 'name' für Kurznamen wie "CC BY 4.0"
* CollectionRoles bekommen weitere Optionen
* Personen bekommen Spalte 'opus_id', dass aber noch nicht verwendet wird

### Weitere Update-Schritte

Nach der Aktualisierung des Datenbankschemas werden weitere Schritte für 
das Update ausgeführt.

* Sammlung für Importe (durch SWORD) wird hinzugefügt
* Wahlweise werden die Creative Commons 4.0 Lizenzen hinzugefügt
* Alte Creative Commons Lizenzen werden, wenn möglich, um Kurznamen ergänzt
* Führende Nullen werden von GND-Nummern für Personen entfernt
* Verlinkung zum 'schema'-Verzeichnis im Framework wird entfernt 

