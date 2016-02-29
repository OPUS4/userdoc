---
title: Veröffentlichen
weight: 30
---

# Veröffentlichen

Neben der Suche und dem Browsen stellt das Veröffentlichen von Dokumenten die dritte zentrale Funktion in OPUS dar.
Grundlage für das Veröffentlichen von Dokumenten bilden die [Dokumenttypen](../documenttypes/index.html).

Die Dokumente werden über ein 3-stufiges Formular in OPUS eingestellt. Im ersten Schritt werden ein Dokumenttyp
ausgewählt und (optional) die entsprechenden Datei(en) hochgeladen. Zusätzlich kann das Dokument durch das Setzen
eines Häkchens zur Bibliographie hinzugefügt werden.

Im zweiten Schritt werden dann die Metadaten basierend auf dem gewählten Dokumenttyp eingegeben.
Es gibt Pflicht- und optionale Felder. Pflichtfelder werden durch einen Stern
gekennzeichnet. Wenn alle (Pflicht-)Felder ausgefüllt wurden, werden die Formulardaten durch den Klick auf den
Senden- Button validiert. Im Falle eines Fehlers wird zurück auf das Formular geleitet und Fehler können berichtigt
werden.

Waren alle Eingaben korrekt, gibt es im Schritt drei die Möglichkeit, die Eingaben erneut zu prüfen und durch Klicken
des Zurück-Buttons gegebenenfalls zu korrigieren. Darüber hinaus besteht in diesem Schritt die Möglichkeit, das
Dokument (optional) einer Sammlung zuzuordnen. Ein Klick auf den Button 'Abspeichern' speichert das Dokument mit dem
Status "unpublished" auf dem Dokumentenserver und es muss nach einer Prüfung durch den Administrator oder (eine)
berechtigte Person(en) freigeschaltet werden. Anschließend ist das Dokument mit dem Status "published" verfügbar.

## Untergeordnete Dokumenttypen

Die Standardversion von OPUS4 enthält
[Dokumenttypen](../documenttypes/index.html), die prinzipiell anderen Dokumenttypen untergeordnet sind
(z.B. "Teil eines Buches" und "Buch (Monographie)"). Diese Form der Beziehung wird jedoch in der aktuellen Version
nicht funktionell unterstützt,
das heißt, es gibt keine Möglichkeit, beispielsweise Dokumente, die als "Teil eines Buches" im Repositorium
aufgenommen wurden, dem entsprechenden übergeordneten Dokument "Buch (Monographie)" funktional zuzuordnen. Wenn man
innerhalb eines Dokumenttyps auf ein übergeordnetes Dokument verweisen möchte, kann man hierfür das Feld
"TitleParent/Übergeordnetes Werk" benutzen. Der Inhalt dieses Feldes ist dann suchbar, das heißt, eine Suche über
alle Felder oder eine Titelsuche nach dem betreffenden übergeordneten Werk würde als Ergebnis auch die Dokumente
anzeigen, die nur auf dieses übergeordnete Werk verweisen.
