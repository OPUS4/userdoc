---
title: Layout
weight: 10
---

# Layout oder Logo anpassen

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


# Logo anpassen

Bei der  Installation von OPUS wird das Standard-Logo „OPUS“ ausgeliefert.
In der Datei `$BASEDIR/public/layouts/mylayout/common.phtml` ist das Logo definiert.

{% highlight php %}
 <h1 id="logo">
        <a href="<?= $this->optionUrl('logoLink') ?>" title="<?= $this->translate('logo_title') ?>"></a>
 </h1>
{% endhighlight %}


Die individuellen Anpassungen für das Logo müssen in folgenden Dateien erfolgen:


* Änderung der Logoeinstellung (Größe, Position und Image-URL) in der Datei `$BASEDIR/public/layouts/mylayout/css/custom.css`

{% highlight text %}
/* CSS for standard logo - modify to change logo*/
#logo a{
    height: 81px;
    width: 175px;
    background: white url(../img/logo/logo-inividuell.png) no-repeat right;
}

{% endhighlight %}

* Änderung des Logo-Links in der Datei `$BASEDIR/application/configs/config.ini`

{% highlight ini %}
; Link for main logo
logoLink = https://www.domain-individuell.de/

{% endhighlight %}



* Änderung des Logo-Titels in der Datei `$BASEDIR/modules/default/language_custom/default.tmx`

{% highlight php %}
<tu tuid="logo_title">
          <tuv xml:lang="en">
            <seg>Individueller Titel</seg>
          </tuv>
          <tuv xml:lang="de">
            <seg>Individueller Titel</seg>
          </tuv>
        </tu>

{% endhighlight %}

## Verwendung von 2 Logos

* Anpassungen in der Datei `$BASEDIR/public/layouts/mylayout/css/custom.css`

{% highlight text %}
/* CSS for standard logo - modify to change logo*/
#logo a{
    height: 81px;
    width: 175px;
    background: white url(../img/logo/logo-individuell-1.png) no-repeat right;
}

#logo a.logo2{
    height: 81px;
    width: 171px;
    background: white url(../img/logo/logo-individuell-2.png) no-repeat right;
}

{% endhighlight %}

* Eintrag der Logo-Links in der Datei `$BASEDIR/application/configs/config.ini`

{% highlight ini %}
; Link for main logo
logoLink = https://www.domain-individuell-1.de/
logoLink2 = https://www.domain-individuell-2.de/
{% endhighlight %}

* Eintrag beider Titel in der Datei `$BASEDIR/modules/default/language_custom/default.tmx`

{% highlight php %}
<tu tuid="logo_title">
          <tuv xml:lang="en">
            <seg>Individueller Titel-1</seg>
          </tuv>
          <tuv xml:lang="de">
            <seg>Individueller Titel-1</seg>
          </tuv>
</tu>

<tu tuid="logo2_title">
          <tuv xml:lang="en">
            <seg>Individueller Titel-2</seg>
          </tuv>
          <tuv xml:lang="de">
            <seg>Individueller Titel-2</seg>
          </tuv>
</tu>

{% endhighlight %}


* Eintrag des 2. Logos mit dem Attribut class="logo2" in der Datei `$BASEDIR/public/layouts/mylayout/common.phtml`

{% highlight php %}
<h1 id="logo">
    <a href="<?= $this->optionUrl('logoLink') ?>" title="<?= $this->translate('logo_title') ?>"</a>
   <a class="logo2" href="<?= $this->optionUrl('logoLink2') ?>" title="<?= $this-> translate('logo2_title') ?>"</a>	
    </h1>
{% endhighlight %}
