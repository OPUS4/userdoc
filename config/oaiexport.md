---
title: OAI Export
---

# OAI Export

An dieser Stelle werden die OAI-Parameter eingetragen.

{% highlight ini %}
; OAI SETTINGS
oai.baseurl =
oai.repository.name = Opus4 Demo Instance
oai.repository.identifier = opus4.demo
oai.sample.identifier = oai:opus4.demo:90
oai.ddb.contactid =
{% endhighlight %}

Bei dem Parameter `oai.baseurl` wird die URL eingetragen, unter der die OAI-Schnittstelle
erreichbar ist. Diese wird in der Schnittstelle unter `<baseURL>` angezeigt und wird normalerweise
automatisch auf den Hostnamen der Opus-Instanz gesetzt. Sie sollte daher nur geändert werden,
falls eine abweichende URL gewünscht wird (z.B. bei Rechnern, die mehrere DNS-Einträge
besitzen). Der Parameter `oai.repository.name` wird in der OAI-Schnittstelle unter
`<repositoryName>` und `oai.repository.identifier` unter `<repositoryIdentifier>` angezeigt. Bei
`oai.sample.identifier` kann ein existierendes Dokument eingetragen werden, das in der
Schnittstelle unter `<sampleIdentifier>` (d.h. Beispiel-Dokument) angezeigt wird. Schließlich kann bei
`oai.ddb.contactid` eine DNB-Contact-ID (wenn vorhanden) eingetragen werden.

Die darüber hinaus existierenden Parameter oai.max.listrecords (Anzahl der Einträge für das
Kommando `ListRecords`) und oai.max.listidentifiers (Anzahl der Einträge für das Kommando
`ListIdentifiers`) werden bereits bei der Installation mit Standardwerten befüllt und müssen in der
Regel nicht angepasst werden.
