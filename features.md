---
title: Begriffe und Funktionen
weight: 10
---

# Begriffe und Funktionen

Das verwendete Vokabular für Funktionen und Bereiche ist in einigen Punkten spezifisch für OPUS.
An dieser Stelle werden daher alle Funktionen vorgestellt, auf die in der Applikation zugegriffen
werden kann. Dabei werden spezifische Begriffe entsprechend definiert und erläutert.

<p class="warning">
OPUS ist nur sinnvoll zu benutzen, wenn im Webbrowser Cookies eingeschaltet sind. Sind
Cookies nicht erlaubt, so funktioniert der Login in die Administration nicht und der normale Anwender
kann ohne Cookies keine Dokumente über das Veröffentlichungsformular einstellen.
</p>

## Startseite

Auf der Startseite besteht die Möglichkeit, einen eigenen Willkommenstext zu verfassen.

## Suche

Die Suche wird in OPUS4 über Apache Solr realisiert. Dass bedeutet, dass alle gängigen Funktionen zur Verfügung stehen,
die Nutzer von anderen Suchmaschinen her kennen, wie beispielsweise Phrasensuche, Trunkierung und eine einfache Suche
über alle relevanten Felder hinweg.

### Einfache Suche

In der einfachen Suche wird in den Titeln (Haupt- und Untertitel, Übergeordneter Titel, Übersetzter Titel), den
Körperschaften, den Abstracts, allen Personen, allen Identifiern, den Volltexten (wenn vorhanden), den Schlagwörtern
(SWD und freie) und Verlagsinformationen (Name und Ort) der Dokumente gesucht.

### Erweiterte Suche

In der Erweiterten Suche kann gezielt nach Autoren, Titeln, Weiteren Personen, Gutachtern, Zusammenfassungen,
Volltexten und Jahren gesucht werden. Diese Suchfelder können miteinander kombiniert werden ('Alle Wörter' 'Mindestens
ein Wort' 'Keines der Wörter').

### RSS-Feeds auf Suchanfragen

In OPUS4 können beliebige Suchen (inkl. ausgewählter Facetten) als RSS-Feed abonniert werden. Dazu muss einfach nur
```/export/rss``` an die URL angehängt werden.

Ein Beispiel aus der Suche, um alle neuen Dokumente zu abonnieren, die eine Suche nach dem Stichwort "doe" und dem
Schlagwort "eBook" liefert:

<http://example.org/solrsearch/index/search/searchtype/simple/query/doe/subjectfq/eBook>

wird zu

<http://example.org/solrsearch/index/search/searchtype/simple/query/doe/subjectfq/eBook/export/rss>

Ein Beispiel aus dem Browsing, um alle neuen Dokumente einer Schriftenreihe zu abonnieren:

<http://example.org/solrsearch/index/search/searchtype/series/id/1>

wird zu

<http://example.org/solrsearch/index/search/searchtype/series/id/1/export/rss>

Stehen in der URL die Parameter start, rows, sortfield und/oder sortorder, so werden diese automatisch entfernt
(und ignoriert).

<p class="warning">
Die Dokumente im RSS-Feed werden nach <code>server_date_published</code> absteigend sortiert. Es werden immer 25
Einträge ausgegeben. Es können auch RSS-Feeds auf Suchanfragen abonniert werden, die aktuell noch keine Treffer liefern.
</p>

## Browsing

Die Funktion 'Browsen' dient dazu, sich einen Überblick über Dokumente nach bestimmten Ordnungskriterien wie z.B.
anhand des Dokumenttyps oder der Zugehörigkeit zu einer Sammlung, zu verschaffen.

### Zuletzt veröffentlichte Dokumente im Repositorium

Diese Funktion listet für einen schnellen Überblick die zuletzt veröffentlichten Dokumente im Repositorium auf. Die
Reihenfolge orientiert sich an der erstmaligen Veröffentlichung des Dokuments (Datum der Freischaltung).

### Dokumenttypen

Diese Funktion ermöglicht es, nach Dokumenten anhand des Dokumenttyps zu browsen. OPUS4 wird in der Standardversion
mit den im Anhang 207 beschriebenen und in der Beschreibungssprache XML formulierten Dokumenttypen ausgeliefert. Diese
Dokumenttypen können geändert (S.83) und es können neue Dokumenttypen (S. 95 definiert werden.

### Schriftenreihen

Die Schriftenreihe (auch Serie, Serienwerk, Reihenwerk, Nummerierte Reihe) gehört – in der Fachsprache des
Bibliothekswesens – gemeinsam mit den Periodika zu den fortlaufenden Sammelwerken. Schriftenreihen sind wie Periodika
zeitlich unbegrenzt, haben also keinen festgelegten Abschluss. Im Gegensatz zu den Periodika (z. B. Tageszeitung)
erscheinen die einzelnen Teile einer Schriftenreihe in der Regel jedoch nicht in regelmäßigen zeitlichen Abständen. Die
fortlaufend veröffentlichten einzelnen Werke einer Schriftenreihe erhalten eigene Titel, diese Stücktitel bezeichnen den
einzelnen Teil (Heft (Broschüre), Band), der Gesamttitel oder Serientitel hingegen die gesamte Schriftenreihe. Der
Serientitel hält die Stücktitel übergeordnet zusammen. Die einzelnen Stücktitel sind jeweils in sich abgeschlossen und
stammen meist von verschiedenen Autoren. Die Hefte und Bände von Schriftenreihen sind in der Regel durchnummeriert
und/oder alphabetisiert, ungezählte Serien sind seltener.

Diese Schriftenreihen sind über das Browsing zugänglich und können im Administrationsbereich angelegt und editiert
werden. Die Konfiguration ist weiter unten unter "Schriftenreihen verwalten" 153 beschrieben.

### Sammlungen

Hierarchische Systeme, wie z.B. Institutionen (z.B. Organigramme von Universitäten, Arbeitsgruppen, Forschungsbereiche)
und Klassifikationen, werden in OPUS4 über die Sammlungen verwaltet. Mit OPUS4 werden standardmäßig folgende
Klassifikationen ausgeliefert: DDC, CCS, PACS, JEL, MSC und BKL. Diese Sammlungen sind über das Browsing zugänglich und
können im Administrationsbereich angelegt und editiert werden. Die Konfiguration ist weiter unten unter "Sammlungen
verwalten 145" beschrieben.

## Veröffentlichen

Neben der Suche und dem Browsen stellt das Veröffentlichen von Dokumenten die dritte zentrale Funktion in OPUS dar.
Grundlage für das Veröffentlichen von Dokumenten bilden die Dokumenttypen. Die Standardversion von OPUS4 enthält
Dokumenttypen, die prinzipiell anderen Dokumenttypen untergeordnet sind (z.B. "Teil eines Buches" und
"Buch (Monographie)"). Diese Form der Beziehung wird jedoch in der aktuellen Version nicht funktionell unterstützt,
das heißt, es gibt keine Möglichkeit, beispielsweise Dokumente, die als "Teil eines Buches" im Repositorium
aufgenommen wurden, dem entsprechenden übergeordneten Dokument "Buch (Monographie)" funktional zuzuordnen. Wenn man
innerhalb eines Dokumenttyps auf ein übergeordnetes Dokument verweisen möchte, kann man hierfür das Feld
"TitleParent/Übergeordnetes Werk" benutzen. Der Inhalt dieses Feldes ist dann suchbar, das heißt, eine Suche über
alle Felder oder eine Titelsuche nach dem betreffenden übergeordneten Werk würde als Ergebnis auch die Dokumente
anzeigen, die nur auf dieses übergeordnete Werk verweisen.

Die Dokumente werden über ein 3-stufiges Formular in OPUS eingestellt. Im ersten Schritt werden ein Dokumenttyp
ausgewählt und (optional) die entsprechenden Datei(en) hochgeladen. Zusätzlich kann das Dokument durch das Setzen
eines Häkchens zur Bibliographie hinzugefügt werden. Im zweiten Schritt werden dann die Metadaten basierend auf dem
gewählten Dokumenttyp eingegeben. Es gibt Pflicht- und optionale Felder. Pflichtfelder werden durch einen Stern
gekennzeichnet. Wenn alle (Pflicht-)Felder ausgefüllt wurden, werden die Formulardaten durch den Klick auf den
Senden- Button validiert. Im Falle eines Fehlers wird zurück auf das Formular geleitet und Fehler können berichtigt
werden.

Waren alle Eingaben korrekt, gibt es im Schritt drei die Möglichkeit, die Eingaben erneut zu prüfen und durch Klicken
des Zurück-Buttons gegebenenfalls zu korrigieren. Darüber hinaus besteht in diesem Schritt die Möglichkeit, das
Dokument (optional) einer Sammlung zuzuordnen. Ein Klick auf den Button 'Abspeichern' speichert das Dokument mit dem
Status "unpublished" auf dem Dokumentenserver und es muss nach einer Prüfung durch den Administrator oder (eine)
berechtigte Person(en) freigeschaltet werden. Anschließend ist das Dokument mit dem Status "published" verfügbar.

## FAQ-Seite

Die FAQ-Seite bietet die Möglichkeit, Hilfetexte für die Benutzer zu häufig gestellten Fragen anzubieten. OPUS4 
liefert bereits einige Texte mit aus, die angepasst beziehungsweise geändert werden können. Im Kapitel FAQ-Seite 
101 wird beschrieben, wie Sie diese Änderungen vornehmen können. 

## Export

## Publikationslisten
