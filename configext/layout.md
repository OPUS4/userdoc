---
title: Layout
weight: 10
---

# Layout

OPUS4 liefert ein Standard-Layout `$BASEDIR/public/layouts/opus4` mit aus. Dieses sollte nicht verändert werden,
da diese Änderungen bei Updates überschrieben werden. Um ein eigenes Layout (im Folgenden mylayout genannt) zu
erstellen, müssen die folgenden Schritte vollzogen werden.

1. Es muss ein Layoutverzeichnis durch Kopieren des mitgelieferten Standardlayouts erstellt werden:

{% highlight text %}
$ cd opus4/public/layouts
$ cp -r opus4 <mylayout>
{% endhighlight %}

2. Nun können die gewünschten CSS-Anpassungen in `$BASEDIR/public/layouts/mylayout/css/custom.css` durchgeführt werden.

Wenn Sie Änderungen am CSS in späteren OPUS4-Releases einfach übernehmen wollen,
dann empfehlen wir die instanzspezifischen Änderungen nur in der Datei `$BASEDIR/public/layouts/mylayout/css/custom.css` (und nicht in den anderen mitgelieferten CSS-Dateien)
vorzunehmen. Bei späteren OPUS4-Updates brauchen Sie lediglich die standardmäßig
ausgelieferte CSS-Datei `$BASEDIR/public/layouts/opus4/css/opus.css` in ihr eigenes
Layoutverzeichnis kopieren.

3. Damit OPUS die CSS-Datei `$BASEDIR/public/layouts/mylayout/css/custom.css` verwendet, müssen Sie in der Datei `$BASEDIR/public/layouts/mylayout/common.phtml` das Kommentarzeichen für folgende Zeile entfernen:

{% highlight php %}
$this->headLink()->appendStylesheet($this->layoutPath() . '/css/custom.css');
{% endhighlight %}

4. In der Konfigurationsdatei `$BASEDIR/application/configs/config.ini` muss nun noch das Layout mylayout aktiviert werden:

{% highlight ini %}
; The 'theme' setting can be used to select a different theme.
theme = mylayout
{% endhighlight %}
