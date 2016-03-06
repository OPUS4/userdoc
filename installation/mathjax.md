---
title: MathJax installieren
---

# MathJax installieren

[MathJax][MATHJAX] kann für die [Anzeige von Latex-Formeln][LATEX] verwendet werden. Es ist nicht automatisch
Bestandteil von OPUS 4. MathJax muss nachträglich installiert und konfiguriert werden.

* [MathJax in der Konfiguration aktivieren](../config/latex.html)
{: class="navlist" }

Die Git-Version von OPUS 4 verwendet [Composer][COMPOSER], um Abhängigkeiten herunterzuladen und zu verwalten.
Mit dem folgenden Kommando lässt sich MathJax automatisch von [Packagist.org][PACKAGIST] herunterladen und lokal
im Verzeichnis `$BASEDIR/vendor` installieren.

    composer require "mathjax/mathjax: 2.6.1"

Die MathJax Dateien befinden sind anschließend unter `$BASEDIR/vendor/mathjax/mathjax`. Damit sie in OPUS verwendet
werden können muss noch manuell eine Verknüpfung für MathJax im Javascript (`js`) Verzeichnis von OPUS angelegt werden.
Dazu wechselt man in das Verzeichnis `$BASEDIR/public/js` (muss gegebenenfalls angelegt werden) und führt folgendes
Kommando aus (Linux).

    ln -sv ../../vendor/mathjax/mathjax MathJax

Die MathJax Dateien sind nun im Javascript Verzeichnis von OPUS 4 verfügbar und der [Support für Latex][LATEX] kann
in der Konfiguration aktiviert werden.

<p class="note" markdown="1">
Bei der Installation mit `require` wird MathJax automatisch in die `composer.json` Datei der OPUS Instanz eingetragen.
</p>

## Installation ohne Composer

MathJax kann auch ohne Composer manuell unter <http://docs.mathjax.org/en/latest/installation.html> heruntergeladen
und unter `$BASEDIR/public/js/` bzw. an beliebiger Stelle installiert werden. Das macht unter anderem Sinn, wenn auf
einem System mehrere OPUS 4 Repositorien betrieben werden und die MathJax Dateien nur einmal lokal abgelegt werden
sollen.

[MATHJAX]: https://www.mathjax.org/
[LATEX]: ../config/latex.html
[COMPOSER]: https://getcomposer.org/
[PACKAGIST]: https://packagist.org/packages/mathjax/mathjax