---
title: SWORD
---

# SWORD 

OPUS 4.6 implementiert die SWORD Schnittstelle in Version 1.3.  Die Details der Spezifikation 
sind unter folgender Adresse verfügbar:

<http://swordapp.org/sword-v1/>

<p class="info">
Es gibt momentan keine Pläne, den Funktionsumfang von SWORD 2 für OPUS 4 umzusetzen.  Die 
Import Funktionen an sich werden weiter ausgebaut werden, um mehr Metadaten einfacher 
verarbeiten zu können, zum Beispiel Verknüpfungen mit Klassifikationssystem usw.
</p>


## Schnittstelle

Das SWORD Service Dokument kann unter der URL

```
https://user:password@[OPUS4-Servername]/[OPUS4-Instanz]/sword/servicedocument
```

abgerufen werden.

<p class="waring">
Das voreingestellte SWORD Service Dokument enthält (unter `<collection href="...">` eine 
falsche Deposit Adresse.  Die korrekte Angabe, die in `href="..."` stehen sollte, lautet:

```
https://user@password@[OPUS4-Servername]/[OPUS4-Instanz]/sword/deposit
```
</p>


## Besonderheiten

Die SWORD Schnittstelle verarbeitet normalerweise mit jedem Request nur *ein* Dokument.  Die 
Antworten der SWORD Schnittstelle sind gemäß der Spezifikation sind nur auf einzele Dokumente 
ausgelegt.  Die SWORD Schnittstelle von OPUS 4 kann zusätzliche Pakete mit **mehreren** 
Dokumenten verarbeiten.  Ein ZIP/TAR-Paket kann die Metadaten und Dateien für mehr als ein 
Dokument enthalten. 


## Konfiguration

Die importierten Dokumente werden mit einer konfigurierbaren Sammlung verknüpft, um sie 
zusätzliche zu markieren. Die Sammlung heißt normalerweise "Import" und ist Teil der 
CollectionRole "Import".  Beide werden bei der Installation bzw. beim Update von OPUS 4 
automatisch angelegt.


## Zugriff

Für Zugriff auf das SWORD Modul muss sich der Client über HTTP Basic Authentication 
identifizieren.  Dafür muss in der Administration ein Account angelegt werden, der 
Zugriff auf das SWORD Modul hat.  Der Nutzername und das Passwort dieses Accounts 
können dann für die Authentifizierung verwendet werden. 

Es wird empfohlen, einen Account zu verwenden, der nur Zugriff auf das SWORD-Modul hat. 

Außerdem macht es Sinn, für jede Datenquelle, zum Beispiel das 
[DeepGreen Projekt](https://deepgreen.kobv.de), einen separaten Account 
einzurichten.  So kann später leicht festgestellt werden, woher ein Dokument 
gekommen ist. 

<p class="warning">
Der Verbindung zum Server sollte über HTTPS erfolgen, damit der Nutzername und das 
Passwort nicht unverschlüsselt übertragen werden. 
</p> 


## Beispiel Skript

Es gibt keinen Standard-Client für den Zugriff auf die SWORD Schnittstelle. 

Ein Beispiel für ein BASH Skript, das eine ZIP Datei, die genau *eine* XML Metadaten 
Datei im NISO JATS Format enthält, in eine ZIP Datei mit einer OPUS4 Import-XML umwandelt
und als Request (via `curl`) an die SWORD Schnittstelle einer OPUS4 Instanz schickt:

<p class="info">
Die Umwandlung des NISO JATS Formats in das benötigte OPUS 4 Format durchführen zu 
können, werden weitere Dateien benötigt! 

Das BASH Skript verwendet für die Transformation NISO JATS ---> OPUS 4 zwei XSLT Dateien, 
die im selben Verzeichnis wie das BASH Skript gespeichert sein sollten.  Zu finden 
sind diese XSLT Dateien unter 

* [OPUS 4 Pakete](packages.html)
{: class="navlist" }

</p>


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


