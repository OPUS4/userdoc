---
title: DOI-Generierung und DOI-Registrierung
---

# DOI-Generierung und Registrierung

Seit der Version 4.6.2 bietet OPUS4 eine Unterstützung für die automatische Generierung und Registrierung von Digital 
Object Identifiern (DOI). Eine DOI ist ein eindeutiger und persistenter Identifikator für beliebige Objekte, z.B. eine
Publikation oder ein Forschungsdatensatz (Datei). Die Granularitätsebene, auf der DOIs vergeben werden, ist nicht 
vorgegeben. Die Implementierung in OPUS verknüpft DOIs allerdings auf der Ebene der OPUS-Dokumente, d.h. einzelne 
Dateien eines OPUS-Dokuments können keine separaten DOIs erhalten. DOIs können von akademischen Institutionen,
wie Universitäten und Hochschulen, über eine direkte [DataCite Mitgliedschaft](https://datacite.org/become.html)
oder über ein DataCite-DOI-Konsortium registriert werden. In Deutschland gibt es zur Zeit (Stand März 2022)
fünf DataCite-DOI-Konsortien (alphabetische Reihenfolge):

* [DARA Konsortium](https://www.da-ra.de/get-a-doi#become-a-user)
* [DOI-Konsortium NRW](https://service-wiki.hbz-nrw.de/display/DOI/FAQ+zum+DOI-Konsortium)
* [SUB Göttingen Konsortium](https://www.eresearch.uni-goettingen.de/de/knowledge-base/howto/getting-an-identifier/)
* [TIB DOI Konsortium](https://projects.tib.eu/pid-service/tib-doi-konsortium/mitglied-werden/)
* [ZB MED DOI-Konsortium](https://www.publisso.de/wir-fuer-sie/doi-service/)

Eine aktuelle Auflistung und Beschreibung der deutschen DOI-Konsortien finden Sie hier:
[https://projects.tib.eu/pid-service/tib-doi-konsortium/faqs/](https://projects.tib.eu/pid-service/tib-doi-konsortium/faqs/).
Vor der Aktivierung der DOI-Registrierung in OPUS muss ein entsprechender Vertrag mit DataCite oder einem Konsortium geschlossen,
ein Repository Konto in Fabrica eingerichtet und ein Präfix zugewiesen werden.
Informationen zu Fabrica finden Sie im [DataCite Fabrica Handbuch](https://wiki.tib.eu/confluence/display/pid/DataCite+Fabrica+Handbuch+Startseite).

Nach dem Abschluss eines Vertrages teilt z.B die TIB der beantragenden Institution ein sogenanntes **DOI-Präfix** zu, 
beispielsweise `10.5072`, welches dann in OPUS hinterlegt wird.

Eine DOI ist grundsätzlich nach folgendem Schema aufgebaut:
```
${prefix}/${localPrefix}-${suffix}
```

Der vordere Teil bis zum Schrägstrich entspricht dem von DataCite zugeteilten **DOI-Präfix**. Der Teil nach dem 
Schrägstrich kann von der Institution frei vergeben werden. Sind innerhalb einer Institution mehrere Anwendungen im 
Einsatz, die DOIs vergeben und registrieren sollen, so bietet sich die Verwendung eines **lokalen DOI-Präfix** an, 
z.B. `opus4` für das OPUS4-Repositorium und `anothersystem` für ein anderes System der Institution, das ebenfalls DOIs
vergibt und registriert. Dies stellt sicher, dass die innerhalb der Institution vergebenen DOIs eindeutig sind und es
zu keinen Kollisionen zwischen DOIs, die von unterschiedlichen Anwendungen erzeugt werden, kommt. Das **DOI-Suffix** 
kann beliebig gesetzt werden. Auch hierbei muss sichergestellt werden, dass die erzeugten DOIs (innerhalb der Anwenfung)
eindeutig sind. Im Kontext von OPUS4 wird als Suffix standardmäßig die ID des zugeordneten OPUS-Dokuments verwendet, 
also eine natürliche Zahl.

**Wichtiger Hinweis:** Die Generierung bzw. Registrierung von DOIs in OPUS4 ist nicht an das Vorhandensein von Dateien
gebunden. Es können somit auch DOIs für Dokumente generiert und registriert werden, für die lediglich Metadaten erfasst
wurden.

## Konfiguration

Vor OPUS 4.6.2 gab es keinen eingebauten DOI-Support, so dass die Funktionen zur **DOI-Generierung** und 
**DOI-Registrierung** standardmäßig in der Konfiguration deaktiviert sind und vor der Verwendung zuerst aktiviert 
werden müssen.

Die Konfiguration erfolgt in der `$BASEDIR/application/configs/config.ini`.

Zum Aktivieren der DOI-Generierung muss die Konfigurationseinstellung
```
doi.autoCreate
```
auf den Wert `1` oder `true` gesetzt werden. In diesem Fall generiert OPUS beim Freischalten eines Dokuments 
automatisch eine passende DOI, sofern das Dokument nicht bereits eine DOI besitzt, und speichert die generierte DOI 
als `Opus_Identifier` des OPUS-Dokuments in der Datenbank ab.

Die Konfigurationseinstellung `doi.autoCreate` kann für einzelne Dokumente überschrieben werden. Dazu existiert im 
Metadatenformular des Dokuments innerhalb des Administrationsbereichs eine entsprechende Checkbox im Abschnitt 
*Identifikatoren*. Durch das Setzen der Checkbox *DOI beim Veröffentlichen generieren* kann die automatische 
Generierung einer DOI beim Freischalten des Dokuments erzwungen werden, auch wenn `doi.autoCreate` in der globalen 
Konfiguration deaktiviert ist. Umgekehrt kann durch das Deaktivieren der Checkbox *DOI beim Veröffentlichen generieren*
die automatische Generierung einer DOI beim Freischalten des Dokuments verhindert werden, obwohl `doi.autoCreate` in der
globalen Konfiguration aktiviert wurde. Der Zustand der Checkbox *DOI beim Veröffentlichen generieren* wird intern in 
einem speziellen OPUS-Enrichment `opus.doi.autoCreate` gespeichert (Wertemenge `true` oder `false`). Dieses Enrichment 
wird im Abschnitt *Enrichments* im Metadatenformular nicht angezeigt.

Neben der erwähnten Checkbox steht im Metadatenformular im Bereich *DOI* ein Button mit der Beschriftung *Generieren* 
zur Verfügung. Dieser Button wird nur angezeigt, wenn noch keine DOI mit dem Dokument verknüpft ist. Durch das Drücken
des Buttons kann sofort eine DOI erzeugt werden (auch wenn das Dokument noch nicht freigeschaltet wurde). Diese DOI 
kann z.B. genutzt werden, um sie bereits in der Publikation im PDF-Volltext anzugeben.

Besitzt ein Dokument mehr als eine DOI (dieser Zustand war vor der Einführung des DOI-Supports in OPUS4 erlaubt), so
wird im Metadatenformular für die zweite bis *n*-te DOI jeweils ein Entfernen-Button angeboten. Das Ändern einer DOI 
(entweder durch Drücken des Generieren-Buttons oder durch das händische Eintragen einer DOI in das entsprechende 
Formularfeld) wird nur zugelassen, wenn das Dokument keine DOI besitzt.

Zum Aktivieren der DOI-Registrierung muss die Konfigurationseinstellung
```
doi.registerAtPublish
```
auf den Wert `1` oder `true` gesetzt werden. In diesem Fall registriert OPUS beim Freischalten eines Dokuments die mit
dem Dokument zu diesem Zeitpunkt verknüpfte **lokale DOI** beim DOI-Provider, der in der Konfigurationsdatei angegeben
wurde.

**Wichtiger Hinweis:** OPUS registriert nur lokale DOIs beim DOI-Provider. Wird einem OPUS-Dokument eine "fremde" DOI
zugewiesen (entweder bei der Eingabe im Publikationsformular oder im Metadatenformular innerhalb der Administration) so
erfolgt für diese DOI **keine** Registrierung beim DOI-Provider. Die Bestimmung der Lokalität einer DOI wird durch die 
Funktion `isLocal`bereitgestellt, die jede DOI-Generator-Klasse in OPUS über 
das Interface `Opus_Doi_Generator_DoiGeneratorInterface` bereitstellen muss. Die Standardimplementierung der 
DOI-Generator-Klasse heißt `Opus_Doi_Generator_DefaultGenerator`. Diese Klasse betrachtet DOIs als lokal, wenn sie mit 
dem DOI-Präfix beginnen und danach mit Schrägstrich getrennt das (optional konfigurierbare) DOI-Präfix folgt.

Die beiden globalen Konfigurationseinstellungen `doi.autoCreate` und `doi.registerAtPublish` können unabhängig 
voneinander aktiviert bzw. deaktiviert werden. 

Es sind hierbei vier unterschiedliche Fälle zu betrachten:

| `doi.autoCreate` | `doi.registerAtPublish` | Verhalten des Systems  |
| ---------------- |-------------------------|------------------------|
| false            | false                   | *dieser Fall entspricht dem Verhalten vor der Einführung des DOI-Supports in OPUS4* <br/> es findet keine automatische Registrierung von lokalen DOIs statt; eine Generierung von DOIs beim Veröffentlichen von Dokumenten erfolgt nur, wenn der Nutzer die Checkbox "DOI-Autogenerierung" explizit anwählt (und das betreffende Dokument noch keine DOI besitzt) |
| false            | true                    | es erfolgt eine automatische Registrierung von lokalen DOIs; eine Generierung von DOIs beim Veröffentlichen von Dokumenten erfolgt nur, wenn der Nutzer die Checkbox "DOI-Autogenerierung" explizit anwählt (und das Dokument noch keine DOI besitzt) |
| true             | false                   | es findet keine automatische Registrierung von lokalen DOIs statt; es erfolgt eine automatische Generierung von DOIs beim Veröffentlichen von Dokumenten, sofern der Nutzer die Checkbox "DOI-Autogenerierung" nicht explizit abgewählt hat (und das Dokument noch keine DOI besitzt) |
| true             | true                    | es erfolgt eine automatische Registrierung von lokalen DOIs; es erfolgt eine automatische Generierung von DOIs beim Veröffentlichen von Dokumenten, sofern der Nutzer die Checkbox "DOI-Autogenerierung" nicht explizit abgewählt hat (und das Dokument noch keine DOI besitzt) |

## Weitere Konfigurationseinstellungen

| Name des Konfigurationsschlüssels | Standardwert und (optional) erlaubte Wertemenge | Beschreibung |
| --------------------------------- |-------------------------------------------------|--------------|
| `doi.prefix`                      | *leer*                                          | DOI-Präfix für die Generierung von DOIs bzw. zur Prüfung der Lokalität von DOIs |
| `doi.localPrefix`                 | *leer*                                          | optional; lokales DOI-Präfix, das frei von der Institution gewählt werden kann |
| `doi.suffixFormat`                | *leer*                                          | optional; kann von der DOI-Generierungsklasse ausgewertet werden, um das Format des DOI-Suffix vorzugeben (wird von der Standardimplementierung **nicht** ausgewertet) |
| `doi.generatorClass`              | Opus_Doi_Generator_DefaultGenerator             | vollqualifizierter Name der DOI-Generierungsklasse |
| `doi.registration.datacite.username` | *leer*                                       | Nutzername für DataCite Metadata Store (MDS) |
| `doi.registration.datacite.password` | *leer*                                       | Passwort für DataCite Metadata Store (MDS) |
| `doi.registration.datacite.serviceUrl` | https://mds.datacite.org                   | Service-URL für DataCite Metadata Store (MDS) |
| `doi.registration.datacite.quota` | *leer*                                          | Quota für Zugriff auf DataCite Registrierungsserver (wird vorerst nicht ausgewertet) |


## Benachrichtigungen via E-Mail

Im Rahmen der Registrierung von DOIs bzw. der Prüfung des Registrierungsstatus von DOIs können vom OPUS-System 
E-Mail-Benachrichtigungen versendet werden. E-Mail-Benachrichtigungen werden grundsätzlich nur bei *Bulk*-Operationen 
(im `ReportController` des Moduls `admin`) sowie bei Operationen, die scriptgesteuert, z.B. über *Cronjobs*, gestartet 
wurden, ausgelöst. Die Benachrichtigung via E-Mail muss in der globalen Konfiguration aktiviert werden. Außerdem muss 
mindestens eine Empfänger-Adresse in der globalen Konfiguration angegeben werden. Der Versand an mehrere 
E-Mail-Empfänger wird unterstützt.

Folgende Konfigurationsparameter bestimmen das Verhalten der E-Mail-Benachrichtigungsfunktion:

| Name des Konfigurationsschlüssels | Standardwert und (optional) erlaubte Wertemenge | Beschreibung |
| --------------------------------- |-------------------------------------------------|--------------|
| `doi.notificationEmailEnabled` | false (true/1 oder false/0)                        | aktiviert bzw. deaktiviert das Verschicken von Benachrichtigungen für (fehlgeschlagene) DOI-Registrierungen |
| `doi.notificationEmail[]` | *leer*                                                  | E-Mail-Adresse(n) für Notifikationsnachrichten für registrierte DOIs (Array); pro E-Mailadresse eine Konfigurationszeile angeben! |


## Verwendung einer eigenen XSLT-Datei für DataCite

Für die Generierung des DataCite-XML mit den erforderlichen Pflichtfeldern zur Registrierung einer DOI, greift OPUS auf eine Standard-XSLT-Datei zurück.
 `$BASEDIR/vendor/opus4-repo/framework/library/Opus/Doi/datacite.xslt`

Sollen darüberhinaus weitere Felder oder angepasste Paramter übergeben werden, kann auf Grundlage der Standard-XSLT-Datei ein eigenes Stylesheet verwendet werden. 
Die angepasste XSLT-Datei sollte an einem Ort abgelegt werden, wo die Datei bei einem Update nicht überschrieben wird.
Der Pfad für die Verwendung einer eigenen XSLT-Datei muss in der `config.ini` mit dem Konfigurationsschlüssel `datacite.stylesheetPath` deklariert werden.

```
datacite.stylesheetPath = APPLICATION_PATH "/application/configs/doi/datacite.xslt"
```

## Automatisierung von Prozessen im Zusammenhang mit der DOI-Registrierung

### Registrierung von lokalen DOIs

Das Script `scripts/cron/cron-register-local-dois.php` sucht in der Datenbank nach OPUS-Dokumenten im `serverState` 
**published**, die lokale DOIs besitzen, die noch nicht bei DataCite registiert wurden. Nicht registrierte 
Identifikatoren vom Typ `doi` sind am Statuswert `null` in der Tabelle `document_identifiers` erkennbar. Für die 
ermittelten DOIs versucht das Script die Registrierung bei DataCite.

Das Script wird, wie unter [Job Ausführung](../config/jobs.html) beschrieben, ausgeführt.
 
### Prüfung des Registrierungsstatus von lokalen DOIs

Das Script `scripts/cron/cron-verify-local-dois.php` sucht in der Datenbank nach OPUS-Dokumenten, die lokale DOIs im 
Status `registered` besitzen und verifiziert diese DOIs bei DataCite. Die Verifikation ist erforderlich, weil nach der 
Registrierung einer DOI bei DataCite bis zu 24-72 Stunden vergehen können, bis die DOI tatsächlich auflösbar ist. Eine 
DOI im Zustand `registered` wird erst dann in OPUS auf den Status `verified` gesetzt, wenn sie über das Handle-System 
tatsächlich auflösbar ist.

Über die Variable `delayInHours` kann der Zeitraum angegeben werden, der nach der Registrierung einer lokalen DOI 
vergehen muss, bevor der Registrierungsstatus der DOI geprüft wird. Setze den Wert von `delayInHours` auf `null`, 
um alle registrierten DOIs unabhängig vom Registrierungszeitpunkt zu prüfen

Das Script wird, wie unter [Job Ausführung](../config/jobs.html) beschrieben, ausgeführt.

### Änderung der URL von Landing-Pages für lokale DOIs

Mit dem Script `scripts/snippets/change-doi-landing-page-url.php` kann die im Handle-System hinterlegte URL der 
Landing-Page einer lokalen DOI geändert werden. Das Script erwartet dazu zwei Parameter: die lokale DOI und die neue 
URL der Landing-Page. Das Script prüft **nicht**, ob die URL der Landing-Page korrekt ist bzw. tatsächlich zum Dokument 
mit der angegebenen DOI gehört.

Das Script wird direkt gestartet.

## Bemerkungen zum Update auf OPUS 4.6.2

Im Rahmen des Updates wird das Script `scripts/update/006-Set-status-of-all-existing-DOIs.php` ausgeführt, das den 
Registrierungsstatus von allen (sowohl lokalen als auch fremden) DOIs auf den Wert `registered` setzt. Es werden 
hierbei allerdings nur OPUS-Dokumente betrachtet, die den `serverState` **published** besitzen.

Außerdem stellt das Script fest, wenn es OPUS-Dokumente in der Datenbank gibt, die mehr als eine zugeordnete DOI 
besitzen. In den OPUS-Versionen vor 4.6.2 wurde dieser Umstand noch unterstützt. Ab der Version 4.6.2 kann ein 
OPUS-Dokument nur höchstens eine zugeordnete DOI besitzen. Werden OPUS-Dokumente detektiert, die mehr als eine DOI 
besitzen, so erscheint eine entsprechende Ausgabe:

```
document $SOME_ID has more than one DOI but only one DOI is expected: consider a cleanup
```

## DOI-Übersichtsseite

Auf der Seite https://my-opus-instance.tld/opus4/admin/report/doi/ kann der Registrierungsstatus für alle **lokalen** 
DOIs eingesehen werden. Für jede DOI kann in Abhängigkeit ihres Registrierungsstatus die Registrierung bzw. Prüfung 
einzeln ausgelöst werden. Lokale DOIs von Dokumenten, die noch nicht freigeschaltet sind, werden ebenfalls aufgelistet.

Des Weiteren bietet die Übersichtsseite den Start von *Bulk*-Operationen an: so können in einem Schritt alle noch nicht
registrierten DOIs für freigeschalteten Dokumenten registriert werden. Ebenso können alle bereits registrierten DOIs in
eine Schritt bezüglich ihres Registrierungsstatus geprüft werden.

## Bemerkungen zum Logging

Für das Logging von DOI-relevanten Aktionen wird eine separate Logdatei verwendet, die im OPUS4-Instanzverzeichnis 
unter `workspace/log/opus-doi.log` gespeichert wird.

In dieser Logdatei werden u.a. folgende Aktionen vermerkt:

* Fehler bei der Generierung von neuen lokalen DOIs
* Erfolg bzw. Fehler bei der Registrierung von lokalen DOIs
* Erfolg bzw. Fehler bei der Prüfung des Registrierungsstatus von DOIs
* Fehler bei der Änderung der URL der Landing-Page einer bereits registrierten DOI
* Fehler beim Deaktivieren von registrierten DOIs

Die Lognachrichten werden zusätzlich in der generischen Applikationslogdatei `opus.log` erfasst.

## DataCite-XML Export für einzelne Dokumente

Als angemeldeter Benutzer mit Administratorrechten kann für jedes Dokument (referenziert durch
seine Dokument-ID `$DOCID`) durch Aufruf der URL

https://example.org/export/index/datacite/docId/$DOCID

das für die DOI-Registrierung generierte DataCite-XML abgerufen werden. 

## Auflistung von Fehlern im DataCite-XML Export für einzelne Dokumente

Treten bei der XML-Generierung Fehler auf, z.B. weil erforderliche Pflichtfelder im
Dokument fehlen, so wird anstatt der XML-Ausgabe eine HTML-Statusseite ausgegeben,
auf der die einzelnen Fehler aufgelistet werden. Soll in diesem Fall dennoch das
DataCite-XML ausgegeben werden, so muss die Export-URL erweitert werden zu

https://example.org/export/index/datacite/docId/$DOCID/validate/no

In diesem Fall wird die Prüfung der Validität des generierten XML gegen das von
DataCite vorgegebene XML-Schema ausgesetzt.

Am Ende der HTML-Statusseite wird zudem ein Link angeboten, der den Export des
(invaliden) DataCite-XML ermöglicht. Befindet sich das betreffende OPUS-Dokument
nicht im Zustand `published` (weil es z.B. noch nicht freigeschaltet oder zurückgezogen
wurde), so erscheint ein Hinweis, dass die manuelle Registrierung der DOI auf Basis
des generierten XML-Exports nicht empfohlen wird.
