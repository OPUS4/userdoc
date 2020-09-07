---
title: Wartung
weight: 100
---

# Wartung des Index

TODO Aufruf vereinfachen

TODO Sicherheitsabfrage vor neuindexierung (override option für Batchmode)

TODO Indexieren ohne Volltext

TODO Was tun bei Problemen?

Für die Wartung des Index gibt es das Skript `SolrIndexBuilder.php`. Das Skript befindet sich im `scripts` Verzeichnis.
Dort kann es direkt aufgerufen werden. 

    $ cd scripts
    $ ./SolrIndexBuilder.php -h
    
## Dokumente indexieren

Wird das Skript ohne Argument aufgerufen werden alle Dokumente neu indexiert.

    $ ./SolrIndexBuilder.php

Ein einzelnes Dokument kann durch die Angabe seiner Idee indexiert werden.

    $ ./SolrIndexBuilder.php 155
    
Durch Angabe einer End-ID kann ein Block von Dokumenten indexiert werden.

    $ ./SolrIndexBuilder.php 40 60

Sollte die zweite ID kleiner als die erste sein, werden die Werte automatisch vertauscht.    
    
Wird statt einer ID das Zeichen `*` verwendet, werden alle Dokumente vom Anfang bzw. bis zum Ende indexiert.

    $ ./SolrIndexBuilder.php * 100
    
    $ ./SolrIndexBuilder.php 100 *  
    
### Optionen für die Indexierung               

## Dokumente entfernen

Mit der Option `-r` bzw. `--remove` kann man Dokumente aus dem Index entfernen. Wie beim Indexieren können einzelne
Dokumente oder ganze Blöcke entfernt werden.

    $ ./SolrIndexBuilder.php -r 45
    $ ./SolrIndexBuilder.php --remove 245 839
    
Ein Aufruf ohne ID entfernt alle Dokumente aus dem Index.

    $ ./SolrIndexBuilder.php --remove

## Index optimieren

Um den Index nach der Indexierung zu optimieren kann die Option `-o` bzw. `--optimize` verwendet werden.

    $ ./SolrIndexBuilder.php -o
    
Um nur die Optimierung des Index ohne eine Neuindexierung durchzuführen kann das Kommando `optimize` verwendet werden.

    $ ./SolrIndexBuilder.php optimize     

