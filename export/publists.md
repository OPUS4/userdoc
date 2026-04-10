---
title: Publikationslisten
weight: 50
---

# Publikationslisten

Opus4 bietet die Möglichkeit [Publikationslisten](../features/publist.html) zu generieren. Dafür
wird ein Standard-Layout ausgeliefert.

Um ein eigenes Layout zu aktivieren und die Sortierreihenfolge der Ergebnisliste nach einem anderen
Kriterium zu sortieren sind in der `config.ini` für die entsprechenden Parameter das
Kommentarzeichen zu entfernen und die Parameter mit den gewünschten Werten zu befüllen:

``` ini
; PUBLICATION LIST SETTINGS
; Per default publication lists are rendered by the default stylehseet.
; Here you can define your own stylesheet for rendering publication lists:
plugins.export.publist.stylesheet =

; Per default publications are grouped by 'published year'.
; Here you can switch grouping to 'completed year':
plugins.export.publist.groupby.completedyear = 1
```

Der Parameter `plugins.export.publist.stylesheet` gibt den Namen des zuvor erstellten eigenen Layout für die
Publikationslisten an.

Der Parameter `plugins.export.publist.groupby.completedyear` ermöglicht die standardmäßig nach 'published
year' sortierte Ergebnisliste umzustellen nach 'completed year' .

Das folgende Beispiel aktiviert anstelle des Standardlayouts für Publikationslisten das eigene
erstellte Layout `mylayout` und ändert die Sortierung der Ergebnisliste nach dem Kriterium
'completed year':

{% highlight ini %}
plugins.export.publist.stylesheet = mylayout
plugins.export.publist.groupby.completedyear = 1
{% endhighlight %}
