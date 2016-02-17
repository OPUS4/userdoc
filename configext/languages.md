---
title: Unterstützte Sprachen
---

# Unterstützte Sprachen

Momentan werden für die Übersetzungsressourcen von OPUS die Sprachen Deutsch und Englisch
unterstützt. Es ist jedoch möglich, OPUS in weiteren Sprachen anzubieten. In diesem Fall kann
folgender Parameter in die `$BASEDIR/application/configs/config.ini` geschrieben und
entsprechend ergänzt werden:

{% highlight ini %}
; SUPPORTED LANGUAGES
supportedLanguages = de,en
{% endhighlight %}

Dieser Parameter ist nicht in der ausgelieferten Datei
`$BASEDIR/application/configs/config.ini.template` enthalten, sondern muss hinzugefügt
werden. Damit die Sprachumschaltung im Web-Interface funktioniert, müssen Cookies aktiviert
sein.
