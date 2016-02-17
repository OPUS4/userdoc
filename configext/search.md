---
title: Konfiguration der Suchoberfläche
---

# Konfiguration der Suchoberfläche

Zum Bearbeiten der Texte und Ausgabebezeichnungen für die Suchoberfläche, die Ergebnisseite und
die Facetten muss die Datei
`$BASEDIR/modules/solrsearch/language_custom/solrsearch.tmx`
angelegt (einmalig)
und entsprechend geändert werden. (Siehe Kapitel "Übersetzungsressourcen" 65 ) Beispielsweise
können hier auch die Werte der Facetten "Volltext vorhanden" und "Gehört zur Bibliographie"
angepasst werden.

{% highlight xml %}
<tu tuid="facetvalue_has_fulltext_true">
  <tuv xml:lang="en">
    <seg>yes</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>ja</seg>
  </tuv>
</tu>

<tu tuid="facetvalue_has_fulltext_false">
  <tuv xml:lang="en">
    <seg>no</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>nein</seg>
  </tuv>
</tu>

<tu tuid="facetvalue_belongs_to_bibliography_true">
  <tuv xml:lang="en">
    <seg>yes</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>ja</seg>
  </tuv>
</tu>

<tu tuid="facetvalue_belongs_to_bibliography_false">
  <tuv xml:lang="en">
    <seg>no</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>nein</seg>
  </tuv>
</tu>
{% endhighlight %}

<p class="note">
Die Bearbeitung von Übersetzungsressourcen sowie statischer Seiten ist seit Version 4.4 über
die Opus4-Oberfläche möglich. Näheres dazu ist in Kapitel Übersetzungsressourcen 65
beschrieben.
</p>
