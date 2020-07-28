---
title: Übersetzungen
weight: 100
---

# Übersetzungen

OPUS4 arbeitet mit Übersetzungsressourcen, die es ermöglichen, in der Applikation zwischen
verschiedenen Sprachen umzuschalten. Diese Übersetzungsressourcen (Schlüssel) sind in
Sprachdateien (`.tmx`-Dateien) definiert und stehen momentan in Deutsch und Englisch zur
Verfügung.  

Lokale Anpassungen an den Übersetzungen können im Bereich "Oberflächenanpassungen" der 
Administration vorgenommen werden. Diese Anpassungen werden in der Datenbank gespeichert.
Die TMX-Dateien liefern also die Standardübersetzungen und die Datenbank die spezifischen 
Anpassungen für eine OPUS 4-Instanz.

Jede Übersetzung besteht aus einem Schlüssel (Key) und einem Wert, dem anzuzeigenden Text
für die unterstützten Sprachen. Jeder Schlüssel darf nur einmal existieren unabhängig von
den Modulen. Es werden immer sämtliche Schlüssel geladen. Bei mehrfach genutzen Schlüsseln
wird nur eine der definierten Übersetzungen geladen.

Um Konflikte zu vermeiden sollten Schlüssel im mit dem Namen des zugehörigen Modules als
Präfix anfangen. Es gibt allerdings momentan einige Ausnahmen von dieser Regel in den 
Übersetzungsressourcen von OPUS 4. 

Für das Editieren von Übersetzungen gibt es mehrere Möglichkeiten. Es gibt die allgemeine
Übersetzungsverwaltung in der Schlüssel editiert und neue angelegt werden können. Zusätzlich
gibt es Seiten für das Editieren von speziellen Inhalten. 

* [Übersetzungsverwaltung](translations.html)
* Statische Seiten
  * [Hauptseite](startpage.html)
  * [Impressum](imprintpage.html)
  * [Kontaktinformationen](contactspage.html)
* [FAQ-Seite](faq.html)
{: class="navlist" }

Die Möglichkeit zum Editieren von Übersetzungen ist zum Teil auch andere Formulare der
Administration eingebaut. Für Sammlungen (CollectionsRoles) können die Übersetzungen
direkt im Add/Edit-Formular editiert werden. Für einzelne, untergeordnete Sammlung ist
noch keine Übersetzung möglich.

<p class="info" markdown="1">
Die Integration von Übersetzungsmöglichkeiten in die andere Formulare soll mit kommenden 
Releases weiter ausgebaut werden.  
</p>

## TMX-Dateien

Die ausgelieferten TMX-Dateien definieren die Standardübersetzungen. Im Normalfall sollten 
sie nicht editiert werden. Einträge in den Dateien sehen wie folgt aus:  

{% highlight xml %}
<tu tuid="example_key"> <!-- Übersetzungsschlüssel/Key -->
  <tuv xml:lang="en"> <!-- Sprache: Englisch -->
    <seg>Text that should be shown.</seg>
  </tuv>
  <tuv xml:lang="de"><!-- Sprache: Deutsch -->
    <seg>Text der angezeigt werden soll.</seg>
  </tuv>
</tu>
{% endhighlight %}

Standardschlüssel sind den Modulen zugeordnet in denen die TMX-Datei liegt, die den 
Schlüssel definiert. Schlüssel dürfen in OPUS 4 jeweils nur einmal vorkommen. Wird ein 
Schlüssel in den TMX-Dateien mehrfach definiert, wird nur eine der Definitionen geladen. 
Die zuletzt geladene TMX-Datei überschreibt die vorhergenden Übersetzungstexte.

TMX-Dateien sollten immer valide XML-Dateien sein. Das heißt, wenn HTML-Tags als Teil 
der Übersetzungswerte verwendet werden sollen müssen diese Werte mit CDATA eingefasst 
werden.

{% highlight xml %}
<tu tuid="example_key"> <!-- Übersetzungsschlüssel/Key -->
  <tuv xml:lang="en">
    <seg><![CDATA[Text with <b>HTML-Tag</b>.]]></seg>
  </tuv>
  <tuv xml:lang="de">
    <seg><![CDATA[Text mit <b>HTML-Tag</b>.]]></seg>
  </tuv>
</tu>
{% endhighlight %}

Es ist wichtig, dass die TMX-Dateien in `UTF-8` kodiert sind (um dies sicherzustellen, 
eignet sich z.B. der Open-Source-Editor Notepad++, bei dem vor der Bearbeitung einer 
Datei die Kodierung auf `UTF-8` umgestellt werden kann.

## Import/Export von Übersetzungen

Übersetzungsressourcen können exportiert bzw. importiert werden. Das ermöglicht es 
Anpassungen von einer Instanz auf eine andere zu übertragen. Verwendet werden TMX-Dateien.
Um die Schlüssel in der Datei ihren Modulen zuordnen zu können wird das Attribut 
`creationtool` verwendet, um den Namen des Moduls zu speichern.

{% highlight xml %}
<tu tuid="bibliographie" creatioltool="publish"> <!-- Schlüssel aus dem Publish-Modul -->
  <tuv xml:lang="en"> <!-- Sprache: Englisch -->
    <seg>Add to bibliography?</seg>
  </tuv>
  <tuv xml:lang="de"><!-- Sprache: Deutsch -->
    <seg>Zur Bibliographie hinzufügen?</seg>
  </tuv>
</tu>
{% endhighlight %}

Beim Import wird das Attribut `creationtool` verwendet, um unbekannte Schlüssel den Modulen 
zuzuordnen. Sollte es einen Konflikt zwischen dem Modul eines Standardschlüssels und der 
zu importierenden TMX-Datei geben, wird das Standardmodul beibehalten. 

Beim Export gibt es vier Möglichkeiten für den Umfang des exportierten Schlüssel. Es kann
entweder das aktuelle Filterergebnis der Übersetzungsverwaltung exportiert werden oder
alle Übersetzungen, unabhängig von der Filterung. Außerdem können entweder nur die lokalen
Anpassungen exportiert werden oder sämtliche Übersetzungen einschließlich der unveränderten 
Standardschlüssel. 

Ein vollständiger Export umfasst momentan mehr als 2000 Schlüssel, wenn man Zugriff auf
sämtliche Module hat. Mit einem solchen Export lassen sich die Texte auch extern bearbeiten 
und später wieder importieren.  

Es besteht die Möglichkeit neue Sprachen zum User Interface von OPUS 4 hinzuzufügen. Weitere
Informationen gibt es hier:

* [Unterstützte Sprachen](languages.html)
{: class="navlist" }
