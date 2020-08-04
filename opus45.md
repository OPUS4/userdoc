---
title: OPUS 4.5
weight: 50
---

# OPUS 4.5

Ist die erste Version von OPUS 4 die auf [GitHub][GITHUB] entwickelt wurde. Durch den Wechsel zu GitHub wird die
Zusammenarbeit mit externen Entwicklern vereinfacht.

## Git

Der Wechsel zu GitHub und damit Git als Entwicklungswerkzeug bietet auch neue Möglichkeiten für
die Installation und das Update von OPUS 4 Instanzen. Git ist hervoragend geeignet die Unterschiede zwischen
zwei Version von Software Sourcen aufzulösen. Es wird in Zukunft einen großen Teil des Update-Skriptes ersetzen.
Die Installation und Updates werden mit Git-Anweisungen durchgeführt werden.

## Composer

In Zunkunft wird [Composer](https://getcomposer.org) eingesetzt werden, um die Abhängigkeiten von OPUS 4 zu verwalten.
Notwendige Softwarebibliotheken wie z.B. das ZendFramework werden in einer Konfigurationsdatei aufgelistet und können
dann durch Composer installiert und aktualisiert werden. Dadurch vereinfachen sich die Installations- und Updateskripte.
Das OPUS 4 Framework, die Verbindung zur Datenbank und zum Suchindex, ist mit Version 4.5 ein eigenständiges Composer
Paket geworden, so daß es ebenfalls als Abhängigkeit von Composer heruntergeladen und aktualisiert werden kann. Die
Pakete werden auf [Packagist.org](https://packagist.org) gehostet. Die OPUS Pakete finden sich dort unter
[opus4-repo](https://packagist.org/packages/opus4-repo).

## Migration Skripte

Der Code für die Migration von OPUS 3 wurde aus der normalen OPUS 4 Release entfernt und in ein eigenes
Repository [migration](https://github.com/opus4/migration) auf GitHub verschoben. Die Migration wird in Zukunft eine
optionale Komponente sein, die bei Bedarf installiert werden kann.

[GITHUB]: https://github.com/OPUS4



