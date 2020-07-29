---
title: Workspace
weight: 160
---

# Workspace

Der Workspace ist ein Verzeichis in dem OPUS 4 die Volltexte, Logs und
 alle anderen für den Betrieb notwendigen Dateien mit Daten speichert. 

| Verzeichnis | Beschreibung |
|-------------+--------------|
| files | Volltexte |
| log | Log Dateien für Web und Konsole |
| export | Export Verzeicnis für Skripte |
| incoming | Import von lokal gespeicherten Dateien |
| cache | Cache für Sprachdateien und extrahierte Volltexte |
| tmp | Temporäre Dateien |

## Verzeichnisrechte

Die Verzeichnisse müssen die notwendigen Schreib- und Leserechte 
eingestellt sein.

Der Webserver, Apache, muss im Betrieb auf die Verzeichnisse zugreifen
können.

Für die Ausführung von Skripten auf der Konsole, z.B. um den Index neu 
aufzubauen, muss der entsprechende Nutzer die notwendigen Rechte 
besitzen.

Im `bin`-Verzeichnis von OPUS 4 befindet sich ein Skript, dass die 
Rechte für die Dateien setzen kann. Es setzt den Besitzer und die Gruppe
für die Dateien und die Zugriffsrechte.

    sudo bin/set-file-permissions.sh

### Rechte manuell setzen

Unter Ubuntu können mit dem folgenden Kommando alle Dateien dem 
`opus`-Nutzer als Besitzer und dem Webserver (`www-data`) als 
Gruppe zugeordnet werden.

    sudo chown -R opus:www-data workspace
    
Dem `opus`-Nutzer und `www-data` können dann mit den folgenden Kommandos 
Schreib- und Leserechte für die Verzeichnisse und Dateien gegeben 
werden.

    sudo find workspace/ -type d -print0 |xargs -r0 chmod 770
    sudo find workspace/ -type f -print0 |xargs -r0 chmod 660  
    


