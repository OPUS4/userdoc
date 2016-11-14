---
title: Zugriffskontrolle
weight: 80
---

# Zugriffskontrolle

Im Bereich Zugriffskontrolle können Nutzerkonten eingerichtet, Nutzerrollen definiert und
IP-Adressbereiche festgelegt werden. Jedem Konto bzw. jedem IP-Adressbereich können eine oder
mehrere Rollen zugewiesen werden. Den Rollen können verschiedene Rechte zugewiesen werden.
Auf diese Art und Weise können unterschiedliche Rollen für verschiedene Nutzergruppen
definiert werden, um z.B. den Zugriff auf einzelne Administrationsfunktionen einzuschränken.

## Nutzerkonten

Im Bereich Nutzerkonten können bereits vorhandene Nutzerkonten editiert oder gelöscht oder neue
Nutzerkonten angelegt werden ('Nutzerkonto hinzufügen').

Beim Anlegen eines neuen Nutzers müssen ein Kontoname ('Login') und ein Passwort vergeben
werden (min. 6 Zeichen lang). Danach wird ausgewählt, welche Rolle das neue Nutzerkonto besitzt.

Ein Klick auf das jeweilige Konto zeigt eine Übersicht darüber, welche Rechte das Nutzerkonto
besitzt und welche Rollen ihm zugewiesen sind.

<p class="warning">
Für den Kontonamen ('Login') dürfen ausschließlich Kleinbuchstaben verwendet werden.
</p>

### Administrator

Der Benutzername für den Administrator lautet "admin" und kann nicht verändert werden. Das
Standardpasswort lautet "adminadmin" und sollte beim ersten Login entsprechend geändert werden,
indem man neben dem Login/Logout-Button auf 'Account' klickt und hier ein neues Passwort festlegt.
Gleichzeitig können dort die Daten des Administrators (Name, E-Mail-Adresse) eingetragen werden.

#### Zurücksetzen des Passworts

Soll das Passwort überschrieben werden (z.B. bei Verlust), so kann das Skript "change-password" aufgerufen
und ausgeführt werden:

    $ opus4/scripts$ php5 change-password.php admin <Neues Passwort>

## Nutzerrollen

Hier können Nutzerrollen definiert werden. Eine Nutzerrolle legt fest, welche Bereiche ein bestimmter
Nutzer sehen und ggf. bearbeiten darf. Die Nutzerrollen sind der zentrale Bestandteil der
Zugriffsverwaltung für Module, Dokumente und Dateien in OPUS4. Standardmäßig gibt es in OPUS4
zwei Nutzerrollen:

* administrator (besitzt uneingeschränkt alle Rechte und kann nicht verändert werden)
* guest (darf: suchen, browsen, veröffentlichen, veröffentlichte nicht-zugriffsgeschützte Dokumente
  sehen, nicht-zugriffsgeschützte Dateien herunterladen,
  exportieren, RSS exportieren, erlaubt das [Indexieren durch Webcrawler](../configext/crawler.html)).

### Anlegen einer neuen Nutzerrolle

Durch einen Klick auf "Neue Nutzerrolle" kann eine neue Nutzerrolle angelegt werden. Zunächst
muss ein Name (hier: "Bibliothek") eingetragen und auf "Speichern" geklickt werden:

Die neue Rolle ist nun angelegt und taucht in der Übersicht der Rollen auf:

Der Name kann auch nachträglich durch einen Klick auf "Editieren" geändert werden. Durch einen
Klick auf "Zugriffsrechte" können die Module und Bereiche der Administration festgelegt werden, für
die Zugriff gewährt werden soll, und es kann angegeben werden, welche Zustandsänderungen des
Dokuments diese Rolle durchführen darf.

### Zugriffsrechte festlegen

#### Module

Im Bereich "Module - Rolle hat Zugriff auf:" können einzeln die Module angeklickt werden, auf welche
die Rolle Zugriff erhalten soll:

<p class="warning">
Es gilt das Prinzip, dass Rechte immer zusätzlich zu denen vergeben werden können, welche
die Rolle guest besitzt ("Bereits erlaubt durch 'guest'-Rolle"). Das heißt, dass nur zusätzliche
Module oder Controller ausgewählt werden müssen.
</p>

#### Bereiche der Administration

Einer Rolle kann der Zugriff auf einzelne Bereiche der Administration eingeräumt werden.
Voraussetzung ist, dass die Rolle den Zugriff auf das Modul "admin" erhält:

Anschließend kann unter "Bereiche der Administration - Rolle hat Zugriff auf:" ausgewählt werden,
auf welche Bereiche die Rolle Zugriff haben soll. Wird hier keine Auswahl getroffen, so hat die Rolle
auf alle Bereiche Zugriff:

Wurde der Bereich "Dokumente verwalten" ausgewählt, muss unter "Bereich 'Dokumente verwalten':
Dokumentstatus - Rolle kann folgende Zustandsänderungen durchführen:" festgelegt werden, welche
Zustandsänderungen eine Rolle für Dokumente durchführen darf.

Wird hier nichts ausgewählt, so kann die Rolle die Metadaten und Zuweisungen des
Dokuments ändern, aber keinerlei Zustandsänderungen vornehmen.

Es ist aktuell nicht möglich eine Rolle für Benutzer zu definieren, die gleichzeitig den Zugriff auf
das Modul "admin" und auf eine einzelne im Modul "setup" enthaltene Funktionen (z.B. "FAQ-
Seiten verwalten", "Statischen Seiten verwalten" bzw. "Übersetzungsressourcen verwalten")
erlaubt.

Soll der Benutzer neben dem Zugriff auf einzelne im Modul "setup" enthaltene Funktionen auch
Zugriff auf das Modul "admin" erhalten, so müssen dem Benutzer dafür zwei getrennte Rollen
zugewiesen werden!

**Beispiel 1:** Nutzerrolle anlegen, die Dokumente nur bearbeiten, aber nicht
freischalten darf

  Die Rolle wird zunächst mit dem gewünschten Namen wie oben beschrieben angelegt. Dann wird ihr
  Zugriff auf das Modul "admin" und auf den Bereich der Administration "Dokumente verwalten"
  gegeben:

  Nun können noch die Zustandsänderungen festgelegt werden, die die Rolle für Dokumente
  durchführen kann, z.B. Dokumente überführen aus dem Zustand "unpublished" in den Zustand "in
  Bearbeitung", aus dem Zustand "in Bearbeitung" in den Zustand "geprüft" und ggf. aus diesem
  wieder zurück in "in Bearbeitung":

  Abschließend wird die Rolle einem bestehenden oder neuen Nutzerkonto zugewiesen 158 . Nach den
  Änderungen zeigt das Menü für die Administration nun nur noch die Funktionen an, auf die die Rolle
  Zugriff hat, alle anderen Funktionen sind ausgegraut:

  Der Link "OAI Link anzeigen" wird immer angezeigt, da es sich nicht um einen geschützten
  Bereich handelt.

**Beispiel 2:** Nutzerrolle anlegen, die Dokumente nur freischalten, aber nicht
bearbeiten darf

  Die Rolle wird zunächst mit dem gewünschten Namen wie oben beschrieben angelegt. Dann wird ihr
  Zugriff auf das Modul "review" gegeben. Abschließend wird die Rolle einem bestehenden oder neuen
  Nutzerkonto zugewiesen 158.

**Beispiel 3:** Nutzerrolle anlegen, die Dokumente verwalten und neue Sammlungen,
Schriftenreihen und Lizenzen anlegen darf

  Die Rolle wird zunächst mit dem gewünschten Namen wie oben beschrieben angelegt. Dann wird ihr
  Zugriff auf das Modul "admin" und auf die Bereiche der Administration "Dokumente verwalten",
  "Lizenzen verwalten", "Sammlungen verwalten", "Schriftenreihen verwalten" und "Sprachen verwalten"
  gegeben. Nun können noch die Zustandsänderungen festgelegt werden, die die Rolle für Dokumente
  durchführen kann. Abschließend wird die Rolle einem bestehenden oder neuen Nutzerkonto
  zugewiesen 158 .

## IP-Adressbereiche

Hier können IP Adressbereiche definiert werden, innerhalb derer bestimmte Nutzerrollen gelten. Das
heißt alle Nutzer, die das Repositorium aus dem festgelegten IP-Bereich aufrufen, besitzen
automatisch die entsprechenden Rechte.

Wird ein neuer IP Bereich hinzugefügt, muss als erstes ein Name eingegeben werden. Dieser darf
nur aus Buchstabe und Zahlen bestehen (keine Sonderzeichen, keine Leerzeichen). Darunter gibt
man den entsprechenden IP Bereich von der Anfangs-IP bis zu End-IP ein. Handelt es sich um eine
einzelne IP-Adresse, so wird diese in das Feld 'Anfangs-IP' eingetragen. Abschließend wird die
Nutzerrolle gewählt.

