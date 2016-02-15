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
ausgelieferten Dokumenttypen definiert (s. Anhang 196). Dieser Standard wird weiterentwickelt und gestattet es den
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

URN steht für Uniform Resource Name und ist ein Identifikator für digitale Objekte. Der in OPUS4 generierte URN bezieht
sich auf die Expression "Frontdoor" (also die bibliographische Beschreibung des Dokuments) und nicht auf die (einzelnen)
Dateien. URNs können in OPUS4 automatisch vergeben werden ([URN Einstellungen](config/urn.html)). URNs bilden die
Grundlage für die
Ablieferung der Dokumente an die Deutsche Nationalbibliothek über die xepicur-Schnittstelle, die in OPUS4 standardmäßig
integriert ist. Für weitere Informationen zu URNs konsultieren Sie bitte
[Persistent Identifier][PERSISTENTID]
bzw. [nestor Handbuch][NESTOR].

### Zeichenkodierung

OPUS4 akzeptiert in den Formularfeldern nur Zeichen, die im XML-1.0-Standard erlaubt sind. Werden Sonderzeichen
(z.B. per Copy-Paste) in die Formularfelder eingetragen, die in XML-1.0 nicht erlaubt sind (in Hexadezimal lauten sie
`[\x00-\x08\x0B\x0C\x0E-\x1F]`), dann werden diese
Zeichen für die Frontdoor durch das Mojibake-Zeichen "TODO" ersetzt, das in UTF-8 für nicht darstellbare Zeichen
benutzt wird.

## Bibliographiefunktion

Unter der Bibliographiefunktion wird die Möglichkeit verstanden, alle Publikationen einer Institution innerhalb eines
bestimmten Zeitraums über OPUS nachzuweisen, unabhängig davon, ob es sich um elektronische Publikationen handelt und ob
ein Volltext vorliegt oder nicht. Prinzipiell gehören alle in OPUS eingestellten Dokumente zum Repositorium. Darüber
hinaus kann es Dokumente geben, die zusätzlich noch zur Bibliographie gehören. Dies wird dadurch gekennzeichnet, dass
beim Veröffentlichen eines Dokuments ein Häkchen bei 'Zur Bibliographie hinzufügen?' gesetzt wird.

Um Dokumente, die zur Bibliographie gehören, zu exportieren, führt man eine Suche nach allen Dokumenten durch (Klick
auf "Alle Dokumente" unter dem Suchschlitz). Danach schränkt man die Treffer mit Hilfe der Facette "Gehört zur
Bibliographie -> Ja" ein und exportiert diese (vgl. Kapitel "Export 15").

<p class="info">
Selbstverständlich kann man die Dokumente auch noch zusätzlich nach anderen Aspekten einschränken.
</p>

[GNUGPL]: http://www.gnu.org/copyleft/gpl.html
[DINI]: http://nbn-resolving.de/urn:nbn:de:kobv:11-100109998
[DNBMDKERN]: http://d-nb.info/1020730110/34
[XMETADISSPLUS]: http://d-nb.info/1020009535/34
[PERSISTENTID]: http://www.persistent-identifier.de/?link=3352
[NESTOR]: http://nestor.sub.uni-goettingen.de/handbuch/artikel/nestor_handbuch_artikel_336.pdf

