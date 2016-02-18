---
title: Bedeutung der Felder
---

# Bedeutung der Felder

In den folgenden Tabellen sind alle Felder aufgeführt, die für Dokumente in OPUS 4 verfügbar sind. Im Gegensatz zu
den Labeln können die Feldbezeichnungen nicht geändert werden. Die Felder sind in unterschiedliche Bereiche geteilt.

* [Allgemein](#allgemein)
* [Identifier](#identifier)
* [Personen](#personen)
* [Klassifikationen](#klassifikationen)

## Allgemein

| Feld | Label | Beschreibung |
|------+-----------------+--------------|
| CompletedDate | Veröffentlichungsdatum (online) | Standarddatum in jedem Dokumenttyp, wird per default mit dem aktuellen Datum beim Einstellen des Dokuments belegt |
| CompletedYear | Jahr der Fertigstellung | |
| ContributingCorporation | Beteiligte Körperschaft | Name der Organisation, die einen bedeutsamen intellektuellen Beitrag zum Dokument geleistet hat |
| CreatingCorporation | Urhebende Körperschaft | Name der Organisation, die den intellektuellen Inhalt des Dokuments verantwortet (bibliographische Angabe) |
| Edition | Auflage | z.B. Auflage eines Buches (bibliographisches Feld) |
| Issue | Heft | Heft, in dem bspw. ein Artikel erschienen ist; bibliographisches Feld |
| Language | Sprache der Veröffentlichung | Sprache, in der die elektronische Ressource verfasst wurde |
| Licence | Lizenz beschreibt die Rechte / den Zugriff auf das Dokument (mit / ohne Print on Demand, welche CC-Lizenz ) |
| Note | Bemerkung | freies Feld für (öffentliche und private) Anmerkungen |
| PageFirst | Erste Seite | Nummer der ersten Textseite |
| PageLast | Letzte Seite | Nummer der letzten Textseite |
| PageNumber | Seitenzahl |Anzahl der Seiten des Dokuments |
| PublishedDate | Datum der Erstveröffentlichung | kommt zum Einsatz, wenn das Dokument bereits veröffentlicht wurde (z.B. in einem Verlag); bibliographisches Feld |
| PublishedYear | Jahr der Erstveröffentlichung | kommt zum Einsatz, wenn das Dokument bereits veröffentlicht wurde (z.B. in einem Verlag); bibliographisches Feld |
| PublisherName | Verlag | Name des Verlags;bibliographisches Feld |
| PublisherPlace | Verlagsort | Ort des Verlags; bibliographisches Feld |
| Series | Schriftenreihen | Browsingfeld zur Auswahl der verfügbaren Schriftenreihen |
| ThesisDateAccepted | Datum der Annahme der Abschlussarbeit | Datum, an dem die Abschlussarbeit im Sinne der Prüfungsordnung angenommen wurde; i.d.R. das Datum der mündlichen Prüfung |
| ThesisYearAccepted | Jahr der Annahme der Abschlussarbeit | Jahr, in dem die Abschlussarbeit im Sinne der Prüfungsordnung angenommen wurde; i.d.R. das Jahr der mündlichen Prüfung |
| ThesisGrantor | Titel verleihende Institution | der Inhalt dieses Feldes wird über die Institute (Verbreitende Stelle) im Administrationsbereich verwaltet. |
| ThesisPublisher | Veröffentlichende Institution | der Inhalt dieses Feldes wird über die Institute (Verbreitende Stelle) im Administrationsbereich verwaltet. |
| TitleAbstract | Abstract / Kurzfassung | Eine Zusammenfassung der Arbeit
| TitleAdditional | Übersetzter Titel | dieses Feld kommt zum Einsatz, wenn neben dem Originaltitel noch ein übersetzter Titel gefordert ist |
| TitleMain | Haupttitel | Originaltitel des Dokuments oder des Objekts |
| TitleParent | Titel des übergordneten Werkes | z.B. Titel der Zeitschrift, des Sammelwerks etc. |
| TitleSub | Untertitel | Untertitel (Zusatz zum Sachtitel) des Dokuments oder des Objekts |
| Type | Dokumenttyp | |
| Volume | Band | Band, in dem bspw. ein Artikel erschienen ist; bibliographisches Feld |

## Identifier

| Feld | Label | Beschreibung |
|------+-----------------+--------------|
| IdentifierArxiv | Arxiv-ID | <http://arxiv.org/help/arxiv_identifier> |
| IdentifierDoi | DOI | Digital Object Identifier, <http://de.wikipedia.org/wiki/Digital_Object_Identifier> |
| IdentifierHandle | Handle | Handle, Allg. Aufbau: http://hdl.handle.net/Prefix/Suffix |
| IdentifierIsbn | ISBN | ISBN-Nummer |
| IdentifierIssn | ISSN | ISSN-Nummer |
| IdentifierOld | alter Identifier | kann genutzt werden, um Datensätze zu referenzieren, die bereits eine ID in einem Vorgängersystem hatten |
| IdentifierOpac | OPAC-ID | |
| IdentifierOpus3 |  | Feld für die alte OPUS3-ID |
| IdentifierPubmed | | |
| IdentifierSerial | SICI | [Serial Item and Contribution Identifier](http://en.wikipedia.org/wiki/Serial_Item_and_Contribution_Identifier) |
| IdentifierUrl | URL | kann z.B. benutzt werden, um eine externe URL zum Dokument zu erfassen |
| IdentifierUrn | URN | eindeutiger Identifikator des Dokuments, der bei der Freischaltung eines Dokuments automatisch vergeben wird, siehe URN SETTINGS 54 (Wichtiger Hinweis zu diesem Feld siehe unten.) |
| IdentifierUuid | UUID | Universal Identifier |

<p class="note" markdown="1">
Seit OPUS 4.4 wird beim Veröffentlichen geprüft, ob die vom Anwender im Feld
IdentifierUrn eingegebene URN kollisionsfrei ist. Besteht eine Kollision, so erfolgt eine
Fehlermeldung mit der Aufforderung die URN zu ändern. Hier ist jedoch folgendes zu beachten:

* Die Überprüfung der Kollisionsfreiheit erfolgt immer nur bezüglich der in der OPUS-Datenbank (in der Tabelle document_identifiers) gespeicherten URNs.
* Es können daher keine globalen Aussagen bezüglich der Kollisionsfreiheit getroffen werden.
* Insbesondere kann der Benutzer auch URNs eingeben, die aus einem anderen Namensraum kommen.

Wir empfehlen, das Feld IdentifierUrn möglichst gar nicht mehr im Publikationsformular zu
verwenden. Wenn es dennoch verwendet wird, dann muss beim Freischalten des Dokuments darauf
geachtet werden, dass die URN aus dem eigenen Namensraum kommt.
</p>

## Personen

| Feld | Label | Bescreibung |
|------+-------+-------------|
| PersonAdvisor | Betreuer | verantwortlicher Betreuer einer Abschluss- oder Studienarbeit |
| PersonAuthor | Autor(en) | Angaben zu(m) Autor(en) |
| PersonContributor | Beteiligte Person | Name der Person, die einen bedeutsamen intellektuellen Beitrag zum Dokument geleistet hat |
| PersonEditor | Herausgeber | der herausgeber des Werks (bibliographische Angabe) |
| PersonReferee | Gutachter | ein externer Gutachter, der über die Freischaltung eines Dokuments entschieden hat |
| PersonSubmitter | Kontaktdaten des Einstellers | Kontaktdaten des Einstellers, Feld für den internen Gebrauch |
| PersonTranslator | Übersetzer | der Übersetzer eines Werkes |
| PersonOther | Sonstige beteiligte Personen | Weitere Personen, die nicht den anderen Rollen entsprechen |

## Klassifikationen

| Feld | Label | Beschreibung |
|------+-------+--------------|
| SubjectBKL | BKL-Klassifikation | Browsingfeld zur Auswahl einer Klassifikation |
| SubjectCCS | CCS-Klassifikation | Browsingfeld Auswahl einer Klassifikation zur CCS- |
| SubjectDDC | DDC-Klassifikation | Browsingfeld Auswahl einer Klassifikation zur DDC- |
| SubjectJEL | JEL-Klassifikation | Browsingfeld Auswahl einer Klassifikation zur JEL- |
| SubjectMSC | MSC-Klassifikation | Browsingfeld zur Auswahl einer MSC-Klassifikation |
| SubjectPACS | PACS-Klassifikation | Browsingfeld zur Auswahl einer PACS-Klassifikation |
| SubjectSwd | SWD-Schlagwort | kontrolliertes Vokabular (SWD) |
| SubjectUncontrolled | Freies Schlagwort / Tag | frei wählbare Beschreibung (kein kontrolliertes Vokabular) |





