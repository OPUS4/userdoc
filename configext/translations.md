---
title: Übersetzungsressourcen
---

# Übersetzungsressourcen

OPUS4 arbeitet mit Übersetzungsressourcen, die es ermöglichen, in der Applikation zwischen
verschiedenen Sprachen umzuschalten. Diese Übersetzungsressourcen (Schlüssel) werden in
Sprachdateien (.tmx-Dateien) verwaltet. OPUS4 liefert für OPUS-Module, in denen
Übersetzungsressourcen angepasst werden können, ein Verzeichnis

    $BASEDIR/(modulname)/language_custom/

mit aus. Beim Laden der Sprachdateien gilt folgende Reihenfolge:

1. modules/default/language/*.tmx
2. modules/default/language_custom/*.tmx
3. modules/(modulname)/language/*.tmx
4. modules/(modulname)/language_custom/*.tmx

Das heißt, dass ein Schlüssel, der in 1 existiert, in 2 durch einen individuellen Text überschrieben
werden kann. Ein Schlüssel, der in 3 existiert, überschreibt in dem speziellen Modul mögliche
Schlüsseldefinitionen aus 1 und 2. Ein individueller Schlüssel aus 4 überschreibt für das spezielle
Modul alle Definitionen aus 1 bis 3. Generell müssen Übersetzungsschlüssel nur dann im Modul
default geändert / erstellt werden, wenn sie "modulübergreifend" genutzt werden sollen (z.B. im Fall
der Namen der Dokumenttypen).

## Aufbau der Schlüssel und Bearbeitung

Im Verzeichnis `$BASEDIR/(modulname)/language_custom/` existiert bereits eine
Beispielsprachdatei example.tmx.template, die als Vorlage genutzt werden kann und bereits einen
Beispielschlüssel enthält. Anhand dieses Beispielschlüssels wird im Folgenden der grundlegende
Aufbau eines Übersetzungsschlüssels in einer .tmx-Datei erläutert:

{% highlight xml %}
<tu tuid="example_key"> <!-- Übersetzungsschlüssels -->
  <tuv xml:lang="en"> <!-- Sprache: english -->
    <seg>Text that should be shown.</seg>
  </tuv>
  <tuv xml:lang="de"><!-- Sprache: deutsch -->
    <seg>Text der angezeigt werden soll.</seg>
  </tuv>
</tu>
{% endhighlight %}

Die gewünschten Texte können direkt in den entsprechenden .tmx-Dateien editiert werden. Für
Hilfetexte (FAQ) existiert zusätzlich die Möglichkeit, diese in Textdateien in das Verzeichnis
`$BASEDIR/application/configs/help` auszulagern (vgl. Kapitel "FAQ-Seite" 97 ).

Nach der Bearbeitung der .tmx-Datei wird die Endung '.template' entfernt und sie wird wieder im
Verzeichnis `$BASEDIR/(modulname)/language_custom/` gespeichert. Es können beliebig
viele .tmx-Dateien angelegt werden. Dateien in diesem Verzeichnis werden bei einem Update nicht
überschrieben und die geänderten Schlüssel behalten weiter ihre Gültigkeit. Deshalb sollten
Übersetzungsschlüssel ausschließlich an dieser Stelle geändert werden.

## Bearbeitung von Übersetzungsressourcen und statischen Inhalten über die Oberfläche

<p class="warning">
Bisher ist diese Funktionalität erst prototypisch umgesetzt. Insbesondere die Bearbeitung von
Übersetzungsressourcen setzt Kenntnisse darüber voraus, wie Übersetzungsressourcen im
Dateisystem abgelegt werden. Vor der Benutzung wird daher empfohlen, sich mit dem Konzept der
Übersetzungsressourcen vertraut zu machen.
</p>

Die Bearbeitung von Übersetzungsressourcen sowie statischer Seiten ist seit Version 4.4 über die
Opus4-Oberfläche möglich. In der Administration gibt es unter dem Punkt "Oberflächenanpassungen"
vier Einstiegspunkte:

1. Benutzerdefinierte Felder (Enrichments)
2. FAQ-Seite
3. Statische Seiten (Hauptseite, Kontaktinformationen, Impressum)
4. Übersetzungen (Feldnamen, Feldüberschriften, Feldhilfen)

<p class="warning" markdown="1">
Um diese Funktion zu nutzen muss zunächst konfiguriert werden, welche Module für die
Bearbeitung freigegeben werden sollen. Dies geschieht in der Datei 
`$BASEDIR/application/configs/config.ini` über den Konfigurationsschlüssel 
`setup.translation.modules.allowed`. Die
zu erlaubenden Modulnamen sind dort ohne Leerzeichen durch ein Komma getrennt aufzuführen.
</p>

{% highlight ini %}
; SETUP CONFIGURATION SETTINGS
; Define for which modules translation resources may be edited through
; the web interface
setup.translation.modules.allowed = default,home,publish
{% endhighlight %}

<p class="warning">
Da diese Ressourcen im Dateisystem liegen ist es notwendig, dem Webserver die Rechte für die
Bearbeitung der entsprechenden Dateien einzuräumen. Das sind Zugriffs- und Schreibrechte für die
Verzeichnisse, in denen Dateien angelegt oder geändert werden sollen, sowie Schreibrechte für die
Dateien selbst (sofern sie schon existieren). Details zu den betreffenden Verzeichnissen bzw.
Dateien finden sich in den entsprechenden Abschnitten. Es wird empfohlen, diese Schreibrechte nur
bei Bedarf zu setzen und nach dem Bearbeiten wieder zu entfernen, da Schreibzugriffe des
Webservers auf die Instanz generell als Sicherheitsrisiko angesehen werden müssen.
</p>

### 1. Benutzerdefinierte Felder (Enrichments)

Unter diesem Punkt können Benutzerdefinierte Felder (sogenannte "Enrichments") neu angelegt und
vorhandene, noch nicht in Verwendung befindliche, umbenannt und gelöscht werden. Momentan ist
es noch notwendig, die erste Definition der Übersetzungen wie bisher auf Systemebene
vorzunehmen (s. Kapitel Felder 68 und dessen Unterkapitel). Vorhandene Übersetzungen können
dann wie unter Punkt 4. "Übersetzungen (Feldnamen, Feldüberschriften, Feldhilfen)" beschrieben
bearbeitet werden.

### 2. FAQ-Seite

Für die Bearbeitung der Hilfeseite (FAQ) steht ein Formular zur Verfügung. Die Konfiguration der
Hilfeseite findet weiter wie im Kapitel FAQ-Seite 97 beschrieben statt, d.h. das Anlegen oder
Umstrukturieren von Abschnitten ist über die Oberfläche bisher nicht möglich. Für die Bearbeitung
über die Oberfläche sind folgende Schreibrechte nötig:

In diese Datei werden alle geänderten Übersetzungsschlüssel eingetragen:

    $BASEDIR/modules/home/language_custom/help_custom.tmx

Alle Dateien mit der Endung " .txt" im Verzeichnis: 

    $BASEDIR/application/configs/help/

### 3. Statische Seiten (Hauptseite, Kontaktinformationen, Impressum)

Hier können die Startseite, die Kontaktdaten und das Impressum angepasst werden.
Dafür sind folgende Schreibrechte erforderlich:

    $BASEDIR/application/configs/help/<Seitenname>.de.txt
    $BASEDIR/application/configs/help/<Seitenname>.en.t t

    $BASEDIR/modules/home/language_custom/<Seitenname>.tmx (wenn bereits vorhanden, ansonsten das Verzeichnis)

Dabei ist `<Seitenname>` jeweils durch home , contact oder imprint zu ersetzen.

<p class="warning">
Bei Änderungen an den Übersetzungsschlüsseln werden die geänderten Übersetzungen in den
Dateien `$BASEDIR/modules/home/language_custom/<Seitenname>.tmx` gespeichert.
Sind in diesem Verzeichnis bereits anders benannte Dateien angelegt, die die gleichen Schlüssel
beinhalten, dann kann es sein, dass die Änderung nicht übernommen wird.
</p>

### 4. Anzeige und Bearbeitung von Übersetzungsschlüssen

Über eine Suchfunktion können aus allen Übersetzungsschlüsseln diejenigen herausgefiltert werden,
in denen der Suchbegriff vorkommt. Dabei bezieht sich die Suche bisher auf den Namen des
Übersetzungsschlüssels und nicht auf den Inhalt der Übersetzung. Die gefundenen
Übersetzungsschlüssel nebst Inhalten und weiteren Informationen werden in einer Tabelle dargestellt
und können nach den Tabellenspalten sortiert werden.

Zu jedem Eintrag wird ein Link angeboten, der auf eine Bearbeitungsseite für den
Übersetzungsschlüssel führt. Liegt der Inhalt in einer nicht zu bearbeitenden Datei (also im
Unterverzeichnis " language "), so werden die Inhalte für diesen Schlüssel für die Bearbeitung
übernommen, aber in der zu bearbeitenden Datei (im Verzeichnis " language_custom ")
gespeichert.Auch hier muss sichergestellt werden, dass der Webserver Schreibzugriff auf die
entsprechende Datei hat (bzw. auf das entsprechende Verzeichnis, sofern noch keine Anpassungen
vorgenommen wurden).
