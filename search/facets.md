---
title: Facetten
weight: 20 
---

# Konfiguration von Facetten

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

Es werden standardmäßig maximal die 10 am häufigsten in der Treffermenge vorkommenden Werte für jede Facette
angezeigt. Dies kann global für alle Facetten geändert werden:

    search.facet.default.limit = 20

Es kann auch für einzelne Facetten festgelegt werden, wie viele Werte pro Facette angezeigt werden:

    search.facet.<FACET_NAME>.limit =
    search.facet.subject.limit = 30

Als Wert für `<facetname>` sind nur die Werte im Schlüssel searchengine.solr.facets zulässig.

* `author_facet`
* `year`
* `doctype`
* `language`
* `has_fulltext`
* `belongs_to_bibliography`
* `subject`
* `institute`
* `enrichment_<ENRICHMENT_NAME>`

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

    search.facet.<FACET_NAME>.sort = lexi

Als Wert für `<FACET_NAME>` können die im Schlüssel `searchengine.solr.facets` konfigurierten Facetten
verwendet werden.

## Anzeige von Facetten einschränken

Es ist möglich die Anzeige von Facetten einzuschränken, damit diese nicht für alle Nutzer angezeigt 
werden. Die Facette __server_state__ wird zum Beispiel nur für Administratoren mit Zugriff auf die
Dokumentenverwaltung angezeigt. Dafür kann die Option __accessResource__ verwendet werden. 

{% highlight ini %}
search.facet.server_state.accessResource = 'documents'
{% endhighlight %}

Der Wert muss dem Namen einer Ressource im Rechtemanagement von OPUS 4 entsprechen. Mit dem Wert
`admin` ist die Facette für alle Administratoren sichtbar.

Diese Funktionalität kann verwendet werden, um die Sichtbarkeit von Enrichment-Facetten einzuschränken.  

## Übersetzung von Facetten-Werten

Die Werte werden bei der Anzeige der Facetten in vielen Fällen nicht übersetzt. Die Werte für die 
Facette `doctype` wird übersetzt, um die korrekte Bezeichnung für die Dokumenttypen anzuzeigen.

Um die Übersetzung einer Facette zu beeinflussen können die Optionen __translated__ und __translationPrefix__
verwendet werden. Damit lässt sich die Übersetzung aktivieren und ein Präfix für die Übersetzungsschlüssel
für die Werte definieren. 

    search.facet.enrichment_opus-source.translated = true
    search.facet.enrichment_opus-source.translationPrefix = 'opus_source_'
    
In diesem Beispiel werde die Werte des Enrichment `opus.source` mit den Schlüsseln `opus_source_<WERT>` übersetzt.    
    
Ohne einen Präfix, wird versucht die Werte der Facette direkt als Schlüssel für die Übersetzung zu verwenden. Abhängig 
von den verwendeten Werten in der Facette kann das zu unerwünschten Ergebnissen führen, wenn ein entsprechender 
Schlüssel für einen anderen Zweck in OPUS 4 existiert. Eine Kollision kann zum Beispiel leicht mit den Übersetzungen
für Dokumenttypen passieren, da diese bisher keinen Präfix haben. 

## Übersicht aller Facetten-Optionen

| Option | Beschreibung |
|--------+--------------|
|limit| Maximal angezeigte Werte für eingeklappte Facette |
|sort| Sortierung der Facette (`lexi` odr `index`)|
|accessResource| Resource auf die der Nutzer Zugriff haben muss, um die Facette angezeigt zu bekommen. |
|translated| Soll die Facette übersetzt werden. |
|translationPrefix| Präfix für die Übersetzungsschlüssel für die Facetten-Werte. |
|type| Biete die Möglichkeit eine spezielle Klasse für die Facette zu verwenden, um komplexere Anforderungen umzusetzen. |

Die Option __type__ ist für Entwickler gedacht.
