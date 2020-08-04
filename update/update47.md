---
title: OPUS 4.7 Update
---

# OPUS 4.7 Update

Das Update auf OPUS 4.7 muss in mehreren Schritten durchgeführt werden. Es kann länger dauern und erfordert 
manuelle Eingriffe, insbesondere, wenn eine Instanz umfangreich angepasst wurde.

<p class="warning">
Vor einem Update sollte immer ein Backup der Instanz und ihrer Daten angelegt werden. Das Update sollte 
zuerst in einer Testinstanz geprüft werden. Da OPUS 4 Instanzen häufig modifiziert werden, ist es schwer
vorherzusehen, welche Probleme lokal auftreten könnten.
</p>  

## 1. Code aktualisieren

Beim Update müssen wie immer die OPUS 4 Dateien mit `git pull` auf den neusten Stand gebracht werden. Die 
aktuelle Release Version liegt auf dem __master__-Branch im OPUS 4 
[__application__](https://github.com/OPUS4/application) Repository auf GitHub.

Das Update auf OPUS 4.7 setzt mindestens OPUS 4.5-RC1 voraus. Falls es sich um eine ältere Version handelt,
muss zuerst auf die [Git-Version umgestiegen](from445.html) werden.

Für OPUS 4.7 wurden sehr viele Dateien verändert. Bei Instanzen mit Anpassungen im PHP-Code oder z.B. den 
XSLT-Dateien für den Export, OAI oder die Indizierung, kann es so Konflikten kommen, die mit den für Git
üblichen Werkzeugen manuell behoben werden müssen. 

<p class="info" markdown="1">
Wenn sie beim Update feststellen, dass sie lokale Anpassungen manuell mit den Änderungen der neuen Version
zusammenführen müssen, lohnt es sich vielleicht den Anwendungsfall für Ihre Anpassungen in einem 
[__Issue__](https://github.com/OPUS4/application/issues) auf GitHub zu schildern bzw. einen 
[__Pull Request__](https://docs.github.com/de/github/collaborating-with-issues-and-pull-requests/about-pull-requests) 
für die Anpassungen einzureichen. Sollte der Anwendungsfall nicht im Konflikt mit der allgemeinen Nutzung 
und der weiteren Entwicklung von OPUS 4 stehen, kann er vielleicht im Standardcode direkt unterstützt 
werden.
Wir versuchen mit jedem Release die Notwendigkeit für Eingriffe in den Code zu verringern und Anpassungen 
durch Konfiguration zu unterstützen. Das macht Updates langfristig hoffentlich immer einfacher und sorgt
für weniger Überraschungen bei der Entwicklung, wenn wir feststellen, dass OPUS 4 auf eine unerwartete Art
und Weise genutzt wird, die es schwer macht größere Änderungen vorzunehmen.
</p>

## 2. Libraries aktualisieren

Wenn die OPUS 4 Dateien aktualisiert und alle Konflikte aufgelöst wurden, müssen die Composer Pakete mit 
folgendem Kommando auf den neusten Stand gebracht werden.

    $ composer update
    
Dabei wird es vermutlich einige Warnungen geben für Pakete, die nicht länger weiterentwickelt werden. Das
liegt daran, dass OPUS 4 immer noch Zend Framework 1 verwendet. Einer der wichtigsten nächsten 
Entwicklungsschritte wird der Umstieg auf Zend Framework 3 bzw. [Laminas](https://getlaminas.org/), dem 
Zend Nachfolger, sein. 

## 3. Solr 7.7.2 installieren  

OPUS 4.7 verwendet eine neue Version von [Apache Solr](https://lucene.apache.org/solr/). Es wurde mit    
Solr 7.7.2 getestet. Vermutliche funktioniert OPUS 4.7 auch mit allen anderen, insbesondere neueren
Solr 7.7.x Versionen. 

<https://lucene.apache.org/solr/downloads.html>

Für Informationen zur Installation von Apache Solr und die Absicherung eines Solr Servers sollte die  
[Apache Solr Dokumentation](https://lucene.apache.org/solr/guide/7_7/index.html) herangezogen werden.

Wir empfehlen die Installation als Service wie beschrieben in 
[Taking Solr to Production](https://lucene.apache.org/solr/guide/7_7/taking-solr-to-production.html#taking-solr-to-production).

<p class="warning" markdown="1">
Wir können hier in der Dokumentation für OPUS 4 nicht auf alle Aspekte eines im Internet betriebenen
Servers eingehen. Dafür ist das Thema zu umfangreich und vor allem entwickelt es sich ständig weiter. 
Für den sicheren Betrieb eines Servers sollte ein erfahrener System-Administrator zu rate gezogen und 
die aktuellen Empfehlungen berücksichtig werden. 
</p>

In dem neuen Solr-Server muss ein Core für OPUS 4 angelegt werden. Die Konfigurationsdateien dafür 
finden sich im OPUS 4 __search__ Paket.

    vendor/opus4-repo/search/conf/schema.xml
    vendor/opus4-repo/search/conf/solrconfig.xml
    
Die Dateien sollten mit dem Konfigurationsverzeichnis für den Solr-Core verlinkt werden, damit 
nach einem Update automatisch die neuesten Dateien verwendet werden.    

## 4. Updateskript ausführen

Für das Update auf OPUS 4.7 müssen Veränderungen an der Datenbank und andere Schritte vorgenommen 
werden. Dafür muss das Updateskript ausgeführt werden.

    $ bin/update.sh
    
Für OPUS 4.7 werden dabei folgende Schritte ausgeführt.

### Zeichensatz der Datenbank umstellen

Die MySQL Datenbank wird zum Zeichensatz __utf8mb4__ konvertiert, damit sämtliche Zeichen
gespeichert werden können und es nicht mehr zu Fehlermeldungen kommt, wenn z.B. beim Kopieren
von Zusammenfassungen Steuerzeichen mit übertragen wurden.
   
### Angepasste Übersetzungen in Datenbank importieren
   
Angepassten Übersetzungen werden in die Datenbank migriert. Das heißt die Inhalte der TMX-Dateien
in den `language_custom` Verzeichnissen werden in die Datenbank übertragen. Die Verzeichnisse
werden nach Möglichkeit automatisch entfernt, müssen aber evtl. manuell bereinigt werden, wenn 
dort z.B. auch noch andere Dateien gespeichert sind.
   
### Statische Seiten in die Datenbank importieren

Die Dateien (TXT) für die statischen Texte im Verzeichnis `application/configs/help` werden in 
die Datenbank übertragen und als `.imported` markiert. Das betrifft Startseite, Impressum und
Kontaktseite.

### Enricment `opus.source` anlegen   
   
Es wird das Enrichment `opus.source` angelegt. Es wird dafür verwendet Dokumente, die über SWORD
importiert wurden, von Dokumenten zu unterscheiden, die mit dem Publish-Modul eingetragen wurden.
   
### FAQ-Texte in die Datenbank importieren
   
Die Textdateien für die FAQ-Seite werden in die Datenbank migriert und mit `.imported` markiert.
Die Datei `help.ini` wird weiterhin verwendet, kann nun aber in der Administration editiert werden.

### Namen von Sammlungen (CollectionRole) validieren 

Die Namen von Sammlungen (CollectionRole) werden validiert. Da diese Namen in Übersetzungsschlüsseln
verwendet werden, dürfen sie keine Sonderzeichen enthalten. Es findet eine automatische Bereinigung 
statt, bei der ungültige Namen als Übersetzungen in der Datenbank gespeichert werden, damit nach
dem Update die Anzeige immer noch korrekt sein sollte.

Die Veränderungen werden im Update-Log protokolliert, damit eine Überprüfung möglich ist.

Falls eine CollectionRole mit einem ungültigen Namen in angepassten XSLT-Dateien verwendet wurde, 
muss diese Anpassung manuell nachgezogen werden. 

Die Namen und Übersetzungen für Sammlungen (CollectionRole) können in der Administration editiert
werden. 

## 5. Dokument erneut indizieren

Nach dem erfolgreichen Update aller Dateien und der Datenbank, müssen die Dokumente indiziert werden.

    $ php scripts/SolrIndexBuilder.php
    
Je nach Größe der Instanz kann dies von einigen Minuten bis zu mehreren Stunden dauern.

## Viel Erfolg!

Nach den oben beschriebenen Schritten sollte Ihnen OPUS 4.7 mit den neuesten Funktionen zur Verfügung
stehen.

Falls es Probleme gibt wenden Sie sich bitte an die 
[OPUS 4 Tester Mailingliste](http://listserv.zib.de/mailman/listinfo/kobv-opus-tester)
oder an die OPUS 4 Hosting Teams beim 
[KOBV](https://www.kobv.de/entwicklung/software/opus-4/#acc-tb_3ex4758-3) 
oder BSZ.  

<p style="text-align: center">Viel Spaß und Erfolg bei der Nutzung von OPUS 4.7!</p>
