---
title: APPLICATION_ENV
---

# APPLICATION_ENV

Mit Hilfe der Environmentvariable `APPLICATION_ENV` kann OPUS zwischen Konfigurationen für unterschiedliche Umgebungen
umgeschaltet werden. Die Konfigurationsdateien, wie `config.ini` und `application.ini` (intern genutzt) enthalten
mehrere Bereiche mit Einstellungen für unterschiedliche Umgebungen. Die unterstützen Umgebungen sind:

| Wert | Beschreibung |
|------+--------------|
| production | Normalbetrieb einer Instanz (default) |
| staging | Produktive "Testinstanz" |
| development | Spezielle Einstellungen für die Entwicklung |
| testing | Einstellungen für Tests, insbesondere Continuous Integration |

Im Normalfall läuft OPUS 4 im `production` Modus für Instanzen die sich im produktiven Betrieb befinden.

Alle anderen Modi erben die Einstellungen aus `production`, modifizieren aber die einige Optionen. Zum Beispiel sind
im `testing` Modus die Sicherheitsprüfungen abgeschaltet. Dieser sollte also nicht für normale Instanzen verwendet
werden.

<p class="info" markdown="1">
Die Einstellungen `staging` und `development` werden momentan nicht weiter verwendet. Für normale Instanzen wird
`production` verwendet. In der Entwicklung in der Regel `testing`.
</p>

Es kann nicht einfach eine weitere Umgebungen zur `config.ini` hinzugefügt werden. Die verfügbaren Umgebungen
müssen in allen verwendeten Konfigurationsdateien gleich sein, da es sonst zu Fehlern beim laden der Dateien kommt.
In der Regel sollten die vier verschiedenen Modi für jede Instanz ausreichend sein.

## Umgebung ändern

Die Einstellung kann in der Apache2 Konfiguration (z.B. `apacheconf/apache.conf`) geändert werden in folgender Zeile
das Kommentarzeichen entfernt und der Wert editiert wird.

    # SetEnv APPLICATION_ENV testing

Diese Einstellung greift aber nur bei Requests durch den Webserver. Dieser muss nach einer Änderung neu gestartet
werden. Zum Beispiel mit:

    $ sudo service apache2 restart

Um die Umgebung für die OPUS Skripte, die auf der Console ausgeführt werden, zu ändern, muss entweder folgende Datei
editiert werden

    scripts/common/bootstap.php

oder es muss die Umgebungsvariable mit dem selben Namen gesetzt werden, z.B. in der `.bashrc` Datei.

    export APPLICATION_ENV = testing

<p class="note" markdown="1">
Bei allen Einstellungen außer `production` wird die Kopfzeile der Webseiten rot hervorgehoben mit der Mitteilung, daß
die Instanz nicht mit den Produktiveinstellungen läuft. Das soll verhindern, daß eine Instanz ausversehen mit den
falschen Einstellung und somit z.B. ohne Sicherheitsfunktionen läuft.
</p>
