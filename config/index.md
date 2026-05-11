---
title: Konfiguration
weight: 40
---

# Konfiguration

## Einstellungen (config.ini)

Nach der erfolgreichen [Installation][INSTALL] von OPUS 4 können weitere Konfigurationen vorgenommen werden.
Die wichtigste Datei dafür ist die `config.ini`:

    $BASEDIR/application/configs/config.ini

Die Datei wurde während der Installation angelegt und alle aus technischer Sicht (zwingend) notwendigen Einträge
wurden dabei bereits vorgenommen.

Weitere Optionen, die hier beschrieben sind, ermöglichen die Anpassung der OPUS 4 Instanz an die individuellen
Bedürfnisse Ihres Repositoriums.

<p class="warning" markdown="1">
Die Defaultwerte für viele Konfigurationseinstellungen befinden sich in der `application.ini`. Diese Datei
sollte lokal nicht editiert werden. Sie enthält viele Parameter, die bestimmten wie OPUS 4 intern funktioniert.
</p>

## Optionen in der Administration

Einige Optionen können in der Administration unter Einstellungen->Optionen im Browser editiert werden. Diese
Einstellungen werden in der Datenbank gespeichert.

Welche Optionen hier verfügbar sind, wird über die Datei `application/configs/options.yml` bestimmt. 

## Erweiterte Konfiguration

In der erweiterten Konfiguration geht es um Anpassungen und Erweiterungen von OPUS 4, wie z.B. das Erstellen
eigener Dokumenttypen oder die Anpassung der Texte und Bezeichnungen.

Diese Anpassungen erfordern häufig das Editieren oder Hinzufügen von weiteren Dateien und gehen über das
Modifizieren der `config.ini` hinaus.

[INSTALL]:../installation/index.html

* [Dokumententypen erstellen und editieren](doctypes.html)
{: class="navlist" }
