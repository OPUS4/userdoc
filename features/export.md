---
title: Export
weight: 50
---

# Export

Mit OPUS Version 4.4.4 gibt es nun die Möglichkeit, einen Button für den Export nach XML auf der Frontdoor und auf den
Ergebnisseiten der Suche anzuzeigen. Dieser Button wird über Parameter in der `config.ini` aktiviert, wie in
[Export Einstellungen](../config/export.html) beschrieben, und steht dann für den Administrator und für alle
Nutzerrollen mit dem Recht `export` zur Verfügung.

<p class="note" markdown="1">
In der Standardauslieferung ist der Zugriff auf das Modul nur für Admins erlaubt. Soll der Zugriff weiteren Personen
erlaubt sein, muss die ihnen zugewiesene Rolle das Recht erhalten, auf das Modul "export" zuzugreifen. Die
Einstellungen der [Zugriffskontrolle](../admin/security.html) können in der Administration vorgenommen werden.
</p>

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

## Export durch GET-Parameter

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
