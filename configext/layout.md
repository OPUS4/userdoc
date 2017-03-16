---
title: Layout
weight: 10
---

# Layout

OPUS 4 enthält ein Standard-Layout in `$BASEDIR/public/layouts/opus4`.

Kleine Anpassungen können direkt in diesem Layout vorgenommen werden.
Das hat den Vorteil, dass Git bei einem Update erkennen kann, ob lokale
Änderungen im Konflikt mit der zentralen Version stehen. Diese können
dann gezielt aufgelöst werden, mit den Tools die für Git zur Verfügung
stehen (z.B. `melt`). Änderungen in der neuen Version, die keinen 
Konflikt verursachen werden automatisch übernommen. 
 
## CSS anpassen 
 
Anpassungen am verwendeten CSS können in folgender Datei vorgenommen
werden.
 
    $BASEDIR/public/layouts/mylayout/css/custom.css
    
### Farbe von Export Links in Frontdoor
    
In der Frontdoor werden Exportlinks für Formate wie BibTeX und RIS 
angezeigt. Diese haben alle die gleiche Farbe. Mit folgendem CSS kann
das Aussehen dieser Links beeinflusst und zum Beispiel jedem eine eigene 
Farbe zugewiesen werden.

    #export a.export.bibtex {
        background: darkorange;
    }
  
## Eigenes Layout verwenden
 
Um ein eigenes Layout zu erstellen (im Folgenden `mylayout` genannt), 
müssen die folgenden Schritte vollzogen werden.

1\. Es muss ein Layoutverzeichnis durch Kopieren des mitgelieferten Standardlayouts erstellt werden:

{% highlight text %}
$ cd opus4/public/layouts
$ cp -r opus4 <mylayout>
{% endhighlight %}

2\. Nun können die gewünschten CSS-Anpassungen in `$BASEDIR/public/layouts/mylayout/css/custom.css` durchgeführt werden.

Wenn Sie Änderungen am CSS in späteren OPUS4-Releases einfach übernehmen wollen,
dann empfehlen wir die instanzspezifischen Änderungen nur in der Datei
`$BASEDIR/public/layouts/mylayout/css/custom.css` (und nicht in den anderen mitgelieferten CSS-Dateien)
vorzunehmen. Bei späteren OPUS4-Updates brauchen Sie lediglich die standardmäßig
ausgelieferte CSS-Datei `$BASEDIR/public/layouts/opus4/css/opus.css` in ihr eigenes
Layoutverzeichnis kopieren.

3\. Damit OPUS die CSS-Datei `$BASEDIR/public/layouts/mylayout/css/custom.css` verwendet, müssen Sie in
  der Datei `$BASEDIR/public/layouts/mylayout/common.phtml` das Kommentarzeichen für folgende Zeile entfernen:

{% highlight php %}
$this->headLink()->appendStylesheet($this->layoutPath() . '/css/custom.css');
{% endhighlight %}

4\. In der Konfigurationsdatei `$BASEDIR/application/configs/config.ini` muss nun noch das Layout mylayout aktiviert werden:

{% highlight ini %}
; The 'theme' setting can be used to select a different theme.
theme = mylayout
{% endhighlight %}
