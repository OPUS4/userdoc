---
title: DOI-Generierung und DOI-Registrierung
---

# Einführung

Seit der Version 4.6.2 bietet OPUS4 eine Unterstützung für die automatische Generierung und Registrierung von Digital Object Identifiern (DOI). Eine DOI ist ein eindeutiger und persistenter Identifikator für beliebige Objekte, z.B. eine Publikation oder ein Forschungsdatensatz (Datei). Die Granularitätsebene, auf der DOIs vergeben werden, ist nicht vorgegeben. Die Implementierung in OPUS verknüpft DOIs allerdings auf der Ebene der OPUS-Dokumente, d.h. einzelne Dateien eines OPUS-Dokuments können keine separaten DOIs erhalten. DOIs können von akademischen Institutionen, wie Universitäten und Hochschulen, mit dem Fokus auf Forschungsdaten beim DataCite-Konsortium kostenfrei registriert werden. In Deutschland ist hierfür die Technische Informationsbibliothek (TIB) in Hannover als DataCite-Konsortialmitglied zuständig. Vor der Aktivierung der DOI-Registrierung in OPUS muss ein entsprechender Vertrag mit der TIB geschlossen werden. In diesem Zusammenhang teilt die TIB der beantragenden Institution ein sogenanntes **DOI-Präfix** zu, beispielsweise `10.5072`.

Eine DOI ist grundsätzlich nach folgendem Schema aufgebaut:
```
${prefix}/${localPrefix}-${suffix}
```

Der vordere Teil bis zum Schrägstrich entspricht dem von der TIB zugeteilten **DOI-Präfix**. Der Teil nach dem Schrägstrich kann von der Institution frei vergeben werden. Sind innerhalb einer Institution mehrere Anwendungen im Einsatz, die DOIs vergeben und registrieren sollen, so bietet sich die Verwendung eines **lokalen DOI-Präfix** an, z.B. `opus4` für das OPUS4-Repositorium und `anothersystem` für ein anderes System der Institution, das ebenfalls DOIs vergibt und registriert. Dies stellt sicher, dass die innerhalb der Institution vergebenen DOIs eindeutig sind und es zu keinen Kollisionen zwischen DOIs, die von unterschiedlichen Anwendungen erzeugt werden, kommt. Das **DOI-Suffix** kann beliebig gesetzt werden. Auch hierbei muss sichergestellt werden, dass die erzeugten DOIs (innerhalb der Anwenfung) eindeutig sind. Im Kontext von OPUS4 wird als Suffix standardmäßig die ID des zugeordneten OPUS-Dokuments verwendet, also eine natürliche Zahl.

# Konfiguration

Vor OPUS 4.6.2 gab es keinen eingebauten DOI-Support, so dass die Funktionen zur **DOI-Generierung** und **DOI-Registrierung** standardmäßig in der Konfiguration deaktiviert sind und vor der Verwendung zuerst aktiviert werden müssen.

Zum Aktivieren der DOI-Generierung muss die Konfigurationseinstellung
```
doi.autoCreate
```
auf den Wert `1` oder `true` gesetzt werden. In diesem Fall generiert OPUS beim Freischalten eines Dokuments automatisch eine passende DOI, sofern das Dokument nicht bereits eine DOI besitzt, und speichert die generierte DOI als `Opus_Identifier` des OPUS-Dokuments in der Datenbank ab.

Die Konfigurationseinstellung `doi.autoCreate` kann für einzelne Dokumente überschrieben werden. Dazu existiert im Metadatenformular des Dokuments innerhalb des Administrationsbereichs eine entsprechende Checkbox im Abschnitt *Identifikatoren*. Durch das Setzen der Checkbox *DOI beim Veröffentlichen generieren* kann die automatische Generierung einer DOI beim Freischalten des Dokuments erzwungen werden, auch wenn `doi.autoCreate` in der globalen Konfiguration deaktiviert ist. Umgekehrt kann durch das Deaktivieren der Checkbox *DOI beim Veröffentlichen generieren* die automatische Generierung einer DOI beim Freischalten des Dokuments verhindert werden, obwohl `doi.autoCreate` in der globalen Konfiguration aktiviert wurde. Der Zustand der Checkbox *DOI beim Veröffentlichen generieren* wird intern in einem speziellen OPUS-Enrichment `opus.doi.autoCreate` gespeichert (Wertemenge `true` oder `false`). Dieses Enrichment wird im Abschnitt *Enrichments* im Metadatenformular nicht angezeigt.

Zum Aktivieren der DOI-Registrierung muss die Konfigurationseinstellung
```
doi.registerAtPublish
```
auf den Wert `1` oder `true` gesetzt werden. In diesem Fall registriert OPUS beim Freischalten eines Dokuments die mit dem Dokument zu diesem Zeitpunkt verknüpfte **lokale DOI** beim DOI-Provider, der in der Konfigurationsdatei angegeben wurde.

**Wichtiger Hinweis:** OPUS registriert nur lokale DOIs beim DOI-Provider. Wird einem OPUS-Dokument eine "fremde" DOI zugewiesen (entweder bei der Eingabe im Publikationsformular oder im Metadatenformular innerhalb der Administration) so erfolgt für diese DOI **keine** Registrierung beim DOI-Provider. Die Bestimmung der Lokalität einer DOI wird durch die Funktion `isLocal`bereitgestellt, die jede DOI-Generator-Klasse in OPUS über das Interface `Opus_Doi_Generator_DoiGeneratorInterface` bereitstellen muss. Die Standardimplementierung der DOI-Generator-Klasse heißt `Opus_Doi_Generator_DefaultGenerator`. Diese Klasse betrachtet DOIs als lokal, wenn sie mit dem DOI-Präfix beginnen und danach mit Schrägstrich getrennt das (optional konfigurierbare) DOI-Präfix folgt.

Die beiden globalen Konfigurationseinstellungen `doi.autoCreate` und `doi.registerAtPublish` können unabhängig voneinander aktiviert bzw. deaktiviert werden. 

Es sind hierbei vier unterschiedliche Fälle zu betrachten:

| `doi.autoCreate` | `doi.registerAtPublish` | Verhalten des Systems  |
| ---------------- |-------------------------|------------------------|
| false            | false                   | *dieser Fall entspricht dem Verhalten vor der Einführung des DOI-Supports in OPUS4* <br/> es findet keine automatische Registrierung von lokalen DOIs statt; eine Generierung von DOIs beim Veröffentlichen von Dokumenten erfolgt nur, wenn der Nutzer die Checkbox "DOI-Autogenerierung" explizit anwählt (und das betreffende Dokument noch keine DOI besitzt) |
| false            | true                    | es erfolgt eine automatische Registrierung von lokalen DOIs; eine Generierung von DOIs beim Veröffentlichen von Dokumenten erfolgt nur, wenn der Nutzer die Checkbox "DOI-Autogenerierung" explizit anwählt (und das Dokument noch keine DOI besitzt) |
| true             | false                   | es findet keine automatische Registrierung von lokalen DOIs statt; es erfolgt eine automatische Generierung von DOIs beim Veröffentlichen von Dokumenten, sofern der Nutzer die Checkbox "DOI-Autogenerierung" nicht explizit abgewählt hat (und das Dokument noch keine DOI besitzt) |
| true             | true                    | es erfolgt eine automatische Registrierung von lokalen DOIs; es erfolgt eine automatische Generierung von DOIs beim Veröffentlichen von Dokumenten, sofern der Nutzer die Checkbox "DOI-Autogenerierung" nicht explizit abgewählt hat (und das Dokument noch keine DOI besitzt) |


