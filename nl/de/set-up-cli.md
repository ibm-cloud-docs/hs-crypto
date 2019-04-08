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

# Auf die {{site.data.keyword.keymanagementserviceshort}}-CLI in einer {{site.data.keyword.hscrypto}}-Instanz zugreifen
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ist in das {{site.data.keyword.keymanagementservicelong_notm}}-CLI-Plug-in integriert, sodass Sie das {{site.data.keyword.keymanagementservicelong_notm}}-CLI-Plug-in zum Erstellen, Importieren und Verwalten von Verschlüsselungs-Rootschlüsseln und -Standardschlüsseln verwenden können.

Bevor Sie das Plug-in für die {{site.data.keyword.keymanagementserviceshort}}-CLI in einer {{site.data.keyword.hscrypto}}-Instanz (kurz: Serviceinstanz) verwenden können, müssen Sie die Umgebungsvariable KP_KP_PRIVATE_ADDR auf Ihrer Workstation definieren: 

* Führen Sie unter Linux oder MacOS den folgenden Befehl aus: 

  ```
  export KP_PRIVATE_ADDR=<URL>
  ```
  {: pre}

  In diesem Befehl ist *URL* der Endpunkt, der auf der Registerkarte **Verwalten** Ihres bereitgestellten {{site.data.keyword.hscrypto}}-Dashboards angezeigt wird. Beispiel:

  ```
  export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
  ```
  {: pre}

* Unter Windows geben Sie in der **Systemsteuerung** in das Suchfeld `Umgebungsvariable` ein, um das Fenster für Umgebungsvariablen zu finden. Erstellen Sie eine Umgebungsvariable KP_PRIVATE_ADDR und setzen Sie den Wert auf den Endpunkt, der auf der Registerkarte **Verwalten** Ihres bereitgestellten {{site.data.keyword.hscrypto}}-Dashboards angezeigt wird. Beispiel: `https://us-south.hs-crypto.cloud.ibm.com:<port>`.

Sie können die Endpunkt-URL auch über die API abrufen. Weitere Details [finden Sie in der {{site.data.keyword.hscrypto}}-API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto){: new_window}. 

- Weitere Informationen zur Verwendung der Befehlszeilenschnittstelle finden Sie in der [Referenzdokumentation zur Befehlszeilenschnittstelle von {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/cli-reference.html).
- Weitere Informationen zum Zugriff auf die CLI finden Sie unter [{{site.data.keyword.keymanagementserviceshort}}-CLI einrichten](/docs/services/key-protect/set-up-cli.html).
