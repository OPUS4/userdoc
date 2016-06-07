---
title: Datenbank
---

# Datenbank

[MySQL](https://www.mysql.com/)


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

