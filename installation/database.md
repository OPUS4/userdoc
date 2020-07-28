---
title: Datenbank
weight: 20
---

# MySQL Datenbank

[MySQL](https://www.mysql.com/)

## Installation

Unter Ubuntu kann MySQL mit folgendem Kommando installiert werden. Für OPUS wird mindestens die Version 5.1
vorausgesetzt.

    sudo apt-get install mysql-server

## Datenbank manuell erstellen

Die Datenbank wird normalerweise vom Installationsskript erstellt, kann aber auch manuell angelegt werden. 
Um die Datenbank für OPUS 4 zu erstellen logged man sich als MySQL Root Nutzer ein und führt die folgenden
Kommandos aus.

{% highlight sql %}
create database opusdb default character set = utf8 default collate = utf8_general_ci;
{% endhighlight %}

Der *opus4admin* Nutzer wird verwendet um die Datenbank zu initialisieren.

{% highlight sql %}
create user 'opus4admin'@'localhost' identified by '<passwd>';
grant all privileges on opusdb.* to 'opus4admin'@'localhost';
{% endhighlight %}

Die Webapplikation verwendet den normalen *opus4* Nutzer, um lesend und schreibend auf die Datenbank zuzugreifen.

{% highlight sql %}
create user 'opus4'@'localhost' identified by '<passwd>';
grant select,insert,update,delete on opusdb.* to 'opus4'@'localhost';
{% endhighlight %}

## MariaDB

OPUS 4 funktioniert auch mit MariaDB.

<p class="warning" markdown="1">
Unter RHEL 6 gab es Probleme beim Einspielen der Masterdaten. Die SQL Datei mit den Klassifikationen
(`011_create_collections_data.sql`) ist mehr als 1 MB
groß und nach dem Aufbau der Datenbank haben diese Sammlungen gefehlt. Es gab dabei leider keine weitere Fehlermeldung.
Wenn dieses Problem auftritt muss die Option `max_allowed_packet` auf z.B. 2000000 (2 MB) erhöht werden. Weitere
Informationen können in der
[Dokumentation von MariaDB](https://mariadb.com/kb/en/mariadb/server-system-variables/#max_allowed_packet)
gefunden werden.
</p>

