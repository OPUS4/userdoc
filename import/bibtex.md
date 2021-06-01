---
title: BibTeX
---


# BibTeX-Import

Dokumentmetadaten können aus einer BibTeX-Datei, die beliebig viele BibTeX-Records enthält, sowohl über einen
**Kommandozeilen-Befehl** (CLI) als auch über ein **Web-Formular** im Administrationsbereich importiert werden.

Beim Import wird jeder in der BibTeX-Datei enthaltene BibTeX-Record auf ein OPUS4-Metadatendokument abgebildet
(das sogenannte _Feld-Mapping_). Über eine Konfigurationsdatei lässt sich die Abbildung der einzelnen
BibTeX-Felder auf die OPUS4-Metadatenfelder gezielt steuern.

Ferner kann die Abbildung der BibTeX-Dokumenttypen auf die OPUS4-Dokumenttypen ebenfalls über eine Konfigurationsdatei
gesteuert werden (das sogenannte _Dokumenttyp-Mapping_).

OPUS4 liefert eine Standardkonfiguration sowohl für das Dokumenttyp-Mapping als auch für das Feld-Mapping, 
die als Ausgangsbasis für instanzspezifische Konfigurationen genutzt werden kann.

## Import-Optionen

Sowohl der Kommandozeilen-Befehl für den BibTeX-Import als auch das Import-Formular im Administrationsbereich bieten
eine Reihe von Optionen, mit denen der Verarbeitungsprozess an die eigenen Bedürfnisse angepasst werden kann.

Folgende Optionen werden angeboten:

* Vorgabe der zu verwendenden INI-Konfigurationsdatei (absoluter Pfad), in der das Dokumenttyp-Mapping angegeben wird
  als auch die Feld-Mappings registriert werden. Hierbei können in einer Instanz mehrere Feld-Mappings registriert sein.
* Vorgabe des zu verwendenden Feld-Mappings: jedes Feld-Mapping wird durch eine JSON-Konfigurationsdatei definiert und
  es kann über seinen Namen eindeutig referenziert werden – über diese Option kann ein Feld-Mapping auf Basis seines
  Namens aus den in der INI-Konfigurationsdatei registrierten Feld-Mappings ausgewählt werden
* kommaseparierte Liste von Sammlung-IDs: jedes erfolgreich aus der BibTeX-Datei importierte Dokument wird mit den
  Sammlungen verknüpft, deren IDs in der Liste enthalten sind; hierbei werden unbekannte IDs ignoriert (es erfolgt ein
  Hinweis in der Logausgabe, wenn Sammlungen mit angegebenen IDs nicht existieren)
* _Verbose Mode_: erhöht die Anzahl der Meldungen, die in die Import-Protokollausgabe während des Importvorgangs
  geschrieben werden, so dass der Importprozess im Detail verfolgt werden kann; so werden bei der Aktivierung dieses
  Modus u.a. die IDs der neu erzeugten OPUS-Dokumente ausgegeben
* Trockenlauf-Modus / _Dry Mode_: dieser Modus erlaubt die Durchführung des Importvorgangs (d.h. das Parsing der
  BibTeX-Datei und schließlich die Erzeugung von OPUS-Dokumenten aus den in den BibTeX-Feldern gespeicherten Werten)
  **ohne** dabei die erzeugten OPUS-Dokumente tatsächlich in die OPUS-Datenbank zu speichern – dieser Modus bietet sich
  daher an, wenn eine BibTeX-Datei initial importiert werden soll und in einem ersten Schritt geprüft werden soll, 
  ob der Import der Datei fehlerfrei möglich ist
  
## Dokumenttyp-Mapping

Ein Dokumenttyp-Mapping besteht aus einer Map, die BibTeX-Dokumenttypen auf OPUS4-Dokumenttypen abbildet. Im
Dokumenttyp-Mapping können auch Nicht-Standard-BibTeX-Typen verwendet werden.

Das Mapping wird in einer INI-Konfigurationsdatei definiert und hat folgende Struktur (hier als Beispiel ein Auszug aus
der Standard- Konfigurationsdatei `import.ini`):

```ini
; Mapping der BibTeX-Typen auf OPUS-Dokumenttypen
documentTypeMapping[article]    = article
documentTypeMapping[techreport] = report
```
Hier wird der BibTeX-Dokumenttyp `article` bzw. `techreport` auf den OPUS4-Dokumenttyp `article` bzw. `report`
abgebildet.

Ferner ist es möglich einen Fallback-Dokumenttyp anzugeben, der immer dann zur Anwendung kommt, wenn für den 
vorliegenden BibTeX-Dokumenttyp kein Mapping konfiguriert wurde. In diesem Fall wird als OPUS4-Dokumenttyp der 
Fallback-Dokumenttyp verwendet:

```ini
; Standard-OPUS-Dokumenttyp, sofern für den im BibTeX-Record vorliegenden BibTeX-Typ kein Typ-Mapping auf einen
; OPUS-Dokumenttyp existiert
defaultDocumentType = misc
```

Soll das Dokumenttyp-Mapping in einer Instanz überschrieben werden, so empfiehlt es sich eine neue
INI-Konfigurationsdatei im Dateisystem, z.B. im zentralen Konfigurationsverzeichnis `application/configs` anzulegen, 
indem die Standard-Konfigurationsdatei `import.ini` kopiert und anschließend an die eigenen Bedürfnisse angepasst wird.
Bei der Ausführung des BibTeX-Imports (sowohl via Kommandozeile als auch über das Import-Formular) kann dann der Pfad 
zu der instanzspezifischen INI-Konfigurationsdatei als Option übergeben werden (CLI-Option `-i`).

## Feld-Mapping

Ein Feld-Mapping definiert, wie die Inhalte der Felder eines BibTeX-Datensatzes auf die Felder eines OPUS-Dokuments
abgebildet werden sollen. Die Konfigurationsmöglichkeiten sind mannigfaltig und reichen weit über einfache
1-zu-1-Mappings zwischen BibTeX-Feldern und OPUS4-Metadatenfeldern hinaus. Eine ausführliche Beschreibung kann im
OPUS4-Modul [opus4-bibtex](https://github.com/OPUS4/opus4-bibtex/blob/master/README.md#field-mapping) nachgeschlagen
werden.

Ein Feld-Mapping wird in einer JSON-Datei beschrieben. Die Standard-Konfigurationsdatei `default-mapping.json` kann
auch hier als Ausgangspunkt für instanzspezifische Feld-Mappings genutzt werden.

Jedes Feld-Mapping hat einen eindeutigen Namen, über den es beim Import (sowohl via Kommandozeile als auch über das
Import-Formular) referenziert werden kann.

Eine Instanz kann – z. B. für die Verarbeitung unterschiedlichen BibTeX-Varianten – mehrere Feld-Mappings besitzen.
Die einzelnen Feld-Mappings sind über ihren Dateinamen in der INI-Konfigurationsdatei (siehe oben) zu registrieren.
Als Beispiel sei hier die Registrierung des Standard-Feld-Mappings in der Standard-Konfigurationsdatei `import.ini`
angegeben:

```ini
fieldMappings[] = default-mapping.json
```

Die JSON-Dateien sollten im Verzeichnis vorgehalten werden, in der auch die INI-Konfigurationsdatei abgelegt ist.

## Prozessierung der BibTeX-Datei

Die zu importierende BibTeX-Datei wird zuerst mit einem **BibTeX-Parser** ausgelesen und dabei in die einzelnen
BibTeX-Records aufgeteilt. Tritt dabei ein Fehler auf, z. B. weil die zu importierende Datei nicht konform zum
BibTeX-Standard ist, so wird der Import beendet. Es wird eine Fehlermeldung ausgegeben, die weitere Details zum Fehler,
beispielsweise die Zeilennummer, enthält.

Nach dem erfolgreichen Parsen der BibTeX-Datei erzeugt ein **BibTeX-Processor** aus jedem BibTeX-Record auf Basis der
beim Aufruf des Imports angegebenen Konfigurationseinstellungen (siehe oben) ein OPUS4-Metadatendokument.

Tritt während der Erzeugung eines OPUS4-Metadatendokument ein Fehler auf, so wird das Dokument verworfen und der
BibTeX-Processor springt zum nächsten BibTeX-Record bzw. beendet die Verarbeitung, wenn alle BibTeX-Records verarbeitet
wurden.

Wird der Import nicht im Trockenlauf-Modus gestartet, so wird vom BibTeX-Prozessor schließlich geprüft, ob bereits
ein OPUS4-Metadatendokument in der Datenbank existiert, das aus einem identischen BibTeX-Record erzeugt wurde. Die
Prüfung erfolgt hierbei auf Basis einer Hashsumme, die für den BibTeX-Record ermittelt wird und in einem Enrichment
(`opus.import.dataHash`). Als Hashfunktion wird momentan `md5` verwendet – der Name der verwendeten Hashfunktion wird
als Präfix (getrennt durch `:`) im Enrichment gespeichert.

Wird in der OPUS4-Datenbank ein Dokument gefunden, das im Enrichment `opus.import.dataHash` einen Hashwert besitzt,
der mit dem Hashwert des aktuell vom BibTeX-Processor verarbeiteten BibTeX-Record übereinstimmt, so verwirft der
Prozessor das gerade in der Verarbeitung befindliche OPUS4-Metadatendokument. Es erfolgt in diesem Fall keine
Speicherung des OPUS4-Metadatendokuments in der Datenbank.

Diese Vorgehensweise ermöglicht das wiederholte Importieren von BibTeX-Dateien. So kann z. B. eine wachsende
BibTeX-Datei jährlich (oder häufiger, je nach Anwendungsfall) importiert werden und es ist dennoch sichergestellt, dass
beim Import keine Duplikate in der OPUS4-Datenbank entstehen. Die zu importierende BibTeX-Datei muss vorher auch nicht
von den bereits in einem früheren Import in die OPUS4-Datenbank eingefügten Dokumente befreit werden.

## Auszeichnung von OPUS4-Metadatendokumenten, die durch den BibTeX-Import erzeugt wurden

Jedes OPUS4-Metadatendokument, das über den BibTeX-Import erzeugt wurde, besitzt eine Menge von Enrichments, die es
eindeutig klassifizieren:

| Name des Enrichments   | Inhalt |
|------------------------|--------|
| `opus.import.data`     | enthält den ursprünglichen BibTeX-Record, aus dem das OPUS4-Metadatendokument erzeugt wurde |
| `opus.import.dataHash` | enthält die Hashsumme des BibTeX-Records; der Name der verwendeten Hashfunktion wird als Präfix getrennt durch `:` angegeben |
| `opus.import.date`     | Importdatum |
| `opus.import.file`     | Name der BibTeX-Datei, aus dem der BibTeX-Record stammt |
| `opus.import.format`   | hat den festen Wert `bibtex` |
| `opus.import.id`       | eindeutige ID des Importvorgangs (jeder Importvorgang einer BibTeX-Datei erhält eine eindeutige ID) |

