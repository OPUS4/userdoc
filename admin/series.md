---
title: Schriftenreihen
weight: 40
---

# Schriftenreihen

In diesem Bereich können Schriftenreihen angelegt und verwaltet werden.
In OPUS4 gilt folgende Spezifikation für Schriftenreihen:

* endliche Hierarchie (Schriftenreihen -> SchriftenreiheXYZ -> Serientitel)
* spezielle Informationen, die mit den einzelnen Serientiteln verknüpft sind (Logo etc.)
* ein Dokument kann beliebig vielen Schriftenreihen zugeordnet werden, in jeder zugeordneten
  Schriftenreihe besitzt es genau eine Bandnummer
* eine Schriftenreihe kann beliebig viele Dokumente (Stücktitel) enthalten
* eine Bandnummer (z.B. "15") kann beliebig oft pro Dokument vorkommen, in jeder einzelnen
  Schriftenreihe aber nur genau einmal

Anlegen einer neuen Schriftenreihe

Um eine neue Schriftenreihe anzulegen, stehen nach einem Klick auf den Button "Neu" folgende
Parameter zur Verfügung (Pflichtfelder sind orange markiert):

| Parameter | Erläuterung |
|-----------+-------------|
| **Titel*** | Der Titel der Schriftenreihe, wird im Browsing und auf der Frontdoor verknüpfter Dokumente angezeigt |
| Info | Eine HTML-fähige Infobox, in die ergänzende Informationen zur Schriftenreihe eingetragen werden können, wie z.B. Links, Herausgeber, ISSN etc. |
| sichtbar | Schriftenreihe ist sichtbar (voreingestellt) / unsichtbar |
| Sortierreihenfolge | Sortierung der Schriftenreihen (für die Anzeige im Browsing) |

Nach dem Speichern wird die neue Schriftenreihe an der gewählten Position (Sortierreihenfolge) im
Administrationsbereich "Schriftenreihen" angezeigt. Sie kann ggf. durch einen Klick auf "Ändern"
editiert oder mit "Löschen" entfernt werden:

## Sortierreihenfolge ändern

Die Sortierung der Schriftenreihen entsteht automatisch durch die Reihenfolge, in der sie angelegt
werden. Um die Sortierung zu ändern, muss der jeweilige Eintrag im Parameter "Sortierreihenfolge"
manuell für alle betreffenden Schriftenreihen verändert werden. Hier sollte darauf geachtet werden,
dass der Wert nicht doppelt vergeben wird (ansonsten wird die Schriftenreihe, die einen bereits
vergebenen Wert erhält, z. B. "5" direkt unter die Schriftenreihe sortiert, die bereits den Wert "5"
hat).

Die Sortierung beginnt mit 0 (0,1,2,3,...).

## Anzeige verknüpfter Dokumente

Es gibt die Möglichkeit, sich die mit einer Schriftenreihe verknüpften Dokumente anzeigen zu lassen,
indem man auf "Dokumente anzeigen" klickt. Dieser Link wird nur angeboten, wenn mit der
Schriftenreihe bereits Dokumente verknüpft sind:

<p class="note">
Die Funktion "Dokumente anzeigen" liefert alle Dokumente zu einer Schriftenreihe, unabhängig
davon, welchen Status (unpublished, inprogress, restricted, published) sie besitzen.
</p>

## Anzeige eines Logos

Es kann pro Schriftenreihe ein Logo angelegt werden, indem unter `$BASEDIR/public/series_logos` je ein neues
Verzeichnis angelegt und die gewünschte Datei dort abgelegt wird. Als
Verknüpfung zwischen Schriftenreihe und Logo dient die ID der gewünschten Schriftenreihe.

Beispiel: Logo für die Schriftenreihe "MySeries" anlegen

Zunächst wird die ID der Schriftenreihe "MySeries" benötigt. Diese wird in der Übersicht der
Schriftenreihen angezeigt:

Die ID kann auch durch einen Klick auf den Namen der Schriftenreihe ermittelt werden:
In diesem Beispiel handelt es sich um die ID 1. Das bedeutet, dass für das Logo das Verzeichnis
`$BASEDIR/public/series_logos/1` angelegt werden muss. In diesem Verzeichnis wird nun
ein Logo abgelegt.
Der Dateiname und das Dateiformat des Logos sind beliebig. Akzeptiert werden alle gängigen
Bildformate (z.B. jpeg, png, gif).
Das Logo ist optional, die maximale Breite beträgt 400px. Ist für eine Schriftenreihe kein Logo
abgelegt, wird auf der Browsing-Seite für die Infobox die gesamte Seitenbreite genutzt. Existiert auch
die (optionale) Infobox nicht, so werden die Dokumente der Schriftenreihe direkt unterhalb der
Navigation angezeigt.

## Sichtbarkeit

Schriftenreihen können auf sichtbar oder unsichtbar geschaltet werden. Wird die Option "sichtbar"
gewählt, dann ist die betreffende Schriftenreihe im Browsing, im Veröffentlichungsformular, auf der
Frontdoor eines verknüpften Dokuments und im Bereich 'Dokumente' 110 in der Administration
verfügbar.

Eine Schriftenreihe wird erst dann im Browsing angezeigt, wenn sie folgende Bedingungen
erfüllt:

* sichtbar
* enthält mindestens 1 Dokument im Zustand "published"

## Schriftenreihen umbenennen

Soll eine Schriftenreihe umbenannt werden, genügt es, im Bereich Schriftenreihen verwalten bei der
gewünschten Schriftenreihe auf "Ändern" zu klicken und den Namen entsprechend zu editieren:
