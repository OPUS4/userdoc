---
title: Import-Regeln
---

## Import-Regeln

Import Regeln sind momentan nur für die SWORD-Schnittstelle verfügbar. Sie erlauben
es Regeln zu definieren mit denen importierte Dokumente zusätzlich manipuliert werden 
können.

<p class="info" markdown="1">
Im folgenden werden die Begriffe **Keyword** und **Subject** synonym verwendet. Im 
OPUS 4 Datenmodel werden Schlagwörter als **Subject** bezeichnet.
</p>

Import-Regeln sind unabhängig von Import-Formaten. Sie dienen nicht dazu Daten von 
einem externen Format in das OPUS 4 Datenmodel zu übersetzen. Dafür ist der Code für
das entsprechende Format zuständig. Die Regeln dienen der nachträglichen Verarbeitung
und können in einer Reihe von Anwendungsszenarien helfen. Einige davon sind unten
beschrieben. 

Ideen für die Nutzung oder den weiteren Ausbau der Import-Regeln können gerne auf
GitHub festgehalten werden, um anderen Nutzern zu helfen oder die Weiterentwicklung
zu unterstützen.

[OPUS 4 Discussions (GitHub.com)](https://github.com/orgs/OPUS4/discussions)

Die Regeln werden in Zukunft auch für andere Import-Schnittstellen, wie z.B. den 
BibTeX-Import anwendbar sein. 

## Konfiguration

Um die Import-Regeln zu nutzen, müssen sie für SWORD aktiviert werden und es muss eine 
Konfigurationsdatei mit den Regeln angegeben werden.

~~~ ini
sword.enableImportRules = true
import.rulesConfigFile = APPLICATION_PATH "/application/configs/import-rules.ini"
~~~

In der INI Datei können dann beliebige Regeln definiert werden. Sie werden in der
Reihenfolge ausgeführt, die der sie in der Datei auftauchen.

~~~ ini
col1.type = 'AddCollection'
col1.condition.account = 'sword1'
col1.collection.id = 16457

lic1.type = 'AddLicence'
lic1.condition.keyword.value = 'ccby'
lic1.condition.keyword.remove = true
lic1.licenceId = 1
~~~

Die Reihenfolge der Regeln kann wichtig sein, wenn wie im Beispiel oben ein Keyword 
automatisch entfernt wird.

## Unterstützte Regeln

| Regel          | Beschreibung                                |
|----------------|---------------------------------------------|
| AddCollection  | Verknüpft Dokumente mit einer Sammmlung     |
| AddKeyword     | Fügt ein Subject/Keyword zum Dokument hinzu |
| AddLicence     | Verknüpft Dokument mit einer Lizenz         |
| RemoveKeywords | Entfernt Subjects/Keywords vom Dokument     |

### AddCollection-Regel

Mit der `AddCollection` Regel lassen sich automatisch Sammlungen zu den importierten 
Dokumenten hinzufügen. Wenn für die Regel keine Bedingung angeben wurde, wird die 
angegebene Sammlung zu allen Dokumenten hinzugefügt. 

~~~ ini
col1.type = 'AddCollection'
col1.condition.account = 'sword1'
col1.collection.id = 16457
~~~
 
Es werden folgende Optionen unterstützt, um die hinzuzufügende Sammlung anzugeben.

| Option      | Beschreibung                                |
|-------------|---------------------------------------------|
| id          | Datenbank-**Id** einer Sammlung             |
| roleName    | **Name** einer CollectionRole               |
| roleOaiName | OAI-Name (**OaiName**) einer CollectionRole |
| number      | **Number** einer Sammlung                   |
| name        | **Name** einer Sammlung                     |

Die Datenbank-ID einer Sammlung kann direkt angegeben werden.

~~~ ini
col1.collection.id = 32453
~~~

Für die Optionen `name` und `number` muss immer auch mit `roleName` oder `roleOaiName`
die CollectionRole angegeben werden, der die Sammlung zugeordnet ist.

~~~ ini
col1.collection.roleName = 'institutes'
col1.collection.number = 'insitute1'
~~~

~~~ ini
col1.collection.roleOaiName = 'departments'
col1.collection.number = 'department1'
~~~

Der Name einer Sammlung kann auch als Option verwendet werden. Da die Namen von 
Sammlungen auch für die Anzeige im User Interface verwendet werden, sind sie häufig
etwas unhandlicher. Die Option ist case-sensitive. Der Name muss mit der korrekten 
Groß/Kleinschreibung angegeben werden.

~~~ ini
col1.collection.roleName = 'institutes'
col1.collection.name = 'Mathematics'
~~~

### AddKeyword-Regel

Mit der `AddKeyword` Regel lassen sich automatisch Subjects/Keywords zu einem Dokument
hinzufügen.

| Option | Beschreibung                                         |
|--------|------------------------------------------------------|
| value  | Keyword                                              |
| type   | `swd` (GND), `psyndex`, **`uncontrolled`** (default) |
| lang   | Sprache, z.B. **`deu`** (default), `eng`             |

Wenn die Defaultwerte für Typ und Sprache passen, kann das Keyword auch direkt 
angegeben werden.

~~~ ini
kw1.type = 'AddKeyword'
kw1.keyword = 'Imported'
~~~

In Kombination mit einer `Keyword`-Bedingung, kann die `AddKeyword`-Regel verwendet
werden, um Keywords zu ersetzen. 

### AddLicence-Regel

Mit der `AddLicence` Regel lassen sich Dokumente automatisch mit einer Lizenz in OPUS 4
verknüpfen. In Kombination mit einer `Keyword`-Bedingung lässt sich so die Verknüpfung
automatisieren und von außen steuern. Der Sword-Client muss wissen, welche Lizenzen
in der OPUS 4-Instanz verfügbar sind, für welche Lizenzen Regeln konfiguriert wurden. 
Der Client muss aber nicht die Datenbank-IDs der Lizenzen kennen, sondern nur ein 
festgelegtes Schlüsselwort mitliefern.

Die `AddLicence` Regel unterstützt nur die Option `licenceId`. Es muss die Datenbank-ID
einer Lizenz angegeben werden.

~~~ ini
licence1.type = AddLicence
licence1.condition.keyword = 'CCBY'
licence1.licenceId = 1

licence2.type = AddLicence
licence2.condition.keyword = 'CCBYNA'
licence2.licenceId = 2
~~~

Auf diese Weise können alle Lizenzen auf Keywords gemappt werden.

<p class="info">
Eine komplett automatische Lizenz-Erkennung wäre vom Import-Format abhängig. An welcher 
Stelle sind die Lizenz-Informationen gespeichert, in welcher Form? Die Import-Regeln sollen
unabhängig von Import-Formaten sein. Sie sind ein Werkzeug für die Automatisierung, wenn   
Client und Server bekannt sind und konfiguriert werden können. 
</p>

### RemoveKeywords-Regel

Wenn Keywords als Bedingung (Condition) verwendet werden, z.B. für die automatische 
Verknüpfung von Dokumenten mit Lizenzen, können sie dabei automatisch entfernt werden.
Falls für ein Keyword mehrere Regeln definiert oder Keywords gefiltert werden sollen,
kann mit `RemoveKeywords` eine Liste von Keywords konfiguriert werden, die automatisch
entfernt werden.

Die Optionen sind ähnlich 

| Option        | Beschreibung                                            | Default  |
|---------------|---------------------------------------------------------|----------|
| keywords      | Keyword, Array oder CSV-Liste von Keywords              | required |
| keywordType   | `swd` (GND), `psyndex`, `uncontrolled`                  | alle     |
| caseSensitive | Soll Groß/Kleinschreibung berücksichtigt werden? (bool) | false    |

In folgendem Beispiel werden drei Keywords entfernt, die vorher vielleicht in anderen
Regeln verwendet wurden.

~~~ ini
remove.type = 'RemoveKeywords'
remove.keywords = 'oa-green,oa-gold,oa-gray' 
~~~

Die Keywords können auch als Array angegeben werden.

~~~
remove.type = 'RemoveKeywords'
remove.keywords[] = 'oa-green'
remove.keywords[] = 'oa-gold'
remove.keywords[] = 'oa-gray'
~~~

Mit den Optionen `keywordType` und `caseSensitive` lässt sich einschränken welche 
Schlüsselwörter entfernt werden.

~~~ ini
remove.type = 'RemoveKeywords'
remove.keywords = 'oa-green, oa-gold, oa-gray'
remove.keywordType = 'uncontrolled'
remove.caseSensitive = true 
~~~

## Unterstützte Bedingungen

Mit einer `Condition` kann eine Regel von Bedingungen abhängig gemacht werden. Momentan 
werden die folgenden Bedingungen unterstützt.

| Bedingung | Beschreibung                   |
|-----------|--------------------------------|
| Account   | Prüft den aktiven User Account |
| Keyword   | Prüft auf Subject/Keyword      |

### Account-Bedingung

Die Account-Bedingungen unterstützt nur die Option `account`, um den Namen eines aktiven
User-Accounts anzugeben. Damit kann man zum Beispiel in Abhängigkeit von dem Account, mit 
dem auf die SWORD-Schnittstelle zugegriffen wird, die importierten Dokumente mit einer 
Sammlung verknüpfen. 

~~~ ini
department1.type = 'AddColletion'
department1.condition.account = 'dep1sword'
department1.collection.roleName = 'departments'
department1.collection.number = 'opus4dev'
~~~

Das kann zum Beispiel im Zusammenhang mit DeepGreen verwendet werden, wenn Dokumente für
mehrere Institutionen an eine OPUS 4 Instanz geliefert werden sollen. Jede Institution
kann einen anderen OPUS 4-Account verwenden.

### Keyword-Bedingung

Die Aufführung der verknüpften Regel hängt davon ab, ob ein Subject bzw. Keyword gefunden 
wird. Das Keyword kann optional automatisch entfernt werden.

Es werden vier Optionen unterstützt.

| Option        | Beschreibung                                            | Default  |
|---------------|---------------------------------------------------------|----------|
| value         | Keyword                                                 | required |
| type          | `swd` (GND), `psyndex`, `uncontrolled`                  | alle     |
| remove        | Soll das Keyword entfernt werden? (bool)                | false    |
| caseSensitive | Soll Groß/Kleinschreibung berücksichtigt werden? (bool) | false    |

Mit folgender Regel würden Dokumente automatisch mit der ersten Lizenz (ID = 1) verknüpft
werden, wenn das Keyword `ccby` auftaucht, egal ob groß oder kleingeschrieben. Wenn die
`type` Option weggelassen wird, kann das Keyword einen beliebigen Typ haben. Das Keyword
wird automatisch entfernt. 

``` ini
licence1.type = 'AddLicence'
licence1.condition.keyword.value = 'ccby'
licence1.condition.keyword.type = 'uncontrolled'
licence1.condition.remove = true
licence1.condition.caseSensitive = false
licence1.licenceId = 1
```

Alternativ kann das Keyword auch direkt angegeben werden. Es gelten dann die oben 
beschriebenen Default-Optionen. Das heißt die Schreibung wird nicht berücksichtigt und
das Keyword wird nicht automatisch entfernt. Der Typ ist egal. 

``` ini
licence1.type = 'AddLicence'
licence1.condition.keyword = 'ccby'
licence1.licenceId = 1
```

<p class="note" markdown="1">
Wenn die automatische Entfernung aktiviert ist und das gleiche Keyword im Dokument 
für mehrere Typen auftaucht, also z.B. `swd` und `uncontrolled`, wird das Schlagwort
für alle Typen entfernt, wenn die Option `type` nicht angegeben wurde.
</p>
