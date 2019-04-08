---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: regional service endpoint, Hyper Protect Crypto Services resources, API endpoints

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Regioni e ubicazioni
{: #regions}

Puoi connettere le tue applicazioni con {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} specificando un endpoint del servizio regionale.
{: shortdesc}

<!-- ## Available regions
{: #available-regions}

{{site.data.keyword.hscrypto}} is available in the following regions and locations: -->


## Endpoint del servizio
{: #endpoints}

Se stai gestendo le tue risorse {{site.data.keyword.hscrypto}} in modo programmatico, vedi la seguente tabella per determinare gli endpoint API da utilizzare quando ti connetti all'API [{{site.data.keyword.hscrypto}}](https://{DomainName}/apidocs/hs-crypto):

<table>
    <tr>
        <th>Nome regione</th>
        <th>Ubicazione geografica</th>
        <th>Endpoint API del servizio</th>
    </tr>
  <!--
    <tr>
        <td>Germany</td>
        <td>Frankfurt, Germany</td>
        <td>
            <code></code>
        </td>
    </tr>
    <tr>
        <td>Sydney</td>
        <td>Sydney, Australia</td>
        <td>
            <code></code>
        </td>
    </tr>
    <tr>
        <td>United Kingdom</td>
        <td>London, England</td>
        <td>
            <code></code>
        </td>
    </tr>
    <tr>
        <td>US East</td>
        <td>Washington D.C., US</td>
        <td>
            <code></code>
        </td>
    </tr> -->
    <tr>
        <td>Stati Uniti Sud</td>
        <td>Dallas, USA</td>
        <td>
            <code>us-south.hs-crypto.cloud.ibm.com</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">Tabella 1. Mostra l'endpoint disponibile per l'API {{site.data.keyword.hscrypto}}}</caption>
</table>

<!--For {{site.data.keyword.hscrypto}} service instances that exist within a Cloud Foundry org or space, use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} API.
{: tip}-->

Per ulteriori informazioni sull'autenticazione con {{site.data.keyword.hscrypto}}, vedi [Accesso all'API](/docs/services/hs-crypto/access-api.html).
