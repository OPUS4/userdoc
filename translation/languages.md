---
title: Unterstützte Sprachen
weight: 10
---

# Unterstützte Sprachen

Momentan enthalten die Übersetzungsressourcen von OPUS die Sprachen Deutsch und Englisch. 
Es ist möglich OPUS auf eine Sprache festzulegen bzw. auch neue Sprachen hinzuzufügen.
Dafür muss folgender Parameter in die `$BASEDIR/application/configs/config.ini` Datei geschrieben 
und entsprechend geändert werden:

{% highlight ini %}
; SUPPORTED LANGUAGES
supportedLanguages = de,en
{% endhighlight %}

Dieser Parameter ist nicht in der ausgelieferten Template-Konfiguration, 
`$BASEDIR/application/configs/config.ini.template`, enthalten, sondern muss hinzugefügt
werden. Damit die Sprachumschaltung im Web-Interface funktioniert, müssen Cookies aktiviert
sein.

Ist nur eine Sprache eingetragen, wird die Sprachumschaltung abgeschaltet. Wird eine Sprache 
hinzugefügt, die in den Übersetzungsressourcen nicht enthalten ist, kann sie in der
Übersetzungsverwaltung editiert werden. Sobald mindestens ein Übersetzungsschlüssel die neue 
Sprache unterstützt, kann sie in den Einstellungen die Übersetzungen ausgewählt werden.

Im Hintergrund wird ein zweiter Parameter verwendet `activatedLanguages`, der über die 
Einstellungen in der Übersetzungsverwaltung gesetzt werden kann. Er bestimmt welche Sprachen
für die Nutzung in der Weboberfläche freigeschaltet sind. So lässt sich eine neue Sprache 
in der Administration editieren und erst später freischalten.  


