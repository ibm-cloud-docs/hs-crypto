---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: IBM Cloud CLI plug-in, ibmcloud commands, IBM Cloud command-line interface

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Befehlszeilenschnittstelle einrichten
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ist in das {{site.data.keyword.keymanagementservicelong_notm}}-CLI-Plug-in integriert, sodass Sie das {{site.data.keyword.keymanagementservicelong_notm}}-CLI-Plug-in zum Erstellen, Importieren und Verwalten von Verschlüsselungs-Rootschlüsseln und -Standardschlüsseln verwenden können.

- Weitere Informationen zur Verwendung der Befehlszeilenschnittstelle finden Sie in der [Referenzdokumentation zur Befehlszeilenschnittstelle von {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/cli-reference.html).
- Weitere Informationen zum Zugriff auf die CLI finden Sie unter [{{site.data.keyword.keymanagementserviceshort}}-CLI einrichten](/docs/services/key-protect/set-up-cli.html).

Um das {{site.data.keyword.keymanagementserviceshort}}-CLI-Plug-in in einer {{site.data.keyword.hscrypto}}-Instanz verwenden zu können, führen Sie zuerst den folgenden Befehl aus:

```
export KP_PRIVATE_ADDR=<URL>
```
{: pre}

In diesem Befehl ist die *URL* der Endpunkt, der auf der Seite **Verwalten** der Benutzerschnittstelle angezeigt wird. Alternativ können Sie die Endpunkt-URL über die API abrufen. Beispiel:

```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
```
{: pre}

Weitere Informationen finden Sie in der [{{site.data.keyword.hscrypto}}-API-Referenzdokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
