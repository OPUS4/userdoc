---
title: Anzeige von Latex-Formeln
weight: 40
---

# Anzeige von Latex-Formeln

Latex-Formeln können nun in OPUS gerendert werden. Um das zu ermöglichen ist MathJax unter
`$BASEDIR/public/js/` zu installieren. MathJax ist eine browserübergreifende, auf JavaScript
basierende Bibliothek, die mathematische Formeln und Gleichungen in Webbrowsern, die LaTeX und
MathML Markup beinhalten, grafisch darstellt. Sie wird als freie Software (Open-Source) unter
Apache-Lizenz veröffentlicht.

MathJax kann unter <http://docs.mathjax.org/en/latest/installation.html> heruntergeladen werden und ist
nicht Bestandteil der OPUS-Auslieferung.

Der Pfad, unter dem MathJax zu finden ist, wird in der `$BASEDIR/application/configs/config.ini`
definiert. Dazu ist folgender Eintrag aus der `config.ini.template` in die `config.ini` zu
übernehmen, die Kommentarzeichen zu entfernen und der Pfad ggf. anzupassen. Der Pfad ist relativ
zu `$BASEDIR/public/` anzugeben.

~~~ ini
; JAVASCRIPT SETTINGS
javascript.latex.mathjax = "/js/MathJax/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
~~~

