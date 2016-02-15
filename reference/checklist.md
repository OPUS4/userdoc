---
title: Checkliste vor Liveschaltung einer OPUS 4-Instanz
weight: 10
---

# Checkliste vor Liveschaltung einer OPUS 4-Instanz

Anhand dieser Checkliste kann überprüft werden, ob alle wesentlichen instanzspezifischen Konfigurationen vorgenommen wurden:

Individualisierung der Oberfläche:

* [Layout](layout.html) anpassen
* [Startseite](startpage.html) anpassen
* Dokumenttypen 58 wählen
* FAQ-Seite 101 anpassen

Rechtliches:

* Impressum 108 einstellen
* Kontaktinformationen 107 einstellen
* Leitlinien (inkl. Deposit Licence / Rechtseinräumung und Haftungsausschluss) einstellen
* Lizenzen 157 anpassen

Wenn der Zugriff für bestimmte Nutzergruppen beschränkt werden soll:

* Zugriffsschutz 46 anpassen (Dateien, Module, Rollen)

Wenn die maximale Dateigröße und die Anzahl der hochladbaren Dateien angepasst, sowie weitere als die Standard-Dateiformate für den Upload erlaubt werden sollen:

* Einstellungen für Dateien 97 anpassen

Wenn die OAI-Schnittstelle genutzt werden soll:

* OAI-Parameter 60 eintragen, OAI-Schnittstelle aktivieren

Wenn Hochschulschriften per XMetaDissPlus an die DNB geliefert werden sollen:

* Verbreitende Stelle und Vergabeinstitution (DNB) 161 anlegen

Wenn automatisch URNs vergeben werden sollen:

* automatische Vergabe von URNs 57 aktivieren

Wenn die Bibliographiefunktion genutzt werden soll:

* Bibliographiefunktion 59 aktivieren

Wenn keine Revision-Nummer angezeigt werden soll:

* Codeabschnitt "debug revision" auskommentieren oder entfernen 98

<p class="info" markdown="1">
Es wäre schön, wenn Sie uns nach der Liveschaltung eine kurze Nachricht an opus4@kobv.de mit der Instanz-URL schicken würden,
so dass wir die Instanz in die Liste der bekannten OPUS4- Instanzen unter Referenzen (<http://www.kobv.de/opus4/referenzen/>)
auf der OPUS-Homepage aufnehmen können. Wir empfehlen darüber hinaus, dass der Admin sich auf der OPUS4-User-Mailingliste unter
<http://listserv.zib.de/mailman/listinfo/kobv-opus-tester> einträgt. Dort werden neue Releases bekannt gegeben und Fragen direkt
von den Entwicklern beantwortet.
</p>
