---
title: Workflow
weight: 200
---

# Workflow

Für die Dokumentverwaltung in OPUS4 existieren folgende Zustände, in denen sich ein Dokument
befinden kann:

* unpublished (Nicht publiziert)
* inprogress (In Bearbeitung/ In Arbeit)
* audited (Geprüft)
* published (Publiziert/ Freigegeben)
* restricted (Geschützt)
* deleted (Gelöscht)

Werden Dokumente neu in OPUS4 eingebracht, bekommen sie zunächst den Status "unpublished".
Für die interne Bearbeitung der Metadaten und Dateien können Dokumente in die Zustände
"inprogress" und "audited" gesetzt werden. Beim Freischalten erhält das Dokument den Zustand
"published". In diesem Zustand ist es für die Öffentlichkeit sicht-, such- und exportierbar. Der
Zustand "restricted" kann für Dokumente genutzt werden, die bereits in OPUS4 eingebracht und
fertig bearbeitet wurden, aber (z.B. aus urheberrechtlichen Gründen) noch nicht sichtbar sein sollen.
Werden Dokumente gelöscht, bekommen sie den Status "deleted", bleiben aber zunächst in der
Datenbank erhalten und sind nur noch für angemeldete Benutzer mit den entsprechenden Rechten
sichtbar. Aus dem Zustand "deleted" können Dokumente, falls sie versehentlich gelöscht wurden,
"gerettet" oder nach Prüfung endgültig gelöscht werden.

Der Status eines Dokuments kann im  oberen Bereich der Metadatenübersicht verändert werden.

<p class="warning">
Dokumente sollten nur aus triftigen Gründen gelöscht werden. Nach dem Löschen erhalten sie
den Status "deleted". Wird das gelöschte Dokument von außerhalb (Lesezeichen, OAI-
Schnittstelle) aufgerufen, erscheint ein Hinweis, dass das Dokument mit der gewünschten ID
gelöscht wurde.
</p>

<p class="note">
Wird der Status der Dokumente über das oben beschriebene Dropdownmenü im
Metadatenformular geändert muss man noch einmal bestätigen, dass man den Status wirklich
ändern möchte. Das Abschalten der Bestätigungsseite ist möglich, siehe Notification Settings.
</p>

## Beziehung der Stati untereinander

Die folgende Beschreibung gilt für Administratoren. Für andere Nutzer können die erlaubten
 Übergänge noch weiter eingeschränkt werden.

`unpublished`
: Aus dem Status `unpublished` kann direkt in alle anderen Stati gewechselt werden.

`inprogress`
: Aus dem Status `inprogress` kann direkt in die Stati `audited`, `published`, `restricted` und `deleted`
  gewechselt werden. Es kann nicht in den Status `unpublished` zurück gewechselt werden.

`audited`
: Aus dem Status `audited` kann direkt in die Stati `published`, `restricted` und `deleted` gewechselt
  werden. Es kann in den Status `inprogress` zurück gewechselt werden. Es kann nicht in den Status
  `unpublished` zurück gewechselt werden.

`published`
: Aus dem Status `published` kann direkt in die Stati `restricted` und `deleted` gewechselt werden. Es
  kann in den Status `inprogress` zurück gewechselt werden. Es kann nicht in den Status `unpublished`
  zurück gewechselt werden. Es kann nicht direkt in den Status `audited` zurück gewechselt werden.

`restricted`
: Aus dem Status `restricted` kann direkt in die Stati `published` und `deleted` gewechselt werden. Es
  kann in den Status `inprogress` zurück gewechselt werden. Es kann nicht in den Status `unpublished`
  zurück gewechselt werden. Es kann nicht direkt in den Status `audited` zurück gewechselt werden.

`deleted`
: Aus dem Status `deleted` kann in den Status `inprogress` zurück gewechselt werden. Es kann nicht in
  den Status `unpublished` zurück gewechselt werden. Es kann nicht direkt in die Stati `audited`,
  `published` und `restricted` zurück gewechselt werden.
