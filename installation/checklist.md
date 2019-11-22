---
title: Checkliste vor Liveschaltung
weight: 100
---

# Checkliste vor Liveschaltung

Anhand dieser Checkliste kann überprüft werden, ob alle wesentlichen instanzspezifischen Konfigurationen vorgenommen
wurden:

## Individualisierung der Oberfläche:

* [Layout](../configext/layout.html) anpassen
* [Startseite](../configext/startpage.html) anpassen
* [Dokumenttypen](../config/doctype.html) wählen
* [FAQ-Seite](../configext/faq.html) anpassen

## Rechtliches:

* [Impressum](../configext/imprintpage.html) einstellen
* [Kontaktinformationen](../configext/contactspage.html) einstellen
* [Leitlinien](../configext/policies.html) (inkl. Deposit Licence / Rechtseinräumung und Haftungsausschluss) einstellen
* [Lizenzen](../admin/licences.html) anpassen

## Weiteres

* **Wenn der Zugriff für bestimmte Nutzergruppen beschränkt werden soll:**

  [Zugriffsschutz](../admin/security.html) anpassen (Dateien, Module, Rollen)

* **Wenn die maximale Dateigröße und die Anzahl der hochladbaren Dateien angepasst, sowie weitere als die
  Standard-Dateiformate für den Upload erlaubt werden sollen:**

  Einstellungen für [Dateien](../configext/upload.html) anpassen

* **Wenn die OAI-Schnittstelle genutzt werden soll:**

  [OAI-Parameter](../config/configini.html#oai-export) eintragen, OAI-Schnittstelle aktivieren

* **Wenn Hochschulschriften per XMetaDissPlus an die DNB geliefert werden sollen:**

  [Verbreitende Stelle und Vergabeinstitution (DNB)](../admin/institutes.html) anlegen

* **Wenn automatisch URNs vergeben werden sollen:**

  automatische Vergabe von [URNs](../config/urn.html) aktivieren

* **Wenn die Bibliographiefunktion genutzt werden soll:**

  [Bibliographiefunktion](../config/configini.html#bibliographiefunktion) aktivieren

<p class="info" markdown="1">
Es wäre schön, wenn Sie uns nach der Liveschaltung eine kurze Nachricht an `opus4@kobv.de` mit der
Instanz-URL schicken würden, so dass wir die Instanz in die Liste der bekannten OPUS4-Instanzen
unter Referenzen (<http://www.kobv.de/opus4/referenzen/>) auf der OPUS-Homepage aufnehmen können.
Wir empfehlen darüber hinaus, dass der Admin sich auf der OPUS4-User-Mailingliste unter
<http://listserv.zib.de/mailman/listinfo/kobv-opus-tester> einträgt. Dort werden neue
Releases bekannt gegeben und Fragen direkt von den Entwicklern beantwortet.
</p>
