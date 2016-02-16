---
title: Dokumenttyp Einstellungen
weight: 100
---

# Dokumenttyp Einstellungen

In der $BASEDIR/opus4/application/configs/config.ini besteht die Möglichkeit, Einstellungen an den Dokumenttypen
vorzunehmen. Es kann definiert werden, welche Dokumenttypen dem Benutzer zur Auswahl stehen sollen ( include ). Ist
dieser Parameter auskommentiert, werden alle Dokumenttypen angezeigt. Sollen nur einzelne Dokumenttypen nicht
angezeigt werden, können diese durch exclude ausgeschlossen werden.

{% highlight ini %}
; DOCUMENTTYPE SETTINGS
; You can define which document types should be shown in the publish module or
; which ones should be excluded (comma separated names of XML files without
; extension). If you don't set documentTypes.include and documentTypes.exclude
; all document types will be shown.
documentTypes.include = preprint, doctype1
documentTypes.exclude = doctype2
{% endhighlight %}

Darüber hinaus kann über documentTypes.templates für ausgewählte Dokumenttypen angegeben werden, welches Template für
die Formulargenerierung benutzt werden soll.

{% highlight ini %}
; Use to configure templates names that do not match the document type name
documentTypes.templates.preprint = defaulttmpl
documentTypes.templates.doctype1 = doctype2
{% endhighlight %}

<p class="info">
Um diese Funktion nutzen zu können, müssen die Templates, für die der gleiche Dokumenttyp benutzt werden soll,
identische Felder enthalten.
</p>

Die folgenden Parameter werden im Kapitel "Dateien" 97 näher erläutert.

{% highlight ini %}
; publish.maxfilesize defines the allowed maximum size of a file.
; This does not changes any values of your Apache or php.ini. Please assure
; the values in your Apache or php settings are big enough.
publish.maxfilesize = 10240000
; publish.filetypes.allowed defines which filetypes can be uploaded.
publish.filetypes.allowed = pdf,txt,html,htm ; filetypes that are accepted in publication form
{% endhighlight %}

