---
title: SWORD
---

# SWORD 

OPUS 4.6 implementiert die SWORD Schnittstelle in Version 1.3. Die Details der Spezifikation sind unter folgender 
Adresse verfügbar.

<http://swordapp.org/sword-v1/>

<p class="info">
Es gibt momentan keine Pläne den Funktionsumfang von SWORD 2 für OPUS 4 umzusetzen. Die Import Funktionen
an sich werden weiter ausgebaut werden, um mehr Metadaten einfacher verarbeiten zu können, zum Beispiel
Verknüpfungen mit Klassifikationssystem usw.
</p>

## Schnittstelle

Das SWORD Service Dokument kann unter der URL


abgerufen werden.

TODO




## Besonderheiten

SWORD verarbeitet normalerweise mit jedem Request nur ein Dokument und die Antworten, die vom Server
kommen sind darauf ausgerichtet. Die SWORD Schnittstelle von OPUS 4 kann zusätzliche Pakete mit 
mehreren Dokumenten verarbeiten. Ein ZIP/TAR-Paket kann die Metadaten und Dateien für mehr als ein 
Dokument enthalten. 

## Konfiguration

Die importierten Dokumente werden mit einer konfigurierbaren Sammlung verknüpft, um sie zusätzliche zu 
markieren. Die Sammlung heißt normalerweise "Import" und ist Teil der CollectionRole "Import". Beide
werden bei der Installation bzw. beim Update von OPUS 4 automatisch angelegt.

## Zugriff

Für Zugriff auf das SWORD Modul muss sich der Client über HTTP Basic Authentication identifizieren. Dafür 
muss in der Administration ein Account angelegt werden, der Zugriff auf das SWORD Modul hat. Der Nutzername 
und das Passwort dieses Accounts können dann für die Authentifizierung verwendet werden.

Es wird empfohlen einen Account zu verwenden, der nur Zugriff auf das SWORD-Modul hat.

Außerdem macht es Sinn für jede Datenquelle, zum Beispiel das [DeepGreen Projekt](https://deepgreen.kobv.de),
einen separaten Account einzurichten, so dass später festgestellt werden kann woher ein Dokument gekommen ist.

<p class="warning">
Der Verbindung zum Server sollte über HTTPS erfolgen, damit der Nutzername und das Passwort nicht
unverschlüsselt übertragen werden.
</p> 

## Beispiel Skript

Es gibt keinen Standard-Client für den Zugriff auf die SWORD-Schnittstelle. 

TODO
