---
title:  Reverse Proxy
weight: 600
---

# Reverse Proxy

### Server-Anpassung

Es ist möglich, OPUS hinter einem `Reverse Proxy` zu betreiben.

Hinweise für die Einstellungen im Apache-File des Proxy Servers:

{% highlight bash %}
<VirtualHost <ip-address>:443>
    ServerName <servername>
[...]
    ProxyRequests Off
    ProxyPass "/<opus-path>" "https://<backend-server>/<opus-path>"
    ProxyPassReverse "/<opus-path>" "https://<backend-server>/<opus-path>"
    ProxyPassReverseCookieDomain "<backend-server>" "<servername>"
[...]
    SSLEngine on
[...]
</VirtualHost>
{% endhighlight %}

<p class="info">
Auf der Seite des Proxys muss "X-Forwarded-For-Header" (XFF) aktiviert sein, damit die Client-IP-Adressen durchgereicht werden.
</p>

<p class="warning" markdown="1">
Ohne XFF-Header sieht ein Webserver nur die IP-Adresse des Proxys, nicht aber die echte IP-Adresse des Clients.
Der XFF-Header ist dadurch für Fälschungen anfällig ("IP-Spoofing"). Abhilfe schafft hier eine Liste von bekannten, vertrauenswürdigen Proxys.
Ist der Proxy bekannt, so ist anzunehmen, dass die von ihm übergebene Client-IP-Adresse in Ordnung ist.
</p>

### OPUS-Anpassung

Der Paramter `url` muss in der `$BASEDIR/application/configs/config.ini` gesetzt sein.
```ini
url = https://<servername>/<opus-path>
```


