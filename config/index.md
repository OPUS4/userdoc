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

Weitere Optionen, die hier beschrieben sind ermöglichen die Anpassung der OPUS 4 Instanz an die individuellen
Bedürfnisse Ihres Repositoriums.

<p class="note" markdown="1">
Die Administration enthält in OPUS 4.5 die Möglichkeit einige wenige Konfigurationseinstellungen im Browser
zu editieren. Diese Funktionalität ist noch in der Entwicklung. Die so modifizierten Einstellungen werden
in der Datei `config.xml` gespeichert. Die Werte in dieser Datei überschreiben die Einstellungen der
`config.ini`.
</p>

<!--p class="warning" markdown="1">
Die Defaultwerte für viele Konfigurationseinstellungen befinden sich in der `application.ini`. Diese Datei
sollte lokal nicht editiert werden. Sei enthält viele Parameter, die bestimmten wie OPUS 4 intern funktioniert.
</p-->

## Erweiterte Konfiguration

In der erweiterten Konfiguration geht es um Anpassungen und Erweiterungen von OPUS 4, wie z.B. das Erstellen
eigener Dokumenttypen oder die Anpassung der Texte und Bezeichnungen.

Diese Anpassungen erfordern häufig das Editieren oder Hinzufügen von weiteren Dateien und gehen über das
Modifizieren der `config.ini` hinaus.

[INSTALL]:../installation/index.html

* [Dokumententypen erstellen und editieren](doctypes.html)
{: class="navlist" }
