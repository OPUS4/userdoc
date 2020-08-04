---
title: Oberflächenanpassungen
weight: 90
---

# Oberflächenanpassungen

Im Setup Bereich der Administration können die Übersetzungen von OPUS 4 angepasst werden. Jeder 
übersetzte Text hat einen Schlüssel. Manche Übersetzungen können direkt in verschiedenen 
Formularen der Administration editiert werden, z.B. für Sammlungen und Enrichments. Es gibt
eine allgemeine übersetzungsverwaltung weitere Einträge editieren lassen. Mehr dazu in der 
Dokumentation für die [Übersetzungen][TRANSLATIONS].

Die Bearbeitung von Übersetzungsressourcen sowie statischer Seiten ist seit Version 4.4 über die
Opus4-Oberfläche möglich. In der Administration gibt es unter dem Punkt "Oberflächenanpassungen"
vier Einstiegspunkte:

1. Benutzerdefinierte Felder (Enrichments)
2. FAQ-Seite
3. Statische Seiten (Hauptseite, Kontaktinformationen, Impressum)
4. Übersetzungen (Feldnamen, Feldüberschriften, Feldhilfen)

Im Kapitel [Übersetzungsressourcen][TRANSLATIONS] ist beschrieben, wie die Bearbeitung über die Oberfläche
aktiviert werden kann. Die folgenden Seiten widmen sich den vier genannten Themen.

## FAQ-Seite

Die Hilfeseite (FAQ) kann im Setup-Bereich der Administration bearbeitet werden. Die Inhalte und die Struktur der
Seite können editiert werden. Für weitere Informationen:

* [FAQ-Seite](../translation/faq.html)
{: class="navlist" }

## Statische Seiten

Hier können die Startseite, die Kontaktdaten und das Impressum angepasst werden. Dazu ist zuerst
auszuwählen, welches der drei Themen bearbeitet werden soll.

## Übersetzungen

Über eine Suchfunktion können aus allen Übersetzungsschlüsseln diejenigen herausgefiltert werden,
in denen der Suchbegriff vorkommt. Dabei bezieht sich die Suche bisher auf den Namen des
Übersetzungsschlüssels und nicht auf den Inhalt der Übersetzung. Die gefundenen
Übersetzungsschlüssel nebst Inhalten und weiteren Informationen werden in einer Tabelle dargestellt
und können nach den Tabellenspalten sortiert werden.

Zu jedem Eintrag wird ein Link angeboten, der auf eine Bearbeitungsseite für den
Übersetzungsschlüssel führt. Liegt der Inhalt in einer nicht zu bearbeitenden Datei (also im
Unterverzeichnis `language`), so werden die Inhalte für diesen Schlüssel für die Bearbeitung
übernommen, aber in der zu bearbeitenden Datei (im Verzeichnis `language_custom`) gespeichert.

[TRANSLATIONS]: ../translation/index.html
