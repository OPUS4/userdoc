---
title: Mapping der HTML-Meta-Tags in der Frontdoor
weight: 10
---

# Mapping der HTML-Meta-Tags in der Frontdoor

OPUS gibt die Metadaten zu einem Dokument in der Frontdoor auch in maschinenlesbarer Form aus. Sie werden im HTML-Quellcode in Meta-Tags gemäß den beiden Standards [*Dublin Core*](http://www.dublincore.org/specifications/dublin-core/dcmi-terms/) sowie den *Highwire Press Tags* abgebildet. Letztere empfiehlt u.a. Google, um eine gute Indexierung des eigenen Repositoriums in Google Scholar zu erzielen. Die Generierung der Highwire Press Tags in OPUS basiert auf den [Inclusion Guidelines for Webmasters](https://scholar.google.de/intl/de/scholar/inclusion.html) für Google Scholar und berücksichtigt weitere Spezifikationen wie jene im Aufsatz "Invisible institutional repositories: addressing the low indexing ratios of IRs in Google"[^1].

Die 25 Standard-Dokumenttypen in OPUS4 lassen sich für das Mapping in 7 Dokumentkategorien - 6 definierte sowie eine Sammelkategorie für die übrigen Dokumenttypen - einteilen. Für jede Dokumentkategorie ist ein anderes Mapping definiert, um eine bestmögliche Indexierung in den aggregierenden Diensten zu erreichen. 

Die Zuordnung der Dokumenttypen erfolgt in der `application.ini` über die Konfigurationsschlüssel
~~~~
metatags.mapping.book[]
metatags.mapping.book_part[]
metatags.mapping.conference_paper[]
metatags.mapping.journal_paper[]
metatags.mapping.thesis[]
metatags.mapping.working_paper[]
~~~~
Alle Dokumenttypen, die keinem der 6 Konfigurationsschlüssel zugeordnet sind, werden als Sonstige behandelt und mit einem unspezifischen Standard-Set an Metadaten dargestellt.

Legt man neue Dokumenttypen an, sollte man die Zuordnung zu einer der Dokumentkategorien prüfen und in der `config.ini` zuweisen, um eine optimale Ausgabe der Daten und damit auch bessere Indexierung zu erreichen.




----
[^1]: Arlitsch, Kenning and O’Brien, Patrick S.: Invisible institutional repositories : addressing the low indexing ratios of IRs in Google. In: Library Hi Tech, Vol. 30 (2012), No. 1, pp. 60-81. [https://doi.org/10.1108/07378831211213210](https://doi.org/10.1108/07378831211213210)
