---
title: Allgemeine Exportformate
weight: 10
---

# Allgemeine Exportformate

Es gibt in OPUS die folgenden Möglichkeiten, Metadaten zu exportieren:

1. Export über Ergebnislisten von Suche und Browsen im BibTeX-, CSV-, RIS- und XML-Format
2. Export über die Frontdoor im BibTeX-, RIS- und XML-Format

<p class="note" markdown="1">
In der Standardauslieferung ist der Zugriff auf das Modul nur für Administratoren erlaubt. Soll der Zugriff weiteren 
Personen erlaubt sein, muss die ihnen zugewiesene Rolle das Recht erhalten, auf das Modul `export` zuzugreifen. Die
Einstellungen der [Zugriffskontrolle](../admin/security.html) können in der Administration vorgenommen werden.
</p>

Seit OPUS Version 4.4.4 gibt es die Möglichkeit, einen Button für den Export nach XML auf der Frontdoor und auf den
Ergebnisseiten von Suche und Browsen anzuzeigen. Dieser Button wird über Parameter in der `config.ini` aktiviert, wie in
[Export Settings](../export/exportsettings.html) beschrieben, und steht dann für den Administrator und für alle
Nutzerrollen mit dem Recht `export` zur Verfügung.

## Export über Ergebnislisten von Suche und Browsen

Für die Ergebnislisten von Suche und Browsen kann in der Oberfläche ausgewählt werden, wie viele Dokumente auf einer 
Seite angezeigt werden (10 = default, 20, 50, 100). Im Standard ist der Export für normale Nutzer auf 100 Dokumente und
für eingeloggte Nutzer auf 500 Dokumente begrenzt (dafür ist der Rows-Parameter in der URL anzupassen). Um diese 
Standardwerte zu ändern, können die folgenden Parameter von der `$BASEDIR/application/configs/application.ini` in die
`config.ini` übernommen und angepasst werden:

{% highlight ini %}
; PLUGINS
plugins.export.default.maxDocumentsGuest = 100
plugins.export.default.maxDocumentsUser = 500
{% endhighlight %}

Der angemeldete Administrator kann für eine unbegrenzte Anzahl von Dokumenten Metadaten exportieren. Dafür ist der 
Rows-Parameter in der URL anzupassen.

## Besonderheiten des CSV-Exports

### Auswahl des gewünschten CSV-Formats: "CSV" oder "CSV_FN"

Für den Export von Ergebnislisten im CSV-Format kann zwischen zwei Formatierungen gewählt werden. Standardmäßig aktiviert ist das Format "__csv__" (mit dem XSLT-Stylesheet $BASEDIR/modules/export/views/scripts/stylesheets/csv.xslt). Dieses liefert die Metadaten spaltenweise getrennt aus. Beim Import in z.B. Excel ist darauf zu achten, dass als "Dateiursprung" der Zeichensatz "Unicode (UTF-8)" ausgewählt wird. 

Alternativ kann das CSV-Format "__csv_fn__" (zugehöriges XSLT-Stylesheet: $BASEDIR/modules/export/views/scripts/stylesheets/csv_fn.xslt) eingestellt werden. Dieses liefert die wesentlichen Metadaten in einer Spalte aus, ähnlich einer Zitation. Dieses Format ist hilfreich, wenn der Export z.B. für einen Jahresforschungsbericht genutzt werden soll. 

Um das Format "csv_fn" einzustellen, muss in der `config.ini` die Zeile
```
; EXPORT SETTINGS
plugins.export.csv.stylesheet = 'csv'
```
geändert werden in 
```
; EXPORT SETTINGS
plugins.export.csv.stylesheet = 'csv_fn'
```

### Ergänzung des CSV-Exports um weitere Spalten
Beide CSV-Formate können um weitere Spalten mit Metadaten aus Enrichment-Feldern und Collections ergänzt werden. Dazu können die folgenden Parameter von der `$BASEDIR/application/configs/application.ini` in die `config.ini` übernommen und angepasst werden:
```
; ENRICHMENTS AND COLLECTIONS TO BE EXPORTED IN CSV
export.csv.enrichments = 
export.csv.enrichments_labels = 
export.csv.collections = 
export.csv.collections_labels =  
; Visibility in CSV: 1 = All users, 0 = Logged in users only
export.csv.enrichments_visible = 
export.csv.collections_visible = 
```
In die Zeile
```
export.csv.enrichments =
```
werden die internen Namen des/der gewünschten Enrichments (kommasepariert) eingetragen. 
Beipiel:
```
export.csv.enrichments = ConferenceName,ConferencePlace
```

In die Zeile
```
export.csv.enrichments_labels =
```
werden die gewünschten Spaltenüberschriften des/der gewünschten Enrichments (kommasepariert) eingetragen.
Beispiel:
``` 
export.csv.enrichments_labels = Name der Konferenz,Ort der Konferenz
```

In die Zeile
```
export.csv.enrichments_visible =
```
werden die die Werte "0" oder "1" (kommasepariert) eingetragen. "0" bedeutet, dass das Enrichment für alle User (guest) angezeigt wird. "1" bedeutet, dass das Enrichment nur für eingeloggte User sichtbar ist, die Zugriff auf den Administrationsbereich "Dokumente verwalten" haben. 
Beispiel:
``` 
export.csv.enrichments_visible = 0,1
```

Die Anpassung der Zeilen für die Sammlungszugehörigkeit 
```
export.csv.collections = 
export.csv.collections_labels =
export.csv.collections_visible =
```
erfolgt analog.

### Ausgabe von __öffentlichen__ und __internen__ Bemerkungen
Die Spalte "Öffentliche Bemerkungen" wird allen Usern (guest) angezeigt. Die Spalte "Interne Bemerkungen" wird nur eingeloggten Usern angezeigt, die Zugriff auf den Administrationsbereich "Dokumente verwalten" haben. Diese Einstellung ist nicht änderbar.

### Hervorhebung von hochschulangehörigen Autoren und Herausgebern
Hochschulangehörige Autoren und Herausgeber können im Format "csv_fn" durch ein Asterisk (*) kenntlich gemacht werden. Dazu muss in der Personenverwaltung das Feld `Interne ID` der jeweiligen Person einen (beliebigen) Eintrag enthalten.

## Export im XML-Format

Standardmäßig wird die Datei

    $BASEDIR/modules/export/views/scripts/stylesheets-custom/example.xslt

als Beispiel-Stylesheet mitgeliefert. Es gibt alle Metadaten eines Dokuments aus, außer:

* Bemerkungsfelder (notes), die im Zustand private sind,
* Personen mit einer anderen Rolle als der Autor
* Lizenzen, die nicht im Status aktiv sind (und von aktiven Lizenzen nur das Feld NameLong),
* Sammlungen, die als unsichtbar markiert sind (und von den sichtbaren nur das Feld Name und den RoleName),
* Dateien, für die nicht gilt: sichtbar in OAI (`visible_in_oai = TRUE`) und
  sichtbar auf der Frontdoor (`visible_in_frontdoor = TRUE`).

Vom Autor werden nur Vor- und Nachname und von ThesisPublisher und ThesisGrantor nur das Feld Name exportiert.

Die bisherige Export-Funktion über eine URL bleibt bestehen, wie nachfolgend beschrieben.

### Export durch GET-Parameter

Jede URL in Suche oder Browsing, aber auch die Frontdoor-URL, kann als Eingabe für den Export von Dokumenten dienen.

Folgende Parameter müssen der URL hinzugefügt werden und steuern so den Export:

|----------+--------------|
|Name      |Beschreibung  |
|----------|--------------|
|export    |legt das Ausgabeformat für den Export fest (aktuell wird nur der Wert xml unterstützt); wird im HTTP Response-Header ContentType mit dem Wert text/xml angezeigt|
|stylesheet|legt den Namen des serverseitig anzuwendenden XSLT-Stylesheets fest|
|----------+-------------------------------------------------------------------|

<p class="note">
Der Aufruf des Exports ohne den Parameter stylesheet ist nur noch dem Administrator zu Testzwecken erlaubt,
weil hier u.U. sensible und personenbezogene Daten ausgegeben werden können.
</p>

Als Beispiel hier die URL für den Export sämtlicher Treffer des Repositoriums:

    http://example.org/solrsearch/index/search/searchtype/all/export/xml/stylesheet/example

Der Aufruf dieser Export-URL führt zu einem Redirect auf:

    http://example.org/export/index/index/searchtype/all/export/xml/stylesheet/example

Die zuletzt genannte URL kann auch direkt genutzt werden, wenn der Redirect ausbleiben soll
(hier wurde lediglich `/solrsearch/index/search` durch `export/index/index` ausgetauscht und die URL-Parameter `start`,
`rows` und `export` in der URL entfernt.

<p class="note" markdown="1">
Es werden auch die in der URL vorhandenen Paginierungsparameter `start` und `rows` übernommen. Das bedeutet, dass der
Export nur die in der aktuellen Suchergebnisseite aufgeführten Treffer ausliefert. Sollen explizit alle Ergebnisse
einer Suche exportiert werden, so muss man die beiden Paginierungsparameter aus der URL entfernen oder ihre Werte
entsprechend hoch setzen.
</p>

In manchen URLs kann es vorkommen (vor allem in der Suche 'Neueste Dokumente'), dass sogenannte "get-Parameter"
vorhanden sind. Diese sind daran erkennbar, dass Sonderzeichen wie `ß` und `?` in der URL stehen. In diesem Fall
sollte darauf geachtet werden,

die Exportparameter entweder vor dem `?` einzufügen:

    http://example.org/solrsearch/index/search/export/xml/stylesheet/example?rows=10&searchtype=latest

oder die Exportparameter auch als "get-Parameter" anzuhängen:

    http://example.org/solrsearch/index/search?rows=10&searchtype=latest&export=xml&stylesheet=example
