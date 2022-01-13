---
title: OPUS 4.7
weight: 49
---

# OPUS 4.7 Überblick

OPUS 4.7 bringt viele Verbesserungen und ist der umfangreichste Release seit dem OPUS 4.0 geworden.
Die Konfigurierbarkeit von Enrichments wurde weiter ausgebaut. Die Suche kann nun auch von 
Administratoren genutzt werden und es gibt eine völlig neue Übersetzungsverwaltung. Für weitere
Informationen folgen Sie bitte den folgenden Links. 

* [OPUS 4.7 Update](update/update47.html)
* [Release Notes](https://github.com/OPUS4/application/blob/4.7/RELEASE_NOTES.md)
* [Change Log](https://github.com/OPUS4/application/blob/4.7/CHANGES.md)
* [OPUS 4 auf GitHub](https://github.com/OPUS4/application)
{: class="navlist"}

## Erweiterte Enrichments

Für Enrichments können jetzt Typen festgelegt werden. Diese Typen können zum Teil konfiguriert 
werden. Damit kann die Eingabe dem Typ entsprechend vereinfacht werden. Für Enrichments vom 
Typ __Boolean__ wird in der Administration nun zum Beispiel eine Checkbox angezeigt.

<p class="info">
Wir sind uns bewusst, dass die Entwicklung der Enrichments noch nicht abgeschlossen ist. Unter 
anderem haben diese Änderungen noch keine Auswirkungen auf das Publish-Modul. Dieses Modul muss
noch überarbeitet werden. Sie können uns bei der weiteren Entwicklung helfen, in dem Sie Ihre 
Anwendungsfälle melden, die wir so noch nicht abdecken und über die wir vielleicht auch noch 
nicht nachgedacht haben.   
</p> 

## Suche für Administratoren

Es werden jetzt alle Dokument indiziert, nicht nur die freigeschalteten. Dadurch kann die Suche
jetzt auch von Administratoren verwendet werden, um zu bearbeitende Dokumente zu finden und mit
den Facetten zu filtern.

Im Rahmen dieser Entwicklung wurde die Konfigurierbarkeit von Facetten erweitert. Damit ist es
nun möglich, die Anzeige von Facetten zu beschränken. Die Facette für den Dokumentstatus 
(`server_state`) wird zum Beispiel nur für Administratoren angezeigt.  

* [Facetten konfigurieren](search/facets.html)
{: class="navlist" }

### Enrichments als Facetten

Enrichments werden nun automatisch indiziert. Sie können als Facetten für die Suche konfiguriert 
werden. 

* [Enrichments als Facetten](search/enrichment.html)
{: class="navlist" }
 
### Konfigurierbare Jahr-Facette

Für die Anpassung der Jahr-Facette ist keine Veränderung der XSLT-Datei für die Indizierung mehr 
notwendig. Es kann konfiguriert werden, welche Datums- bzw. Jahr-Felder in die Indizierung für die
Jahr-Facette einfließen sollen und in welcher Reihenfolge.

* [Anpassung der Jahr-Facette](search/yearfacet.html)
{: class="navlist" }  

## Übersetzungsverwaltung

Es gibt eine völlig neue Übersetzungsverwaltung im Setup-Bereich der Administration. Damit
lassen sich die Übersetzungen in OPUS 4 nun leichter editieren. Die Anpassungen können auch
exportiert bzw. importiert werden, z.B. um Anpassungen von einer Instanz auf eine andere zu
übertragen. So lassen sich auch Texte extern bearbeiten und dann importieren. 

* [Übersetzungsverwaltung](translatiop/index.html)
{: class="navlist" }
 
Es wurde angefangen, das Editieren von Übersetzungen direkt in die Formulare der Administration
zu integrieren. Die Übersetzungen von Sammlungen (CollectionRole) und Enrichments können direkt 
in den jeweiligen Edit-Formularen angepasst werden. Diese Integration wird in kommenden Versionen
weiter ausgebaut werden.

Die FAQ-Seite kann in ihrem Inhalt und ihrer Struktur nun auch komplett in der Administration 
editiert werden. 

Die Anpassungen werden nicht mehr in TMX-Dateien, sondern in der Datenbank gespeichert. Die bisher
verwendeten  `language_custom`-Verzeichnisse werden nicht länger benötigt. Die Standardtexte 
werden weiterhin in TMX-Dateien ausgeliefert.
 
## Weitere Veränderungen

OPUS 4.7 beinhaltet viele weitere große und kleine Veränderungen, sowie eine Reihe von 
Fehlerbehebungen.

### Neuer Zeichensatz für Datenbank

Der Zeichensatz in der MySQL Datenbank wurde auf __utf8mb4__ umgestellt, damit alle Zeichen 
abgespeichert werden können. Das soll verhindern, dass es zu Fehlermeldungen kommt, wenn 
ausversehen Steuerzeichen in den Eingabefeldern landen, z.B. wenn eine Zusammenfassung in ein
Formular hineinkopiert wurde. 

### MARC21-XML Export

Der Export unterstützt nun MARC21-XML. Ob dieses Format für alle Nutzer verfügbar ist oder nur
für Administratoren lässt sich konfigurieren. 
