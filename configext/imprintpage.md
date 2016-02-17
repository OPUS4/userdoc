---
title: Impressumsseite
---

# Impressumsseite

Zum Bearbeiten der Impressumseite muss die Datei

    $BASEDIR/modules/home/language_custom/imprint.tmx

angelegt werden (einmalig) und es müssen folgende Änderungen vorgenommen werden.

* zum Ändern des Seitentitels muss der Text im Schlüssel `home_index_imprint_pagetitle`
  angepasst werden
* zum Ändern der Überschrift muss der Text im Schlüssel `home_index_imprint_title` angepasst
 werden.

Der eigentliche Inhalt wird angepasst über den Schlüssel `help_content_imprint` in der Datei

    $BASEDIR/modules/home/language_custom/help_custom.tmx

{% highlight xml %}
<tu tuid="help_content_imprint">
<tuv xml:lang="en">
<seg>imprint.en.txt</seg>
</tuv>
<tuv xml:lang="de">
<seg>imprint.de.txt</seg>
</tuv>
</tu>
{% endhighlight %}

(Siehe auch Kapitel "FAQ-Seite" 97 "3. Inhalt eines Eintrags (Sektionseintrag) ändern")

<p class="note">
Die Bearbeitung von Übersetzungsressourcen sowie statischer Seiten ist seit Version 4.4 über
die Opus4-Oberfläche möglich. Näheres dazu ist in Kapitel Übersetzungsressourcen 65
beschrieben.
</p>
