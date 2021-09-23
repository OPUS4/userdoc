---
title: Bedeutung der Felder
---

# Bedeutung der Felder

In den folgenden Tabellen sind alle Felder aufgeführt, die für Dokumente in OPUS 4 verfügbar sind. Im Gegensatz zu
den Labeln können die Feldbezeichnungen nicht geändert werden. Die Felder sind in unterschiedliche Bereiche geteilt.

* [Allgemein](#allgemein)
* [Datumsangaben](#datumsangaben)
* [Identifier](#identifier)
* [Personen](#personen)
* [Klassifikationen](#klassifikationen)
{: class="navlist" }

## Allgemein

| Feld | Label | Beschreibung |
|------+-----------------+--------------|
| ContributingCorporation | Beteiligte Körperschaft | Name der Organisation, die einen bedeutsamen intellektuellen Beitrag zum Dokument geleistet hat |
| CreatingCorporation | Urhebende Körperschaft | Name der Organisation, die den intellektuellen Inhalt des Dokuments verantwortet (bibliographische Angabe) |
| Edition | Auflage | z.B. Auflage eines Buches (bibliographisches Feld) |
| Issue | Heft | Heft, in dem bspw. ein Artikel erschienen ist; bibliographisches Feld |
| Language | Sprache der Veröffentlichung | Sprache, in der die elektronische Ressource verfasst wurde |
| Licence | Lizenz | beschreibt die Rechte / den Zugriff auf das Dokument (mit / ohne Print on Demand, welche CC-Lizenz ) |
| Note | Bemerkung | freies Feld für (öffentliche und private) Anmerkungen |
| PageFirst | Erste Seite | Nummer der ersten Textseite |
| PageLast | Letzte Seite | Nummer der letzten Textseite |
| PageNumber | Seitenzahl |Anzahl der Seiten des Dokuments |
| PublisherName | Verlag | Name des Verlags;bibliographisches Feld |
| PublisherPlace | Verlagsort | Ort des Verlags; bibliographisches Feld |
| Series | Schriftenreihen | Browsingfeld zur Auswahl der verfügbaren Schriftenreihen |
| ThesisGrantor | Titel verleihende Institution | der Inhalt dieses Feldes wird über die Institute (Verbreitende Stelle) im Administrationsbereich verwaltet. |
| ThesisPublisher | Veröffentlichende Institution | der Inhalt dieses Feldes wird über die Institute (Verbreitende Stelle) im Administrationsbereich verwaltet. |
| TitleAbstract | Abstract / Kurzfassung | Eine Zusammenfassung der Arbeit
| TitleAdditional | Übersetzter Titel | dieses Feld kommt zum Einsatz, wenn neben dem Originaltitel noch ein übersetzter Titel gefordert ist |
| TitleMain | Haupttitel | Originaltitel des Dokuments oder des Objekts |
| TitleParent | Titel des übergordneten Werkes | z.B. Titel der Zeitschrift, des Sammelwerks etc. |
| TitleSub | Untertitel | Untertitel (Zusatz zum Sachtitel) des Dokuments oder des Objekts |
| Type | Dokumenttyp | |
| Volume | Band | Band, in dem bspw. ein Artikel erschienen ist; bibliographisches Feld |

## Datumsangaben

| Feld | Label | Beschreibung |
|------+-----------------+--------------|
| CompletedDate | Datum der Veröffentlichung (online) | Standarddatum in jedem Dokumenttyp, wird per default mit dem aktuellen Datum beim Einstellen des Dokuments belegt; Datum, ab wann wann das Dokument frühestens im Repository freigeschaltet werden darf |
| CompletedYear | Jahr der Fertigstellung | Datumsfeld für die Angabe zum Erstellungsjahr oder Erscheinungsjahr; ursprünglich aus OPUS3 als Jahresangabe zum Erscheinungsjahr |
| PublishedDate | Datum der Erstveröffentlichung | Datum, an dem die Publikation bereits veröffentlicht wurde (z.B. in einem Verlag) oder die Publikation als Erstveröffentlichung im Repository erscheint |
| PublishedYear | Jahr der Erstveröffentlichung | Jahr, in dem die Publikation bereits veröffentlicht wurde (z.B. in einem Verlag) oder die Publikation als Erstveröffentlichung im Repository erscheint |
| EmbargoDate| Embargo-Datum | Datum, an dem das Embargo der Publikation (Volltext) durch den Verlag endet und der Zugriff auf den Volltext in dem Repository frühestens möglich ist |
| ThesisDateAccepted | Datum der Abschlussprüfung | Datum, an dem die Abschlussarbeit im Sinne der Prüfungsordnung angenommen wurde (i.d.R. das Datum der mündlichen Prüfung) |
| ThesisYearAccepted | Jahr der Abschlussprüfung | Jahr, in dem die Abschlussarbeit im Sinne der Prüfungsordnung angenommen wurde (i.d.R. das Jahr der mündlichen Prüfung) |

Die Jahresangabe im Feld "Datum der Erstveröffentlichung" (PublishedDate) wird in der Standardumgebung von OPUS 4 für die Generierung der Facette "Erscheinungsjahr", 
für die "Jahresangabe" bei der erweiteren Suche sowie für die "Sortierreihenfolge nach Jahr" in der einfachen Suche herangezogen. Wenn dieses Datumsfeld nicht gefüllt 
ist, wird das Feld "Jahr der Erstveröffentlichung" (PublishedYear) verwendet. Alternativ dazu besteht die Möglichkeit, die Indexierung der Jahresfacette individuell 
zu konfigurieren und dafür z.B. das Datumsfeld "Jahr der Fertigstellung"  (CompletedDate) zu verwenden. Eines dieser Datumsfelder sollte demnach in allen Dokumenten 
gesetzt sein.

Für die Ablieferung von Abschlussarbeiten erwartet die DNB eine Angabe, an dem die Abschlussarbeit im Sinne der Prüfungsordnung angenommen wurde. Vorzugsweise wird hier 
das Datum im Feld "Datum der Abschlussprüfung" (ThesisDateAccepted) verwendet. Ist dieses nicht bekannt, wird auch das Jahr im Feld "Jahr der Abschlussprüfung" 
(ThesisYearAccepted) akzeptiert.

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
| [IdentifierUrn](#identifierurn) | URN | eindeutiger Identifikator des Dokuments, der bei der Freischaltung eines Dokuments automatisch vergeben wird, siehe URN SETTINGS 54 (Wichtiger Hinweis zu diesem Feld siehe unten.) |
| IdentifierUuid | UUID | Universal Identifier |

### IdentifierUrn

Seit OPUS 4.4 wird beim Veröffentlichen geprüft, ob die vom Anwender im Feld
IdentifierUrn eingegebene URN kollisionsfrei ist. Besteht eine Kollision, so erfolgt eine
Fehlermeldung mit der Aufforderung die URN zu ändern. Hier ist jedoch folgendes zu beachten:

* Die Überprüfung der Kollisionsfreiheit erfolgt immer nur bezüglich der in der OPUS-Datenbank (in der Tabelle
  `document_identifiers`) gespeicherten URNs.
* Es können daher keine globalen Aussagen bezüglich der Kollisionsfreiheit getroffen werden.
* Insbesondere kann der Benutzer auch URNs eingeben, die aus einem anderen Namensraum kommen.

Wir empfehlen, das Feld IdentifierUrn möglichst gar nicht mehr im Publikationsformular zu
verwenden. Wenn es dennoch verwendet wird, dann muss beim Freischalten des Dokuments darauf
geachtet werden, dass die URN aus dem eigenen Namensraum kommt.

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

### Unterfelder zu Personen
* Nachname
* Vorname
* Akademischer Grad
* E-Mail
* Geburtsort
* Geburtsdatum
* GNDID
* ORCID
* Interne ID

<p class="note" markdown="1">
In manchen Kulturkreisen kann die Namensbezeichnung der Person nur aus einem Namen bestehen.
Auch bei Persönlichkeiten aus anderen Epochen (z.B. bei Digitalisaten)kann es vorkommen, dass der Name nur aus einem s.g. Givenname besteht.
Wenn kein Vorname zur Namensbezeichnung zugehörig ist, dann muss der Eintrag ins Feld "Nachname" erfolgen. 
</p>

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





