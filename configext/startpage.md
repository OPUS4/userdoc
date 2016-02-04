---
title: Startseite anpassen
weight: 90
---

# Startseite anpassen

Zum Bearbeiten der Startseite muss die Datei opus4/modules/home/language_custom/
home_custom.tmx angelegt werden (einmalig) und es müssen folgende Änderungen vorgenommen
werden.

## Reitertitel

Zum Ändern des Reitertitels muss der Text für den Schlüssel **home_index_index_pagetitle** geändert werden:

{% highlight xml %}
<tu tuid="home_index_index_pagetitle">
  <tuv xml:lang="en">
    <seg>My Home</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Meine Startseite</seg>
  </tuv>
</tu>
{% endhighlight %}

## Seitentitel

Zum Ändern des Seitentitels muss der Text für den Schlüssel **home_index_index_title** geändert werden:

{% highlight xml %}
<tu tuid="home_index_index_title">
  <tuv xml:lang="en">
    <seg>My Publication Server</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Mein Dokumentenserver</seg>
  </tuv>
</tu>
{% endhighlight %}

## Inhalt

Für den Inhalt der Startseite stehen zwei Spalten zur Verfügung.

Zum Ändern des Inhalts der linken Spalte muss der Text für den Schlüssel **home_index_index_left** geändert werden:

{% highlight xml %}
<tu tuid="home_index_index_welcome">
  <tuv xml:lang="en">
    <seg>My text for the left side...</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Mein Text für die linke Seite...</seg>
  </tuv>
</tu>
{% endhighlight %}

Zum Ändern des Inhalts der rechten Spalte muss der Text für den Schlüssel **home_index_index_right** geändert werden:

{% highlight xml %}
<tu tuid="home_index_index_instructions">
  <tuv xml:lang="en">
    <seg>My text for the right side...</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Mein Text für die rechte Seite...</seg>
  </tuv>
</tu>
{% endhighlight %}

<p class="info" markdown="1">
Die Bearbeitung von Übersetzungsressourcen sowie statischer Seiten ist seit Version 4.4 über die Opus4-Oberfläche
möglich. Näheres dazu ist in Kapitel Übersetzungsressourcen 65 beschrieben.
</p>
