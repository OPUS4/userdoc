---
title: Leitlinien
---

# Leitlinien

## Erstellung

Besonders wichtig ist es, die Leitlinien des Betreibers anzugeben, weil dort die Übertragung der
Rechte beim Veröffentlichen geregelt wird. Die entsprechenden Texte müssen in die Dateien:

    $BASEDIR/application/configs/help/policies.en.txt
    $BASEDIR/application/configs/help/policies.de.txt

Es existieren viele gute Beispiele für Leitlinien und Rechtseinräumung im Internet (z.B. für den edoc-
Server der Humboldt Universität zu Berlin: http://edoc.hu-berlin.de/e_info/leitlinien.php bzw. http://
edoc.hu-berlin.de/e_info/license.php). Diese sollten aber nicht einfach übernommen werden.
Besonders im Hinblick auf Rechtssicherheit beim Betrieb des Repositoriums (Übertragung eines
einfachen Nutzungsrechts bei Veröffentlichung, Haftungsausschluss) sollten diese Texte von der
Rechtsabteilung o.ä. geprüft werden.

<p class="note">
Leitlinien werden auch vom DINI-Zertifikat 240 verlangt.
</p>

## Verlinkung

Bevor ein Nutzer ein Dokument veröffentlichen kann, muss er oder sie die rechtlichen Bedingungen
des Dokumentenservers akzeptieren. Dies geschieht durch das Setzen eines Häkchens in einer
Checkbox. Der Hilfetext zu dieser Checkbox sollte einen Link auf die Leitlinien enthalten. Dies wird
umgesetzt, indem man den folgenden Übersetzungsschlüssel in der Datei
`$BASEDIR/modules/publish/language_custom/field_hints.tmx` mit Instanz-spezifischen
Informationen ergänzt.

{% highlight xml %}
<tu tuid="hint_rights">
  <tuv xml:lang="en">
    <seg>Please confirm that you read and commit to the legal notices and <a href="http://localhost/mydomain/home/index/help#policies">policies</a> of our document server.</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Bitte bestätigen Sie, dass Sie die rechtlichen Hinweise sowie die <a href="http://localhost/mydomain/home/index/help#policies">Leitlinien</a> unseres Dokumentenservers gelesen haben und damit einverstanden sind.</seg>
  </tuv>
</tu>
{% endhighlight %}

<p class="note">
Der Hintergrund dieser Maßnahme ist der, dass man in den Sprachdateien nicht auf Variablen
verweisen kann, damit auch nicht auf relative Links innerhalb von OPUS4, die in jeder Instanz gültig
sind. Es sind nur absolute Links möglich.
</p>
