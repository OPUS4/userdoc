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

* [Inhalt eines Eintrags (Sektionseintrag) ändern](faq.html#inhalt-eines-eintrags-sektionseintrag-ndern)
{: class="navlist" }

<p class="note" markdown="1">
Die Bearbeitung von [Übersetzungsressourcen](translations.html) sowie statischer Seiten ist seit Version 4.4 über
die Opus4-Oberfläche möglich.
</p>
