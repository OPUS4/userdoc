---
title: NISO JATS-Format
---


# Beispiel-Skripte zur Verarbeitung von Metadaten im NISO JATS-Format

Hier finden Sie Beispiel-Skripte, um Metadaten, die im NISO JATS-Format vorliegen,
nach OPUX-XML zu konvertieren, zu packen und an die SWORD-Schnittstelle zu senden. 

Bei JATS handelt es sich um die Journal Article Tag Suite, eine gängige
XML-Auszeichnungssprache für Artikelmetadaten, die z.B. von PubMed Central und Nature 
verwendet wird. JATS ist in der Norm NISO Z39.96 standardisiert.


## Bash-Skript

Das folgende Bash-Skript wandelt eine ZIP-Datei, die genau *eine* XML-Metadaten-Datei
im NISO JATS-Format enthält, in eine ZIP-Datei mit einer OPUS 4-Import-XML-Datei um und
schickt sie als Request (via `curl`) an die SWORD-Schnittstelle einer OPUS 4-Instanz.

Das Bash-Skript verwendet für die Transformation NISO JATS ---> OPUS 4 zwei XSLT-Dateien, 
die im selben Verzeichnis wie das Bash-Skript gespeichert sein sollten. Diese finden Sie
auf dieser Seite im Anschluss an das Bash-Skript.

``` bash
#! /usr/bin/env bash

function usage() {
  echo
  echo "usage: `basename $0` [-d] [-u user] [-p passwd] [-h host] [-i instance] {zip-file}"
  echo
  echo "   zip-file     : simple (i.e. flat hierarchy) .zip file with exactly"
  echo "                  one .xml file and (possibly) multiple binary files"
  echo
  echo "   -u user      : sword user name allowed to do deposits [curr. '${user}']"
  if [ -z "${pw}" ]; then
    echo "   -p passwd    : sword password for sword user [curr. not set!]"
  else
    echo "   -p passwd    : sword password for sword user [curr. '***']"
  fi
  echo "   -h host      : opus4 host http address [curr. '${opus4_host}']"
  echo "   -i instance  : opus4 instance (i.e. sword api root) [curr. '${opus4_instance}']"
  echo "   -d           : debug switch; if given, no delivery at all(!) [curr. '${debug}']"
  echo
  echo " Currently using '${opus4_host}/${opus4_instance}/sword/deposit' as SWORD deposit point." 
  echo
  exit -1
}

debug="false"
opus4_host="https://opus4mig.kobv.de"
opus4_instance="opus4-fau"
user="green"
pw=""

xmlstarlet=`which xmlstarlet`
xml_pp=`which xml_pp`
head=`which head`
cat=`which cat`
cut=`which cut`
curl=`which curl`
zip=`which zip`
unzip=`which unzip`
zipgrep=`which zipgrep`
md5sum=`which md5sum`
mktemp=`which mktemp`
wc=`which wc`
getopt=`which getopt`

${getopt} --test >/dev/null
if [ $? -ne 4 ]; then
  echo "error: 'getopt --test' failed in this environment, stop."
  exit 1
fi

parsed=`${getopt} --options dh:p:u:i: --longoptions debug,passwd:,user:,instance:,host: --name "$0" -- "$@"`
if [ $? -ne 0 ]; then usage ; fi

eval set -- "${parsed}"
while true; do
  case "$1" in
      -d|--debug) debug="true" ; shift ;;
       -u|--user) user="$2" ; shift 2 ;;
     -p|--passwd) pw="$2" ; shift 2 ;;
   -i|--instance) opus4_instance="$2"; shift 2 ;;
       -h|--host) opus4_host="$2"; shift 2 ;;
              --) shift ; break ;;
               *) echo "Internal error!" ; exit 1 ;;
  esac
done

if [ $# -ge 1 ]; then
  zip_file="$1"
else
  usage
fi

if [ "${opus4_host#https://}" == "${opus4_host}" -a "${opus4_host#http://}" == "${opus4_host}" ]; then
  opus4_host="${opus4_host##*:}"
  opus4_host="${opus4_host#*/}"
  opus4_host="https://${opus4_host}"
fi

if [ -z "${pw}" ]; then
  read -p "[sword password] for ${user}: " -s pw
  echo
fi

abs_xsl="./nlm_jats2opus_xml.xsl"
abs_xsl_add="./add_files2opus_xml.xsl"
pkg_fmt="https://datahub.deepgreen.org/FilesAndJATS"
has_xml=`${zipgrep} "DOCTYPE article" ${zip_file} | ${wc} -l`

if [ ${has_xml} -eq 1 ]; then
  is_jrnl=`${zipgrep} "//NLM//DTD Journal " ${zip_file} | ${wc} -l`
  is_jats=`${zipgrep} "//NLM//DTD JATS " ${zip_file} | ${wc} -l`
  is_rsc=`${zipgrep} "//RSC//DTD RSC " ${zip_file} | ${wc} -l`
  if [ ${is_jrnl} -eq 1 ]; then
    abs_xsl="./Util/nlm_jats2opus_xml.xsl"
    pkg_fmt="https://datahub.deepgreen.org/FilesAndJATS"
  elif [ ${is_jats} -eq 1 ]; then
    abs_xsl="./Util/nlm_jats2opus_xml.xsl"
    pkg_fmt="https://datahub.deepgreen.org/FilesAndJATS"
  elif [ ${is_rsc} -eq 1 ]; then
    abs_xsl="./Util/rsc_rsc2opus_xml.xsl"
    pkg_fmt="https://datahub.deepgreen.org/FilesAndRSC"
  else
    echo "error: no valid .xml (Journal or JATS or RSC) in zip archive found: stop."
    exit -2
  fi
else
  echo "error: no valid (or too many?!) .xml (Journal xor JATS xor RSC) in zip archive found: stop."
  exit -3
fi

echo "`basename $0`: packaging format in zip archive found:"
echo "`basename $0`: ${pkg_fmt}"

tmp_dir=`${mktemp} -q -d`
trap "rm -rf ${tmp_dir}" 0 2 3 15

${unzip} -q ${zip_file} -d "${tmp_dir}/xfer"


meta_xml="`ls -1 ${tmp_dir}/xfer/*.xml | ${head} -1`"
${cat} ${meta_xml} | ${xmlstarlet} -q tr --omit-decl ${abs_xsl} | ${xml_pp} >"${tmp_dir}/opus.xml"
for f in "${tmp_dir}"/xfer/*; do
  [ "${f%.xml}" != "${f}" ] && continue
  MD5=`${md5sum} --binary "${f}" | ${cut} -d" " -f1`
  FL=`basename ${f}`
  ${cat} "${tmp_dir}/opus.xml" | ${xmlstarlet} -q tr --omit-decl ${abs_xsl_add} -s md5="${MD5}" -s file="${FL}" | ${xml_pp} >"${tmp_dir}/tmp.xml"
  mv "${tmp_dir}/tmp.xml" "${tmp_dir}/opus.xml"
done
rm -f ${meta_xml}
## mv "${tmp_dir}/opus.xml" ${meta_xml}
mv "${tmp_dir}/opus.xml" "${tmp_dir}/xfer/opus.xml"
${zip} -j -r "${tmp_dir}/package.zip" "${tmp_dir}/xfer" 

MD5=`${md5sum} --binary "${tmp_dir}/package.zip" | ${cut} -d" " -f1`
echo "`basename $0`: md5sum: ${MD5}"

if [ "${debug}" = "true" ]; then 
  cp "${tmp_dir}/xfer/opus.xml" . 
  cp "${tmp_dir}/package.zip" opus.zip
  echo 
  echo "Files 'opus.xml' and 'opus.zip' written to `pwd`"
  echo
  exit 1 
fi

## header="Content-Type: application/zip"

echo
echo ${curl} --verbose --header "Content-Type: application/zip" --header "Content-Disposition: filename=package.zip" --header "Content-MD5: ${MD5}" --data-binary "@${tmp_dir}/package.zip" -u "${user}:***" "${opus4_host}/${opus4_instance}/sword/deposit"
${curl} --verbose --header "Content-Type: application/zip" --header "Content-Disposition: filename=package.zip" --header "Content-MD5: ${MD5}" --data-binary "@${tmp_dir}/package.zip" -u "${user}:${pw}" "${opus4_host}/${opus4_instance}/sword/deposit"
```

## Eingebettete XSLT-Skripte

Das folgende XSLT-Skript wandelt das NISO JATS-Format in das OPUS 4-Importformat um:

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

Folgendes XSLT-Skript dient dazu, weitere (Binär-)Dateien zu einem OPUS 4-Paket
hinzuzufügen:

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
