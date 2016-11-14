---
title: Indexieren durch Webcrawler
---
# Indexieren durch Webcrawler

Das OPUS-Modul `crawlers` erleichtert Suchmaschinen die Indexierung, indem es sogenannte
Deeplinks auf die Frontdoors der veröffentlichten Dokumente auflistet. Das ist u.a. für die 
Sichtbarkeit in Google Scholar hilfreich. Der Nutzerrolle `guest` wird im Standard der 
Zugriff auf das  Modul `crawlers` gewährt ([Zugriffskontrolle](../admin/security.html)).

## Indexieren durch Webcrawler verhindern

Aber auch wenn das Modul `crawlers` nicht freigeschaltet ist, können Suchmaschinen durchaus Inhalte indexieren, 
z.B. wenn sie über das Browsing auf die Frontdoors gelangen. Das Anlegen einer `robots.txt`-Datei schützt nicht in 
jedem Fall davor, dass alle Suchmaschinen-Crawler die Indexierung unterlassen, da es lediglich ein Hinweis
oder eine Bitte ist, dies zu unterlassen.

<p class="note">
Um Crawler wirkungsvoll abzuhalten wird der Zugriff bereits über den Apache Webserver
gesperrt, in dem z.B. explizit IP-Adressen bzw. IP-Adressbereiche angegeben werden, die Zugriff
auf OPUS haben dürfen. Insbesondere für Testsysteme, deren Daten nicht nach außen gelangen
sollen, ist dies dringend zu empfehlen.
</p>

Für weniger kritische Fälle kann, um eine Suchmaschine davon abzuhalten, die Seite zu
durchsuchen, folgender Tag im html-head in der `$BASEDIR/public/layouts/opus4/common.phtml`
ergänzt werden:

    <meta name="robots" content="noindex, nofollow">

Der Eintrag sieht dann folgendermaßen aus:

{% highlight html %}
<head>
    <?= $this->headMeta() ?>
    <?= $this->headTitle() ?>
    <?= $this->headLink() ?>
    <?= $this->headScript() ?>

    <!--[if IE 6]>
    <link rel="stylesheet" type="text/css" href="<?= $this->layoutPath() ?>/css/opus-ie.css" />
    <![endif]-->

    <!--[if lt IE 9]>
    <link rel="stylesheet" type="text/css" href="<?= $this->layoutPath() ?>/css/opus-ie-7.css" />
    <![endif]-->

    <meta name="robots" content="noindex, nofollow">
</head>
{% endhighlight %}

<p class="note" markdown="1">
Die Datei `common.phtml` muss innerhalb des entsprechenden (aktuell genutzten
Verzeichnisses geändert werden.
</p>
