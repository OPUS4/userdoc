---
title: Suche
---

# Suche

## Facetten ein/-ausblenden und Reihenfolge verändern

Darüber hinaus ist es möglich, die Reihenfolge der Facetten durch Vertauschen der Einträge zu
modifizieren und Facetten ein- oder auszublenden. Standardmäßig werden in der Ergebnisanzeige
nach einer Suche alle Facetten angezeigt.

{% highlight ini %}
; Facets fields to be considered.
searchengine.solr.facets = author_facet,year,doctype,language,has_fulltext,belongs_to_bibliography,subject,institute
{% endhighlight %}

<p class="warning">
In und zwischen den Facettennamen dürfen keine Leerzeichen verwendet werden.
</p>

## Anzahl der angezeigten Werte pro Facette ändern

Es werden standardmäßig 10 am häufigsten in der Treffermenge vorkommenden Werte pro Facette
angezeigt. Dies kann global für alle Facetten geändert werden:

    searchengine.solr.globalfacetlimit =

Es kann auch für einzelne Facetten festgelegt werden, wieviele Werte pro Facette angezeigt werden:

    searchengine.solr.facetlimit.<facetname> =

Als Wert für `<facetname>` sind nur die Werte im Schlüssel searchengine.solr.facets zulässig.

* `author_facet`
* `year`
* `doctype`
* `language`
* `has_fulltext`
* `belongs_to_bibliography`
* `subject`
* `institute`

Werden beide Schlüssel in Kombination benutzt, so gilt:

* `searchengine.solr.globalfacetlimit` überschreibt den Standardwert global
* `searchengine.solr.facetlimit.<facetname>` überschreibt
  `searchengine.solr.globalfacetlimit` für die gewählte(n) Facette(n)

<p class="note" markdown="1">
Diese Parameter sind nicht in der ausgelieferten Datei `$BASEDIR/application/configs/config.ini.template`
enthalten, sondern müssen hinzugefügt werden.
</p>

<p class="note">
Die hier eingetragenen Werte bezeichnen die Maximalanzahl: sind nach einer Suche weniger
Werte in einer Facette vorhanden, werden also auch weniger Werte als im entsprechenden
Parameter angegeben angezeigt.
</p>

## Sortierkriterium für Facetten ändern

Standardmäßig werden alle Facetten absteigend nach Häufigkeit sortiert. Es gibt die Möglichkeit, für
eine oder mehrere der vorhandenen Facetten das Sortierkriterium auf "lexikographisch aufsteigend"
zu ändern. Dies geschieht pro Facette mit dem folgenden Eintrag:

    searchengine.solr.sortcrit.<facetname> = lexi

Als Wert für `<facetname>` sind nur die Werte im Schlüssel searchengine.solr.facets zulässig
(`author_facet`, `year,doctype`, `language`, `has_fulltext`, `belongs_to_bibliography`, `subject,institute`).

## Absteigende Sortierung für die Facette Erscheinungsjahr

Für die Facette "Erscheinungsjahr" gibt es die Möglichkeit eine absteigende Sortierung nach dem
Jahr, d.h. mit dem neuesten Jahr beginnend, einzustellen. Dazu sind die folgenden Änderungen
notwendig:

* Wenn der Schlüssel `searchengine.solr.facets` vorhanden ist diesen modifizieren: `year`
  ersetzen durch `year_inverted`.
* Wenn der Schlüssel searchengine.solr.facets noch nicht vorhanden ist diesen Schlüssel aus
  der Datei `$BASEDIR/application/configs/application.ini` in die `config.ini` übernehmen
  und `year` in `year_inverted` ändern.
* In beiden Fällen zusätzlich den Schlüssel `searchengine.solr.sortcrit.year_inverted` auf
  den Wert `lexi` setzen:

{% highlight ini %}
searchengine.solr.sortcrit.year_inverted = lexi
{% endhighlight %}
