---
title: RSS Feeds
---

# RSS Feeds

Der Titel und die Beschreibung der RSS-Feeds können konfiguriert werden. Die Konfigurationschlüssel dafür können
in der `config.ini` gesetzt werden.

| Parameter | Default |
|-----------+---------|
| rss.default.feedTitle | "%4$s" - Volle URL, z.B. "http://opus4.kobv.de/opus4-zib" |
| rss.default.feedDescription | "OPUS documents" |

Für den Feed-Title kann ein beliebiger String angegeben werden. Dabei ist es möglich die folgenden vier Platzhalter
zu verwenden.

| Platzhalter | Beschreibung |
|-------------|--------------|
| %1$s | Name der Instanz (Schlüssel 'name' in config.ini)|
| %2$s | Hostname, z.B. `opus4.kobv.de` |
| %3$s | Base URL, z.B. `opus4-zib` |
| %4$s | Volle URL, z.B. `http://opus4.kobv.de/opus4-zib` |

Wenn auf einem Server mehrere Instanzen gehostet werden kann zum Beispiel die Base URl verwendet werden, um sie zu
unterscheiden. Bei Instanzen mit einer eigenen Domain kann der Hostname eingesetzt werden.
