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

# Regionen und Standorte
{: #regions}

Sie können Ihre Anwendungen mit {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} verbinden, indem Sie einen regionalen Serviceendpunkt angeben.
{: shortdesc}

<!-- ## Available regions
{: #regions}

{{site.data.keyword.hscrypto}} is available in the following regions and locations: -->


## Serviceendpunkte
{: #endpoints}

Wenn Sie Ihre {{site.data.keyword.hscrypto}}-Ressourcen programmgesteuert verwalten, können Sie mithilfe der folgenden Tabelle die API-Endpunkte bestimmen, die für die Verbindung zur [{{site.data.keyword.hscrypto}}-API](https://cloud.ibm.com/apidocs/hs-crypto) verwendet werden:

<table>
    <tr>
        <th>Regionsname</th>
        <th>Standort</th>
        <th>Service-API-Endpunkt</th>
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
        <td>Vereinigte Staaten (Süden)</td>
        <td>Dallas, USA</td>
        <td>
            <code>us-south.hs-crypto.cloud.ibm.com</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">Tabelle 1. Verfügbarer Endpunkt für die {{site.data.keyword.hscrypto}}}-API</caption>
</table>

<!--For {{site.data.keyword.hscrypto}} service instances that exist within a Cloud Foundry org or space, use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} API.
{: tip}-->

Weitere Informationen zur Authentifizierung mit {{site.data.keyword.hscrypto}} finden Sie in [Auf die API zugreifen](/docs/services/hs-crypto/access-api.html).
