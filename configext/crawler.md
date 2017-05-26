---
title: Indexieren durch Suchmachinen
---

# Indexieren durch Suchmaschinen (Webcrawler)

Das OPUS-Modul `crawlers` erleichtert Suchmaschinen die Indexierung, indem es sogenannte
Deeplinks auf die Frontdoors der veröffentlichten Dokumente auflistet. Das ist u.a. für die 
Sichtbarkeit in Google Scholar hilfreich. Der Nutzerrolle `guest` wird im Standard der 
Zugriff auf das  Modul `crawlers` gewährt ([Zugriffskontrolle](../admin/security.html)).

## robots.txt

Suchmaschinen sollten normalerweise nur die Module __frontdoor__ und
__crawlers__ besuchen. Über __crawlers__ stehen Links zu allen Dokumenten zu Verfügung. In
der Frontdoor finden sich die öffentlichen Metadaten zu den Dokumenten. Mit einer `robots.txt`
Datei im Root-Verzeichnis des Webservers kann das gesteuert werden. Die Datei könnte wie folgt
aussehen, wobei `/opus4` für die jeweilige URL des Repositories angepasst werden muss.

    disallow: /opus4
    allow: /opus4/frontdoor
    allow: /opus4/crawlers
    
Mit folgender Regel kann auch noch der Zugriff auf die Volltextdateien erlaubt werden.

    allow: /opus4/files
        
Die Datei `robots.txt` liegt häufig nicht im OPUS 4 Verzeichnis, da sie für einen Server
bzw. eine Subdomain nur einmal angelegt werden kann. Werden mehrere Repositorien gehostet
enthält die Datei dann mehrere unterschiedliche Einträge.

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
