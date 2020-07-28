---
title: Leitlinien
---

# Leitlinien

## Erstellung

Besonders wichtig ist es, die Leitlinien des Betreibers anzugeben, weil dort die Übertragung der
Rechte beim Veröffentlichen geregelt wird. Die entsprechenden Texte sind unter dem Übersetzungsschlüssel 
`help_content_policies` gespeichert und können entweder in der [Übersetzungsverwaltung][TRANSLATIONS] oder über die  
FAQ-Seite editiert werden. 

Es existieren viele gute Beispiele für Leitlinien und Rechtseinräumung im Internet (z.B. für den edoc-
Server der Humboldt Universität zu Berlin: `http://edoc.hu-berlin.de/e_info/leitlinien.php` bzw.
`http://edoc.hu-berlin.de/e_info/license.php`). Diese sollten aber nicht einfach übernommen werden.
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
umgesetzt, indem man den Übersetzungsschlüssel `hint_rights` mit Instanz-spezifischen
Informationen ergänzt, z.B.

{code}
Please confirm that you read and commit to the legal notices and 
<a href="http://localhost/mydomain/home/index/help#policies">policies</a> of our document server.
{code}

{code}
Bitte bestätigen Sie, dass Sie die rechtlichen Hinweise sowie die 
<a href="http://localhost/mydomain/home/index/help#policies">Leitlinien</a> unseres Dokumentenservers gelesen haben 
und damit einverstanden sind.
{code}

<p class="warning">
In den Übersetzungen kann man keine relative Links oder Variablen verwenden. Es sind nur absolute Links möglich.
</p>

[TRANSLATIONS]: ../translation/index.html
