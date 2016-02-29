---
title: Publish-Formular
---

# Publishformular

## Bibliographiefunktion

Der Parameter form.first.bibliographie gibt an, ob eine Checkbox für die Zuordnung zur
Bibliographie angezeigt werden soll. Mögliche Werte: 0 - nicht anzeigen / 1 - anzeigen, Standard ist 0.

{% highlight ini %}
; If you would like to use opus to save bibliographical items you should set
; this to 1. It will ask on the first site of the publish module if a new
; document should be added to the bibliography.
form.first.bibliographie = 0
{% endhighlight %}

## Datei-Upload abschalten

Mit dem Parameter `form.first.enable_upload` kann das Hochladen einer Datei im ersten Schritt
des Veröffentlichungsvorgangs abgeschaltet werden. Mögliche Werte: 0 - abgeschaltet / 1 -
angeschaltet, Standard ist 1.

{% highlight ini %}
; uncomment next line if file upload in first publish form should be disabled
form.first.enable_upload = 0
{% endhighlight %}

## Datei-Upload als Pflichtfeld

Der Parameter form.first.require_upload gibt an, ob das Hochladen einer Datei obligatorisch
ist. Mögliche Werte: 0 - optional / 1 - obligatorisch, Standard ist 1.

{% highlight ini %}
; States, if the upload-fields are required to enter the second form.
form.first.require_upload = 0
{% endhighlight %}

## Einräumen eines Nutzungsrechts

Der Parameter form.first.show_rights_checkbox gibt an, ob das Auswählen der Checkbox für
das Einräumen eines Nutzungsrechts auf der ersten Seite des Veröffentlichungsformulars
obligatorisch ist. Mögliche Werte: 0 - optional / 1 - obligatorisch, Standard ist 1.

{% highlight ini %}
; States, if a checkbox for the institutions legal notices is shown.
form.first.show_rights_checkbox = 1
{% endhighlight %}

Sollte kein Interesse bestehen, dieses Feld anzuzeigen, entfernen Sie bitte den Kommentar bei dem
Parameter in Ihrer config.ini und setzen Sie den Wert auf 0. Für den Fall, dass nur bei bestimmten
Dokumenttypen das Ankreuzen der Checkbox für das Einräumen eines Nutzungsrechts verpflichtend
sein soll, besteht die Möglichkeit, die Checkbox direkt in den Dokumenttyp aufzunehmen (Kapitel
Grundlage: Templates 85 ).
