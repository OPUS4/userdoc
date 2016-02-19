---
title: Systeminformationen
weight: 100
---

# Systeminformationen

In diesem Bereich finden sich

## Systemparameter

Hier werden einige wichtige Systemparameter zum Laden von Dateien in OPUS 4 angezeigt.

## OAI-Links

Dieser Bereich zeigt Beispiele für OAI-Links, wenn die Metadaten des Repositoriums in andere Dienste eingebunden
werden sollen (z.B. BASE).

## Veröffentlichungsstatistik

In diesem Menüpunkt kann aktuell die Veröffentlichungsstatistik des Repositoriums für ein
bestimmtes Jahr abgerufen werden: Gesamtanzahl der Dokumente, neu eingestellte Dokumente pro
Monat, Dokumente pro Dokumenttyp und Dokumente pro Institut.

## Job-Verarbeitung

Es ist möglich, in OPUS4 bestimmte lang laufende Jobs (z.B. die Indexierung großer Dokumente)
asynchron zu verarbeiten. Auf diese Weise können Timeouts (weiße Seite) vermieden werden. Die
asynchrone Verarbeitung nutzt den Mechanismus des Unix cron-Daemon, der die zeitbasierte
Ausführung von Prozessen und wiederkehrende Aufgaben in sogenannten Cron-Jobs automatisiert.
Die Aktivierung der asynchronen Jobverarbeitung wird in Kapitel 7.13 JOB EXECUTION SETTINGS
58 beschrieben.

Über die Administration kann nun der Status der Jobverarbeitung überprüft werden:

## Verwaltung des Solr-Index

Durch die verteilte Datenhaltung in OPUS4 kann es u.U. zu Inkonsistenzen zwischen MySQL
Datenbank und Solr Index kommen. Drei Fälle sind hierbei zu unterscheiden:

* ein publiziertes Dokument befindet sich in der Datenbank, aber nicht im Suchindex,
* ein publiziertes Dokument befindet sich im Suchindex, aber nicht in der Datenbank,
* ein publiziertes Dokument befindet sich sowohl in der Datenbank als auch im Suchindex,
  allerdings stimmen die beiden Versionen nicht überein (die Versionsprüfung erfolgt über das Datum
  der letzten Änderung – ServerDateModified –, das bei jeder direkten oder indirekten Änderung an
  einem Dokument aktualisiert wird).

Die Konsistenzprüfung findet sich im Administrationsbereich unter Systeminformationen, Verwaltung
des Solr-Index.

Hinweis: Für die Suche werden nur publizierte Dokumente betrachtet.
Aus diesem Grund ist aktuell auch nur die Konsistenzprüfung dieser Dokumente möglich.

Da die Prüfung der Konsistenz eine ressourcenintensive Operation ist, wird diese nur angeboten,
wenn die asynchrone Jobverarbeitung 58 in der Konfiguration aktiviert wurde. Zusätzlich ist es
möglich, die asynchrone Jobverarbeitung nur für dieses Feature zu aktivieren. Dazu muss der Eintrag

    runjobs.indexmaintenance.asynchronous = 1

in die Konfigurationsdatei config.ini aufgenommen werden bzw. der Wert (1) angepasst werden,
sofern der Schlüssel bereits existiert.

Ist keiner der beiden Einträge gesetzt, so wird das Feature innerhalb der Administration nicht
angeboten und es erscheint ein entsprechender Hinweistext.

Ist das Feature aktiviert, so kann es über den Button "Starten" ausgeführt werden:

Gleichzeitig wird – sofern verfügbar – die Logausgabe des letzten Durchlaufs angezeigt.

Nachdem der Button gedrückt wurde, erscheint eine grüne Meldung, die angibt, dass ein
entsprechender Job in die Verarbeitungswarteschlange eingetragen wurde.

Die Ausführungszeit des Jobs kann je nach Konfiguration und Arbeitsaufwand variieren.

Je nach Anzahl der veröffentlichten Dokumente kann die Konsistenzprüfung einiges an Zeit in
Anspruch nehmen.

Sie können die Seite immer wieder aufrufen, um zu kontrollieren, ob der Job bereits verarbeitet wird.
Solange der Vorgang noch in der Warteschlange liegt, wird die Logausgabe des letzten Durchlaufs
angezeigt.

Sobald der Job an der Reihe ist und die Ausführung beginnt, wird eine entsprechende Meldung
angezeigt:

Nun wird auch nicht mehr die Logausgabe des letzten Durchlaufs angezeigt. Sie können die Seite
immer wieder aufrufen, um zu kontrollieren, ob der Job vollständig beendet wurde.

Sobald die Verarbeitung des Jobs beendet wurde, erscheint wieder der Button "Starten". Außerdem
wird die Logausgabe aktualisiert. Neben dem Ende der Verarbeitungszeit werden die einzelnen
Operationen aufgelistet.

Im Screenshot sehen Sie jeweils die Ausgabe für die drei in der Einleitung besprochenen
Beispielfälle von Inkonsistenz.

Hinweis: Bitte beachten Sie, dass die Logausgabe nur in englischer Sprache erfolgt.

## Dokumenttypen

Diese Seite listet die lokal verfügbaren Dokumenttypen, die deutsche oder englische Bezeichnung,
den Dateinamen und ob der Dokumenttyp aktiv ist, also beim Hinzufügen eines neuen Dokuments
ausgewählt werden kann. Darüber hinaus werden die XML Definitionsdateien gegen das Schema validiert
und die Fehlermeldungen gegebenenfalls angezeigt.
