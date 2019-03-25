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

# Régions et emplacements
{: #regions}

Vous pouvez connecter vos applications à {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} en indiquant un point d'extrémité de service régional.
{: shortdesc}

<!-- ## Available regions
{: #regions}

{{site.data.keyword.hscrypto}} is available in the following regions and locations: -->


## Points d'extrémité de service
{: #endpoints}

Si vous gérez vos ressources {{site.data.keyword.hscrypto}} programmatiquement, reportez-vous au tableau suivant pour déterminer les points d'extrémité d'API à utiliser lorsque vous vous connectez à l'[API {{site.data.keyword.hscrypto}}](https://cloud.ibm.com/apidocs/hs-crypto) :

<table>
    <tr>
        <th>Nom de région</th>
        <th>Emplacement géographique</th>
        <th>Point d'extrémité d'API de service</th>
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
        <td>Sud des Etats-Unis</td>
        <td>Dallas, US</td>
        <td>
            <code>us-south.hs-crypto.cloud.ibm.com</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">Tableau 1. Montre les points d'extrémité disponibles pour l'API {{site.data.keyword.hscrypto}}</caption>
</table>

<!--For {{site.data.keyword.hscrypto}} service instances that exist within a Cloud Foundry org or space, use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} API.
{: tip}-->

Pour plus d'informations sur l'authentification auprès de {{site.data.keyword.hscrypto}}, voir la rubrique [Accès à l'API](/docs/services/hs-crypto/access-api.html).
