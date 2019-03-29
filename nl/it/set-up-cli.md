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

# Configurazione della CLI
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} è integrato con il plug-in della CLI {{site.data.keyword.keymanagementservicelong_notm}}, per cui puoi utilizzare il plug-in della CLI {{site.data.keyword.keymanagementservicelong_notm}} per creare, importare e gestire le chiavi root e le chiavi standard di crittografia.

- Per ulteriori informazioni sull'utilizzo della CLI, consulta la [documentazione di riferimento della CLI {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/cli-reference.html).
- Per ulteriori informazioni sull'accesso alla CLI, consulta [Configurazione della CLI {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/set-up-cli.html).

Prima di poter utilizzare il plug-in della CLI {{site.data.keyword.keymanagementserviceshort}} su un'istanza {{site.data.keyword.hscrypto}}, immetti il seguente comando:

```
export KP_PRIVATE_ADDR=<URL>
```
{: pre}

In questo comando, l'*URL* è l'endpoint che viene visualizzato nella pagina **Manage** dell'interfaccia utente. In alternativa, puoi richiamare l'URL endpoint tramite l'API. Ad esempio:

```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
```
{: pre}

Per i dettagli, [consulta la documentazione di riferimento API {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
