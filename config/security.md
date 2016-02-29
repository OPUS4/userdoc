---
title: Sicherheit
---

# Accounts

Um in OPUS angemeldeten Nutzern die Möglichkeit zum Editieren des eigenen Accounts zu geben
gibt es in der `$BASEDIR/application/configs/application.ini` folgende Parameter, die in
der `config.ini` überschrieben werden können:

{% highlight ini %}
;ACCOUNT MODULE SETTINGS
account.changeLogin = 1; Turn on to allow users to change their own account login
account.editOwnAccount = 1 ; Turn on to allow users to edit their own account information
account.editPasswordOnly = 0 ; Turn on to restrict editing to just the password
{% endhighlight %}

1. `account.editOwnAccount` legt fest, ob Nutzer ihren eigenen Account ändern dürfen.
2. `account.changeLogin legt` fest, ob Nutzer ihren eigenen Account-Namen ändern dürfen.
3. `account.editPasswordOnly` legt fest, ob Nutzer lediglich ihr eigenes Password, nicht aber ihren
   Namen und ihre Email-Adresse ändern dürfen.

<p class="note">
Damit Nutzer ihren eigenen Account editieren können benötigen sie Zugriff auf das account
Modul. Standardmäßig hat kein Nutzer Zugriff auf das Modul, da die Rolle guest im Standard nicht
darauf zugreifen darf. Um die Möglichkeit für alle Nutzer freizugeben kann guest der Zugriff
eingeräumt werden. Andernfalls kann Nutzern über ihre eigene Rolle der Zugriff auf das account
Modul eingeräumt werden (s. a. Kapitel 9.8 Zugriffskontrolle).
</p>

# Sicherheit

Neu geladenen Dateien wird im Standard die Rolle " guest " als Zugriffsrecht zugewiesen. Dies kann
nun über den Parameter securityPolicy.files.defaultAccessRole konfiguriert werden. Dazu ist
der Konfigurationsschlüssel aus der config.ini.template in die config.ini zu übernehmen, die
Kommentarzeichen vor dem Schlüssel zu entfernen und die gewünschten Anpassungen an der
Rollendefinition vorzunehmen. Hinweise zur Zugriffskontrolle und zu Nutzerrollen finden sich in den
Kapiteln 9.8 Zugriffskontrolle 158 und 9.8.2 Nutzerrollen 160.

{% highlight ini %}
; SECURITY SETTINGS
; Change default role for newly uploaded files (default is "guest").
securityPolicy.files.defaultAccessRole = 'guest'
{% endhighlight %}




