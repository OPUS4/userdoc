---
title: config.ini
---

# Optionen in der config.ini

Hier sind die Optionen in der `config.ini` beschrieben, mit denen eine OPUS 4 Instanz angepasst werden kann. Die
technisch notwendigen Parameter, z.B. für die Datenbankverbindung, die bereits bei der Installation konfiguriert
wurden, werden auf separaten Seiten beschrieben.

## Theme

Dieser Parameter dient dazu, ein anderes als das Standard-Layout zu aktivieren. (siehe Kapitel Layout 94 )

{% highlight ini %}
; The 'theme' setting can be used to select a different theme.
theme = opus4
{% endhighlight %}

## Suche

### Facetten ein/-ausblenden und Reihenfolge verändern

Darüber hinaus ist es möglich, die Reihenfolge der Facetten durch Vertauschen der Einträge zu
modifizieren und Facetten ein- oder auszublenden. Standardmäßig werden in der Ergebnisanzeige
nach einer Suche alle Facetten angezeigt.

{% highlight ini %}
; Facets fields to be considered.
searchengine.solr.facets = author_facet,year,doctype,language,has_fulltext,belongs_to_bibliography,subject,institute
{% endhighlight %}

<p class="warning">
In und zwischen den Facettennamen dürfen keine Leerzeichen verwendet werden.
</p>

### Anzahl der angezeigten Werte pro Facette ändern

Es werden standardmäßig 10 am häufigsten in der Treffermenge vorkommenden Werte pro Facette
angezeigt. Dies kann global für alle Facetten geändert werden:

    searchengine.solr.globalfacetlimit =

Es kann auch für einzelne Facetten festgelegt werden, wieviele Werte pro Facette angezeigt werden:

    searchengine.solr.facetlimit.<facetname> =

Als Wert für `<facetname>` sind nur die Werte im Schlüssel searchengine.solr.facets zulässig.

* `author_facet`
* `year`
* `doctype`
* `language`
* `has_fulltext`
* `belongs_to_bibliography`
* `subject`
* `institute`

Werden beide Schlüssel in Kombination benutzt, so gilt:

* `searchengine.solr.globalfacetlimit` überschreibt den Standardwert global
* `searchengine.solr.facetlimit.<facetname>` überschreibt
  `searchengine.solr.globalfacetlimit` für die gewählte(n) Facette(n)

<p class="note" markdown="1">
Diese Parameter sind nicht in der ausgelieferten Datei `$BASEDIR/application/configs/config.ini.template`
enthalten, sondern müssen hinzugefügt werden.
</p>

<p class="note">
Die hier eingetragenen Werte bezeichnen die Maximalanzahl: sind nach einer Suche weniger
Werte in einer Facette vorhanden, werden also auch weniger Werte als im entsprechenden
Parameter angegeben angezeigt.
</p>

### Sortierkriterium für Facetten ändern

Standardmäßig werden alle Facetten absteigend nach Häufigkeit sortiert. Es gibt die Möglichkeit, für
eine oder mehrere der vorhandenen Facetten das Sortierkriterium auf "lexikographisch aufsteigend"
zu ändern. Dies geschieht pro Facette mit dem folgenden Eintrag:

{% highlight ini %}
searchengine.solr.sortcrit.<facetname> = lexi
{% endhighlight %}

Als Wert für `<facetname>` sind nur die Werte im Schlüssel searchengine.solr.facets zulässig
(`author_facet`, `year,doctype`, `language`, `has_fulltext`, `belongs_to_bibliography`, `subject,institute`).

### Absteigende Sortierung für die Facette Erscheinungsjahr

Für die Facette "Erscheinungsjahr" gibt es die Möglichkeit eine absteigende Sortierung nach dem
Jahr, d.h. mit dem neuesten Jahr beginnend, einzustellen. Dazu sind die folgenden Änderungen
notwendig:

* Wenn der Schlüssel `searchengine.solr.facets` vorhanden ist diesen modifizieren: `year`
  ersetzen durch `year_inverted`.
* Wenn der Schlüssel searchengine.solr.facets noch nicht vorhanden ist diesen Schlüssel aus
  der Datei `$BASEDIR/application/configs/application.ini` in die `config.ini` übernehmen
  und `year` in `year_inverted` ändern.
* In beiden Fällen zusätzlich den Schlüssel `searchengine.solr.sortcrit.year_inverted` auf
  den Wert `lexi` setzen:

{% highlight ini %}
searchengine.solr.sortcrit.year_inverted = lexi
{% endhighlight %}

## Mail

Die folgenden Einstellungen legen fest, welche E-Mailadresse benutzt wird, wenn OPUS4 Mails
verschickt:

{% highlight ini %}
; MAIL SETTINGS
; mail.opus.smtp = localhost ; SMTP server for sending email
; mail.opus.port = 25 ; SMTP server port for sending email
mail.opus.address = <E-Mail-Adresse, z.B. noreply@bibliothekxyz.de>
mail.opus.name = <Name, z.B. BibliothekXYZ>
{% endhighlight %}

## Benachrichtigungen (Notification)

In OPUS4 kann eine Benachrichtigungsfunktion konfiguriert werden. Das System kann dann zu den
Ereignissen "Submission" (Neues Dokument wurde eingestellt) und "Publication" (Dokument wurde
freigeschaltet) E-Mails an vorher festgelegte E-Mail-Adressen verschicken.
Grundsätzlich ist die Benachrichtigungsfunktion per Default deaktiviert. Sie kann getrennt für die
Ereignisse "Submission" und "Publication" in der config.ini aktiviert werden, indem die
entsprechenden Schlüssel aus der config.ini.template kopiert und die Kommentarzeichen entfernt
werden:

{% highlight ini %}
;NOTIFICATION SETTINGS
; comma separated list of email addresses that should receive a
; submission notification email
notification.document.submitted.email = ""

; comma separated list of email addresses that should receive a
; publication notification email
notification.document.published.email = ""

; uncomment the next line if notification emails should be sent
; if a new document is submitted
notification.document.submitted.enabled = 1

; uncomment the next line if notification emails should be sent
; if a document is published
notification.document.published.enabled = 1
{% endhighlight %}

Zusätzlich ist es notwendig, dass der generelle Mailversand in den [Mail Einstellungen](#Mail) konfiguriert
ist.

### Konfiguration der "Submission"-Benachrichtigung

1. Benachrichtigungsfunktion aktivieren, indem das Kommentarzeichen vor dem Schlüssel
`notification.document.submitted.enabled = 1` entfernt wird:

{% highlight ini %}
;NOTIFICATION SETTINGS
; uncomment the next line if notification emails should be sent
; if a new document is submitted
notification.document.submitted.enabled = 1
{% endhighlight %}

2. Den Schlüssel notification.document.submitted.email aktivieren und die E-Mail-Adressen
eintragen, an die die Submission-Mail verschickt werden soll. Mehrere Adressen werden durch
Komma getrennt:

{% highlight ini %}
;NOTIFICATION SETTINGS
; comma separated list of email addresses that should receive a
; submission notification email
notification.document.submitted.email = "mustermann@example.org,musterfrau@example.org,bibliothek@unixyz.de"
{% endhighlight %}

### Konfiguration der "Publication"-Benachrichtigung

1. Benachrichtigungsfunktion aktivieren, indem das Kommentarzeichen vor dem Schlüssel
`notification.document.published.enabled = 1` entfernt wird:

{% highlight ini %}
;NOTIFICATION SETTINGS
; uncomment the next line if notification emails should be sent
; if a document is published
notification.document.published.enabled = 1
{% endhighlight %}

2. Den Schlüssel notification.document.published.email aktivieren und die E-Mail-Adressen
eintragen, an die die Publication-Mail verschickt werden soll. Mehrere Adressen werden durch
Komma getrennt:

{% highlight ini %}
;NOTIFICATION SETTINGS
; comma separated list of email addresses that should receive a submission
notification email
notification.document.submitted.email = "mustermann@example.org,musterfrau@example.org,bibliothek@unixyz.de"
{% endhighlight %}

### Konfiguration der E-Mail-Inhalte (Subject und Body)

Der Inhalt der E-Mails wird über PHP-Templates gesteuert. In der Standardauslieferung sind im
Verzeichnis `$BASEDIR/application/configs/mail_templates` zwei Templates enthalten:

    submitted.phtml
    published.phtml

Diese sollten nicht verändert werden, da sie beim Update überschrieben werden. Ist eine
Veränderung gewünscht, so sollten in dem gleichen Verzeichnis neue Templates angelegt werden.
Die Aktivierung dieser Templates erfolgt dann durch Angabe des Dateinamens im Schlüssel
`notification.document.submitted.template` bzw. im Schlüssel
`notification.document.published.template`, die in die `config.ini` eingetragen werden müssen:

{% highlight ini %}
notification.document.submitted.template = "my_submitted.phtml"
notification.document.published.template = "my_published.phtml"
{% endhighlight %}

In den Templates stehen vier Variablen zur Verfügung:

* `$authors` (Array der Autorennamen)
* `$title` (Haupttitel in Dokumentsprache)
* `$docId` (Dokument-ID)
* `$url` (Deeplink auf Administration (bei Submission-Mail) bzw. Frontdoor (bei Publication-Mail))

Der Betreff der E-Mails kann ebenfalls verändert werden über die Schlüssel
`notification.document.submitted.subject` bzw.
`notification.document.published.subject`, die in die `config.ini` eingetragen werden müssen. Die
Standardeinstellungen lauten:

{% highlight ini %}
notification.document.submitted.subject = "Dokument #%1$s im OPUS4-Dokumentenserver eingestellt: %2$s : %3$s"
notification.document.published.subject = "Dokument #%1$s im OPUS4-Dokumentenserver veröffentlicht: %2$s : %3$s"
{% endhighlight %}

Die Platzhalter bezeichnen dabei:

| Platzhalter | Beschreibung |
|-------------+--------------|
| %1$s | Dokument-ID |
| %2$s | Liste der Autorennamen (getrennt durch Semikolon) |
| %3$s | Haupttitel in Dokumentsprache |

Sind keine Autoren bzw. kein Haupttitel vorhanden, wird "n/a" ausgegeben.

<p class="warning">
Die "Submission"-Benachrichtigung übernimmt direkt die Eingaben bezüglich Haupttitel und
Autorennamen aus dem Formular. Ein Benutzer kann hier durchaus beliebigen Inhalt eintragen,
also auch HTML-Markup oder beliebige URLs, die beim Anklicken Schaden verursachen können
(z.B. Phishing). Die Benachrichtigungs-E-Mails werden zwar mit `Content-Type: text/plain;
charset=utf-8` ausgeliefert, es sollte aber dennoch darauf hingewiesen werden, dass nur der
OPUS4-Deeplink in der Mail angeklickt wird (da einige Mail-Clients, z.B. Thunderbird, automatisch
auch URLs in text/plain-Mails als Link anbieten).
</p>

### Benachrichtigung von Autor(en) und Einsteller

Ist die "Publication"-Benachrichtigung aktiviert, kann zusätzlich der Einsteller (Submitter) und jeder
Autor des Dokuments eine E-Mail (einzeln) erhalten, sofern für diese im System eine E-Mailadresse
hinterlegt ist.

Hierfür wird beim Freischalten eines Dokuments nachgefragt, wer eine E-Mail erhalten soll:

![Menü](../img/config/sc_notification_authors.png){:width="640px"}

Für den Fall, dass es sich bei Einsteller und Autor um dieselbe Person handelt, wird nur einmal eine
E-Mail verschickt.

<p class="warning" markdown="1">
ACHTUNG: In OPUS4 erscheint beim Freischalten (Publizieren) eines Dokumentes eine
Zwischenseite, in der um Bestätigung des Vorganges gebeten wird. Die Konfigurationseinstellung
für diese Bestätigungsseite wird ebenfalls in der `config.ini` festgelegt (der Defaultwert = 1 sorgt
dafür, dass die Bestätigungsseite erscheint).
Seit OPUS 4.4.1 ist es möglich diese Seite mit der Konfigurationseinstellung
`confirmation.document.statechange.enabled = 0` auszuschalten. Damit stehen dann auch die
oben beschriebenen Funktionen nicht zur Verfügung, da OPUS4 sich die Änderung des Status
eines Dokuments nicht mehr bestätigen lässt, sondern diese sofort durchführt.
</p>

## Benachrichtigungen bei Applikationsfehlern

Hier kann eingetragen werden, an wen Fehlermeldungen per Mail verschickt werden.

{% highlight ini %}
;ERROR CONTROLLER SETTINGS - who should receive error mails?
errorController.mailTo.name = Name
errorController.mailTo.address = E-Mail-Adresse
{% endhighlight %}

## Checksummen

OPUS4 kann automatisch Hashwerte für Dateien von Dokumenten erzeugen, welche die Integrität
der jeweiligen Datei überprüfen. Diese Hashwerte werden beim Einstellen von neuen Dateien
berechnet, in der Datenbank abgespeichert und im Dateimanager 112 im Administrationsbereich
angezeigt. Da die Berechnung der Hashwerte bei großen Dateien sehr lange dauern kann (was zu
Fehlermeldungen führt), kann in der Datei `$BASEDIR/application/configs/config.ini` eine
Höchstgrenze für die Dateigröße eingestellt werden:

{% highlight ini %}
; Maximum filesize in MB (default 50 MB) for calculating MD5 and SHA512 hashes
; of files. The maximum filesize is limited to avoid excessive load on the
; server.
; In order to raise or reduce the limit remove the comment character below and
; adjust the value.
; 0 : Turns generation of hashes completely off.
; -1 : Enables calculation of hashes for all files without upper limit.
checksum.maxVerificationSize = 50
{% endhighlight %}

Um diese Funktion zu nutzen, muss der Parameter `checksum.maxVerificationSize` durch
Entfernen des Kommentarzeichens aktiviert werden. Folgende Werte sind möglich:

| Wert | Beschreibung |
|------+--------------|
|   0  | schaltet die Funktion aus |
|  -1  | ermöglicht die Berechnung des Hashwerts ohne Höchstgrenze |
| **n** | Berechnung des Hashwerts mit Höchstgrenze **n** MB |

## Publishformular

### Bibliographiefunktion

Der Parameter form.first.bibliographie gibt an, ob eine Checkbox für die Zuordnung zur
Bibliographie angezeigt werden soll. Mögliche Werte: 0 - nicht anzeigen / 1 - anzeigen, Standard ist 0.

{% highlight ini %}
; If you would like to use opus to save bibliographical items you should set
; this to 1. It will ask on the first site of the publish module if a new
; document should be added to the bibliography.
form.first.bibliographie = 0
{% endhighlight %}

### Datei-Upload abschalten

Mit dem Parameter `form.first.enable_upload` kann das Hochladen einer Datei im ersten Schritt
des Veröffentlichungsvorgangs abgeschaltet werden. Mögliche Werte: 0 - abgeschaltet / 1 -
angeschaltet, Standard ist 1.

{% highlight ini %}
; uncomment next line if file upload in first publish form should be disabled
form.first.enable_upload = 0
{% endhighlight %}

### Datei-Upload als Pflichtfeld

Der Parameter form.first.require_upload gibt an, ob das Hochladen einer Datei obligatorisch
ist. Mögliche Werte: 0 - optional / 1 - obligatorisch, Standard ist 1.

{% highlight ini %}
; States, if the upload-fields are required to enter the second form.
form.first.require_upload = 0
{% endhighlight %}

### Einräumen eines Nutzungsrechts

Der Parameter form.first.show_rights_checkbox gibt an, ob das Auswählen der Checkbox für
das Einräumen eines Nutzungsrechts auf der ersten Seite des Veröffentlichungsformulars
obligatorisch ist. Mögliche Werte: 0 - optional / 1 - obligatorisch, Standard ist 1.

{% highlight ini %}
; States, if a checkbox for the institutions legal notices is shown.
form.first.show_rights_checkbox = 1
{% endhighlight %}

Sollte kein Interesse bestehen, dieses Feld anzuzeigen, entfernen Sie bitte den Kommentar bei dem
Parameter in Ihrer config.ini und setzen Sie den Wert auf 0. Für den Fall, dass nur bei bestimmten
Dokumenttypen das Ankreuzen der Checkbox für das Einräumen eines Nutzungsrechts verpflichtend
sein soll, besteht die Möglichkeit, die Checkbox direkt in den Dokumenttyp aufzunehmen (Kapitel
Grundlage: Templates 85 ).

## OAI Export

An dieser Stelle werden die OAI-Parameter eingetragen.

{% highlight ini %}
; OAI SETTINGS
oai.baseurl =
oai.repository.name = Opus4 Demo Instance
oai.repository.identifier = opus4.demo
oai.sample.identifier = oai:opus4.demo:90
oai.ddb.contactid =
{% endhighlight %}

Bei dem Parameter oai.baseurl wird die URL eingetragen, unter der die OAI-Schnittstelle
erreichbar ist. Diese wird in der Schnittstelle unter <baseURL> angezeigt und wird normalerweise
automatisch auf den Hostnamen der Opus-Instanz gesetzt. Sie sollte daher nur geändert werden,
falls eine abweichende URL gewünscht wird (z.B. bei Rechnern, die mehrere DNS-Einträge
besitzen). Der Parameter oai.repository.name wird in der OAI-Schnittstelle unter
<repositoryName> und oai.repository.identifier unter <repositoryIdentifier> angezeigt. Bei
oai.sample.identifier kann ein existierendes Dokument eingetragen werden, das in der
Schnittstelle unter <sampleIdentifier> (d.h. Beispiel-Dokument) angezeigt wird. Schließlich kann bei
oai.ddb.contactid eine DNB-Contact-ID (wenn vorhanden) eingetragen werden.

Die darüber hinaus existierenden Parameter oai.max.listrecords ( Anzahl der Einträge für das
Kommando "ListRecords) und oai.max.listidentifiers (Anzahl der Einträge für das Kommando
"ListIdentifiers") werden bereits bei der Installation mit Standardwerten befüllt und müssen in der
Regel nicht angepasst werden.

## Print on Demand

Es ist möglich, in OPUS4 eine Print on Demand-Funktion (PoD) anzubieten. Wenn diese Funktion
konfiguriert ist, wird auf der Frontdoor eines Dokuments ein entsprechender Link zum PoD-Service
angezeigt. Ob ein Dokument auf diese Weise bestellbar ist, wird über die Lizenz des Dokuments
geregelt. Nur wenn dort durch ein Häkchen PoD erlaubt ist, erfolgt die Anzeige auf der Frontdoor.

Um diese Funktion auf der Frontdoor zu aktivieren, sind in der config.ini für die entsprechenden
Parameter die Kommentarzeichen zu entfernen und die Parameter mit entsprechenden Werten zu
befüllen:

{% highlight ini %}
; PRINT ON DEMAND SETTINGS
; To enable print on demand services specifiy the provider's url
; and (optionally) the name of a button image.
; The image must reside in the current layout's image folder
; ($BASEDIR/public/layouts/<LAYOUT>/img/)
;
; When a provider is specified, the print on demand button or link will
; be displayed if the document's licence allows it.
printOnDemand.url =
printOnDemand.button =
{% endhighlight %}

Bei dem Parameter printOnDemand.url wird die URL eines Anbieters eingetragen. Optional kann
für den Parameter printOnDemand.button eine Bild-Datei für einen Button eingetragen werden.
Diese Datei muss im image-Ordner ($BASEDIR/opus4/public/layouts/<LAYOUTNAME>/img/) des
verwendeten Layouts 94 abgelegt werden.
Bsp:

{% highlight ini %}
printOnDemand.url = http://www.epubli.de/oai/<OAI.REPOSITORY.IDENTIFIER>/
printOnDemand.button = mybutton.png
{% endhighlight %}

Wird dieser Parameter nicht angegeben, erscheint statt des Buttons ein Link mit dem Text "gedruckt
bestellen" bzw. "order print".

## Job Ausführung

Es ist möglich, in OPUS4 bestimmte lang laufende Jobs (z.B. die Indexierung großer Dokumente)
asynchron zu verarbeiten. Auf diese Weise können Timeouts (weiße Seite) vermieden werden. Die
asynchrone Verarbeitung nutzt den Mechanismus des Unix cron-Daemon, der die zeitbasierte
Ausführung von Prozessen und wiederkehrende Aufgaben in sogenannten Cron-Jobs automatisiert.
Die Aktivierung der asynchronen Jobverarbeitung wird im folgenden beschrieben.

<p class="warning">
Beim Aktivieren der asynchronen Jobverarbeitung ist zu beachten, dass die Änderungen im
System immer mit einer zeitlichen Verzögerung eintreten. So werden beispielsweise Änderungen
an Dokumenten erst über die Suche auffindbar, wenn die Solr-Indexierung erfolgt ist. In der
Zwischenzeit befindet sich der Solr-Index in einem inkonsistenten Zustand.
</p>

<p class="warning">
Achtung: Die Aktivierung erfolgt global für alle asynchronen Jobs (derzeit Solr-Indexierung, Mail-
Versand und Löschen temporärer Dokumente).
</p>

### Erstellen von Cron-Jobs auf dem Server

Im Verzeichnis `$BASEDIR/scripts/cron` existiert jeweils ein PHP-Skript für jeden Job. Diese
Skripte werden dem Shell-Skript `cron-php-runner.sh` als Argument übergeben. Als weiteres
Argument muss das Verzeichnis für die lock-Datei angegeben werden, mit der die mehrfache,
parallele Ausführung desselben Skripts verhindert wird. Als optionales Argument kann ein Log-
Verzeichnis angegeben werden. Wird es nicht angegeben, dann erfolgt die Ausgabe des Skripts
direkt auf der Kommandozeile. Für die Ausführung als Cron-Job wird die Angabe des Log-
Verzeichnisses empfohlen. Eine Information über fehlgeschlagene Jobs kann auch in der
Administration unter "System Informationen" eingesehen werden.

<p class="warning">
Wird für einen der implementierten Verarbeitungsmechanismen kein Cron-Job angelegt, führt
das zu einem fehlerhaften Verhalten des Systems, weil die entsprechenden Jobs dann nicht
verarbeitet werden.
</p>

Zur Zeit ist die asynchrone Verarbeitung der Solr-Indexierung, des Mail-Versands und für das
Löschen temporärer Dokumente implementiert. Sie können folgendermaßen aufgerufen werden:

#### Solr-Indexierung

{% highlight shell %}
$ cd $BASEDIR/scripts/cron
$ cron-php-runner.sh cron-solr-update.php /somepath/lock/ /somepath/log/
{% endhighlight %}

Ein Cron-Job (hier als Beispiel für die Ausführung alle 5 Minuten) wird wie folgt angelegt:

{% highlight shell %}
$ crontab –e 5 * * * *
    $BASEDIR/scripts/cron/cron-php-runner.sh
    $BASEDIR/scripts/cron/cron-solr-update.php
    $BASEDIR/workspace/lock
    $BASEDIR/workspace/log > /dev/null 2> /dev/null
{% endhighlight %}

#### Mailversand

{% highlight shell %}
$ cd $BASEDIR/scripts/cron
$ cron-php-runner.sh cron-send-notification.php /somepath/var/lock/ /somepath/var/log/
{% endhighlight %}

Ein Cron-Job (hier als Beispiel für die Ausführung alle 5 Minuten) wird wie folgt angelegt:

{% highlight shell %}
$ crontab –e 5 * * * *
    $BASEDIR/scripts/cron/cron-php-runner.sh
    $BASEDIR/scripts/cron/cron-send-notification.php
    $BASEDIR/workspace/lock
    $BASEDIR/workspace/log > /dev/null 2> /dev/null
{% endhighlight %}

#### Löschen temporärer Dokumente

{% highlight shell %}
$ cd $BASEDIR/scripts/cron
$ cron-php-runner.sh cron-db-clean-temporary.php /somepath/var/lock/ /somepath/var/log/

$ crontab –e 0 0 * * *
    $BASEDIR/scripts/cron/cron-php-runner.sh
    $BASEDIR/scripts/cron/cron-send-notification.php
    $BASEDIR/workspace/lock
    $BASEDIR/workspace/log > /dev/null 2> /dev/null
{% endhighlight %}

Beim Erstellen von Dokumenten werden in der Datenbank temporäre Dokumente angelegt und
normalerweise wieder gelöscht, sobald das Dokument endgültig angelegt oder der Vorgang explizit
abgebrochen wurde. Geschieht das nicht (bspw. durch Schließen des Browsers), dann verbleiben die
temporären Dokumente in der Datenbank.

<p class="warning">
Bei der Definition des cronjobs ist zu beachten, dass das Skript nach temporären Dokumenten
sucht, die mindestens einen Tag alt sind. Das heißt, dass der cronjob sinnvoller Weise höchstens
einmal täglich ausgeführt werden sollte.
</p>

### Aktivieren der asynchronen Jobverarbeitung

Jobs werden im System nur generiert, wenn in der `config.ini` der Wert für `runjobs.asynchronous`
auf 1 gesetzt wird (Standard ist 0):

{% highlight ini %}
; JOB EXECUTION SETTINGS
; To enable asynchronous job execution, set this to 1
; You will need to set up appropriate cron jobs for
; scripts/cron/cron-php-runner.sh
runjobs.asynchronous = 0
{% endhighlight %}

<p class="info">
Bei Bedarf: Einrichten des Monitoring (z.B. Nagios)
Die URL $BASEDIR/admin/info/worker-monitor gibt den Wert 1 zurück, wenn es Jobs gibt, die
nicht verarbeitet werden konnten. Ansonsten wird der Wert 0 zurückgeliefert. Es ist so möglich, die
erfolgreiche Jobverarbeitung mit Monitoring-Systemen zu überwachen. Dafür muss im Admin-
Bereich unter Zugriffskontrolle der IP-Bereich 164 für das Monitoring freigeschaltet werden,
ansonsten ist die URL von außen nicht erreichbar.
</p>

## Publikationslisten

Opus4 bietet die Möglichkeit, Publikationslisten zu generieren (siehe Publikationslisten 18). Dafür
wird ein Standard-Layout ausgeliefert.

Um ein eigenes Layout zu aktivieren und die Sortierreihenfolge der Ergebnisliste nach einem anderen
Kriterium zu sortieren sind in der config.ini für die entsprechenden Parameter das
Kommentarzeichen zu entfernen und die Parameter mit den gewünschten Werten zu befüllen:

; PUBLICATION LIST SETTINGS
; Per default publication lists are rendered by the default stylehseet.
; Here you can define your own stylesheet for rendering publication lists:
publist.stylesheet =

; Per default publications are grouped by 'published year'.
; Here you can switch grouping to 'completed year':
publist.groupby.completedyear = 1

Der Parameter `publist.stylesheet` gibt den Namen des zuvor erstellten eigenen Layout für die
Publikationslisten an.

Der Parameter `publist.groupby.completedyear` ermöglicht die standardmäßig nach 'published
year' sortierte Ergebnisliste umzustellen nach 'completed year' .

Das folgende Beispiel aktiviert anstelle des Standardlayouts für Publikationslisten das eigene
erstellte Layout 'mylayout' und ändert die Sortierung der Ergebnisliste nach dem Kriterium
'completed year':

{% highlight ini %}
publist.stylesheet = mylayout
publist.groupby.completedyear = 1
{% endhighlight %}

## Accounts

Um in OPUS angemeldeten Nutzern die Möglichkeit zum Editieren des eigenen Accounts zu geben
gibt es in der `$BASEDIR/application/configs/application.ini` folgende Parameter, die in
der `config.ini` überschrieben werden können:

{% highlight ini %}
;ACCOUNT MODULE SETTINGS
account.changeLogin = 1; Turn on to allow users to change their own account login
account.editOwnAccount = 1 ; Turn on to allow users to edit their own account information
account.editPasswordOnly = 0 ; Turn on to restrict editing to just the password
{% endhighlight %}

1. `account.editOwnAccount` legt fest, ob Nutzer ihren eigenen Account ändern dürfen.
2. `account.changeLogin legt` fest, ob Nutzer ihren eigenen Account-Namen ändern dürfen.
3. `account.editPasswordOnly` legt fest, ob Nutzer lediglich ihr eigenes Password, nicht aber ihren
   Namen und ihre Email-Adresse ändern dürfen.

<p class="note">
Damit Nutzer ihren eigenen Account editieren können benötigen sie Zugriff auf das account
Modul. Standardmäßig hat kein Nutzer Zugriff auf das Modul, da die Rolle guest im Standard nicht
darauf zugreifen darf. Um die Möglichkeit für alle Nutzer freizugeben kann guest der Zugriff
eingeräumt werden. Andernfalls kann Nutzern über ihre eigene Rolle der Zugriff auf das account
Modul eingeräumt werden (s. a. Kapitel 9.8 Zugriffskontrolle).
</p>

## Sicherheit

Neu geladenen Dateien wird im Standard die Rolle " guest " als Zugriffsrecht zugewiesen. Dies kann
nun über den Parameter securityPolicy.files.defaultAccessRole konfiguriert werden. Dazu ist
der Konfigurationsschlüssel aus der config.ini.template in die config.ini zu übernehmen, die
Kommentarzeichen vor dem Schlüssel zu entfernen und die gewünschten Anpassungen an der
Rollendefinition vorzunehmen. Hinweise zur Zugriffskontrolle und zu Nutzerrollen finden sich in den
Kapiteln 9.8 Zugriffskontrolle 158 und 9.8.2 Nutzerrollen 160.

{% highlight ini %}
; SECURITY SETTINGS
; Change default role for newly uploaded files (default is "guest").
securityPolicy.files.defaultAccessRole = 'guest'
{% endhighlight %}

## BibTeX Export

Mit dem Konfigurationsschlüssel citationExport.bibtex.enrichment kann ein vorhandenes
Enrichment angegeben werden, das beim Bibtex-Export als "note" ausgegeben wird. Dazu wird der
Schlüssel in die `config.ini` wie folgt eingetragen:

{% highlight ini %}
citationExport.bibtex.enrichment=<Name des Enrichments>
{% endhighlight %}

Beispiel:
Das Enrichment mit dem Namen SubmissionStatus ist im OPUS angelegt und für ein Dokument
mit dem Wert "accepted for publication" gefüllt. Die Angabe in der `config.ini` muss dann lauten:

{% highlight ini %}
;BIBTEX EXPORT SETTINGS
citationExport.bibtex.enrichment=SubmissionStatus
{% endhighlight %}

Die Bibtex-Ausgabe enthält dann u.a. die Angabe:

{% highlight bibtex %}
note = {accepted for publication}
{% endhighlight %}



