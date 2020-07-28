---
title: FAQ-Seite
weight: 60
---

# FAQ-Seite

Die Inhalte der FAQ-Seite sind in sogenannte Hauptbereiche (Sections) unterteilt, die beliebig viele
Einträge (Fragen) mit entsprechenden Texten (Antworten) enthalten können:

Um die Inhalte der FAQ-Seite editieren zu können muss man Zugriff auf das Setup-Modul haben. Hat man
den, werden auf der FAQ-Seite Editier-Icons mit Links zu den entsprechenden Formularen im Setup-Modul 
angezeigt.

Über den Link hinter den Sektions-Überschriften lässt sich die jeweilige Überschift editieren. Bei 
den Einträge gibt es einen Link hinter der Überschrift des Einträge (Frage). In dem verlinkten 
Formular lassen sich Überschift und Inhalt des Eintrags editieren. 

Das Editier-Icon hinter der Überschrift der FAQ-Seite für zur Hauptseite für das Editieren der FAQs
im Setup-Modul. Von hier aus gelangt man zu einem Formular, dass es erlaubt die Struktur der FAQ-Seite
zu verändern, Sektionen und Einträge hinzuzufügen oder zu entfernen. 

Die angepassten Übersetzungen für die FAQ-Seite werden in der Datenbank gespeichert. Die verwendeten
Schlüssel folgen folgender Struktur.
 
| Beschreibung | Präfix | Beispiel |
|--------------+--------+----------|
| Sektionsüberschrift | `help_index_` | `help_index_general` |
| Überschrift eines Eintrags (Frage) | `help_title_` | `help_title_searchtipps` |
| Inhalt eines Eintrags (Antwort) | `help_content_` | `help_content_searchtipps` |

Die  Übersetzungsschlüssel sind dem Help-Modul zugeordnet und können auch direkt in der allgemeinen
Übersetzungsverwaltung editiert werden. Dort lassen sich die Übersetzungen auch exportieren, z.B. 
um sie extern zu bearbeiten und dann wieder zu importieren. So lassen sich die Texte auch von einer 
Instanz auf eine andere Übertragen. 

Die Inhalte dürfen HMTL-Tags enthalten. 

## Impressum und Kontakt editieren

Die Inhalte der Seiten für Impressum und Kontakt werden standardmäßig auch auf der FAQ-Seite 
verwendet. Dafür werden die Schlüssel `help_content_imprint` und `help_content_contact` verwendet. Im Gegensatz zu
den anderen Schlüsseln für die FAQ-Seite sind diese nicht dem Help-Modul zugeordnet, sondern gehören zum Home-Modul.

Es ergeben sich mindestens drei Wege die Inhalte zu editieren, einmal über die FAQ-Seite, über die Edit-Funktionen
für die statischen Seiten und über die allgemeine Übersetzungsverwaltung. Wichtig ist dabei zu beachten, dass sich
die Inhalte dabei immer sowohl auf der FAQ-Seite als auch auf den separaten Seiten für Impressum oder Kontakt ändern. 

## Struktur der FAQ-Seite editieren

### Allgemeines

Die Hauptbereiche und Einträge werden in der Datei
`$BASEDIR/application/configs/help/help.ini` verwaltet. Der Inhalt dieser Datei kann im Setup-Bereich
der Administration editiert werden. Nutzer mit Zugriff auf das Setup-Modul können auf der FAQ-Seite
dem Editier-Link hinter der Seitenüberschrift folgen.

Die Datei ist wie folgt aufgebaut. Auf der linken Seite stehen die Schlüssel für die Sektionen der
FAQ-Seite, z.B. `help_index_general`, und auf der rechten Seite stehen die Namen der Einträge ohne
den Präfix `help_title_`, also z.B.  `searchtipps` für den Eintrag `help_title_searchtipps`. Hat eine
Sektion mehrere Einträge muss ihr Schlüssel auf der linken Seite für jeden Eintrag wiederholt werden.  

    SEKTIONSSCHLÜSSEL[] = 'NAME_DES_EINTRAGS'
    
    help_index_general[] = 'searchtipps'
    help_index_authorhelp[] = 'contact'
    help_index_formfields[] = 'publicationprocess'
    help_index_formfields[] = 'metadata'
    help_index_legal_title[] = 'legal_parallel'
    help_index_legal_title[] = 'legal_license'
    help_index_misc[] = 'policies'
    help_index_misc[] = 'documentation'
    help_index_misc[] = 'imprint'

### Neuen Bereich anlegen

Um einen neuen Bereich "MyFAQ" anzulegen, fügt man zu den bestehenden Schlüsseln an der
gewünschten Stelle (hier im Beispiel ganz am Schluss) eine neue Zeile hinzu:

    help_index_general[] = 'searchtipps'
    help_index_authorhelp[] = 'contact'
    help_index_formfields[] = 'publicationprocess'
    help_index_formfields[] = 'metadata'
    help_index_legal_title[] = 'legal_parallel'
    help_index_legal_title[] = 'legal_license'
    help_index_misc[] = 'policies'
    help_index_misc[] = 'documentation'
    help_index_misc[] = 'imprint'
    help_index_MyFAQ[] = 'MyFAQ_Eintrag'

Nach dem Speichern der Änderung tauchen der neue Bereich und der Eintrag auf der FAQ-Seite auf. Da die 
Übersetzungsschlüssel noch nicht existieren werden erst einmal nur die Schlüssel angezeigt, `help_index_MyFAQ`
und `help_title_MyFAQ_Eintrag`. Folgt man nun den Editier-Links hinter der Bereichsüberschrift oder dem 
Eintrag können die Inhalte erstellt werden. 

Bitte beachten Sie, dass es einen Eintrag (eine Zeile) pro Hauptbereichsschlüssel-
Bereichsschlüssel-Paar geben muss. Das bedeutet für einen Hauptbereich, der z.B. 3 Einträge
enthält (wie etwa der Bereich 'misc'), dass dieser Hauptbereichsschlüssel mit jedem
Bereichsschlüssel einmal, also insgesamt dreimal, vorkommen muss.

## Anzeige der Einträge auf separaten Seiten

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

wobei `http://examplehost/faq` die URL der externen FAQ ist.

<p class="note">
Bei dieser Variante wird die externe Website nicht in OPUS4 eingebunden, sondern der Nutzer
verlässt beim Klick auf diesen Link die Anwendung.
</p>

## Direktverlinkungen in den FAQ

Um in der FAQ externe Websites direkt zu verlinken, kann im Schlüssel für die Überschrift
(`help_title_...`) der gewünschten Link eintragen werden. Die Übersetzung würde
also zum Beispiel so aussehen:

{% highlight html %}
<a href="http://www.example.org" target="_blank">Impressum</a>
{% endhighlight %}

<p class="warning" markdown="1">
Wichtig ist, dass es sich um eine absolute URL handelt, die mit `http://` bzw. `https://` beginnt.
</p>

In diesem Fall darf es keinen Schlüssel für den Inhalt dieses Eintrags geben (`help_content_...`),
damit kein Link zu dem Inhalt generiert wird. Der Inhalt kann in dem Formular zum Editieren des
Eintrags einfach leer gelassen werden.

Der Editier-Link taucht bei Einträgen ohne Inhalt direkt in der Übersicht am Anfang der FAQ-Seite
auf.
