---
title: Sammlungen
weight: 30
---

# Sammlungen

In OPUS4 können Sammlungen (Collections) angelegt werden, um Dokumente über das Browsing
beispielsweise thematisch, geografisch oder institutionell strukturiert anzubieten. Jede Sammlung
kann beliebig viele Sammlungseinträge (Collection Entries) besitzen. Standardmäßig werden die
folgenden Sammlungen mit OPUS4 ausgeliefert:

* Institute (institutes)
* DDC-Klassifikation (ddc)
* CCS-Klassifikation (ccs)
* PACS-Klassifikation (pacs)
* JEL-Klassifikation (jel)
* MSC-Klassifikation (msc)
* BKL-Klassifikation (bkl)

Eine Sammlung wird nur dann im Browsing angezeigt, wenn sie mindestens einen
Sammlungseintrag oder mindestens ein verknüpftes Dokument enthält.

## Anlegen einer neuen Sammlung

Soll eine neue Sammlung ("Testsammlung") angelegt werden, müssen folgende Einstellungen nach
dem Klick auf "Hinzufügen" ausgefüllt werden (Pflichtfelder sind orange markiert):

| Parameter | Erläuterung |
|-----------+-------------|
| **Name*** | der Name der Sammlung, z.B. "Neue Sammlung"
| Angezeigter Name | Übersetzungen der neuen Sammlung |
| **Bezeichnung des OAI-Sets*** | Muss ausgefüllt werden, wenn die Sammlung über OAI-PMH 146 ausgeliefert werden soll. Die Bezeichnung des OAI-Sets kann beliebig sein, aber: erlaubte Zeichen: A-Za-z0-9-_.!~*'() |
| Sortierreihenfolge | legt fest, welche Position die neue Sammlung in der Anzeige bekommt, standardmäßig wird die neue Sammlung ganz unten angelegt |
| sichtbar | Sammlung ist vollständig sichtbar / unsichtbar (Vgl. weiter unten in diesem Kapitel "Sichtbarkeit") Wird hier das Häkchen entfernt, (z.B. um eine Änderung an der Sammlung vorzunehmen), so gilt dies global (für Browsing, Frontdoor und OAI) |
| Sammlung wird auf Browsing-Startseite angezeigt | Sammlung ist im Browsing sichtbar / unsichtbar |
| Sammlungszugehörigkeit auf der Frontdoor anzeigen | Sammlung ist auf der Frontdoor sichtbar / unsichtbar |
| Sammlung als OAI-Set ausgeben | Sammlung kann als OAI-Set ausgegeben / nicht ausgegeben werden |
| **Anzuzeigende Metadaten-Felder im Browsing*** | hier kann für die Darstellung der Sammlungseinträge jeweils zwischen "Name", "Nummer", "Name, Nummer" bzw. "Nummer, Name" gewählt werden |
| **Anzuzeigende Metadaten-Felder auf der Frontdoor*** | hier kann für die Darstellung der Sammlungseinträge jeweils zwischen "Name", "Nummer", "Name, Nummer" bzw. "Nummer, Name" gewählt werden |

Nach dem Speichern wird die neue Sammlung an der gewählten Position (Sortierreihenfolge) im
Administrationsbereich "Sammlungen verwalten" angezeigt:

Falls notwendig, kann sie durch einen Klick auf "Editieren" bearbeitet werden. Auch die Sortierung
kann mit den Pfeilen "Hoch" und "Runter" angepasst werden. Mit dem Befehl "Ausblenden" wird die
Sammlung in der Frontdoor nicht angezeigt, der Name der Sammlung wird rot gekennzeichnet.

## Anlegen eines neuen Sammlungseintrags

Soll innerhalb einer Sammlung ein neuer Sammlungseintrag (z. B. "Test") erstellt werden, müssen
folgende Einstellungen nach dem Klick auf 'Einen neuen Sammlungseintrag hier einfügen' ausgefüllt
werden:

| Parameter | Erläuterung |
|-----------+-------------|
| Name | der Name des Sammlungseintrags, z. B. "Neuer Sammlungseintrag" |
| Nummer | die Nummer des Sammlungseintrags, z. B. "01" |
| sichtbar | Sammlungseintrag wird angezeigt (Browsing, Frontdoor, etc.) |
| OAI-Subset | Bezeichnung des OAI-Subsets (bildet die Grundlage für die Ausgabe von Sammlungseinträgen über OAI-PMH 146 ). Die Bezeichnung kann beliebig sein, aber: erlaubte Zeichen: A-Za-z0-9-_.!~*'() |
| Theme | falls unter `$BASEDIR/public/layouts` mehrere Layouts hinterlegt sind, kann hier eines nur für die Anzeige dieses Sammlungseintrags angegeben werden (optional) |

Nach dem Speichern erscheint der Sammlungseintrag in der vorher festgelegten Sortierreihenfolge:

Wenn nötig, kann man den Sammlungeintrag über "Editieren" bearbeiten, wieder "Entfernen" oder
mit "Ausblenden" in der Frontdoor unsichtbar schalten. Sind mehrere Sammlungseinträge vorhanden,
kann auch die Sortierreihenfolge mit den Pfeilen "Hoch" und "Runter" verändert werden.

Sammlungseinträge können momentan nicht in die verschiedenen Sprachen der Oberfläche übersetzt werden.

## Sammlungen umbenennen

Im Edit-Formular der entsprechenden Sammlung lassen sich die Übersetzungen für eigene und auch Standardsammlungen
editieren. 

Die Schlüssel für Sammlungen entsprechen folgendem Format `default_collection_role_NAME`, also z.B.
`default_collection_role_ddc` oder `default_collection_role_Testsammlung`. Diese Schlüssel können auch in der 
[Übersetzungsverwaltung][TRANSLATIONS] editiert werden.

## Sortierreihenfolge ändern

### Browsing

Die Reihenfolge der Sammlungen im Browsing entspricht der angezeigten Reihenfolge im Bereich
"Sammlungen" in der Administration. Soll also die Reihenfolge der Sammlungen im Browsing
geändert werden, genügt es, diese im Administrationsbereich nach oben oder unten zu verschieben.
Gleiches gilt für Sammlungseinträge.

### Frontdoor

Standardmäßig wird eine neu erstellte Sammlung "Testsammlung" immer an letzter Stelle aller
Sammlungen in der Frontdoor eines Dokuments angezeigt. Soll die Reihenfolge der Sammlungen
geändert werden, muss in der Datei `$BASEDIR/modules/frontdoor/views/scripts/index/index_custom.xslt`
das folgende Statement

    <xsl:apply-templates select="Collection[@RoleName='Testsammlung']" />

im Bereich

    <!-- Collection Roles Section: add the collection roles keys 
         that have to be displayed in frontdoor -->
    ...
    <!-- End Collection Roles -->

aufgenommen werden.

Existiert noch keine Datei `$BASEDIR/modules/frontdoor/views/scripts/index/index_custom.xslt` so
ist diese als erstes zu erstellen, in dem die Datei index.xslt kopiert wird:

    $ cd $BASEDIR/modules/frontdoor/views/scripts/index
    $ cp index.xslt index_custom.xslt

<p class="warning">
Änderungen der Anzeige auf der Frontdoor können in der Datei
`$BASEDIR/modules/frontdoor/views/scripts/index/index_custom.xslt` vorgenommen werden. Bei einem OPUS-
Software-Update wird diese Datei nicht verändert, so dass eventuelle Änderungen an der originalen
`index.xslt` bei Bedarf manuell in die lokal angepasste `index_custom.xslt` Datei übernommen
werden müssen.
</p>

## Anzeige verknüpfter Dokumente

Es gibt die Möglichkeit, sich die mit einer Sammlung oder einem Sammlungseintrag verknüpften
Dokumente anzeigen zu lassen, indem man auf "Verknüpfte Dokumente" (Verknüpfung mit einer
Sammlung) oder "Zeige verknüpfte Dokumente" (Verknüpfung mit einem Sammlungseintrag) klickt.
Dieser Link wird nur angeboten, wenn mit der Sammlung oder dem Sammlungseintrag Dokumente
verknüpft sind, ansonsten ist er ausgegraut dargestellt.

Die Funktion "Verknüpfte Dokumente" oder "Zeige verknüpfte Dokumente" liefert alle
Dokumente zu einer Sammlung oder einem Sammlungseintrag, unabhängig davon, welchen Status
(unpublished, inprogress, restricted, published) sie besitzen.

## Sichtbarkeit

Sammlungen und Sammlungseinträge können auf sichtbar oder unsichtbar geschaltet werden. Da
die Sichtbarkeitseinstellung von Sammlungen nicht an die Sammlungseinträge "vererbt" wird, ist es
prinzipiell möglich, die ID eines Sammlungseintrags, der nicht die Sichtbarkeitseinstellung
'unsichtbar' besitzt, zu erraten. Dieser Sammlungseintrag wird dann in der aktuellen Implementierung
angezeigt, wie auch die angehängten Dokumente und eventuell vorhandene tiefer liegende
Sammlungseinträge (sofern diese nicht die Sichtbarkeitseinstellung unsichtbar besitzen).
Wenn man wirklich sichergehen will beziehungsweise muss, dass keine Sammlungseinträge einer
Sammlung mit Sichtbarkeit "unsichtbar" im Frontend angezeigt werden können, dann muss man
manuell die Sichtbarkeit aller Sammlungseinträge der entsprechenden Sammlung auf 'unsichtbar'
setzen.

<p class="warning">
Die Möglichkeit, Sammlungen auf unsichtbar zu schalten, kann auch für den internen Workflow
benutzt werden.
</p>

## Sammlungen über OAI-PMH ausgeben lassen

Sammlungen (z.B. Klassifikationen) können über OAI-PMH in Form von OAI-Sets ausgegeben
werden. Die Ausgabe erfolgt über eine URL mit der entsprechenden Syntax unter Angabe des OAI-
Sets bzw. des OAISubsets. Hierzu ist es erforderlich, den Parameter Bezeichnung des OAI-Sets
bei der gewünschten Sammlung entsprechend zu befüllen und ein Häkchen bei der Option Sammlung
als OAI-Set ausgeben zu setzen. Darüber hinaus muss die Sammlung als Ganzes sichtbar
sein.

Sollen auch Sammlungseinträge ausgegeben werden, muss bei diesen der Parameter OAISubset
entsprechend befüllt werden und es muss ein Häkchen bei der Option sichtbar gesetzt sein.

Ist dies erfolgt, kann die Sammlung in der OAI-Schnittstelle per " Bezeichnung des OAI-Sets "
abgefragt werden. Für Sammlungseinträge muss zusätzlich das OAISubset angegeben werde, so
dass die Syntax: " Bezeichnung des OAI-Sets ":" OAI-Subset " lautet.

Beispielausgabe "Sammlungseintrag DDC-Klassifikation 72 Architektur"

Es sollen alle Dokumente ausgegeben werden, die der DDC-Klassifikation "72 Architektur"
zugeordnet sind. Der Parameter Bezeichnung des OAI-Sets hat für die Sammlung "DDC-
Klassifikation" den Wert "ddc", die oben beschriebenen Optionen "sichtbar" und "Sammlung als
OAI-Set ausgeben" sind ausgewählt:

Der Parameter OAI-Subset hat für den gewünschten Sammlungseintrag "72 Architektur" den Wert:
"72", die oben beschriebene Option "sichtbar" ist ausgewählt:

Daraus ergibt sich für die Abfrage der Dokumente der folgende Link:

    http://example.org/oai?verb=ListRecords&metadataPrefix=oai_dc&set=ddc:72

Um sich eine Übersicht über die verfügbaren OAI-Sets zu verschaffen, kann man in der
Administration im Bereich "OAI-Link" 169 den Link "OAI Anfrage mit dem Verb ListSets" anklicken.
Eine Beispielausgabe liefert der Link "OAI Anfrage mit dem Verb ListRecords (mit OAI-Set)".

[TRANSLATIONS]: ../translation/translations.html
