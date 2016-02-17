---
title: FAQ Seite
---

# FAQ Seite

Die Inhalte der FAQ-Seite sind in sogenannte Hauptbereiche (Sections) unterteilt, die beliebig viele
Einträge mit entsprechenden Inhalten (Contents) enthalten können:

Um die FAQ-Seite anzupassen, sind folgende Änderungen möglich:

1. vorhandenen Hauptbereich (Sektion) umbenennen
2. vorhandenen Eintrag (Sektionseintrag) umbenennen
3. Inhalt eines Eintrags (Sektionseintrag) ändern
4. neuen Hauptbereich (Sektion) und neuen Eintrag (Sektionseintrag) anlegen
5. Inhalt eines Eintrag (Sektionseintrag) neu anlegen

<p class="note">
Bevor Sie mit den Änderungen beginnen, sollten Sie sich eine Struktur für die gesamte Seite
überlegen und Texte (im .txt.-Format) vorbereiten, die dann später nur noch an die richtige Stelle im
Verzeichnis gelegt werden müssen.
</p>

<p class="note">
Die Bearbeitung von Übersetzungsressourcen sowie statischer Seiten ist seit Version 4.4 über
die Opus4-Oberfläche möglich. Näheres dazu ist in Kapitel Übersetzungsressourcen 65
beschrieben.
</p>

## 1. Vorhandenen Hauptbereich (Sektion) umbenennen

Um die Überschrift eines bereits vorhandenen Hauptbereich der FAQ-Seite umzubenennen, muss die
Datei $BASEDIR/modules/home/language_custom/help_custom.tmx angelegt werden
(einmalig, z.B. durch Kopieren der Datei $BASEDIR/modules/home/language/help.tmx) und die
Übersetzungsressourcen für den
gewünschten Schlüssel geändert werden. Die Schlüssel für die Überschriften finden sich in der Datei
im Bereich "headlines help sections" und besitzen den Aufbau 'help_index_Hauptbereichsname'.

Hier ein Beispiel:

{% highlight xml %}
<tu tuid="help_index_general">
  <tuv xml:lang="en">
    <seg>What you should know about this publication server</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Was Sie über diesen Dokumentenserver wissen müssen</seg>
  </tuv>
</tu>
{% endhighlight %}

## 2. Vorhandenen Eintrag (Sektionseintrag) umbenennen

Um die Überschrift eines bereits vorhandenen Eintrags der FAQ-Seite umzubenennen, muss die
Datei $BASEDIR/opus4/modules/home/language_custom/help_custom.tmx angelegt werden
(siehe oben) und die Übersetzungsressourcen für den gewünschten Schlüssel geändert werden. Die
Schlüssel für die Überschriften der Einträge finden sich unterhalb des Bereichs "headlines help
sections" und besitzen den Aufbau 'help_title_Eintragsname'

{% highlight xml %}
<tu tuid="help_title_searchtipps">
  <tuv xml:lang="en">
    <seg>How to search</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Wie man sucht</seg>
  </tuv>
</tu>
{% endhighlight %}

## 3. Inhalt eines Eintrags (Sektionseintrag) ändern

Die eigentlichen Inhalte (Texte) der einzelnen Einträge liegen als .txt-Dateien im Verzeichnis
$BASEDIR/opus4/application/configs/help/. Vorhandene Inhalte können mit Hilfe eines Editors
geöffnet, verändert und wieder an der gleichen Stellen gespeichert werden. Es sollten
selbstverständlich immer alle Versionen (deutsch, englisch, etc.) geändert werden. Eine
Auszeichnung der Texte mit HTML-Markup ist möglich.

## 4. Neuen Hauptbereich (Sektion) und neuen Eintrag (Sektionseintrag) anlegen

### Allgemeines

Die Hauptbereiche und Einträge werden in der Datei
$BASEDIR/opus4/application/configs/help/help.ini verwaltet. Der Aufbau der Schlüssel lautet

{% highlight ini %}
Hauptbereichsschlüssel[] = 'Bereichsschlüssel' :
help_index_general[] = 'searchtipps'
help_index_authorhelp[] = 'contact'
help_index_formfields[] = 'publicationprocess'
help_index_formfields[] = 'metadata'
help_index_legal_title[] = 'legal_parallel'
help_index_legal_title[] = 'legal_license'
help_index_misc[] = 'policies'
help_index_misc[] = 'documentation'
help_index_misc[] = 'imprint'
{% endhighlight %}

### Schritt 1

Um einen neuen Bereich "MyFAQ" anzulegen, fügt man zu den bestehenden Schlüsseln an der
gewünschten Stelle (hier im Beispiel ganz am Schluss) eine neue Zeile hinzu:

{% highlight ini %}
help_index_general[] = 'searchtipps'
help_index_authorhelp[] = 'contact'
help_index_formfields[] = 'publicationprocess'
help_index_formfields[] = 'metadata'
help_index_legal_title[] = 'legal_parallel'
help_index_legal_title[] = 'legal_license'
help_index_misc[] = 'policies'
help_index_misc[] = 'documentation'
help_index_misc[] = 'imprint'
help_index_MyFAQ[] = 'MyFAQ-Eintrag'
{% endhighlight %}

Bitte beachten Sie, dass es einen Eintrag (eine Zeile) pro Hauptbereichsschlüssel-
Bereichsschlüssel-Paar geben muss. Das bedeutet für einen Hauptbereich, der z.B. 3 Bereiche
enthält (wie etwa der Bereich 'misc'), dass dieser Hauptbereichsschlüssel mit jedem
Bereichsschlüssel einmal, also insgesamt dreimal, vorkommen muss.

### Schritt 2

Durch das Anlegen des neuen Hauptbereichs und eines neuen Eintrags darin wurden vom System 2
neue Schlüssel angelegt: `help_index_MyFAQ` und `help_title_MyFAQ-Eintrag`. Diese müssen nun
noch in die Datei `$BASEDIR/modules/home/language_custom/help_custom.tmx`
geschrieben werden.

Dabei wird der Schlüssel `help_index_MyFAQ` (wie oben bereits beschrieben) im Bereich "headlines
help sections" eingetragen:

<tu tuid="help_index_MyFAQ">
  <tuv xml:lang="en">
    <seg>My FAQ</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Meine FAQ's</seg>
  </tuv>
</tu>

Der zweite neue Schlüssel `help_title_MyFAQ-Eintrag` wird unterhalb des Bereichs "headlines help
sections" eingetragen:

{% highlight xml %}
<tu tuid="help_title_MyFAQ-Eintrag">
  <tuv xml:lang="en">
    <seg>This are my FAQ's</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Dies sind meine FAQ's</seg>
  </tuv>
</tu>
{% endhighlight %}

## 5. Inhalt eines Eintrags (Sektioneintrag) neu anlegen

Die eigentlichen Inhalte (Texte) der einzelnen Einträge liegen als .txt-Dateien im Verzeichnis
`$BASEDIR/application/configs/help/`. Es können auch neue .txt-Dateien (für unser Beispiel
etwa myfaq.de.tx t und myfaq.en.txt) an dieser Stelle abgelegt werden. Die Benennung der .txt-
Dateien ist frei wählbar, es bietet sich jedoch im Hinblick auf die Übersichtlichkeit die Form
`name.de.txt` bzw. `name.en.txt` an. Damit das System die Texte benutzt, müssen die Dateinamen in
einen eigenen Schlüssel vom Typ `help_content_Eintragsname` in der Datei
`$BASEDIR/modules/home/language_custom/help_custom.tmx` eingetragen
werden.
Diese Schlüssel werden direkt unter den Schlüssel des Eintrags, zu dem der Text gehört,
geschrieben.

Hier das Beispiel von oben mit entsprechendem Schlüssel für den Inhalt:

{% highlight xml %}
<tu tuid="help_title_MyFAQ-Eintrag">
  <tuv xml:lang="en">
    <seg>These are my FAQs</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Dies sind meine FAQs</seg>
  </tuv>
</tu>

<tu tuid="help_content_MyFAQ-Eintrag">
  <tuv xml:lang="en">
    <seg>myfaq.en.txt</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>myfaq.de.txt</seg>
  </tuv>
</tu>
{% endhighlight %}

## Anzeige

Anzeige
Es gibt zwei Möglichkeiten, die Inhalte der FAQ-Seite anzuzeigen: alle Hilfetexte auf einer Seite
(default) oder pro Hilfetext eine neue Seite. Für diese zweite Möglichkeit muss folgender Wert in die
Datei `$BASEDIR/application/configs/config.ini` geschrieben werden:

{% highlight ini %}
help.separate = true
{% endhighlight %}

## Externe FAQ einbinden

Wenn auf externe FAQ verlinkt werden soll (z.B. weil bereits eine entsprechende Website vorhanden
ist), dann muss der FAQ-Menüeintrag angepasst werden. Die externe URL muss dazu in der Datei
`$BASEDIR/application/configs/navigation.xml` eingetragen werden:

Dazu muss

{% highlight xml %}
<help>
  <type>mvc</type>
  <label>help_menu_label</label>
  <title>help_menu_label</title>
  <module>home</module>
  <controller>index</controller>
  <action>help</action>
  <class>last</class>
  <id>primary-nav-help</id>
</help>
{% endhighlight %}

ersetzt werden durch

{% highlight xml %}
<help>
  <type>uri</type>
  <label>help_menu_label</label>
  <title>help_menu_label</title>
  <uri>http://examplehost/faq</uri>
  <class>last</class>
  <id>primary-nav-help</id>
</help>
{% endhighlight %}

wobei http://examplehost/faq die URL der externen FAQ ist.

<p class="note">
Bei dieser Variante wird die externe Website nicht in OPUS4 eingebunden, sondern der Nutzer
verlässt beim Klick auf diesen Link die Anwendung.
</p>

## Direktverlinkungen in den FAQ

Um in der FAQ externe Websites direkt zu verlinken, kann im Schlüssel für die Überschrift
('help_title_...') in der Custom-Sprachdatei der gewünschten Link eintragen werden. Es darf kein
Schlüssel für eine Textdatei ("help_content_...") angeben werden. Also z.B. so:

{% highlight xml %}
<tu tuid="help_title_imprint">
  <tuv xml:lang="en">
    <seg><a href="http://www.example.org" target="_blank">Impressum</a></seg>
  </tuv>
  <tuv xml:lang="de">
    <seg><a href="http://www.example.org" target="_blank">Impressum</a></seg>
  </tuv>
</tu>
{% endhighlight %}

<p class="warning">
Wichtig ist, dass es sich um eine absolute URL handelt (also unbedingt mit "http://").
</p>


