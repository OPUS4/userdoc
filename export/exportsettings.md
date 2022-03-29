---
title: Export Settings
weight: 30
---

# Export Settings

Um den [XML-Export][EXPORT] aus OPUS zu erleichtern gibt es seit der Version 4.4.4 die Möglichkeit, einen Button auf der
Frontdoor und auf den Ergebnisseiten der Suche anzuzeigen. Dieser Button wird über Parameter in der config.ini
aktiviert, indem die entsprechenden Schlüssel aus der `config.ini.template` kopiert und die Kommentarzeichen entfernt
werden, und steht dann dem Administrator und allen Nutzerrollen mit dem Recht export zur Verfügung.

{% highlight ini %}
; EXPORT SETTINGS
; Use to specify default XSLT stylesheet for exports in search or frontdoor
export.stylesheet.frontdoor = example
export.stylesheet.search = example
{% endhighlight %}

Diese Werte triggern zum einen die Anzeige des Buttons und gibt zum anderen das zu verwendende Stylesheet an. Die
Stylesheets werden unter `$BASEDIR/modules/export/views/scripts/stylesheets-custom` abgelegt, wobei das
`example.xslt` in der OPUS-Standardauslieferung enthalten ist (siehe auch die Beschreibung zum
[XML-Export][EXPORT]).
Die Parameter können auch einzeln gesetzt werden.

[EXPORT]: exportlist.html