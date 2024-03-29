---
title: Wartung
weight: 100
---

# Wartung des Index

Für die Wartung des Index kann das Skript `opus4` im `bin`-Verzeichnis verwendet werden. Mit folgendem Aufruf wird
die Hilfe für die Indexierung angezeigt.

    $ bin/opus4 help index:index
    
Für das Index-Kommando gibt es außerdem den Alias `index`, damit es auch ohne Angabe den Namespaces aufgerufen 
werden kann.

    $ bin/opus4 index    
    
Um sich alle verfügbaren Kommandos anzeigen zu lassen, kann man das `list`-Kommando verwenden.

    $ bin/opus4 list   
    
## Dokumente indexieren

Wird das Index-Kommando ohne Argumente aufgerufen, werden alle Dokumente neu indexiert. Dabei werden dann vorher
sämtliche Dokumente aus dem Index entfernt. 

    $ bin/opus4 index
    $ bin/opus4 index:index
    
Das Kommando kann auch kürzer geschrieben werden. Falls ein Kommando durch die Kürzung nicht mehr eindeutig ist,
gibt das Skript einen entsprechenden Hinweis aus.
    
    $ bin/opus4 i:i

Ein einzelnes Dokument kann durch die Angabe seiner ID indexiert werden. Sollte die ID nicht existieren gibt es eine
entsprechende Fehlermeldung.

    $ bin/opus4 index:index 155
    
Durch Angabe einer Anfangs- und einer End-ID kann ein Block von Dokumenten indexiert werden. Sollte die zweite ID 
kleiner sein als die erste, werden die Werte automatisch vertauscht.    

    $ bin/opus4 index:index 40 60
    
Wird statt einer ID ein Bindestrich (`-`) verwendet, werden alle Dokumente vom Anfang bzw. bis zum Ende indexiert.

    $ bin/opus4 index:index - 100
    
    $ bin/opus4 index:index 100 -  
    
### Optionen für die Indexierung

#### Dokumente for der Indexierung entfernen

Um die Dokumente vor der Indexierung aus dem Index zu löschen, kann die Option `--remove` bzw. `-r` verwendet werden.

    $ bin/opus4 index:index -r
    
Die Option kann nützlich sein, um sicherzustellen, dass bei einer vollständigen Neuindexierung keine alten, nicht mehr     
existierenden Dokumente im Index verbleiben. Diese Situation könnte eintreten, wenn beim Löschen von Dokumenten der 
Index nicht aktualisiert werden konnte.

Eine Neuindexierung ohne vorheriges Löschen hat den Vorteil, dass der Index während der Indexierung weiter genutzt
werden kann.
     
#### Blocksize
    
Mit der Option `-b` bzw. `--blocksize` kann bestimmt werden wie viele Dokumente auf einmal zum Solr-Server geschickt 
werden sollen.

Das Bündeln von Dokumenten erhöht die Performanz. Es kann allerdings zu Problemen kommen, wenn die Indexierung eines 
Dokuments fehlschlägt und dadurch alle Dokumente im Block nicht indexiert werden. Das kann unter anderem passieren,
wenn die Volltexte der Dokumente besonders groß sind. In diesem Fall kann man die Blockgröße auf `1` setzen, damit 
jedes Dokument separat indexiert wird.      

    $ bin/opus4 index:index -b=1
    
    $ bin/opus4 index:index --blocksize=1
    
## Dokumente aus dem Index entfernen

Mit dem Kommando `index:remove` kann man Dokumente aus dem Index entfernen. Wie beim Indexieren können einzelne
Dokumente oder ganze Blöcke entfernt werden.

    $ bin/opus4 index:remove 45
    
    $ bin/opus4 i:r 245 839
    
Ein Aufruf ohne ID entfernt alle Dokumente aus dem Index.

    $ bin/opus4 index:remove
