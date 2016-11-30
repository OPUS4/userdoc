---
title: Installationsskript
---

# Installationsskript

Das Installationsskript führt mehrere Schritte aus. Bevor es 
ausgeführt werden kann müssen die [Voraussetzungen](requirements.html)
für OPUS 4 auf dem System erfüllt sein.

Das Skript kann mit `sudo` oder ohne ausgeführt werden. Einige Schritte
der Installation sind nur mit `sudo` möglich.

|---|
| # | Schritt | Optional | `sudo` |
|----|
| 1 | Pfad für OPUS 4 im Webserver (opus4) |
| 2 | Composer |
| 3 | Apache2 Site Konfiguration |
| 4 | Apache2 Link | X | X |
| 5 | Datenbank | X | X |
| 6 | Erzeugen der Konfigurationsdateien |
| 7 | Workspace |
| 8 | Admin Passwort setzen |
| 9 | Solr installieren | X | X |
| 10 | Solr Konfiguration eintragen | | |
| 11 | Testdaten importieren | X ||
| 12 | Dateirechte setzen | | |
| 13 | Apache2 restart | | |

## Optionen

## Schritte

### 1. Pfad für OPUS 4

Als erstes wird nach dem Pfad für die OPUS 4 Applikation auf dem 
Webserver gefragt.

    Base URL for OPUS [/opus4]: 
    
Mit dem vorgegebenen Wert wird OPUS 4 nach der Installation unter
folgender URL verfügbar sein.
     
     http://localhost/opus4 
     
### 2. Composer Dependencies

Es wird das Skript `bin/install-composer.sh` ausgeführt, das wenn 
notwendig zuerst `composer.phar` herunterlädt und dann die für OPUS 4 
notwendigen Composer Pakete installiert. 

<p class="warning" markdown="1">
Unabhängig davon, ob das Installationsskript mit `sudo` aufgerufen wurde,
wird das Skript für Composer **nicht** mit SUDO-Rechten ausgeführt, sondern
mit den Rechten des Nutzers, der das Installationsskript aufgerufen hat.
</p>

### 3. Webserver (Apache2)

Es wird das Skript `bin/install-apache.sh` ausgeführt. Dabei werden 
mehrere Parameter übergeben.

|---|---|---|
| # | Beschreibung  | Default |
|---|---|---|
| 1 | Serverpfad | `/opus4` |
| 2 | Templatefile | `apache24.conf.template` |
| 3 | Konfigurationsdatei | `apache.conf` |
| 4 | Distribution | `ubuntu` |
| 5 | Restart Apache2 | Nein (?) |

Es wird die Datei `apacheconf/apache.conf` basierend auf der Templatedatei
`apacheconf/apache24.conf.template` angelegt und dabei der in Schritt 1
eingegebene Serverpfad für OPUS 4 eingetragen.

Optional (mit `sudo`) kann ein Link zu der Konfigurationsdatei im 
Verzeichnis `/etc/apache2/sites-available` angelegt und die Site 
aktiviert werden.

    a2ensite opus4
    
Anschließend wird die Konfiguration geprüft und optional der Webserver
neu gestartet.

    service apache2 restart

### 4. Datenbank

Name
Admin Account Name + Passwort
User Account Name + Passwort
Host + Port

Die Zugriffsinformationen werden in die Konfigurationsdateien

    application/configs/config.ini
    application/configs/console.ini
    
eingetragen. Der Adminaccount ist nur durch die `console.ini` verfügbar,
die von den OPUS 4 Skripten verwendet wird, die mit direktem Zugriff auf
das Hostsystem ausgeführt werden können, z.B. um ein Update durchzuführen.

Das Anlegen der Datenbank und der Nutzer ist optional, so dass eine 
existierende Datenbank genutzt werden kann. In diesem Fall werden nur
die Konfiguratonsdateien erzeugt.

Soll die Datenbank angelegt werden, muss der Username und das Passwort
für einen MySQL Account angegeben werden, der eine neue Datenbank anlegen
kann, z.B. MySQL "root".

### 5. Konfigurationsdateien

Mit den eigegebenen Informationen werden die Konfiguratonsdateien für 
OPUS 4 angelegt.

    application/configs/config.ini
    application/configs/console.ini
    
    