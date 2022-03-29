---
title: Installationsskript
weight: 150
---

# Installationsskript

Das Installationsskript führt mehrere Schritte aus. Bevor es 
ausgeführt werden kann, müssen die [Voraussetzungen](requirements.html)
für OPUS 4 auf dem System erfüllt sein.

Das Skript kann mit `sudo` oder ohne ausgeführt werden. Einige Schritte
der Installation sind nur mit `sudo` möglich. 

|---|
| # | Schritt | Optional | `sudo` |
|---|
| 1 | [Serverpfad](#serverpfad) | | |
| 2 | [Composer](#composer-dependencies) | | |
| 3 | [Apache2 Site Konfiguration](#webserver-apache2) |
|   | [Apache2 Link](#apache2-site-link-anlegen) | X | X |
| 4 | [Datenbank](#datenbank) | X | X |
| 5 | [Konfigurationsdateien erzeugen](#konfigurationsdateien) | | |
| 6 | [Workspace-Verzeichnisse anlegen](#workspace-verzeichnisse-anlegen) | | |
| 7 | [Dateirechte setzen](#dateirechte-setzen) | | X |
| 8 | [Admin Passwort setzen](#admin-passwort-setzen) | | |
| 9 | [Solr Konfiguration eintragen](#solr-konfiguration-eintragen) | | |
| 10 | [Testdaten importieren](#testdaten-importieren) | X | |
| 11 | [Apache2 Neustart](#apache2-neustart) | X | X |

Wenn das Skript ohne `sudo` ausgeführt wird, kann es immer noch dafür 
verwendet werden, die notwendigen Konfigurationsdateien mit den Daten
für die Verbindungsinformationen für eine bestehende Datenbank zu erzeugen.

Viele der Installationsschritte sind in einzelnen Skript-Dateien implementiert,
die auch gezielt einzeln ausgeführt werden können.

Die Installation wird folgendermaßen aufgerufen: 

{% highlight bash %}
$ sudo bin/install.sh
{% endhighlight %}

## Parameter

## Schritte

### 1. Serverpfad

Als erstes wird nach dem Pfad für die OPUS 4 Applikation auf dem 
Webserver gefragt.

```
Base URL for OPUS [/opus4]: 
```

Mit dem vorgegebenen Wert wird OPUS 4 nach der Installation unter
folgender URL verfügbar sein.

```
http://localhost/opus4 
```

### 2. Composer Dependencies

Es wird das Skript `bin/install-composer.sh` ausgeführt, das zuerst `composer.phar` 
herunterlädt (wenn notwendig) und dann die für OPUS 4 notwendigen Composer-Pakete 
installiert. 

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

Es wird die Datei `apacheconf/apache.conf` basierend auf der Template-Datei
`apacheconf/apache24.conf.template` angelegt und dabei der in Schritt 1
eingegebene Serverpfad für OPUS 4 eingetragen.

Optional (mit `sudo`) kann ein Link zu der Konfigurationsdatei im 
Verzeichnis `/etc/apache2/sites-available` angelegt und die Site 
aktiviert werden.

```
a2ensite opus4
```

Anschließend wird die Konfiguration geprüft und optional der Webserver
neu gestartet.

```
service apache2 restart
```

### 4. Datenbank

Folgende Informationen werden für die Konfiguration der Datenbank 
abgefragt:

* Name der Datenbank
* Name des OPUS 4 Admin Accounts
* Passwort für OPUS 4 Admin
* Name des OPUS 4 User Accounts
* Passwort für OPUS 4 User
* Hostname für MySQL Server
* Port für MySQL Server

Diese Informationen werden in die Konfigurationsdateien

    application/configs/config.ini
    application/configs/console.ini
    
eingetragen.
 
Der `OPUS 4 Admin Account` wird für das Erstellen und Aktualisieren der
Datenbank verwendet. Der `OPUS 4 User Account` findet Verwendung für den normalen 
Zugriff über die Weboberfläche und hat nur eigeschränkte Rechte.

Der Admin Account ist nur durch die `console.ini` verfügbar,
die von den OPUS 4 Skripten verwendet wird, die mit direktem Zugriff auf
das Hostsystem ausgeführt werden können, z.B. um ein Update durchzuführen.

Das Anlegen der Datenbank und der Nutzer ist optional, so dass eine 
existierende Datenbank genutzt werden kann. In diesem Fall werden nur
die Konfiguratonsdateien erzeugt.

Soll die Datenbank angelegt werden, muss der Username und das Passwort
für einen MySQL Account angegeben werden, der eine neue Datenbank anlegen
kann, z.B. `MySQL root`.

### 5. Konfigurationsdateien

Mit den eigegebenen Informationen werden die Konfiguratonsdateien für 
OPUS 4 angelegt.

    application/configs/config.ini
    application/configs/console.ini
    
### 6. Workspace-Verzeichnisse anlegen

Das Skript `bin/prepare-workspace.sh` legt die für den Betrieb von OPUS
notwendigen Verzeichnisse an.

|-------------+--------------|
| Verzeichnis | Beschreibung |
|-------------+--------------|
| cache | Temporäre Dateien für die Beschleunigung von Operationen |
| export | Verzeichnis für Exportfunktionen in Skripten |
| filecache | Verzeichnis für zukünftige Funktion der PDFs mit Deckblatt |
| files | Volltexte und andere Dateien der Dokumente |
| import | Verzeichnis für Importfunktion in Skripten |
| incoming | Verzeichnis für den Datei-Import in der Administration |
| log | Logdateien |
| tmp | Temporäre Dateien |
| tmp/resumption | Temporäre Dateien für OAI Schnittstelle |
|---+---|

Die Verzeichnisse befinden sich alle unterhalb von `$BASEDIR/workspace`.

### 7. Dateirechte setzen

Das Skript `bin/set-file-permissions.sh` muss mit `sudo` ausgeführt 
werden und setzt die Rechte für die OPUS 4 Dateien und Verzeichnisse.
Zum einen muss auf diese Dateien auf der Konsole zugegriffen werden.
Zum anderen muss der Webserver die Dateien lesen und in manche, wie zum
Beispiel `opus.log`, schreiben können.

### 8. Admin Passwort setzen

In OPUS gibt es einen festen Administrator Account. An dieser Stelle 
der Installation muss ein Passwort für diesen Account festgelegt werden.

```
Please enter password for OPUS 'admin' account:
```

Mit diesem Account kann auf sämtliche Funktionen der Administration
zugegriffen werden.

### 9. Solr Konfiguration eintragen

Es werden folgende Informationen abgefragt.

* Port für Solr Server
* Hostname für Solr Server
* Name des Solr Core (/opus4)

Optional kann eine weitere Verbindung definiert werden, wenn die 
Extraktion der Volltexte einen anderen Solr Core bzw. Server verwenden
soll.

Diese Informationen werden dann in die Konfigurationsdatei eingetragen.

```
application/configs/config.ini
```

### 11. Testdaten importieren

Für Testinstanzen können einige Beispieldokumente installiert werden.
Diese sind auch notwendig, wenn die Unit Tests ausgeführt werden
sollen.

```
Import test data? [Y]
```

Wenn die Testdaten installiert werden sollen, wird eine zusätzliche 
Konfigurationsdatei angelegt.

```
tests/config.ini
```

Dann werden die Workspace-Verzeichnisse unterhalb 

```
tests/workspace
```

angelegt und die Testdokumente zu OPUS hinzugefügt.

### 12. Apache2 Neustart
    
Wird das Skript mit `sudo` ausgeführt, wird am Ende gefragt, ob Apache2
neu gestartet werden soll, damit OPUS 4 aktiviert wird. 

```
$ sudo service apache2 restart
```