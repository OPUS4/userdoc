---
title: RSS Feeds
---

# RSS Feeds

OPUS 4 kann RSS Feeds für verschiedene Suchanfragen zur Verfügung stellen. Der folgende Link zeigt den RSS Feed für
die neuesten Dokumente in der OPUS 4 Demo Instanz.

<https://opus4web.zib.de/opus4-demo/rss>

Der Titel und die Beschreibung der RSS-Feeds können konfiguriert werden. Die Konfigurationschlüssel dafür können
in der `config.ini` gesetzt werden.

| Parameter | Default |
|-----------+---------|
| rss.default.feedTitle | "%4$s" - Volle URL, z.B. "http://opus4.kobv.de/opus4-zib" |
| rss.default.feedDescription | "OPUS documents" |

Für den Feed-Title kann ein beliebiger String angegeben werden, z.B. den Namen der Instanz. Es ist aber auch möglich
die folgenden vier Platzhalter in dem String zu verwenden, um die URL oder Teile der URL der Instanz im Titel zu
verwenden.

| Platzhalter | Beschreibung |
|-------------|--------------|
| %1$s | Name der Instanz (Schlüssel 'name' in config.ini) |
| %2$s | Hostname, z.B. `opus4.kobv.de` |
| %3$s | Base URL, z.B. `opus4-zib` |
| %4$s | Volle URL, z.B. `http://opus4.kobv.de/opus4-zib` |

Wenn auf einem Server mehrere Instanzen gehostet werden kann zum Beispiel die Base URL verwendet werden, um sie zu
unterscheiden. Bei Instanzen mit einer eigenen Domain kann der Hostname eingesetzt werden.

<p class="note">
Die volle URL wird als Standardwert für den Titel verwendet, da damit jede Instanz automatisch einen eindeutigen
Titel bekommen und somit von anderen Instanzen unterschieden werden kann.
</p>
