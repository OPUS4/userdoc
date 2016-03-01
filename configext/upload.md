---
title: Dateien
weight: 200
---

# Dateien

## Dateigröße

Es gibt einige Parameter in OPUS4, mit denen man die Dateiverwaltung konfigurieren kann.

{% highlight ini %}
; publish.maxfilesize defines the allowed maximum size of a file.
; This does not changes any values of your Apache or php.ini. Please assure
; the values in your Apache or php settings are big enough.
publish.maxfilesize = 10240000
{% endhighlight %}

Der Parameter `maxfilesize` definiert die maximale Dateigröße. Initial ist dieser Wert auf 10 MB
gesetzt. Die Angabe erfolgt in Bytes (10 MB = 10240000 Bytes). Wenn ein Benutzer eine Datei
hochlädt, die größer als der angegebene Wert ist, erhält dieser eine Fehlermeldung.

Es gibt zwei Parameter in der php.ini (Ablageort sowohl unter Ubuntu als auch OpenSUSE: /etc/
php5/apache2/php.ini), die in Verbindung mit dem Hochladen von Dokumenten im Publish-
Formular stehen:

1. der Wert von `upload_max_filesize` in der `php.ini` darf nicht kleiner sein als der Wert von
`publish.maxfilesize` (in der OPUS4 `config.ini`).

2. außerdem darf in der `php.ini` der Wert von `post_max_size` nicht kleiner sein als der Wert von
`upload_max_filesize` (genau genommen muss er sogar etwas größer sein)

Außerdem ist zu beachten, dass nach jeder Änderung in der `php.ini` ein Neustart des Apache
erforderlich ist:

    sudo /etc/init.d/apache2 restart

## Dateiformate

{% highlight ini %}
publish.filetypes.allowed defines which filetypes can be uploaded.
publish.filetypes.allowed = pdf,txt ; filetypes that are accepted in publication form
{% endhighlight %}

Über den Wert filetypes.allowed (in der OPUS4 `config.ini`) kann definiert werden, welche
Dateiformate bei den hochgeladenen Dateien zulässig sind. Die Standard-Formate sind pdf und txt.
Zum fehlerfreien Hochladen von Dokumenten muss sichergestellt sein, dass in der `php.ini` der
Parameter file_uploads auf "On" gesetzt ist.

<p class="warning">
Zur eigenen Sicherheit sollte darauf geachtet werden, an dieser Stelle keine ausführbaren
Dateitypen anzugeben.
</p>
