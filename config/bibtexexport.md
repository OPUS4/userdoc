---
title: BibTeX Export
---

# BibTeX Export

Mit dem Konfigurationsschlüssel citationExport.bibtex.enrichment kann ein vorhandenes
Enrichment angegeben werden, das beim Bibtex-Export als "note" ausgegeben wird. Dazu wird der
Schlüssel in die `config.ini` wie folgt eingetragen:

{% highlight ini %}
citationExport.bibtex.enrichment = <Name des Enrichments>
{% endhighlight %}

Beispiel:
Das Enrichment mit dem Namen SubmissionStatus ist im OPUS angelegt und für ein Dokument
mit dem Wert "accepted for publication" gefüllt. Die Angabe in der `config.ini` muss dann lauten:

{% highlight ini %}
;BIBTEX EXPORT SETTINGS
citationExport.bibtex.enrichment = SubmissionStatus
{% endhighlight %}

Die Bibtex-Ausgabe enthält dann u.a. die Angabe:

{% highlight bibtex %}
note = {accepted for publication}
{% endhighlight %}
