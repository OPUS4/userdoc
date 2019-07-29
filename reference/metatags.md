---
title: Mapping der HTML-Meta-Tags in der Frontdoor
weight: 10
---

# Mapping der HTML-Meta-Tags in der Frontdoor

OPUS gibt die Metadaten zu einem Dokument in der Frontdoor auch in maschinenlesbarer Form aus. Sie werden im HTML-Quellcode in Meta-Tags gemäß den beiden Standards [*Dublin Core*](http://www.dublincore.org/specifications/dublin-core/dcmi-terms/) sowie den *Highwire Press Tags* abgebildet. Letztere empfiehlt u.a. Google, um eine gute Indexierung des eigenen Repositoriums in Google Scholar zu erzielen. Die Generierung der Highwire Press Tags in OPUS basiert auf den [Inclusion Guidelines for Webmasters](https://scholar.google.de/intl/de/scholar/inclusion.html) für Google Scholar und berücksichtigt weitere Spezifikationen wie jene im Aufsatz "Invisible institutional repositories: addressing the low indexing ratios of IRs in Google"[^1].

Die 25 Standard-Dokumenttypen in OPUS4 lassen sich für das Mapping in 7 Dokumentkategorien - 6 definierte sowie eine Sammelkategorie für die übrigen Dokumenttypen - einteilen. Für jede Dokumentkategorie ist ein anderes Mapping definiert, um eine bestmögliche Indexierung in den aggregierenden Diensten zu erreichen. 

Die Zuordnung der Dokumenttypen erfolgt in der `application.ini` über die Konfigurationsschlüssel
~~~~
metatags.mapping.book[]
metatags.mapping.book_part[]
metatags.mapping.conference_paper[]
metatags.mapping.journal_paper[]
metatags.mapping.thesis[]
metatags.mapping.working_paper[]
~~~~
Alle Dokumenttypen, die keinem der 6 Konfigurationsschlüssel zugeordnet sind, werden als Sonstige behandelt und mit einem unspezifischen Standard-Set an Metadaten dargestellt.

Legt man neue Dokumenttypen an, sollte man die Zuordnung zu einer der Dokumentkategorien prüfen und in der `config.ini` zuweisen, um eine optimale Ausgabe der Daten und damit auch bessere Indexierung zu erreichen.

| | Metadatum | OPUS-Feld | Dublin Core | Highwire Press Tag | | | | | | | | Anmerkungen |
|:--|:--------|:----------|:------------|:-----------------|:-|:-|:-|:-|:-|:-|:-|:-------|
| Meta-Tag-Dokumentkategorie | | | | | book | bookpart | conference_paper | journal_paper | thesis | working_paper | *Sonstige* | |
| OPUS-Dokumenttypen | | | | | book (Buch) | bookPart (Teil eines Buchs/Kapitel) | conferenceObject (Konferenzveröffentlichung) | article (Wissenschaftl. Artikel)  contributionToPeriodical (Beitrag zu nichtwissenschaft. Zeitschrift)  periodicalPart (Ausgabe/Heft zu einer Zeitschrift)  preprint (Preprint) | bachelorthesis (Bachelorarbeit) diplom (Diplomarbeit) doctoralthesis (Dissertation) examen (Examensarbeit) habilitation (Habilitation) magister (Magisterarbeit) masterthesis (Masterarbeit) studythesis (Studienarbeit) | workingPaper (Arbeitspapier) | courseMaterial (Lehrmaterial) image (Bild) lecture (Vorlesung) movingImage (Bewegte Bilder), other (Sonstiges) periodical (Periodikum/Zeitschrift) review (Rezension) report (Bericht) sound (Ton) | 
|-----
| | Autor | PersonAuthor | DC.creator | citation_author | X | X | X | X | X | X | X | |
| | Erscheinungsdatum | Je nachdem, was vorhanden ist (case):    DatePublished    YearPublished  | DC.date | citation_date | X | X | X | X | X | X | X | |
| | Erscheinungsdatum | Je nachdem, was vorhanden ist (case):    DatePublished    YearPublished  | DC.issued | citation_publication_date | X | X | X | X | X | X | X | | 
| | Titel | TitleMain : TitleSub | DC.title | citation_title | X | X | X | X | X | X | X | |
| | Verlag | PublisherName | DC.publisher | citation_publisher | X | X | X | X | X | X | X | |
| | Titel der Zeitschrift | TitleParent | DC.relation.ispartof | citation_journal_title | | | | X | | | | |
| | Bandzählung | Volume | DC.citation.volume | citation_volume | | | X | X | | X | | |
| | Heftnummer | Issue | DC.citation.issue | citation_issue | | | X | X | | X | | |
| | Erste Seite | PageFirst | DC.citation.spage | citation_firstpage | | X | X | X | | | | |
| | Letzte Seite | PageLast | DC.citation.epage | citation_lastpage | | X | X | X | | | | |
| | DOI | IdentifierDoi | DC.identifier | citation_doi | X | X | X | X | X | X | X | |
| | ISSN | IdentifierIssn | DC.identifier | citation_issn | | | X | X | | X | X | |
| | ISBN | IdentifierIsbn | DC.identifier | citation_isbn | X | X | X | X | X | X | X | |
| 13 | Schlagwörter | | DC.subject | citation_keywords | X | X | X | X | X | X | X | |
| | | ThesisPublisher | DC.publisher | citation_dissertation_institution | | | | | X | | | |
| | Art der Hochschulschrift | *Dokumenttyp* | *n/a* | citation_dissertation_name | | | | | X | | | Konkretisierung der Abschlussarbeit und/oder des akademischen Grades (z.B. PhD, MS) |
| | | Je nachdem, was vorhanden ist (case):    CreatingCorporation    ContributingCorporation    Publisher | DC.publisher | citation_technical_report_institution | | | | | | X | | |
| | Sprache | Language | DC.language | citation_language | X | X | X | X | X | X | X | |
| | | TitleParent | DC.relation.ispartof | citation_conference_title | | | X | | | | | |
| | Titel des Buchs | TitleParent | DC.relation.ispartof | citation_inbook_title | X | X | | | | | | |
| | Frontdoor-URL | *frontdoorUrl* | DC.identifier | citation_abstract_html_url | X | X | X | X | X | X | X | | 
| | URL zur Volltextdatei | *fileUrl* | DC.identifier | citation_pdf_url | X | X | X | X | X | X | X | |
| | Abstract | TitleAbstract | DC.description | *n/a* | X | X | X | X | X | X | X | Kein Mapping in Higwire Press Tags, da kein entsprechendes Element vorhanden |
| | URN | IdentifierUrn | DC.identifier | *n/a* | X | X | X | X | X | X | X | Kein Mapping in Higwire Press Tags, da kein entsprechendes Element vorhanden |
| | Lizenzangabe | *LinkLicence* | DC.rights | *n/a* | X | X | X | X | X | X | X | Kein Mapping in Higwire Press Tags, da kein entsprechendes Element vorhanden |


----
[^1]: Arlitsch, Kenning and O’Brien, Patrick S.: Invisible institutional repositories : addressing the low indexing ratios of IRs in Google. In: Library Hi Tech, Vol. 30 (2012), No. 1, pp. 60-81. [https://doi.org/10.1108/07378831211213210](https://doi.org/10.1108/07378831211213210)
