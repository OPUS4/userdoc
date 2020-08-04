---
title: Übersetzungsverwaltung
weight: 20
---

# Übersetzungsverwaltung

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
vorzunehmen.

* [Felder](fields.html)
* [Übersetzungen in der Administration](../admin/userinterface.html#bersetzungen)
{: class="navlist" }

### 2. FAQ-Seite

Für die Bearbeitung der Hilfeseite (FAQ) steht ein Formular zur Verfügung. Die Konfiguration der
Hilfeseite findet weiter wie im Kapitel [FAQ-Seite](faq.html) beschrieben statt, d.h. das Anlegen oder
Umstrukturieren von Abschnitten ist über die Oberfläche bisher nicht möglich. Für die Bearbeitung
über die Oberfläche sind folgende Schreibrechte nötig:

In diese Datei werden alle geänderten Übersetzungsschlüssel eingetragen:

    $BASEDIR/modules/home/language_custom/help_custom.tmx

Alle Dateien mit der Endung `.txt` im Verzeichnis:

    $BASEDIR/application/configs/help/

### 4. Anzeige und Bearbeitung von Übersetzungsschlüsseln

Über eine Suchfunktion können aus allen Übersetzungsschlüsseln diejenigen herausgefiltert werden,
in denen der Suchbegriff vorkommt. Dabei bezieht sich die Suche bisher auf den Namen des
Übersetzungsschlüssels und nicht auf den Inhalt der Übersetzung. Die gefundenen
Übersetzungsschlüssel nebst Inhalten und weiteren Informationen werden in einer Tabelle dargestellt
und können nach den Tabellenspalten sortiert werden.

Zu jedem Eintrag wird ein Link angeboten, der auf eine Bearbeitungsseite für den
Übersetzungsschlüssel führt. Liegt der Inhalt in einer nicht zu bearbeitenden Datei (also im
Unterverzeichnis `language`), so werden die Inhalte für diesen Schlüssel für die Bearbeitung
übernommen, aber in der zu bearbeitenden Datei (im Verzeichnis `language_custom`)
gespeichert.Auch hier muss sichergestellt werden, dass der Webserver Schreibzugriff auf die
entsprechende Datei hat (bzw. auf das entsprechende Verzeichnis, sofern noch keine Anpassungen
vorgenommen wurden).
