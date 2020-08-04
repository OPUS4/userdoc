---
title: Sprachen
weight: 60
---

# Sprachen

Unter diesem Menüpunkt können die Sprachen verwaltet werden, die beim Veröffentlichungsprozess
und beim Editieren der Metadaten eines Dokuments zur Auswahl stehen sollen. Für das Anlegen
neuer Sprachen müssen entsprechende ISO-Werte der ISO-Normen 639-2 und 639-1 eingetragen
werden (* **Pflichtfelder**):

| Parameter | Bedeutung |
|-----------+-----------|
| 639-2 Bezeichner (bibliografischer Code) | Part2_B-Schlüssel des "bibliographic applications code set" (ISO 639-2), 3 Zeichen, z.B. ger Bei Verwendung der OAI-XMetaDissPlus-Schnittstelle wird der bibliographische Code erwartet und ist dann bei der Sprachdefinition mit anzugeben.
| **639-2 Bezeichner (Terminologie-Code)*** | Part2_T-Schlüssel des "terminology applications code set" (ISO 639-2), 3 Zeichen, z.B. deu |
| 639-1 Bezeichnung | Part1-Schlüssel (ISO 639-1), z.B. de |
| I(ndividuell), M(acrosprache), S(pecial) | Geltungsbereich (scope) |
| A(ntik), C(onstruiert), E(ausgestorben), H(istorisch), L(ebend), S(pecial) | Typ (type) |
| **Sprache*** | Referenzname der Sprache, z.B. German; der dort eingetragene Wert wird in der Übersicht des Bereichs "Sprachen verwalten" angezeigt |
| aktiv | Standard: inaktiv; um eine Sprache in OPUS 4 zu aktivieren (zur Auswahl verfügbar zu machen), muss hier ein Häkchen gesetzt werden |

<p class="info" markdown="1">
Die ISO-Werte der ISO-Normen 639-2 und 639-1 können z.B. bei der
[Library of Congress](http://www.loc.gov/standards/iso639-2/php/code_list.php) abgerufen werden.
</p>

Für die Übersetzung von Sprachbezeichnungen in der Oberfläche werden PHP-Funktionen verwendet (OPUS 4.7+). Damit ist es 
nicht notwendig Übersetzungsschlüssel für neue Sprachen hinzuzufügen.

<p class="warning">
Sprachen können deaktiviert werden! Werden vorhandene Sprachen nicht benötigt, genügt es,
das Häkchen bei "aktiv" zu entfernen. Es ist nicht notwendig, die Sprache zu löschen!
</p>

