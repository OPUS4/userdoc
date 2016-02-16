---
title: OpenAIRE
weight: 60
---

# OpenAIRE

Opus bietet nun die Möglichkeit, Dokumente über oai-dc nach OpenAire 3.0 zu exportieren. OpenAire ist ein
OpenAccess-Repository, welches aus EU-Mitteln geförderte Dokumente beinhaltet und zur Verfügung stellt.

Die Dokumente können über die OAI-Schnittstelle ausgeliefert werden, wenn sie der Sammlung OpenAIRE (und damit dem Set
openaire) zugeordnet werden. (Achtung: für OpenAire 2.0 muss das Set ec_fundedresources heißen.)

Die folgenden Felder sind Pflichtfelder, die für die erfolgreiche Validierung und Export gesetzt sein müssen:

* AccessLevel (wird automatisch generiert)
  <https://guidelines.openaire.eu/wiki/Literature_Guidelines:_Metadata_Field_Access_Level>
* Creator (in Opus: PersonAuthor)
  <https://guidelines.openaire.eu/wiki/Literature_Guidelines:_Metadata_Field_Creator>
* (Publikations-) Date (wird automatisch generiert aus den vorhandenen Datumsangaben)
  <https://guidelines.openaire.eu/wiki/Literature_Guidelines:_Metadata_Field_Date_of_Publication>
* Das Datumsfeld fragt folgende Felder ab. Das erste gesetzte Feld wird übernommen und ausgegeben:
  * Published Date
  * Completed Date
  * Published Year
  * Completed Year
* Server Date Published
* EmbargoEndDate (wenn AccessLevel == embargoedAccess; in OPUS: Embargo Date)
  <https://guidelines.openaire.eu/wiki/Literature_Guidelines:_Metadata_Field_Embargo_End_Date>
* Relation (EU-Projekt-Identifier, Enrichment-Feld der OPUS-Standardauslieferung)
  <https://guidelines.openaire.eu/wiki/Literature_Guidelines:_Metadata_Field_Project_Identifier>
  Syntax: ```info:eu-repo/grantAgreement/Funder/FundingProgram/ProjectID /[Jurisdiction]/[ProjectName]/[ProjectAcronym]```
* (Document) Type
  <https://guidelines.openaire.eu/wiki/Literature_Guidelines:_Metadata_Field_Publication_Type>
* Identifier (in OPUS: Frontdoor-Url, IdentifierUrn, URN-Resolver-Link, IdentifierIsbn, Volltext-Url)
  <https://guidelines.openaire.eu/wiki/Literature_Guidelines:_Metadata_Field_Resource_Identifier>
* Title (in OPUS: TitleMain)
  <https://guidelines.openaire.eu/wiki/Literature_Guidelines:_Metadata_Field_Title>

Weiterhin exportiert Opus noch die folgenden Felder:

* Contributor (in OPUS: PersonContributor)
* Description (in Opus: TitleAbstract)
* Format (Dateiformat, wird automatisch generiert)
* (Document) Language
* Subject (in OPUS: SubjectDDC = DDC-Klassifikation und SubjectSwd = GND-Schlagwort)
* Source (in OPUS: TitleParent)
* Publication Version (fest vorgegeben als publishedVersion)

Im Adminbereich steht ein OAI-Link zur Verfügung, der das Set openaire anzeigt.

Die Guidelines zu OpenAire 3.0 finden sich hier:
<https://guidelines.openaire.eu/wiki/Main_Page>

Die Kompatibilität eines Dokuments kann hier getestet werden:
<https://www.openaire.eu/validator/>
