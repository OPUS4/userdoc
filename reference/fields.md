---
title: Bedeutung der Felder
---

# Bedeutung der Felder

In den folgenden Tabellen sind die Felder aufgeführt, die für Dokumente in OPUS 4 verfügbar sind. Im Gegensatz zu
den Labeln können die Feldbezeichnungen nicht geändert werden. Die Felder sind in unterschiedliche Bereiche geteilt.

* [Allgemein](#allgemein)
* [Datumsangaben](#datumsangaben)
* [Identifier](#identifier)
* [Personen](#personen)
* [Klassifikationen und Schlagwörter](#klassifikationen-und-schlagwörter)
{: class="navlist" }

## Allgemein

| Feld | Label | Beschreibung |
|------+-----------------+--------------|
| ArticleNumber | Artikelnummer | E-Journals verwenden ergänzend oder anstelle von Heftnummern und/oder Seitenzahlen Artikelnummern zur eindeutigen Referenzierung der Artikel |   
| ContributingCorporation | Beteiligte Körperschaft | Name der Organisation, die einen bedeutsamen intellektuellen Beitrag zum Dokument geleistet hat |
| CreatingCorporation | Urhebende Körperschaft | Name der Organisation, die den intellektuellen Inhalt des Dokuments verantwortet |
| Edition | Auflage | Auflage der Veröffentlichung (Ausgabebezeichnung, z.B. "4. Aufl.") |
| Institute | Institut | zur Abbildung der Struktur einer Einrichtung, um die Dokumente den jeweiligen Einheiten zuordnen zu können (an Hochschulen bspw. Fakultäten, Institute, zentrale Einrichtungen oder Studiengänge) |
| Issue | Heft | Bezeichnung (meist Nummer) des Heftes, in dem ein Artikel erschienen ist |
| Language | Sprache der Veröffentlichung | Sprache, in der die elektronische Ressource vorliegt |
| Licence | Lizenz | die Bedingungen, zu denen eine Veröffentlichung nachgenutzt werden darf (urheberrechtliche Regelungen, CC-Lizenzen) |
| Note | Bemerkung | freies Feld für (öffentliche und private) Anmerkungen |
| PageFirst | Erste Seite | Nummer der ersten Textseite |
| PageLast | Letzte Seite | Nummer der letzten Textseite |
| PageNumber | Seitenzahl | Anzahl der Seiten des Dokuments |
| PublicationState | Version | Version der Veröffentlichung im Publikationsprozess (Entwurf, Akzeptiertes Manuskript, Originale Verlagspublikation etc.) |
| PublisherName | Verlag | Name des Verlags |
| PublisherPlace | Verlagsort | Ort des Verlags |
| Series | Schriftenreihen | Browsingfeld zur Auswahl der verfügbaren Schriftenreihen |
| ThesisGrantor | Titel verleihende Institution | der Inhalt dieses Feldes wird über die [Informationen für die DNB](../admin/institutes.html) im Administrationsbereich verwaltet |
| ThesisPublisher | Veröffentlichende Institution | der Inhalt dieses Feldes wird über die [Informationen für die DNB](../admin/institutes.html) im Administrationsbereich verwaltet |
| TitleAbstract | Abstract / Kurzfassung | eine Zusammenfassung der Arbeit |
| TitleAdditional | Übersetzter Titel | Feld für Titel in weiteren Sprachen neben dem Originaltitel |
| TitleMain | Haupttitel | Originaltitel des Dokuments oder des Objekts |
| TitleParent | Titel des übergordneten Werkes | z.B. Titel der Zeitschrift, des Sammelwerks etc. |
| TitleSub | Untertitel | Untertitel (Zusatz zum Sachtitel) des Dokuments oder des Objekts |
| Type | Dokumenttyp | OPUS-Dokumenttyp, vgl. Übersicht über die [Dokumenttypen](../documenttypes/index.html) |
| Volume | Band | i.d.R. Band(nummer)/Jahrgang der Zeitschrift oder Band(zählung) der Schriftenreihe, in der die vorliegende Publiaktion erschienen ist |

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
| IdentifierArxiv | ArXiv-ID | <https://info.arxiv.org/help/arxiv_identifier.html> |
| IdentifierCrisLink | CRIS-Link | Link auf das Forschungsinformationssystem (Current Research Information System, CRIS) |
| IdentifierDoi | DOI | Digital Object Identifier, <https://de.wikipedia.org/wiki/Digital_Object_Identifier> |
| IdentifierHandle | Handle | <https://de.wikipedia.org/wiki/Handle_System> |
| IdentifierIsbn | ISBN | Internationale Stanardbuchnummer (International Standard Book Number, ISBN) |
| IdentifierIsmn | ISMN | Internationale Standardmusiknummer (International Standard Music Number, ISMN) |
| IdentifierIssn | ISSN | Internationale Standardnummer für fortlaufende Sammelwerke (International Standard Serial Number, ISSN) |
| IdentifierOld | alter Identifier | kann genutzt werden, um Datensätze zu referenzieren, die bereits eine ID in einem Vorgängersystem hatten |
| IdentifierOpac | OPAC-ID | Identnummer im lokalen Bibliothekskatalog |
| IdentifierOpus3 | OPUS 3 ID | Feld für die alte OPUS3-ID |
| IdentifierPubmed | Pubmed-ID | ID in der biomedizinischen Datenbank [PubMed](https://de.wikipedia.org/wiki/PubMed) der National Library of Medicine (USA) |
| IdentifierSerial | Sequenznummer | |
| IdentifierSplashUrl | SplashURL |  |
| IdentifierUnionCat | Verbundkatalog-ID | Identnummer im Verbundkatalog, z.B. PPN im K10plus |
| IdentifierUrl | URL | kann z.B. benutzt werden, um eine externe URL zum Dokument zu erfassen |
| IdentifierUrn | URN | eindeutiger Identifikator des Dokuments, der bei der Freischaltung eines Dokuments automatisch vergeben wird, siehe [Konfiguration der URN-Vergabe](../config/urn.html) (wichtiger Hinweis zu diesem Feld [siehe unten](#identifierurn)) |
| IdentifierUuid | UUID | [Universally Unique Identifier](https://de.wikipedia.org/wiki/Universally_Unique_Identifier) (UUID) |

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

| Feld | Label | Beschreibung |
|------+-------+-------------|
| PersonAdvisor | Betreuer\*in | verantwortliche/r Betreuer\*in einer Abschluss- oder Studienarbeit |
| PersonAuthor | Autor\*innen | Autor\*in(nen) der Publikation |
| PersonContributor | Beteiligte Person | Name der Person, die einen bedeutsamen intellektuellen Beitrag zum Dokument geleistet hat |
| PersonEditor | Herausgeber*innen | Herausgeber\*in(nen) des Werks |
| PersonReferee | Gutachter\*innen | Gutachter\*in(nen)/Prüfer\*in(nen) einer Abschluss- oder Studienarbeit |
| PersonSubmitter | Kontaktdaten der Einstellerin/des Einstellers | Kontaktdaten der Einstellerin/des Einstellers, Feld für den internen Gebrauch |
| PersonTranslator | Übersetzer\*in | Übersetzer\*in(nen) eines Werkes |
| PersonOther | Weitere Person | sonstige beteiligte Personen, die nicht den anderen Rollen entsprechen |

### Unterfelder zu Personen
* Nachname
* Vorname
* Akademischer Grad
* E-Mail
* Geburtsort
* Geburtsdatum
* GND-ID
* ORCID iD
* Interne ID

<p class="note" markdown="1">
In manchen Kulturkreisen kann die Namensbezeichnung der Person nur aus einem Namen bestehen.
Auch bei Künstlernamen und Persönlichkeiten aus anderen Epochen (z.B. bei Digitalisaten) kann es vorkommen, dass der Name nur aus einem s.g. "Givenname" besteht.
Wenn kein Vorname zur Namensbezeichnung zugehörig ist, dann muss der Eintrag ins Feld "Nachname" erfolgen. 
</p>

## Klassifikationen und Schlagwörter

| Feld | Label | Beschreibung |
|------+-------+--------------|
| SubjectBKL | BKL-Klassifikation | Browsingfeld zur Auswahl von Notationen der [Basisklassifikation](https://de.wikipedia.org/wiki/Basisklassifikation) (BKL bzw. BK) |
| SubjectCCS | CCS-Klassifikation | Browsingfeld zur Auswahl von Notationen des [ACM Computing Classification System](https://de.wikipedia.org/wiki/ACM_Computing_Classification_System) (CCS) |
| SubjectDDC | DDC-Klassifikation | Browsingfeld zur Auswahl von Notationen der [Dewey-Dezimalklassifikation](https://de.wikipedia.org/wiki/Dewey-Dezimalklassifikation) (Dewey Decimal Classification, DDC) |
| SubjectJEL | JEL-Klassifikation | Browsingfeld zur Auswahl von Notationen der [JEL-Klassifizierung](https://de.wikipedia.org/wiki/JEL-Klassifizierung)(wirtschaftswissenschaftliche Klassifikation des _Journal of Economic Literature_) |
| SubjectMSC | MSC-Klassifikation | Browsingfeld zur Auswahl von Notationen der [Mathematics Subject Classification](https://de.wikipedia.org/wiki/Mathematics_Subject_Classification) (MSC) |
| SubjectPACS | PACS-Klassifikation | Browsingfeld zur Auswahl von Nationen des [Physics and Astronomy Classification Scheme](https://de.wikipedia.org/wiki/Physics_and_Astronomy_Classification_Scheme) (PACS) |
| SubjectPsyndex | Psyndex-Schlagwort | Schlagwort aus dem kontrollierten Vokabular von [Psyndex](https://psyndex.de/ueber/inhalte-aufbau/schlagwoerter-klassifikationen/) |
| SubjectSwd | GND-Schlagwort | Kontrolliertes Vokabular aus der Gemeinsamen Normdatei (GND) |
| SubjectUncontrolled | Freies Schlagwort / Tag | frei wählbare Beschreibung (kein kontrolliertes Vokabular) |
