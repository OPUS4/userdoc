---
title: Sprachen
weight: 60
---

# Sprachen

Die Sprachen, die in den Formularen für Dokumente auswählbar sind, können mit folgenden 
Optionen festgelegt werden.

``` ini
i18n.languages.active = deu, eng, fra, rus, spa, mul
i18n.languages.sortByName = 0
```

Beide Optionen sind auch unter Einstellungen->Optionen in der Administration verfügbar.
Die Sprachen werden in der angegebenen Reihenfolge aufgelistet, können mit der Option
**sortBýName** aber auch alphabetisch sortiert werden.

Es werden momentan 485 ISO 639 Sprachen unterstützt, die im Paket **opus4-i18n** definiert 
sind. 

https://github.com/OPUS4/opus4-i18n/blob/main/src/Languages.php

## Zusätzliche Sprachen definieren

Sollte eine Sprache nicht unterstützt werden, kann sie lokal hinzugefügt werden. Das ist 
momentan nur in den Konfigurationsdateien möglich und sieht wie folgt aus. 

``` ini
; i18n.languages.local.ISO639CODE = PART2_B, PART2_T, PART1, RefName
i18n.languages.local.cmn = cmn, zho, zh, Chinesisch/Mandarin
i18n.languages.local.wuu = wuu, zho, zh, Chinesisch/Wu
```

Die lokal definierten Sprachen können dann zur Liste hingefügt werden.

``` ini
i18n.languages.active = cmn, deu, eng, fra, rus, spa, wuu, mul
```

<p class="info" markdown="1">
Die ISO-Werte der ISO-Normen 639-2 und 639-1 können z.B. bei der
[Library of Congress](http://www.loc.gov/standards/iso639-2/php/code_list.php) abgerufen werden.
</p>

## Übersetzung der Sprachbezeichnungen

Die Bezeichnungen der Sprachen werden in vielen Fällen durch PHP Funktionen automatisch übersetzt.
Sollte eine Sprache von PHP nicht unterstützt werden, wird RefName verwendet. Es können lokal aber
auch Übersetzungsschlüssel für Sprachen angelegt werden. Die Schlüssel haben die folgende Struktur. 

    i18n_language_ISO_639_CODE

Also z.B. 

    i18n_language_cmn
    i18n_language_spa

Die Übersetzungen können in der Administration in der Übersetzungsverwaltung angelegt werden.