# OPUS 4 Handbuch

OPUS 4 Handbuch für Anwender und Administratoren. Das Git-Repository für das Handbuch befindet sich hier:

<https://opus4.github.io/userdoc>

Probleme mit der Dokumentation, Hinweise und Vorschläge, können als [Issues][ISSUES] gemeldet werden. Bitte dabei
vorher prüfen, ob es eventuell schon ein entsprechenden Issue gibt.

## Bei der Dokumentation helfen

Fehlerkorrekturen und Änderungen können als [Pull Requests][PULLREQ] zur Verfügung gestellt werden. Hinweise
dazu finden sich in der GitHub Dokumentation. Auf diesem Weg kann die OPUS 4 Community mit der Dokumentation
helfen. In der Regel sollte ein [Issue][ISSUES] angelegt werden before an neuen Inhalten gearbeitet wird, um
die Änderungen koordinieren zu können und doppelte Arbeit zu vermeiden.

Die Dokumentation verwendet [GitHub Pages][GHPAGES], um aus Markdown Dateien (.md) statische Webseiten zu
generieren. Dafür wird [Jekyll][JEKYLL] verwendet. Für das Rendern der Markdown Dateien verwendet GitHub
Pages momentan [Kramdown][KRAMDOWN].

Eine [Referenz][KRAMDOWNREF] für die von Kramdown unterstützte Synstax ist online verfügbar.
In der Entwicklerdokumentation von OPUS 4 finden sich weitere [Hinweise zum Erstellen der Dokumentation][CREATE].

Hinweise zur [Verwendung von Jekyll][GHPJEKYLL] finden sich in der Dokumentation zu GitHub Pages. Dort
steht auch wie man Jekyll lokal einrichten kann, um die generierten Seiten lokal prüfen zu können bevor
die Änderungen zu GitHub hochgeladen werden.

[CREATE]: htps://opus4.github.io/development/documentation.html
[GHPAGES]: https://pages.github.com/
[GHPJEKYLL]: https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/
[JEKYLL]: http://jekyllrb.com/
[KRAMDOWN]: http://kramdown.gettalong.org/
[KRAMDOWNREF]: http://kramdown.gettalong.org/quickref.html
[ISSUES]: https://github.com/OPUS4/userdoc/issues
[PULLREQ]: https://help.github.com/categories/collaborating-on-projects-using-pull-requests/
