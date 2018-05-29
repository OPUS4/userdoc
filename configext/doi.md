---
title: DOI-Vergabe und DOI-Registrierung
---

# Einführung

Seit der Version 4.6.2 bietet OPUS4 eine Unterstützung für die automatische Vergabe / Generierung und Registrierung von Digital Object Identifiern (DOI). Eine DOI ist ein eindeutiger und persistenter Identifikator für beliebige Objekte, z.B. eine Publikation oder einen Forschungsdatensatz (Datei). Die Granularitätsebene, auf der DOIs vergeben werden, ist nicht vorgegeben. Die Implementierung in OPUS verknüpft DOIs allerdings auf der Ebene der OPUS-Dokumente, d.h. einzelne Dateien eines OPUS-Dokuments können keine separaten DOIs erhalten. DOIs können von akademischen Institutionen, wie Universitäten und Hochschulen, mit dem Fokus auf Forschungsdaten beim DataCite-Konsortium kostenfrei registriert werden. In Deutschland ist hierfür die Technische Informationsbibliothek (TIB) in Hannover als DataCite-Mitglied zuständig. Vor der Aktivierung der DOI-Registrierung in OPUS muss ein entsprechender Vertrag mit der TIB geschlossen werden. In diesem Zusammenhang teilt die TIB der beantragenden Institution ein sogenanntes **DOI-Präfix** mit, z.B. `10.5072`.

Eine DOI ist grundsätzlich nach folgendem Schema aufgebaut:
```
${prefix}/${localPrefix}-${suffix}
```
Der vordere Teil bis zum Schrägstrich entspricht dem zugeteilten **DOI-Präfix**. Der Teil nach dem Schrägstrich kann von der Institution frei vergeben werden. Werden innerhalb einer Institution mehrere Systeme verwendet, die DOIs vergeben und registrieren sollen, so bietet sich die Verwendung eines **lokalen DOI-Präfix** an, z.B. `opus4` für das OPUS4-Repositorium und `anothersystem` für ein anderes System der Institution, das ebenfalls DOIs vergibt und registriert. Dies stellt sicher, dass die innerhalb der Institution vergebenen DOIs eindeutig sind und es zu keinen Kollisionen zwischen DOIs, die von unterschiedlichen Systemen erzeugt werden, kommt. Das **DOI-Suffix** kann beliebig gesetzt werden. Auch hierbei muss sichergestellt werden, dass die erzeugten DOIs eindeutig sind. Im Kontext von OPUS4 wird als Suffix standardmäßig die ID des OPUS-Dokuments verwendet, also eine natürliche Zahl.

# Konfiguration

Vor OPUS 4.6.2 gab es keinen eingebauten DOI-Support, so dass die Funktionen zur **DOI-Vergabe** und **DOI-Registrierung** standardmäßig in der Konfiguration deaktiviert sind und vor der Verwendung zuerst aktiviert werden müssen.

Zum Aktivieren der DOI-Vergabe muss die Konfigurationseinstellung
```
doi.autoCreate
```
auf den Wert `1` oder `true` gesetzt werden. In diesem Fall generiert OPUS beim Freischalten eines Dokuments automatisch eine passende DOI, sofern das Dokument nicht bereits eine DOI besitzt, und speichert die generierte DOI als `Opus_Identifier` des OPUS-Dokuments in der OPUS-Datenbank ab.

Die Konfigurationseinstellung `doi.autoCreate` kann auf der Ebene der einzelnen Dokumente überschrieben werden. Dazu existiert im Metadatenformular des Dokuments innerhalb des Administrationsbereichs eine entsprechende Checkbox im Identifier-Bereich. Über das Setzen der Checkbox kann die Generierung einer DOI beim Freischalten des Dokuments erzwungen werden, auch wenn `doi.autoCreate` in der Konfiguration deaktiviert ist. Umgekehrt kann durch das Deaktivieren der Checkbox die Generierung einer DOI beim Freischalten des Dokuments verhindert werden, obwohl `doi.autoCreate` in der Konfiguration aktiviert wurde. Der Zustand der Checkbox wird intern in einem speziellen OPUS-Enrichment `opus.doi.autoCreate` gespeichert (Wertemenge `true` oder `false`).

Zum Aktivieren der DOI-Registrierung muss die Konfigurationseinstellung
```
doi.registerAtPublish
```
auf den Wert `1` oder `true` gesetzt werden. In diesem Fall registriert OPUS beim Freischalten eines Dokuments die mit dem Dokument verknüpfte lokale DOI beim DOI-Provider, der in der Konfigurationsdatei angegeben wurde.

Die beiden Konfigurationseinstellungen können unabhängig voneinander aktiviert bzw. deaktiviert werden. Es sind hierbei vier unterschiedliche Fälle zu betrachten:

| `doi.autoCreate` | `doi.registerAtPublish` | Verhalten des Systems  |
| ---------------- |-------------------------|------------------------|
| false            | false                   | *dieser Fall entspricht dem Verhalten vor der Einführung des DOI-Supports in OPUS4* <br/> es findet keine automatische Registrierung von lokalen DOIs statt; eine Generierung von DOIs beim Veröffentlichen erfolgt nur, wenn der Nutzer die Checkbox "DOI-Autogenerierung" explizit anwählt (und das Dokument noch keine DOI besitzt) |
| false            | true                    | es erfolgt eine automatische Registrierung von lokalen DOIs; eine Generierung von DOIs beim Veröffentlichen des Dokuments erfolgt nur, wenn der Nutzer die Checkbox "DOI-Autogenerierung" explizit anwählt (und das Dokument noch keine DOI besitzt) |
| true             | false                   | es findet keine automatische Registrierung von lokalen DOIs statt; es erfolgt eine automatische Generierung von DOIs beim Veröffentlichen des Dokuments, sofern der Nutzer die Checkbox "DOI-Autogenerierung" nicht explizit abgewählt hat (und das Dokument noch keine DOI besitzt) |
| true             | true                    | es erfolgt eine automatische Registrierung von lokalen DOIs; es erfolgt eine automatische Generierung von DOIs beim Veröffentlichen des Dokuments, sofern der Nutzer die Checkbox "DOI-Autogenerierung" nicht explizit abgewählt hat (und das Dokument noch keine DOI besitzt) |


