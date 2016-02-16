---
title: Publikationslisten
weight: 70
---

# Publikationslisten

Opus4 bietet die Möglichkeit, Publikationslisten zu generieren. Im folgenden Kapitel wird erläutert,
wie Sie Opus zur Verwaltung von Publikationslisten verwenden, ein eigenes Layout entwerfen und
wie die Listen in einen Webauftritt eingebunden werden. Anhand eines fiktiven Beispiels werden Sie
Schritt für Schritt durch die Anleitung geführt.

## Erstellung einer Sammlung und eines Sammlungseintrags

Um für die Autorin Maxi Musterfrau eine Publikationsliste anzulegen, gehen Sie wie folgt vor:

1. Loggen Sie sich als Administrator ein.
2. Klicken Sie folgenden Pfad: Administration > Sammlungen.
3. Legen Sie eine neue Sammlung mit folgenden Parametern an (siehe Kapitel Anlegen einer neuen
Sammlung 141 ):

| Parameter | Belegung |
|-----------+----------|
| Name | persons |
| Bezeichnung des OAI-Sets | -- egal -- |
| Sortierreihenfolge | -- egal -- |
| sichtbar | ja |
| Sammlung wird auf Browsing-Startseite angezeigt | ja |
| Sammlungszugehörigkeit auf der Frontdoor anzeigen | nein |
| Sammlung als OAI-Set ausgeben | nein |
| Anzuzeigende Metadaten-Felder im Browsing | Name |
| Anzuzeigende Metadaten-Felder in der Frontdoor | -- egal -- |
|------------------------------------------------+------------|
{: class="parameters" }

4. Fügen Sie innerhalb der Sammlung einen neuen Sammlungseintrag ein (siehe Kapitel Anlegen
eines neuen Sammlungseintrages 142 ):

| Parameter | Belegung |
|-----------+----------|
| Name | Maxi Musterfrau |
| Nummer | musterfrau |
| sichtbar | ja |
| OAI-Subset | -- egal -- |
| Theme | -- egal -- |
|-------+------------|

<p class="warning">
Die Nummer des Sammlungseintrages muss innerhalb einer Sammlung eindeutig vergeben werden!
</p>

5. Nun ordnen Sie ein oder mehrere Dokumente dem Sammlungseintrag zu:

  5.1 Klicken Sie den Pfad: Administration > Dokumente und wählen Sie ein Dokument (im Status
publiziert) aus.
  5.2. Verknüpfen Sie diese Dokument mit der Sammlung von Maxi Masterfrau (siehe Kapitel
Sammlung mit Dokument verknüpfen 144 ).
  5.3 Wiederholen Sie diesen Vorgang für weitere Dokumente.

Die Publikationsliste wird als HTML-Snippet ausgeliefert und ist unter folgender URL abrufbar:

```
http://<$BASEDIR>/opus4/export/index/publist/role/persons/number/musterfrau
```

<p class="warning">
Um die Publikationsliste sehen zu können, müssen Sie weiterhin als Administrator eingeloggt
bleiben.
</p>

## Eigenes Layout für Publikationslisten

OPUS4 liefert ein Standard-Layout für Publikationslisten aus:

$BASEDIR/opus4/modules/ex port/view s/scripts/publist/default.xslt

Dieses sollte nicht verändert werden, da diese Änderungen bei Updates überschrieben werden. Um
ein eigenes Layout (im Folgenden mylayout genannt) zu erstellen, müssen die folgenden Schritte
vollzogen werden.

1. Legen Sie unter $BASEDIR/opus4/modules/ex port/view s/scripts/publist die Datei
mylayout.xslt auf Basis von default.xslt an.
2. Ändern Sie den Konfigurationsparameter:

publist.stylesheet = mylayout

<p class="info">
Alternative kann auch /stylesheet/mylayout an die URL angehängt werden.
</p>

## Ausgabe von Dateien

Standardmäßig werden in der Publikationsliste keine Informationen zu den Dateien der Dokumente
ausgegeben. Es besteht jedoch die Möglichkeit, bestimmte Dateitypen abhängig von ihrem Mime-
Typ direkt in der Publikationsliste zu verknüpfen, sodass sie mit einem Klick direkt heruntergeladen
werden können.

Dafür wird der Konfigurationsparameter publist.file.allow.mimetype angepasst. Dieser kann mehrfach
angegeben werden, um mehrere Dateitypen anzuzeigen. Um beispielsweise PDF-Dateien in der
Anzeige zu erlauben, wird folgendes eingetragen:

publist.file.allow.mimetype[application/pdf]=PDF

Der Mime-Typ (hier: application/pdf) wird in eckigen Klammern angegeben und diesem ein Text
zugewiesen, der in der Publikationsliste erscheint (hier: PDF). Für weitere Mime-Typen können
entsprechende Einträge ergänzt werden.

## Einbinden in eigene Webseite

OPUS4 bietet die Möglichkeit, Publikationslisten in eigene Webseiten einzubinden. Es wird
vorausgesetzt, dass auf dem Webserver PHP zur Verfügung steht. Das Einbinden der
Publikationsliste ist hier beispielhaft dargestellt:

{% highlight html %}
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        <link rel="stylesheet" type="text/css" href="mylayout.css">
    </head>
    <body>
        <?php
            function get_data($url, $message) {
                $options = array(
                    CURLOPT_RETURNTRANSFER => true,
                    CURLOPT_FOLLOWLOCATION => true,
                    CURLOPT_CONNECTTIMEOUT => 1,
                    CURLOPT_TIMEOUT        => 1,
                    CURLOPT_MAXREDIRS      => 10
                );

                $ch = curl_init($url);
                curl_setopt_array($ch,$options);
                $data = curl_exec($ch);
                $errno = curl_errno($ch);
                $http_status = curl_getinfo($ch, CURLINFO_HTTP_CODE);
                curl_close($ch);
                return ($errno > 0 || $http_status >= 400) ? $message : $data;
            }

            $errorMessage = "Service Temporarily Unavailable";
            $url = 'http://opus4-server/opus4/export/index/publist/role/persons/number/musterfrau';
            $content = get_data($url, $errorMessage);
            echo $content;
        ?>
    </body>
</html>
{% endhighlight %}


- Stellen Sie sicher, dass auf dem Webserver PHP mit cURL-Unterstützung installiert wurde.
  Einen Überblick über die Optionen für cURL finden Sie hier: http://php.net/manual/de/function.curl-setopt.php.
- Stellen Sie sicher, dass die Codierung der Webseite auf UTF8 eingestellt ist.
- Das Layout der Publikationslisten wird durch das CSS der Webseite realisiert.
- Eine geeignete Fehlermeldung sollte eingebunden werden.

### Zugriffsrechte für den Webserver über Freischaltung eines IP-Bereiches

Abschließend gewähren Sie dem Webserver Zugriffsrechte:

1. Loggen Sie sich als Administrator ein.
2. Klicken Sie folgenden Pfad: Administration > Zugriffskontrolle > Nutzerrollen
3. Legen Sie eine neue Nutzerrolle (Name: "publist") an und gewähren Sie der Nutzerrolle den Zugriff
   auf das Modul "export" (siehe Kapitel Nutzerrollen 160 )
4. Legen Sie einen neuen IP-Adressbereich an unter Administration > Zugriffskontrolle > IP
   Adressbereiche, tragen sie die IP-Adresse des Webservers ein und weisen Sie den IP-
   Adressbereich der Nutzerrolle "publist" zu (siehe Kapitel IP Adressbereiche 164 ).
