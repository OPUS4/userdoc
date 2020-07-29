---
title: Suche
weight: 10
---

# Suche

Die Suche wird in OPUS4 über Apache Solr realisiert. Dass bedeutet, dass alle gängigen Funktionen zur Verfügung stehen,
die Nutzer von anderen Suchmaschinen her kennen, wie beispielsweise Phrasensuche, Trunkierung und eine einfache Suche
über alle relevanten Felder hinweg.

## Einfache Suche

In der einfachen Suche wird in den Titeln (Haupt- und Untertitel, Übergeordneter Titel, Übersetzter Titel), den
Körperschaften, den Abstracts, allen Personen, allen Identifiern, den Volltexten (wenn vorhanden), den Schlagwörtern
(SWD und freie) und Verlagsinformationen (Name und Ort) der Dokumente gesucht.

## Erweiterte Suche

In der Erweiterten Suche kann gezielt nach Autoren, Titeln, Weiteren Personen, Gutachtern, Zusammenfassungen,
Volltexten und Jahren gesucht werden. Diese Suchfelder können miteinander kombiniert werden ('Alle Wörter' 'Mindestens
ein Wort' 'Keines der Wörter').

## RSS-Feeds auf Suchanfragen

In OPUS4 können beliebige Suchen (inkl. ausgewählter Facetten) als RSS-Feed abonniert werden. Dazu muss einfach nur
`/export/rss` an die URL angehängt werden.

Ein Beispiel für eine einfache Suche, um alle neuen Dokumente zu abonnieren, die eine Suche nach dem Stichwort "doe"
und dem Schlagwort "eBook" liefert:

    /solrsearch/index/search/searchtype/simple/query/doe/subjectfq/eBook

wird zu

    /solrsearch/index/search/searchtype/simple/query/doe/subjectfq/eBook/export/rss

Ein Beispiel aus dem Browsing, um alle neuen Dokumente einer Schriftenreihe zu abonnieren:

    /solrsearch/index/search/searchtype/series/id/1

wird zu

    /solrsearch/index/search/searchtype/series/id/1/export/rss

Stehen in der URL die Parameter `start`, `rows`, `sortfield` und/oder `sortorder`, so werden diese automatisch entfernt
(und ignoriert).

<p class="info" markdown="1">
Die Dokumente im RSS-Feed werden nach dem Feld `server_date_published` absteigend sortiert.
Es werden immer 25 Einträge ausgegeben.
Es können auch RSS-Feeds auf Suchanfragen abonniert werden, die aktuell noch keine Treffer liefern.
</p>

## OpenSearch

Die Suchseiten von OPUS unterstützen OpenSearch. Das heißt es ist eine
Beschreibung verlinkt, die es Browsern ermöglicht OPUS als Suchmaschine 
zu erkennen. In Firefox zum Beispiel lässt sich so ein Repositorium zu 
den bekannten Suchmaschinen hinzufügen und kann dann direkt vom 
Suchfeld des Browsers aus durchsucht werden.

<p class="note" markdown="1">
In den Browsern Chrome und Chromium funktioniert dies nur, wenn die 
Suchseite direkt über eine Domain ohne weiteren Pfad aufgerufen werden
kann. Also zum Beispiel: ´https://myrepo.org/´ und **nicht** ´https://mydomain.org/myrepo´.
</p>
