---
title: Anzeige von Latex-Formeln X
weight: 40
---

# Anzeige von Latex-Formeln

Latex-Formeln können in OPUS gerendert werden. Um das zu ermöglichen muss [MathJax][MATHJAX] installiert werden.
MathJax ist eine browserübergreifende, auf JavaScript basierende Bibliothek, die mathematische Formeln
und Gleichungen in Webbrowsern, die LaTeX und MathML Markup beinhalten, grafisch darstellt. Sie wird
als freie Software (Open-Source) unter Apache-Lizenz veröffentlicht.

* [MathJax installieren](../installation/mathjax.html)
{: class="navlist" }

Der Pfad, unter dem MathJax zu finden ist, muss in der Datei `$BASEDIR/application/configs/config.ini`
definiert werden. Dazu muss folgender Eintrag in die `config.ini` aufgenommen werden. Der Pfad muss relativ
zu `$BASEDIR/public/` angegeben werden.

~~~ ini
; JAVASCRIPT SETTINGS
javascript.latex.mathjax = "/js/MathJax/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
~~~

[MATHJAX]: https://www.mathjax.org/
