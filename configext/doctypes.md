---
title: Dokumenttypen
---

# Dokumenttypen

OPUS4 liefert standardmäßig 21 vordefinierte [Dokumenttypen](../documenttypes/index.html)
(plus einen Beispiel-Dokumenttyp "Alle Felder") aus. Jeder Dokumenttyp besteht aus einer XML-
Dokumenttypdefinition und einem Template. Wir empfehlen Ihnen zur Erstellung und Validierung der
Dokumenttypen einen XML-Editor.

Folgende Änderungen sind möglich:

* [Reihenfolge der angezeigten Felder ändern](#reihenfolge-der-angezeigten-felder-ndern)
* [Felder zu einem Dokumenttyp hinzufügen/entfernen](#felder-zu-einem-dokumenttyp-hinzufgenentfernen)
* [Dokumenttypen umbenennen](#dokumenttypen-umbenennen)
* [Neuen Dokumenttyp anlegen](#neuen-dokumenttyp-anlegen)
{: class="navlist" }

In den folgenden beiden Grundlagenkapiteln
[Grundlage: XML-Dokumenttypdefinitionen](#grundlage-xml-dokumenttypdefinition)
und
["Grundlage: Templates](#grundlage-templates)
werden zunächst der generelle Aufbau und die Bedeutung der
Einträge in den XML-Dokumenttypdefinitionen und in den Templates näher erläutert.

## Grundlage: XML-Dokumenttypdefinition

Die XML-Dokumenttypdefinitionen liegen im Ordner

    $BASEDIR/application/configs/doctypes/

In ihnen wird festgelegt, welche Felder ein Dokumenttyp beinhalten soll. Darüber hinaus kann darauf
Einfluss genommen werden, ob ein Feld obligatorisch (required) oder optional ist.

Das Wurzelement in einem Dokumenttyp heißt `documenttype`. Innerhalb dieses Wurzelelements
werden die für diesen Dokumenttyp notwendigen Felder mit dem Element `field` definiert.

### Das Element field

Das Element `field` besitzt die Attribute `name`, `formelement`, `required`, `datatype` und
`multiplicity`. Jedes field im Dokumenttyp muss immer alle fünf Attribute besitzen und diese
müssen deklariert werden, z.B.:

{% highlight xml %}
<field name="PersonAuthor" formelement="text" datatype="Person" required="no" multiplicity="4"/>
{% endhighlight %}

### Das Attribut name

Das Attribut `name` legt die Bezeichnung des Feldes fest. Die Namen der Felder sind in der
CamelCase Schreibweise formuliert. Zur Wahl stehen 70 verschiedene [Standardfelder](../reference/fields.html).
Es können neue, benutzerdefinierte Felder angelegt werden.

* [Einfache Textfelder neu anlegen](fields.html#einfache-textfelder-neu-anlegen)
* [Select-Felder neu anlegen](fields.html#select-felder-neu-anlegen)
* [Benutzerdefinierte Felder (EnrichmentKeys)](../admin/userinterface.html#benutzerdefinierte-felder-enrichmentkeys)
{: class="navlist" }

### Das Attribut required

In diesem Attribut wird festgelegt, ob das Feld ein Pflichtfeld ist. In diesem Fall wird es in der
Anzeige mit einem Stern markiert und muss zwingend ausgefüllt werden. Als mögliche Werte
können `yes` und `no` eingetragen werden.

### Das Attribut formelement

Das Attribut `formelement` gibt an, welches HTML-Formelement zur Darstellung benutzt werden soll.
Folgende Werte sind möglich:

| Werte für formelement | Bedeutung                         |
|:----------------------+:----------------------------------|
| text, Text            | einzeiliges Eingabefeld           |
| textarea, Textarea    | mehrzeiliges größeres Eingabefeld |
| select, Select        | Auswahlfeld                       |
| checkbox, Checkbox    | Ankreuzfeld                       |


### Das Attribut datatype

Das Attribut `datatyp` definiert, welchen Eingaben ein Feld erwartet. Folgende Werte sind möglich:

| Wert für datatype | Bedeutung |
|-------------------+-----------|
| Collection | Browsing-Feld für Sammlungen (Collections) |
| CollectionLeaf | Browsing-Feld 71 für Sammlungen (Collections), bei dem man bis zur untersten verfügbaren Ebene absteigen muss |
| Date | verlangt als Eingabe ein valides Datum |
| Email | prüft, ob die Eingabe dem Schema einer E-Mail-Adresse entspricht |
| Enrichment | muss für benutzerdefinierte Felder verwendet werden |
| Identifier | anderer Bezeichner (DOI, URN, ISSN...) |
| Integer | verlangt als Eingabe nur Zahlen |
| Language | verlangt als Eingabe einen Sprachschlüssel |
| Licence | Auswahl der verfügbaren Lizenzen |
| List | eigene Liste für interne Dokumentfelder (z.B. für PublicationState) |
| Note | Kommentarfeld |
| Person | erzeugt ein Personenfeld mit den Eingabefeldern Vorname und Nachname (Submitter, Author, Referee, Advisor, Translator, Contributor) |
| Series | Browsing-Feld für Schriftenreihen |
| Subject | Schlagwörter (SWD, freie) |
| Text | beliebiger Textinhalt |
| Title | erzeugt ein Titelfeld mit Sprachauswahl (Main, Sub, Additional, Parent, Abstract) |
| ThesisGrantor | Auswahl für Titel verleihende Institution |
| ThesisPublisher | Auswahl für verbreitende Stelle |
| Year | verlangt als Eingabe ein valides Jahr |

### Das Attribut multiplicity

Dieses Attribut gibt an, wie oft ein Feld innerhalb eines Dokumenttyps mit einem Wert belegt werden
darf. Wird als multiplicity
oder * (Sternchen) eingetragen, dann wird im Formuar zu dem Feld
ein Hinzufügen-Button (und dann ein Löschen-Button) angezeigt, mit dem der Nutzer weitere Felder
des gleichen Typs anfordern kann (z. B. um mehrere Autoren einzutragen).

Bestimmte Felder dürfen jedoch pro Dokument nur einmal abgespeichert werden, weshalb bei
diesen Feldern eine multiplicity von 1 zwingend notwendig ist:

* CompletedDate
* CompletedYear
* ContributingCorporation
* CreatingCorporation
* ThesisDateAccepted
* ThesisYearAccepted
* Edition
* Issue
* Language (der Veröffentlichung)
* PageFirst
* PageLast
* PageNumber
* PublishedDate
* PublishedYear
* PublisherName
* PublisherPlace
* Volume

### Das Unterelement required-if-fulltext

Das Element `required-if-fulltext` ist ein optionales Unterelement des Elements `field`. Es kann
benutzt werden um festzulegen, dass ein Feld zum Pflichtfeld wird, sobald im ersten Schritt des
Veröffentlichungsprozesses ein Volltext hochgeladen wurde. Wenn es verwendet wird, dann muss es
als erstes Unterelement angegeben werden.

Beispiel:

{% highlight xml %}
<field name="PersonAuthor" formelement="text" datatype="Person" required="no" multiplicity="4">
    <required-if-fulltext/>
</field>
{% endhighlight %}

### Das Unterelement subfield

Mit `subfield` besteht die Möglichkeit, Unterfelder für `field` zu definieren. Es besitzt analog zu
`field` die Attribute `name`, `required`, `datatype` und `formelement`. Auf `multiplicity` kann hier
verzichtet werden, da ein jedes `subfield` pro Feld nur einmal vorkommen darf.

| Attribute von subfield | Bedeutung |
|------------------------+-----------|
| name | Name des Unterfeldes; zur Auswahl stehen Email, BirthPlace, BirthDate und AcademicTitle |
| formelement | HTML-Formelement; siehe Beschreibung dieses Attributs für das Element field |
| datatype | Typ des Feldinhalts |
| required | legt fest, ob das subfield ein Pflichtfeld ist |

Beispiel:

{% highlight xml %}
<field name="PersonAuthor" formelement="text" datatype="Person" required="no" multiplicity="4">
    <required-if-fulltext/>
    <subfield name="AcademicTitle" formelement="text" datatype="Text" required="no"/>
</field>
{% endhighlight %}

### Das Unterelement value

Es ist möglich, Default-Werte für Felder und Unterfelder festzulegen. Hierzu wird das Element field
bzw. das Element `subfield` um einen Eintrag mit dem Attribut `value` erweitert, in das dann ein
Wert eingetragen wird, der dem Nutzer bereits beim Aufruf des Formulars im entsprechenden Feld
angezeigt wird. Das Element `value` hat drei mögliche Attribute.

| Attribut | Bedeutung |
|--------------------+-----------|
|  value | Wert, der voreingestellt werden soll. Bei Select-Feldern ist das die ID des gewünschten Wertes (sichtbar in der Administration). |
| edit | legt fest, ob der Nutzer diesen Wert verändern kann
| public | legt fest, ob der Wert im Formular angezeigt wird; wird hier "no" gewählt, kann value z.B. dafür genutzt werden, interne Informationen zu einem Dokument zu erfassen, die keine Interaktion mit dem Nutzer erfordern |

Beispiel 1: Vorbelegung des akademischen Titels:

{% highlight xml %}
<field name="PersonAuthor" formelement="text" datatype="Person" required="no" multiplicity="4">
    <required-if-fulltext/>
    <subfield name="AcademicTitle" formelement="text" datatype="Text" required="no"/>
    <default value="Dr." edit="yes" public="yes" />
</field>
{% endhighlight %}

Beispiel 2: Vorbelegung der E-Mail-Adresse:

{% highlight xml %}
<subfield name="Email" required="yes" formelement="text" datatype="Email" >
    <default value="test@mail.com" edit="yes" public="yes"/>
</subfield>
{% endhighlight %}

Beispiel 3: Vorbelegung von Select-Feldern

{% highlight xml %}
<field name="ThesisGrantor" required="yes" formelement="Select" datatype="ThesisGrantor" multiplicity="1">
    <default value="1" edit="no" public="yes" />
</field>

<field name="ThesisPublisher" required="yes" formelement="Select" datatype="ThesisPublisher" multiplicity="1">
    <default value="2" edit="no" public="yes" />
</field>

<field name="Licence" required="yes" formelement="Select" datatype="Licence" multiplicity="1">
    <default value="3" edit="no" public="yes" />
</field>
{% endhighlight %}

### Das Unterelement option

Das Unterelement `option` kann benutzt werden, um bei benutzerdefinierten Select-Feldern
(`datatype="Select"` bzw. `datatype="select"`) Werte für die Auswahl festzulegen.

### Spezialfall "implizite" Felder

Es gibt zwei Fälle, in denen der Benutzer "implizite" Felder erzeugt: bei Personen und Titeln. Das
heißt, dass implizit mehr Felder erzeugt werden, als Zeilen im Dokumenttyp vorhanden sind.

Beispiel 1: Personen

Für Felder des Typs "Person" (Advisor, Author, Contributor, Editor, Referee, Submitter, Translator)
werden die Felder FirstName und LastName automatisch mit erstellt. Möchte man nun diesen
Feldern einen Defaultwert geben, müssen diese vor der Belegung mit einem Wert im Attribut value
noch direkt referenziert werden. Dies geschieht mit dem Attribut `for="FirstName"` bzw.
`for="LastName`:

{% highlight xml %}
<field name="PersonSubmitter" required="yes" multiplicity="1" formelement="text" datatype="Person">
    <default for="FirstName" value="Hans" edit="yes" public="yes"/>
    <default for="LastName" value="Hansmann" edit="yes" public="yes"/>
</field>
{% endhighlight %}

Beispiel 2: Titel

Analog dazu wird für Titel-Felder (Abstract, Additional, Main, Parent, Sub) das Feld Language
automatisch mit erstellt. Dieses Feld kann wie folgt mit einem Defaultwert belegt werden, indem dem
Attribut `value` noch das Attribut `for="Language"` vorangestellt wird:

{% highlight xml %}
<field name="TitleMain" required="no" formelement="text" datatype="Title" multiplicity="4">
    <default for="Language" value="deu" edit="no" public="yes"/>
</field>
{% endhighlight %}

### Deklaration impliziter Felder als Pflichtfelder

Wenn z.B. ein Personenfeld als Pflichtfeld deklariert ist und keine impliziten Felder angegeben sind
wird nur der Nachname als Pflichtfeld behandelt. Um nun z.B. auch den Vornamen als Pflichtfeld zu
erhalten ist die Definition entsprechend zu erweitern und das Attribut `required=yes` anzugeben:

Beispiel: Vorname als Pflichtfeld

{% highlight xml %}
<field name="PersonSubmitter" required="yes" formelement="Text" datatype="Person" multiplicity="1">
    <subfield name="FirstName" required="yes" formelement="text" datatype="Text" />
</field>
{% endhighlight %}

## Grundlage: Templates

Die Templates zu den Dokumenttypen liegen im Verzeichnis

    $BASEDIR/application/configs/doctypes_templates

In den Templates wird festgelegt, in welcher Reihenfolge die Felder
eines Dokumenttyps im Veröffentlichungsformular angezeigt werden.

### Erweiterte Einstellungen

Neben der Möglichkeit, die Reihenfolge der Elemente zu bestimmen, kann über die Veränderung der
eingebundenen css-Klassen auch das Aussehen verändert werden. Darüber hinaus besteht die
Möglichkeit, den Elementen Optionswerte mitzugeben. Die Signatur der Methoden lautet:

{% highlight php %}
element($value, $options = null, $type = null, $name = null)
group($value, $options = null, $name = null)
{% endhighlight %}

Wann Felder als `element` bzw. als `group` benutzt werden müssen, kann der Tabelle
[Feldtypen für die Templates](../reference/templatefields.html) entnommen werden. Der Wert `value` wird immer
mit dem Namen übergeben, `options` sind auch optional und repäsentieren einen String, der
mögliche html-Attribute des Elements enthalten kann. `type` bezeichnet den Typ des Elements und
ist optional, sowie auch der `name`.

So können die Optionswerte benutzt werde:

{% highlight php %}
<?= $this->group($this->groupTitleAbstract, "cols='60' rows='9'"); ?>
{% endhighlight %}

In diesem Beispiel entspricht der String `cols='60' rows='9'` dem Wert `$options` . Um Fehler zu
vermeiden, sollte genau diese Schreibweise angewendet werden. Damit wird festgelegt, dass das
Textfeld für einen Abstract `60` Spalten breit und `9` Zeilen hoch ist. Dieses Element benutzt bereits die
css-Klasse `form-textarea`, in der Sie das Aussehen anpassen können.

{% highlight php %}
<?= $this->group($this->groupTitleMain, "size='60'"); ?>
{% endhighlight %}

Mit diesem Optionswert wird die Länge des Titel-Feldes z.B. auf 60 Zeichen eingestellt. Das Element
benutzt standardmäßig die css-Klasse `form-textfield`, die entsprechend angepasst werden kann.
Für den Fall, dass das Element keine Klasse benutzt, gibt es folgende Variante:

{% highlight php %}
<?= $this->element('button_label_abort', "class='form-button submit-button'", "Submit", "send"); ?>
{% endhighlight %}

Hierbei steht der Optionswert für den Button an zweiter Stelle. Damit wird für den Button jetzt die
css-Klasse `form-button submit-button` benutzt.

<p class="note" markdown="1">
Generell gilt, dass viele unterschiedliche Attribute von html-Elementen verwendet werden
können. Dabei bestimmen Sie im Dokumenttyp mit `formelement`, um welches html-Element es
sich handelt und welche Attribute überhaupt möglich sind. (für `text` sind bspw. andere Werte
möglich als für `textarea`).
</p>

### Anzeige der hochgeladenen Dateien

Um während des Veröffentlichungsvorgangs auch im zweiten Formularschritt (Erfassung der
Metadaten) dem Nutzer anzuzeigen, welche Dateien hochgeladen wurden, kann mit dem Befehl

{% highlight php %}
<?= $this->fileOverview(); ?>
{% endhighlight %}

ein entsprechendes Fieldset eingebunden werden (als Bsp. kann hier das Template des
Testdokumenttyps "all" unter `$BASEDIR/application/configs/doctypes_templates/all.phtml`
dienen).

### Anzeige der Checkbox für rechtliche Hinweise für einzelne Dokumenttypen

Neben der Checkbox für rechtliche Hinweise, die auf der ersten Seite angezeigt wird (siehe
[Publish-Formular](../config/publish.html)), kann die Anzeige dieser Checkbox als Pflichtfeld auch für einzelne
Dokumenttypen erfolgen. Dafür muss im entsprechenden Template folgender Aufruf eingefügt werden
als Bsp. kann hier das Template des Testdokumenttyps "all" unter
`$BASEDIR/application/configs/doctypes_templates/all.phtml` dienen):

{% highlight php %}
<?= $this->legalNotices($this->form); ?>
{% endhighlight %}

Schließlich sollten noch die erläuterten Sprachdateien (Überschrift und Name des
Feldes, Hilfetext) angepasst werden (siehe auch [Leitlinien](../configext/policies.html)).

* [Felder umbenennen](fields.html#felder-umbenennen)
{: class="navlist" }

## Reihenfolge der angezeigten Felder ändern

Die Reihenfolge der Felder im Veröffentlichungsformular kann verändert werden, indem im
entsprechenden Template im Verzeichnis
`$BASEDIR/application/configs/doctypes_templates` die Zeile, in der ein Feld definiert wird,
nach oben oder unten verschoben wird:

Ursprüngliche Reihenfolge:

{% highlight php %}
<?= $this->group($this->groupPersonReferee); ?>
<?= $this->group($this->groupPersonEditor); ?>
<?= $this->group($this->groupPersonAdvisor); ?>
{% endhighlight %}

Feld für Advisor an die erste Stelle verschoben:

{% highlight php %}
<?= $this->group($this->groupPersonAdvisor); ?>
<?= $this->group($this->groupPersonReferee); ?>
<?= $this->group($this->groupPersonEditor); ?>
{% endhighlight %}

## Felder zu einem Dokumenttyp hinzufügen/entfernen

Alle 21 Dokumenttypen, die standardmäßig mit OPUS4 ausgeliefert werden, bestehen aus einem
bestimmten Set an Feldern. Diese Vorauswahl kann individuell angepasst werden, indem Felder aus
den entsprechenden XML-Dokumenttypdefinitionen und den dazugehörigen Templates entfernt oder
hinzugefügt werden. Zur Veranschaulichung wird im Folgenden beispielhaft dem Dokumenttyp
[(wissenschaftlicher) Artikel](../documenttypes/article.html) ([Article) das Feld
`IdentifierUrl` hinzugefügt, um z.B. das Eintragen
einer externen URL zu einem Dokument zu ermöglichen.

### 1. Schritt: XML-Dokumenttypdefinition anpassen

Die Datei `$BASEDIR/application/configs/doctypes/article.xml` mit einem Editor (z.B.
Notepad++) öffnen und die Zeile

{% highlight xml %}
<field name="IdentifierUrl" required="no" formelement="Text" datatype="Identifier" multiplicity="1"/>
{% endhighlight %}

eintragen:

{% highlight xml %}
...
<field name="IdentifierUrl" required="no" formelement="Text" datatype="Identifier" multiplicity="1"/>
...
{% endhighlight %}


Die Reihenfolge der Felder im XML-Dokumenttyp hat keine Auswirkung auf die spätere Darstellung.
Die wird separat über das dazugehörige Template gesteuert.

* [Reihenfolge der angezeigten Felder eines Dokumenttyps ändern](doctypes.html#reihenfolge-der-angezeigten-felder-eines-dokumenttyps-ndern)
{: class="navlist" }

<p class="warning" markdown="1">
Bitte bei der Definition der Attribute `required`, `formelement`, `datatype` und `multiplicity` die
Hinweise in [Grundlage: XML-Dokumenttypdefinition](#grundlage-xml-dokumenttypdefinition) beachten.
</p>

### 2. Schritt: Template anpassen

Die Datei `$BASEDIR/application/configs/doctypes_templates/article.phtml` mit einem
Editor (z.B. Notepad++) öffnen und die Zeile

{% highlight xml %}
<?= $this->element($this->IdentifierUrl); ?>
{% endhighlight %}

eintragen:

<p class="note">
Die neue Zeile kann an einer beliebigen Stelle im Template (nicht zwingend am Ende) eingefügt
werden. Die Reihenfolge der Felder wird über das dazugehörige Template gesteuert.
</p>

* [Reihenfolge der angezeigten Felder eines Dokumenttyps ändern](doctypes.html#reihenfolge-der-angezeigten-felder-eines-dokumenttyps-ndern)
{: class="navlist" }

Auf die gleiche Weise können Felder aus einem Dokumenttyp entfernt werden.

<p class="warning" markdown="1">
Wenn in den Dokumenttypen das Feld `language` entfernt wird, tritt ein Fehler auf, da ein
Dokument ohne Sprache als "unbekannter Titel" angezeigt wird und somit nicht suchbar ist.
</p>

<p class="warning" markdown="1">
Einige Felder sollten im Hinblick auf die Ablieferung von Netzpublikationen an die DNB (über
XMetadissPlus) in allen Dokumenttypen erhalten bleiben. Welche Felder dies sind, kann den
Beschreibungen der [Dokumenttypen](../documenttypen/index.html) entnommen werden.
</p>

## Dokumenttypen umbenennen

Um Dokumenttypen umzubenennen, muss der entsprechende Schlüssel aus der Datei
`$BASEDIR/modules/default/language/doctypes.tmx` in die Datei
`$BASEDIR/modules/default/language_custom/my_doctypes.tmx` kopiert und angepasst
werden:

{% highlight xml %}
<tu tuid="movingimage">
  <tuv xml:lang="en">
    <seg>Video</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Video</seg>
  </tuv>
</tu>
{% endhighlight %}

<p class="note" markdown="1">
Die Bearbeitung von Übersetzungsressourcen sowie statischer Seiten ist seit Version 4.4 über
die Opus4-Oberfläche möglich. Näheres dazu ist in [Übersetzungsressourcen](translations.html) beschrieben.
</p>

## Neuen Dokumenttyp anlegen

Um einen neuen Dokumenttyp zu erstellen, ist es am Einfachsten, einen vorhandenen Dokumenttyp,
der bereits viele der gewünschten Felder enthält, zu kopieren. Hierzu legen Sie bitte eine Kopie der
gewünschten XML-Dokumenttypdefinition im Verzeichnis
`$BASEDIR/application/configs/doctypes/` und eine Kopie des entsprechenden Templates
im Verzeichnis `$BASEDIR/application/configs/doctypes_templates/` an und benennen diese
identisch, z. B. `mydocumenttype.xml` und `mydocumenttype.phtml`.

Die Benennung eines Dokumenttyps muss in folgendem Format erfolgen:

    [a-z]+[a-z0-9]*(_[a-z0-9]+)*

Diese Restriktion bedeutet, dass die Benennung des Dokumenttyps mit einem kleinen Buchstaben
(a-z) anfangen muss; danach kann ein beliebiger Mix aus Kleinbuchstaben (a-z), Ziffern (0-9) und
als einzigem erlaubten Sonderzeichen der Unterstrich folgen (mit der Einschränkung, dass der
Unterstrich nicht zweimal direkt hintereinander auftreten kann und nicht ganz am Ende stehen
darf).

Danach ergänzen bzw. entfernen Sie die Felder.

* [Felder zu einem Dokumenttyp hinzufügen/entfernen](#felder-zu-einem-dokumenttyp-hinzufgenentfernen)
{: class="navlist" }

Nach dem Erstellen eines neuen Dokumenttyps muss in der Datei
`modules/default/language_custom/my_doctypes.tmx` ein entsprechender Eintrag ergänzt
werden:

{% highlight xml %}
<tu tuid="mydocumenttype">
  <tuv xml:lang="en">
    <seg>New Documenttype</seg>
  </tuv>
  <tuv xml:lang="de">
    <seg>Neuer Dokumenttyp</seg>
  </tuv>
</tu>
{% endhighlight %}

### BibTeX Export von neuen Dokumenttypen

Neu angelegte Dokumenttypen werden beim Export in Literaturverwaltungssysteme (RIS- bzw.
BibTeX-Export) standardmäßig dem Typ "Generic" (RIS) bzw. "MISC" (BibTeX) zugeordnet. Um
dies zu ändern, muss der neue Dokumenttyp wie folgt in der Datei
`$BASEDIR/modules/citationExport/views/scripts/index/ris.xslt` (für den RIS-Export) eingetragen werden:

Folgende Zeile muss ergänzt werden:

{% highlight xml %}
<xsl:when test="@Type=' neuer Dok umenttyp '">
<xsl:text>TY - gewünschter RIS-Dok umenttyp </xsl:text>
{% endhighlight %}

Für den BibTeX-Export ist es notwendig, analog zu den im Verzeichnis
`$BASEDIR/modules/citationEx port/views/scripts/index/`
bereits vorhandenen Stylesheets

* bibtex_article.xslt
* bibtex_book.xslt
* bibtex_bookpart.xslt
* bibtex_conferenceobject.xslt
* bibtex_doctoralthesis.xslt
* bibtex_masterthesis.xslt
* bibtex_preprint.xslt
* bibtex_report.xslt

ein weiteres Stylesheet für den neuen Dokumenttyp zu erstellen.

### Ablieferung neuer Dokumenttypen an die DNB

Für die Ablieferung der Dokumente an die Deutsche Nationalbibliothek über die OAI-
Schnittstelle ist es bei neu angelegten Dokumenttypen sinnvoll, sie auf die Publikationstypen des
Gemeinsamen Vokabulars für Publikations- und Dokumenttypen zu mappen, da sie sonst dem
Dokumenttyp [Sonstiges (other)](../documenttypes/other.html) zugeordnet werden. Hierfür muss in der Datei
`$BASEDIR/modules/oai/views/scripts/index/prefixes/XMetaDissPlus.xslt` folgende Zeile ergänzt werden:

{% highlight xml %}
<xsl:when test="@Type='neuer Dokumenttyp'">
  <xsl:text> hier einen passenden Dok umenttyp aus dem Gemeinsamen Vok abular für
             Publik ations- und Dok umenttypen eintragen </xsl:text>
</xsl:when>
{% endhighlight %}

### Prüfung der neu angelegten XML-Dokumenttypdefinition(en)

Nach dem Anlegen kann der neue Dokumenttyp auf Konformität bezüglich des XML-Schemas
`documenttype.xsd` geprüft werden. Dazu bietet sich folgender Befehl an (hier am Beispiel der
Dokumenttypdefinition `beispiel.xml`):

    cd $BASEDIR/application/configs/doctypes
    xmllint --noout --schema
        ../../library/Opus/Document/documenttype.xsd
        beispiel.xml

War die Validierung erfolgreich, so erscheint:

    beispiel.xml validates

Sofern das Programm `xmllint` nicht auf dem System verfügbar ist, kann auch versucht werden, ein
Testdokument über das Publish-Formular einzustellen. Dazu ist im ersten Schritt der neu angelegte
Dokumenttyp auszuwählen. Wird das Formular beim Versuch des Übergangs zur zweiten
Formularseite korrekt aufgebaut, dann war die Valididerung erfolgreich. Ansonsten erscheint die
folgende Fehlermeldung:

    given xml document type definition for document type beispiel is not
    valid
