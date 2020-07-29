---
title: Jahr-Facette
weight: 30
--- 

# Anpassung der Jahr-Facette

Für die Facette "Erscheinungsjahr" (year) wird die Jahresangabe im Feld "Datum der Erstveröffentlichung" 
(`PublishedDate`) verwendet. Wenn dieses nicht vorhanden ist, kommt das Feld "Jahr der Erstveröffentlichung" 
(`PublishedYear`) zum Einsatz.

    search.facet.year.indexFeld = 'published_year'

Alternativ dazu besteht die Möglichkeit, die Indexierung der Jahresfacette individuell zu konfigurieren und dafür z.B. 
das Datumsfeld "Jahr der Fertigstellung" (CompletedDate) zu verwenden.

    search.facet.year.indexFeld = 'year'
    search.index.field.year.order = 'CompletedDate'

Es gibt folgende Felder im Index, die für die Jahr-Facette verwendet werden können.

| Index-Feld                | Beschreibung |
|---------------------------+--------------|
| `year`                    | Konfigurierbare Indizierung. Die Standardkonfiguration entspricht `published_year` |
| `year_inverted`           | Umgekehrte Reihenfolge von `year` |
| `published_year`          | **default** - Verwendet `PublishedDate` oder `PublishedYear` in dieser Reihenfolge. | 
| `published_year_inverted` | Umgekehrte Reihenfolge von `published_year`. |
| `completed_year`          | Verwendet `CompeletedDate` oder `CompletedYear` in dieser Reihenfolge. |
| `completed_year_inverted` | Umgekehrte Reihenfolge von `completed_year`. |

## Absteigend Sortierung

Jedes dieser Felder kann als Wert für `search.facet.year.indexField` verwendet werden. Mithilfe der `_inverted` Felder
kann man dafür sorgen, dass das jüngste Jahr zuerst angezeigt wird. Dazu muss man zusätzlich die Sorting der Facette
konfigurieren, damit die Reihenfolge nicht mehr durch die Anzahl der gefunden Dokumente bestimmt wird.

    search.facet.year.indexField = published_year_inverted
    search.facet.year.sort = lexi

## Konfiguration der Indizierung von `year`

Für das Index-Feld `year` kann die Indizierung konfiguriert werden. Das Feld `year_inverted` entspricht immer der 
umgekehrten Reihenfolge von `year`, muss also nicht separat angepasst werden. Für die Anpassung kann folgender 
Parameter verwendet werden. 

    search.index.field.year.order = 'PublishedYear,PublishedDate'
    
Die möglichen Felder des Datenmodells sind

- PublishedYear
- PublishedDate
- CompletedYear
- CompletedDate

Diese können in beliebiger Reihenfolge miteinander kombiniert werden, um die Facette **Jahr** entsprechend den 
eigenen Vorstellungen zu befüllen.

<p class="note" markdown="1">
Mit der Auswahl von verschiedenen Index-Feldern und der Möglichkeit die Indizierung zu konfigurieren, gibt es 
momentan mehrere redundante Varianten das Verhalten der Jahr-Facette zu verändern. Es ist wahrscheinlich, dass 
in kommenden Releases die Befüllung von `published_year` und `completed_year` nicht mehr die `Date`-Felder 
berücksichtigen wird.
</p> 

### Beispiel

Die Konfiguration, um `CompletedDate` für die Jahr-Facette zu verwenden und dabei das jüngste Jahr zuerst 
anzuzeigen, würde wie folgt aussehen.

{% highlight ini %}
searchengine.solr.facets = author_facet,year,doctype, ...

search.facet.year.indexField = 'year_inverted'
search.facet.year.sort = 'lexi'
search.index.field.year.order = 'CompletedDate'
{% endhighlight %}
     