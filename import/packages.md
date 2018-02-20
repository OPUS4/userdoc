---
title: OPUS 4 Pakete
---

# OPUS 4 Pakete

OPUS 4 unterstützt den Import von Metadaten und Volltexten als **\*.zip** oder **\*.tar** 
Paket.  Diese Pakete müssen die Datei `opus.xml` mit den Metadaten enthalten.

    import.zip
      |-opus.xml
      |-document1.pdf
      |-document1.doc
      |-fulltext2.pdf
      |-image3.png


## Metadaten

Die Metadaten müssen dem Import Schema entsprechen.  Die Datei `opus.xml` kann die Metadaten 
für mehrere Dokumente enthalten.

<http://www.opus-repository.org/schema/opus-import.xsd>

OPUS 4 Import XML sieht wie folgt aus.

``` xml
<import>
    <opusDocument language="deu" type="article">
        <titlesMain>
            <titleMain language="deu">Beispiel Titel</titleMain>
        </titlesMain>
        <persons>
            <person role="author" firstName="Erika" lastName="Musterfrau">
                <identifiers>
                    <identifier type="orcid">0000:...</identifier>
                </identifiers>
            </person>
        </persons>
    </opusDocument>
</import>
```

<p class="note" markdown="1">
Das Import XML wird noch weiter entwickelt, um die Verwendung zu vereinfachen. Es können 
zum Beispiel bereits Verknüpfungen zu Sammlungen importiert werden, aber dafür ist die 
interne Datenbank-ID der Sammlung notwendig.  Klassifikationen werden in OPUS 4 zum Beispiel 
als Sammlungen verwaltet.  Um das Dokument mit einem Eintrag der DDC zu verknüpfen, benötigt 
man eine Nummer wie **16728** und diese kann in jedem Repository unterschiedlich sein. 
<br />
Es ist geplant, für Klassifikationen allgemeinverständliche Angaben zu unterstützen, mit 
denen dann zum Beispiel der Typ **DDC** und der Identifier **345** angegeben werden können. 
</p>


## Volltexte importieren

In den Metadaten müssen die Dokumente mit den Dateien verknüpft werden.  Es findet keine 
automatische Zuordnung anhand der Namen statt. 

``` xml
<files>
    <file name="document1.pdf" />
    <file name="document1.doc" />
</files>
```

Enthält die Datei `opus.xml` nur die Metadaten für ein einziges Dokument, werden 
automatisch alle anderen Dateien zu diesem Dokument hinzugefügt, unabhängig davon, 
ob sie im `files`-Element deklariert wurden.

Der Import unterstützt auch eine Paketstruktur, bei der die Dateien der Dokumente in 
separaten Verzeichnissen gespeichert werden, um Konflikte durch identische Dateinamen 
zu vermeiden.

    import.tar
      |-opus.xml
      |-doc1
      |   |-article.pdf
      |   |-image.png
      |-doc2
          |-article.pdf
          |-article.doc
          
In diesem Fall müssen die Dateien in den Metadaten explizit deklariert werden.  Es reicht 
nicht, das Verzeichnis mit den Dateien für ein Dokument anzugeben.

``` xml
<files>
    <!-- Datei wird mit Namen 'article.pdf' hinzufügen -->
    <file path="doc1/article.pdf" />
</files>
```

oder

``` xml
<files basedir="doc1">
    <!-- Datei wird mit Namen 'article.pdf' hinzufügen -->
    <file path="article.pdf" />
</files>
```

oder

``` xml
<files>
    <!-- Datei wird mit Namen 'article-original.doc' hinzufügen -->
    <file path="doc1/article.doc" name="article-original.doc" />
</files>
```


# Metadaten des NISO JATS Formats nach OPUS 4 Pakete wandeln

Das folgende XSLT Skript wandeln das gängige NISO JATS Format für Artikelmetadaten 
in das OPUS 4 Paketformat um:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

  <!-- <xsl:import href="outputTokens.xsl"/> -->
  <xsl:output method="xml" omit-xml-declaration="yes" indent="yes" encoding="utf-8"/>

  <xsl:variable name="langCodes" select="document('langCodeMap.xml')/langCodeMap/langCode"/>
  <xsl:variable name="langIn" select="translate(/article/@xml:lang,'ABCDEFGHIJKLMNOPQRSTUVWXYZ','abcdefghijklmnopqrstuvwxyz')"/>
  <!-- <xsl:variable name="langOut">eng</xsl:variable> -->
  <xsl:variable name="langOut" select="$langCodes[@iso639-1=$langIn]/@iso639-2"/>

  <xsl:template match="/">
  <import>
    <opusDocument>
          <xsl:attribute name="language"> 
            <xsl:value-of select="$langOut"/>
          </xsl:attribute>
          <xsl:attribute name="type">
            <xsl:text>article</xsl:text>
          </xsl:attribute>
          <xsl:if test="//article-meta/fpage">
            <xsl:attribute name="pageFirst">
              <xsl:value-of select="//article-meta/fpage"/>
            </xsl:attribute>
          </xsl:if>
          <xsl:if test="//article-meta/lpage">
            <xsl:attribute name="pageLast">
              <xsl:value-of select="//article-meta/lpage"/>
            </xsl:attribute>
          </xsl:if>
          <xsl:if test="//article-meta/volume">
            <xsl:attribute name="volume">
              <xsl:value-of select="//article-meta/volume"/>
            </xsl:attribute>
          </xsl:if>
          <xsl:if test="//article-meta/issue">
            <xsl:attribute name="issue">
              <xsl:value-of select="//article-meta/issue"/>
            </xsl:attribute>
          </xsl:if>
          <xsl:attribute name="publisherName">
            <xsl:value-of select="//journal-meta/publisher/publisher-name"/>
          </xsl:attribute>
          <xsl:if test="//journal-meta/publisher/publisher-loc">
            <xsl:attribute name="publisherPlace">
              <xsl:value-of select="//journal-meta/publisher/publisher-loc"/>
            </xsl:attribute>
          </xsl:if>
          <xsl:attribute name="belongsToBibliography">
            <xsl:text>false</xsl:text>
          </xsl:attribute>
          <xsl:attribute name="serverState">
            <xsl:text>unpublished</xsl:text>
          </xsl:attribute>
      <titlesMain>
          <titleMain>
            <xsl:attribute name="language"><xsl:value-of select="$langOut"/></xsl:attribute>
            <xsl:value-of select="//article-meta/title-group/article-title"/>
          </titleMain>
      </titlesMain>
      <titles>
          <xsl:if test="//journal-meta/journal-title-group/journal-title">
            <title> 
              <xsl:attribute name="language"><xsl:value-of select="$langOut"/></xsl:attribute>
              <xsl:attribute name="type"><xsl:text>parent</xsl:text></xsl:attribute> 
              <xsl:value-of select="//journal-meta/journal-title-group/journal-title"/>
            </title>
          </xsl:if>
      </titles>
      <abstracts>
          <xsl:if test="//article-meta/abstract">
            <abstract>
              <xsl:attribute name="language"><xsl:value-of select="$langOut"/></xsl:attribute>
              <xsl:value-of select="//article-meta/abstract"/>
            </abstract>
          </xsl:if>
      </abstracts>
      <persons>
          <xsl:for-each select="//article-meta/contrib-group/contrib">
            <person>
                <xsl:attribute name="role">
                  <xsl:choose>
                    <xsl:when test="@contrib-type='guest-editor'">
                       <xsl:text>editor</xsl:text>
                    </xsl:when>
                    <xsl:otherwise>
                       <xsl:value-of select="@contrib-type"/>
                    </xsl:otherwise>
                  </xsl:choose>
                </xsl:attribute>
                <xsl:attribute name="firstName"><xsl:value-of select="name/given-names"/></xsl:attribute>
                <xsl:attribute name="lastName"><xsl:value-of select="name/surname"/></xsl:attribute>
            </person>
          </xsl:for-each>
      </persons>
      <keywords>
          <keyword> 
            <xsl:attribute name="language"><xsl:value-of select="$langOut"/></xsl:attribute>
            <xsl:attribute name="type"><xsl:text>swd</xsl:text></xsl:attribute>
            <xsl:text>-</xsl:text>
          </keyword>
          <xsl:for-each select="//article-meta/kwd-group/kwd">
            <keyword> 
              <xsl:attribute name="language"><xsl:value-of select="$langOut"/></xsl:attribute>
              <xsl:attribute name="type"><xsl:text>uncontrolled</xsl:text></xsl:attribute>
              <xsl:value-of select="normalize-space(text())"/>
            </keyword>
          </xsl:for-each>
      </keywords>
      <dates>
        <xsl:choose>
          <xsl:when test="//article-meta/pub-date[contains(@pub-type,'epub')]/year">
            <xsl:call-template name="compose-date">
              <xsl:with-param name="xpub" select="'epub'"/>
            </xsl:call-template>
          </xsl:when>
          <xsl:when test="//article-meta/pub-date[contains(@pub-type,'ppub')]/year">
            <xsl:call-template name="compose-date">
              <xsl:with-param name="xpub" select="'ppub'"/>
            </xsl:call-template>
          </xsl:when>
          <xsl:otherwise>
            <date>
              <xsl:attribute name="type"><xsl:text>completed</xsl:text></xsl:attribute>
              <xsl:attribute name="monthDay">
                <xsl:text>--11-11</xsl:text>
              </xsl:attribute>
              <xsl:attribute name="year">
                <xsl:text>1111</xsl:text>
              </xsl:attribute>
            </date>
          </xsl:otherwise>
        </xsl:choose>
      </dates>
      <identifiers>
          <identifier>
             <xsl:attribute name="type"><xsl:text>issn</xsl:text></xsl:attribute>
             <xsl:for-each select="//journal-meta/issn[@pub-type='ppub']">
                <xsl:value-of select="normalize-space(text())"/>
                <xsl:if test="position() != last()">
                   <xsl:text> , </xsl:text>
                </xsl:if>
                <xsl:if test="position() = last()">
                   <xsl:text> (pISSN)</xsl:text>
                </xsl:if>
             </xsl:for-each>
             <xsl:if test="//journal-meta/issn[@pub-type='epub']">
                <xsl:text> ; </xsl:text>
                <xsl:for-each select="//journal-meta/issn[@pub-type='epub']">
                   <xsl:value-of select="normalize-space(text())"/>
                   <xsl:if test="position() != last()">
                      <xsl:text> , </xsl:text>
                   </xsl:if>
                   <xsl:if test="position() = last()">
                      <xsl:text> (eISSN)</xsl:text>
                   </xsl:if>
                </xsl:for-each>
             </xsl:if>
          </identifier>
          <identifier>
             <xsl:attribute name="type"><xsl:text>doi</xsl:text></xsl:attribute>
             <xsl:value-of select="//article-meta/article-id[@pub-id-type='doi']"/>
          </identifier>
        <xsl:if test="//article-meta/article-id[@pub-id-type='pmid']">
          <identifier>
             <xsl:attribute name="type"><xsl:text>pmid</xsl:text></xsl:attribute>
             <xsl:value-of select="//article-meta/article-id[@pub-id-type='pmid']"/>
          </identifier>
        </xsl:if>
      </identifiers>
    </opusDocument>
  </import>
  </xsl:template>

  <xsl:template name="compose-date">
    <xsl:param name="xpub" select="'epub'"/>
          <date>
             <xsl:attribute name="type"><xsl:text>published</xsl:text></xsl:attribute>
             <xsl:attribute name="monthDay">
                <xsl:text>--</xsl:text>
                <xsl:choose>
                  <xsl:when test="//article-meta/pub-date[contains(@pub-type,$xpub)]/month">
                    <xsl:value-of select="format-number(//article-meta/pub-date[contains(@pub-type,$xpub)]/month,'00')"/>
                  </xsl:when>
                  <xsl:otherwise>
                    <xsl:text>12</xsl:text>
                  </xsl:otherwise>
                </xsl:choose>
                <xsl:text>-</xsl:text>
                <xsl:choose>
                  <xsl:when test="//article-meta/pub-date[contains(@pub-type,$xpub)]/day">
                     <xsl:value-of select="format-number(//article-meta/pub-date[contains(@pub-type,$xpub)]/day,'00')"/>
                  </xsl:when>
                  <xsl:otherwise>
                     <xsl:text>01</xsl:text>
                  </xsl:otherwise>
                </xsl:choose>
             </xsl:attribute>
             <xsl:attribute name="year">
                <xsl:value-of select="//article-meta/pub-date[contains(@pub-type,$xpub)]/year"/>
             </xsl:attribute>
          </date>
  </xsl:template>

</xsl:stylesheet>
```


Weitere (Binär-)Dateien können danach mit diesem zusätzlichen XSLT Skript zu einem 
OPUS 4 Paket hinzugefügt werden:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

  <xsl:output method="xml" omit-xml-declaration="yes" indent="yes" encoding="utf-8"/>

  <xsl:param name="file"/>
  <xsl:param name="md5"/>

  <xsl:template match="node()|@*">
    <xsl:copy>
      <xsl:apply-templates select="node()|@*"/>
    </xsl:copy>
  </xsl:template>

  <xsl:template match="/import/opusDocument">
    <xsl:copy>
      <xsl:copy-of select="node()|@*"/>
      <xsl:if test="not(./files) and string-length($file)!=0 and string-length($md5)!=0">
        <files>
           <xsl:attribute name="basedir"><xsl:text>.</xsl:text></xsl:attribute>
           <file>
             <xsl:attribute name="name"><xsl:value-of select="$file"/></xsl:attribute>
             <xsl:attribute name="language"><xsl:value-of select="//opusDocument/@language"/></xsl:attribute>
             <xsl:attribute name="visibleInOai"><xsl:text>true</xsl:text></xsl:attribute>
             <comment>
               <!-- <xsl:text>A component of the fulltext article</xsl:text> -->
             </comment>
             <checksum>
               <xsl:attribute name="type"><xsl:text>md5</xsl:text></xsl:attribute>
               <xsl:value-of select="$md5"/>
             </checksum>
           </file>
        </files>
      </xsl:if>
    </xsl:copy>
  </xsl:template>
  
  <xsl:template match="/import/opusDocument/files">
    <xsl:copy>
      <xsl:copy-of select="node()|@*"/>
      <xsl:if test="string-length($file)!=0 and string-length($md5)!=0">
        <file>
          <xsl:attribute name="name"><xsl:value-of select="$file"/></xsl:attribute>
          <xsl:attribute name="language"><xsl:value-of select="//opusDocument/@language"/></xsl:attribute>
          <xsl:attribute name="visibleInOai"><xsl:text>true</xsl:text></xsl:attribute>
          <comment>
            <!-- <xsl:text>A component of the fulltext article</xsl:text> -->
          </comment>
          <checksum>
            <xsl:attribute name="type"><xsl:text>md5</xsl:text></xsl:attribute>
            <xsl:value-of select="$md5"/>
          </checksum>
        </file>
      </xsl:if>
    </xsl:copy>
  </xsl:template>

</xsl:stylesheet>
```
