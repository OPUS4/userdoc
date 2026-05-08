---
title: DOI-Import
---

DOI-Import [**Import by DOI**] entstammt nicht dem Gemeinsamen Vokabular, sondern
ist ein Pseudo-Dokumenttyp, um den Import von Metadaten aus Crossref über den
Veröffentlichungsvorgang zu ermöglichen. Im Zuge des Imports wird der Datensatz
anhand der Informationen von Crossref automatisiert dem eigentlichen Dokumenttyp
in OPUS zugeordnet.

<p class="info" markdown="1">
Besondere Vorsicht ist bei einer Anpassung der Felder geboten. Im Formular müssen alle
Felder vorhanden sein, die für das Mapping von Crossref nach OPUS 4 in
`$BASEDIR/public/layouts/opus4/js/doiAssist.js` bzw. `$BASEDIR/public/layouts/opus4/js/getDoi.js`
definiert sind. Insbesondere das Entfernen von Standardfeldern kann dazu führen, dass
der DOI-Import nicht mehr (korrekt) funktioniert.
</p>

Standardfelder beim DOI-Import:

* ArticleNumber
* **CompletedYear**
* Edition
* **IdentifierDoi**
* IdentifierIsbn
* IdentifierIssn
* IdentifierUrl
* Issue
* **Language**
* opus_crossrefDocumentType
* opus_crossrefLicence
* opus_doi_flag
* opus_doi_json
* opus_doiImportPopulated
* opus_import_origin
* OpusConferenceName
* OpusConferenceNumber
* OpusConferencePlace
* OpusConferenceYear
* PageFirst
* PageLast
* PageNumber
* PersonAuthor *(Subfields: AcademicTitle, FirstName, IdentifierOrcid)*
* PersonEditor *(Subfields: AcademicTitle, FirstName, IdentifierOrcid)*
* **PersonSubmitter** *(Subfields: AcademicTitle, **Email**, FirstName)*
* PersonTranslator *(Subfields: AcademicTitle, FirstName)*
* PublisherName
* PublisherPlace
* SubjectUncontrolled
* ThesisDateAccepted
* ThesisYearAccepted
* TitleAbstract
* TitleAdditional
* **TitleMain**
* TitleParent
* TitleSub
* Volume
