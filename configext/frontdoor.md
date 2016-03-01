---
title: Anzeige der Zusammenfassungen auf der Frontdoor
---

# Anzeige der Zusammenfassungen auf der Frontdoor

Die Abstracts eines Dokuments werden auf der Frontdoor standardmäßig in voller Länge angezeigt.
Wenn sie eingeklappt dargestellt werden sollen, kann dies über den Parameter
`frontdoor.numOfShortAbstractChars` gesteuert werden. Dieser Parameter wird in der Datei
`$BASEDIR/application/configs/config.ini` konfiguriert (Standardwert 0). Es kann ein
beliebiger Wert für die Anzahl der Zeichen eingetragen werden, die in eingeklapptem Zustand
sichtbar sein sollen. Folgendes Beispiel zeigt die ersten 400 Zeichen des Abstracts an:

{% highlight ini %}
frontdoor.numOfShortAbstractChars = 400
{% endhighlight %}

<p class="note">
Für das Einklappen der Abstracts muss Javascript aktiviert sein. Falls Javascript deaktiviert ist,
werden die Abstracts in voller Länge angezeigt.
</p>

