---
title: Update von 4.4.5
---

# Update auf Git Version von 4.4.5

OPUS wurde bis Version 4.4.5 als Tarball mit einem Update Skript ausgeliefert. Für die Version 4.5 gibt es keinen
Tarball und auch kein Update Skript. Die neues Version ist die erste bei der die Installation auf Git basiert.

* [OPUS mit Git][GITOPUS]
{: class="navlist" }

Um eine existierende OPUS 4.4.5 Instanz auf Git umzustellen, sollte man eine neue Instanz mit Git installieren und
anschließend die Anpassungen der alten Instanz auf die neue übertragen. Dafür kann zum Beispiel ein Werkzeug wie
[MELD][MELD] gut eingesetzt werden, um die die alten Dateien mit den neuen zu vergleichen und die Anpassungen zu
übernehmen.

Bei den Dokumenttypen hat sich die Referenz auf den xml-namespace geändert. Damit eigene oder angepasste Dokumenttypen 
weiter verwendet werden können, muss in den entsprechenden Dateien der Namespace ausgetauscht werden.

So ist z.B. in der Datei '$BASEDIR/application/configs/doctypes/article.xml'  
{% highlight xml %}
xmlns="http://schemas.opus.org/documenttype" 
{% endhighlight %}

zu ersetzen durch:

{% highlight xml %}
xmlns="http://www.opus-repository.org/schema/documenttype"
{% endhighlight %}


* [Installation von OPUS 4][INSTALL]
{: class="navlist" }

[GITOPUS]: ../gitopus.md
[INSTALL]: index.md
[MELD]: http://meldmerge.org/
