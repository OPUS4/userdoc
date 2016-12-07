---
title: Composer Pakete
---

# Composer Pakete

Sollte es bei der Installation der Abhängigkeiten mit Composer Probleme
geben, kann es helfen die Datei `composer.lock` zu löschen und das 
Installationskommando von Composer aufzurufen.

    $ php composer.phar install
    
Für produktive Repositorien können die Entwicklungsabhängigkeiten 
weggelassen werden.

    $ php composer.phar install --no-dev --optimize-autoloader
    
# `composer.lock`    
    
Es ist geplant in Zukunft die Datei `composer.lock` mit über Git 
auszuliefern. Das würde dafür sorgen, dass alle Repositorien der selben
OPUS Version mit genau den selben Composer Paket installiert werden.
Dadurch können Probleme auf anderen Systemen leichter reproduziert 
werden.

Andererseits kann es passieren, dass `composer.lock` Abhängigkeiten 
definiert, die für ältere Systeme nicht geeignet sind, weil zum Beispiel
eine neuere PHP Version verlangt wird. Wenn es Probleme gibt, kann die 
Datei `composer.lock` immer gelöscht und durch eine lokale Version 
ersetzt werden.




