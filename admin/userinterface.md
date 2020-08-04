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

## Benutzerdefinierte Felder (EnrichmentKeys)

Es gibt in OPUS4 die Möglichkeit, benutzerdefinierte Felder (EnrichmentKeys) anzulegen, um
Informationen zu Dokumenten zu erfassen, die nicht durch Standardfelder abgedeckt sind. Hierzu
werden die benutzerdefinierten Felder zunächst in der Administration (Administration >
Oberflächenanpassungen > Benutzerdefinierte Felder (Enrichments)) angelegt, indem nach einem
Klick auf "Neuer EnrichmentKey" der gewünschte Feldname eingetragen wird (z.B. "Lom_Wert")."
Das so angelegte benutzerdefinierte Feld kann nun in den gewünschten Dokumenttypen verwendet
werden. Wie diese Felder in den Dokumenttyp aufgenommen werden ist in der Konfiguration
beschrieben.

* [Einfache Textfelder neu anlegen](../translation/fields.html#einfache-textfelder-neu-anlegen)
* [Select-Felder neu anlegen](../translation/fields.html#select-felder-neu-anlegen)

Es werden ab der Version 4.2 auch einige EnrichmentKeys mitausgeliefert:

Die folgenden Felder sind nur systemintern von Bedeutung und können daher ignoriert werden:

    submitter.user_id
    reviewer.user_id
    review.rejected_by
    review.accepted_by

Darüber hinaus werden bei der Migration von OPUS 3 auf OPUS 4 bereits benutzerdefinierte Felder
angelegt, die bestimmte individuelle Inhalte aus OPUS 3 erfassen:

| Key | Beschreibung |
|-----+--------------|
| BemerkungExtern | Hierhin werden Bemerkungen aus OPUS3 migriert, die eine Darstellung von HTML-Code auf der Frontdoor benötigen (OPUS4 erlaubt aus Sicherheitsgründen kein HTML in den Eingabefeldern) |
| ClassRvk | Opus4 enthält keine RVK-Klassifikation, die Opus3-RVK-Klasse wird in dieses Feld migriert |
| ContributorsName | In Opus3 befinden sich bei Abschlussarbeiten die Namen sämtlicher Betreuer in einem Feld. Es existieren keine einheitlichen Separatoren zwischen den Namen, was beim Aufsplitten zu Fehlern führen kann. Aus dem Grund werden die Betreuer nochmal als Ganzes eingelesen, umsie später korrigieren zu können. |
| InvalidVerification | Dieser Schlüssel wird bei der Migration angelegt, wenn die E-Mail-Adresse des Submitters nicht Zend-Valide ist |
| SourceTitle | Enthält die komplette bibliografische Angaben zur Zweitpublikationen eines Opus3-Dokuments |
| SourceSwb | Die SWB-Ident-Nummer wird in dieses Feld eingetragen, da sie in Opus4 nicht geführt wird. |
| SubjectUncontrolledGerman, SubjectUncontrolledEnglish, SubjectSwd | Diese Felder sind der Tatsache geschuldet, dass die Schlagwörter teilweise gemischte Syntax haben und in OPUS3 nur ein Feld ausgegeben wird. Bei der Migration werden die Schlagwörter in separate Felder aufgesplittet, was mitunter zu falschen Konstellationen führt. Aus dem Grund werden die Schlagwörter |

Diese benutzerdefinierten Felder sind geschützt und nur für die Instanzen verwendbar, die von
OPUS3 migriert wurden. In neu installierten OPUS4 Instanzen können diese Felder nicht verwendet
werden.

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
