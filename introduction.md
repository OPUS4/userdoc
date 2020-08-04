---
title: Was ist OPUS?
weight: 0
---

# Was ist OPUS?

OPUS ist eine Open Source-Software unter der [GNU General Public License][GNUGPL] für den Betrieb von institutionellen
Dokumentenservern bzw. Repositorien. OPUS steht für Online Publikationsverbund Universität Stuttgart und wurde dort
Ende der 90er Jahre vom Rechenzentrum der Universitätsbibliothek entwickelt. Seitdem wird OPUS mit nationalen Partnern
kooperativ weiterentwickelt.

Als frei verfügbare Software basiert OPUS auf PHP und MySQL und kann somit auch mit anderen frei verfügbaren Komponenten
kombiniert werden. Damit ermöglicht OPUS 4 es, elektronischen Dokumente zu archivieren, sie für Benutzer verfügbar zu
machen, darauf zu suchen, zu browsen und den Veröffentlichungsprozess zu vereinfachen.

## Standards

### Dokumenttypen

Für die Erstellung der Dokumenttypen in OPUS4 wurde das "Gemeinsames Vokabular für Publikations- und Dokumenttypen"
[(DINI AG Elektronisches Publizieren, DNB, BSZ, DINI Schriften 12-de, Version 1.0, Juni 2010)][DINI] als Grundlage
genommen. Entsprechend diesem Standard sind die
ausgelieferten [Dokumenttypen][DOCTYPES] definiert. Dieser Standard wird weiterentwickelt und gestattet es den
Betreibern von Repositorien, eigene Dokumenttypen zu definieren, wenn sie bei der Auslieferung über eine
OAI-Schnittstelle auf die entsprechenden DINI-Dokumenttypen gemappt werden. Der Hintergrund hierfür ist das Ziel,
den Metadatenaustausch im Bereich der Dokument- und Publikationstypen auf institutionellen und fachlichen Repositorien
besser zu standardisieren.

### Netzpublikationen

Des Weiteren wurden für die Auslieferung der OPUS-Dokumente über die OAI-Schnittstelle die
Metadaten-Kernset-Definitionen "Lieferung von Metadaten für Netzpublikationen an die Deutsche Nationalbibliothek"
[(Version 1.2, Stand 12. März 2012)][DNBMDKERN] und das
"XMetaDissPlus - Format des Metadatensatzes der Deutschen Nationalbibliothek für Online-Hochschulschriften inklusive
Angaben zum Autor (XMetaPers)" [(DNB, Version 2.2, Stand 21. Februar 2012)][XMETADISSPLUS]
berücksichtigt, um die Grundlage für eine standardisierte Ablieferung an die DNB zu schaffen.

### URN-Vergabe

URN steht für Uniform Resource Name und ist ein Uniform Resource Identifier (URI), der als dauerhafter Bezeichner für 
eine Online-Ressource dient.
Die digitale Publikation ist über die URN weltweit identifizierbar und damit zuverlässig zitierbar.

Der URN-Service ist ein kostenloser Dienst der Deutschen Nationalbibliothek. Die DNB verwaltet URNs aus dem Namensraum 
"urn:nbn:de" und bietet einen URN-Resolving-Dienst für Deutschland und die Schweiz an.
Für die Vergabe eines URN in OPUS 4 ist es erforderlich, dass für das Repository ein eigener URN-Namensraum zur 
Verfügung steht.
Die Beantragung des URN-Namensraum erfolgt durch den Repositorybetreiber bei der DNB. Damit verpflichtet er sich, 
die Regeln dafür anzuerkennen und einzuhalten.
Siehe [URN-Policy][URNPOLICY] für die Vergabe von URNs im Namensraum urn:nbn:de (Version 1.0, Stand: 29. November 2012)

Ein in OPUS 4 generierter URN bezieht sich auf die Expression “Frontdoor” (also die bibliographische Beschreibung des 
Dokuments) und nicht auf die (einzelnen) Dateien.
URNs können in OPUS 4 automatisch vergeben werden ([URN Parameter](config/urn.html)). Sie bilden die Grundlage für die 
Ablieferung der Dokumente an die Deutsche Nationalbibliothek über die OAI-Schnittstelle.

<p class="info">
Das Löschen einer urn:nbn:de ist nicht erlaubt. Wenn Dokumente mit URN  von der Veröffentlichung zurückgezogen werden, 
muss die URN auf eine Ersatzseite mit entsprechenden Informationen verweisen und der URN - Service der Deutschen 
Nationalbibliothek kontaktiert werden, um gegebenenfalls Weiterleitungen einzurichten.
</p>

<p class="info">
Sobald sich ein Objekt, für das eine urn:nbn:de vergeben wurde, auch nur geringfügig ändert, muss es eine neue URN 
erhalten. 
</p>


Für weitere Informationen zu URNs konsultieren Sie bitte die Richtlinien zu [Persistent Identifier][PERSISTENTID].


### Zeichenkodierung

OPUS4 akzeptiert in den Formularfeldern nur Zeichen, die im XML-1.0-Standard erlaubt sind. Werden Sonderzeichen
(z.B. per Copy-Paste) in die Formularfelder eingetragen, die in XML-1.0 nicht erlaubt sind (in Hexadezimal lauten sie
`[\x00-\x08\x0B\x0C\x0E-\x1F]`), dann werden diese
Zeichen für die Frontdoor durch das Mojibake-Zeichen (&#65533;) ersetzt, das in UTF-8 für nicht darstellbare Zeichen
benutzt wird.

## Bibliographiefunktion

Unter der Bibliographiefunktion wird die Möglichkeit verstanden, alle Publikationen einer Institution innerhalb eines
bestimmten Zeitraums über OPUS nachzuweisen, unabhängig davon, ob es sich um elektronische Publikationen handelt und ob
ein Volltext vorliegt oder nicht. Prinzipiell gehören alle in OPUS eingestellten Dokumente zum Repositorium. Darüber
hinaus kann es Dokumente geben, die zusätzlich noch zur Bibliographie gehören. Dies wird dadurch gekennzeichnet, dass
beim Veröffentlichen eines Dokuments ein Häkchen bei 'Zur Bibliographie hinzufügen?' gesetzt wird.

Um Dokumente, die zur Bibliographie gehören, zu exportieren, führt man eine Suche nach allen Dokumenten durch (Klick
auf "Alle Dokumente" unter dem Suchschlitz). Danach schränkt man die Treffer mit Hilfe der Facette "Gehört zur
Bibliographie -> Ja" ein und [exportiert][EXPORT] diese.

<p class="info">
Selbstverständlich kann man die Dokumente auch noch zusätzlich nach anderen Aspekten einschränken.
</p>

[GNUGPL]: http://www.gnu.org/copyleft/gpl.html
[DINI]: http://nbn-resolving.de/urn:nbn:de:kobv:11-100109998
[DNBMDKERN]: http://d-nb.info/1020730110/34
[XMETADISSPLUS]: http://d-nb.info/1020009535/34
[PERSISTENTID]: http://www.persistent-identifier.de/?link=3352
[NESTOR]: http://nestor.sub.uni-goettingen.de/handbuch/artikel/nestor_handbuch_artikel_336.pdf
[DOCTYPES]: documenttypes/index.html
[EXPORT]: features/export.html
[URNPOLICY]: http://nbn-resolving.de/urn:nbn:de:101-2012121200