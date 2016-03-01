---
title: Kontaktseite
---

# Kontaktseite

Zum Bearbeiten der Kontaktseite muss die Datei

    $BASEDIR/modules/home/language_custom/contact.tmx

angelegt werden (einmalig) und es müssen folgende Änderungen vorgenommen werden.

## Seitentitel

Zum Ändern des Seitentitels muss der Text für den Schlüssel `home_index_contact_pagetitle`
angepasst werden:

{% highlight xml %}
<tu tuid="home_index_contact_pagetitle">
  <tuv xml:lang="en">
    <seg>My Contact Information</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Meine Kontaktdaten</seg>
  </tuv>
</tu>
{% endhighlight %}

## Überschrift

Zum Ändern der Überschrift muss der Text für den Schlüssel `home_index_contact_title` angepasst
werden:

{% highlight xml %}
<tu tuid="home_index_contact_title">
  <tuv xml:lang="en">
    <seg>Contact us...</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Nehmen Sie Kontakt mit uns auf...</seg>
  </tuv>
</tu>
{% endhighlight %}

Der eigentliche Inhalt wird über die Dateien

    $BASEDIR/application/configs/help/contact.de.txt
    $BASEDIR/application/configs/help/contact.en.txt

angepasst (siehe [Inhalt eines Eintrags (Sektionseintrag) ändern](faq.html#inhalt-eines-eintrags-sektionseintrag-ndern)).

<p class="note" markdown="1">
Die Bearbeitung von [Übersetzungsressourcen](translations.html) sowie statischer Seiten ist seit Version 4.4 über
die Opus4-Oberfläche möglich.
</p>
