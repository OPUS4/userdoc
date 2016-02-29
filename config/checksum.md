---
title: Checksummen
---

# Checksummen

OPUS4 kann automatisch Hashwerte für Dateien von Dokumenten erzeugen, welche die Integrität
der jeweiligen Datei überprüfen. Diese Hashwerte werden beim Einstellen von neuen Dateien
berechnet, in der Datenbank abgespeichert und im Dateimanager 112 im Administrationsbereich
angezeigt. Da die Berechnung der Hashwerte bei großen Dateien sehr lange dauern kann (was zu
Fehlermeldungen führt), kann in der Datei `$BASEDIR/application/configs/config.ini` eine
Höchstgrenze für die Dateigröße eingestellt werden:

{% highlight ini %}
; Maximum filesize in MB (default 50 MB) for calculating MD5 and SHA512 hashes
; of files. The maximum filesize is limited to avoid excessive load on the
; server.
; In order to raise or reduce the limit remove the comment character below and
; adjust the value.
; 0 : Turns generation of hashes completely off.
; -1 : Enables calculation of hashes for all files without upper limit.
checksum.maxVerificationSize = 50
{% endhighlight %}

Um diese Funktion zu nutzen, muss der Parameter `checksum.maxVerificationSize` durch
Entfernen des Kommentarzeichens aktiviert werden. Folgende Werte sind möglich:

| Wert | Beschreibung |
|------+--------------|
|   0  | schaltet die Funktion aus |
|  -1  | ermöglicht die Berechnung des Hashwerts ohne Höchstgrenze |
| **n** | Berechnung des Hashwerts mit Höchstgrenze **n** MB |
