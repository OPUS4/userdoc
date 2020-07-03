---
title: OPUS mit Git
weight: 90
---

# OPUS mit Git

OPUS 4 ist für die Entwicklung zu GitHub gewechselt. Der Umstieg auf [Git][GIT] wirkt sich aber auch auf die
Installation und das Update von OPUS 4 Instanzen aus.

## Warum Installation und Updates mit Git?

Bis zu Version 4.4.5 wurde OPUS 4 als Tarball veröffentlicht. Der Tarball wurde lokal entpackt und der größte
Teil der Installation dann mit Hilfe eines Skriptes durchgeführt. Für Updates auf eine neue Version gab es
ebenfalls ein Skript.

Nach der Installation werden die meisten Instanzen konfiguriert, aber zum Teil auch
modifiziert. Das soll heißen Dateien, die zum Source Code gehören werden verändert. In der Entwicklung nennt
man das einen Branch bzw. einen Fork. Das heist es entsteht eine Version der Software, die von der
ursprünglichen abweicht. Bei einem Update müssen die lokalen Anpassungen mit den Änderungen, die durch
die weitere Entwicklung entstanden sind, zusammengeführt werden. Das kann kompliziert sein. Bisher gab es
für OPUS 4 ein Update Skript, daß versucht hat das möglichst einfach zu machen. Der Aufwand dafür war aber
sehr hoch und die Updates waren trotzdem noch ziemlich komplex. In der Entwicklung müssen auch ständig
unterschiedliche Versionen zusammengeführt werden. Ein gutes Werkzeug dafür ist Git.

Um mehr Zeit in neue Funktionen zu können werden wir in Zukunft Git für das Update, das Zusammenführen der
neuen und der lokalen Version von OPUS 4 verwenden.

## Installation

Ber der [Installation mit Git][INSTALL] ändert sich nicht viel. Statt einen Tarball herunterzuladen und auszupacken
werden die Sourcen mit einem Git Kommando direkt von GitHub auf das lokale System geholt. Anschließend wird
wie bisher der größte Teil der Installation mit einem Skript durchgeführt.

<p class="note">
Die OPUS 4 Sourcen enthalten einige Ressourcen, wie z.B. Dokumenttypen, die nur für Tests verwendet werden.
Beim Erzeugen des Tarballs wurden diese Ressourcen weggelassen. Bei der Installation mit Git findet diese
Filterung nicht mehr statt. Es wird daran gearbeitet diese Ressourcen aus dem normalen Code zu entfernen, so
daß diese nach der Installation nicht mehr manuell entfernt werden müssen.
</p>

## Update

Der große Unterschied wird in Zukunft das [Update mit Git][UPDATE] sein. Mit Hilfe eines Kommandos, können die lokalen
Dateien auf den aktuellen Stand der GitHub Version gebracht werden. Gibt es dabei keine Konflikte zwischen
lokal angepassten Dateien und Änderungen in OPUS, läuft das Update in wenigen Sekunden automatisch durch. Es
muss nicht mehr wie bisher ein Tarball veröffentlich werden, der dann für das Update verwendet wird und Git
ist viel besser in der Lage die Zusammenführung der Versionen so weit wie möglich zu automatisieren.

Die meisten Updates werden durch dieses Verfahren wesentlich schneller und einfacher werden. Dadurch können
Respositorien sofort mit der neuesten Version arbeiten und müssen nicht darauf warten, daß ein neuer Tarball
veröffentlich wird.

Wenn für ein Update die Datenbank oder der Solr-Index angepasst werden müssen, wird es auch weiterhin notwendig
sein nach der Aktualisierung der Dateien Skripte auszuführen, die dann die weiteren Anpassungen vornehmen.

## Versionen

Manchmal ist es wichtig zu wissen welche Version lokal verwendet wird. Die erste Version mit Git wird OPUS 4.5
sein. Zum Zeitpunkt des Releases wird auf GitHub der MASTER-Branch auf
den gewünschten Stand gebracht und ein Tag für die neue Version angelegt. Neue Instanzen können dann mit dieser
Version installiert bzw. exisitierende Instanzen auf diesen Stand aktualisiert werden. Die Entwicklung findet
dann auf einem anderen Branch statt, bis genügend Änderungen für eine neue Version zusammengekommen sind.

Kritische Bugfixes werden unter Umständen direkt zum MASTER-Branch hinzugefügt, ohne auf eine neue Version zu
warten. Wir eine Instanz dann auf diesen Stand aktualisiert ist die Versionsnummer der Instanz, die Tagnummer,
z.B. "4.5", plus eine Zahl von weiteren Revisionen, z.B. "4.5+6". Darüber hinaus hat jede Revision in Git einen
Hashwert der sie eindeutig identifiziert.

[INSTALL]: installation/index.html
[UPDATE]: update/index.html
[GIT]: https://git-scm.com/