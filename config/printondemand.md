---
title: Print-on-Demand
---

# Print on Demand

Es ist möglich, in OPUS4 eine Print on Demand-Funktion (PoD) anzubieten. Wenn diese Funktion
konfiguriert ist, wird auf der Frontdoor eines Dokuments ein entsprechender Link zum PoD-Service
angezeigt. Ob ein Dokument auf diese Weise bestellbar ist, wird über die Lizenz des Dokuments
geregelt. Nur wenn dort durch ein Häkchen PoD erlaubt ist, erfolgt die Anzeige auf der Frontdoor.

Um diese Funktion auf der Frontdoor zu aktivieren, sind in der `config.ini` für die entsprechenden
Parameter die Kommentarzeichen zu entfernen und die Parameter mit entsprechenden Werten zu
befüllen:

{% highlight ini %}
; PRINT ON DEMAND SETTINGS
; To enable print on demand services specifiy the provider's url
; and (optionally) the name of a button image.
; The image must reside in the current layout's image folder
; ($BASEDIR/public/layouts/\<LAYOUT\>/img/)
;
; When a provider is specified, the print on demand button or link will
; be displayed if the document's licence allows it.
printOnDemand.url =
printOnDemand.button =
{% endhighlight %}

Bei dem Parameter `printOnDemand.url` wird die URL eines Anbieters eingetragen. Optional kann
für den Parameter `printOnDemand.button` eine Bild-Datei für einen Button eingetragen werden.
Diese Datei muss im `image`-Ordner (`$BASEDIR/public/layouts/<LAYOUTNAME>/img/`) des
verwendeten [Layouts](../configext/layout.html) abgelegt werden.
Bsp:

{% highlight ini %}
printOnDemand.url = http://www.epubli.de/oai/\<OAI.REPOSITORY.IDENTIFIER\>/
printOnDemand.button = mybutton.png
{% endhighlight %}

Wird dieser Parameter nicht angegeben, erscheint statt des Buttons ein Link mit dem Text "gedruckt
bestellen" bzw. "order print".
