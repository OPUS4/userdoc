---
title: Import-Regeln
---

## Import-Regeln

Import Regeln sind momentan nur für die SWORD-Schnittstelle verfügbar. Sie erlauben
es Regeln zu definieren mit denen importierte Dokumente zusätzlich manipuliert werden 
können.

## Konfiguration

Um die Import-Regeln zu nutzen, müssen sie für SWORD aktiviert werden und es muss eine 
Konfigurationsdatei mit den Regeln angegeben werden.

    sword.enableImportRules = true
    import.rulesConfigFile = APPLICATION_PATH "/application/configs/impport-rules.ini

In der INI Datei können dann beliebige Regeln definiert werden. Sie werden in der
Reihenfolge ausgeführt, die der sie in der Datei auftauchen.

    col1.type = 'AddCollection'
    col1.condition.account = 'sword1'
    col1.collection.id = 16457

    lic1.type = 'AddLicence'
    lic1.condition.keyword.value = 'ccby'
    lic1.condition.keyword.remove = true
    lic1.licenceId = 1

Die Reihenfolge der Regeln kann wichtig sein, wenn wie im Beispiel oben ein Keyword 
automatisch entfernt wird.

## Unterstützte Regeln

| Regel        | Beschreibung |
|--------------|--------------|
| AddCollection | Verknüpft Dokumente mit einer Sammmlung |
| AddKeyword | Fügt ein Subject/Keyword zum Dokument|
| AddLicence | Verknüpft Dokument mit einer Lizenz |
| RemoveKeywords | Entfernt Subjects/Keywords vom Dokument |


## Unterstützte Bedingungen

| Bedingung | Beschreibung                   |
|-----------|--------------------------------|
| Account   | Prüft den aktiven User Account |
| Keyword   | Prüft auf Subject/Keyword      |

