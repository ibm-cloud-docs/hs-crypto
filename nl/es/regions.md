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

# Regiones y ubicaciones
{: #regions}

Conéctese a sus aplicaciones con {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} especificando un punto final de servicio regional.
{: shortdesc}

<!-- ## Available regions
{: #regions}

{{site.data.keyword.hscrypto}} is available in the following regions and locations: -->


## Puntos finales de servicio
{: #endpoints}

Si va a gestionar sus recursos de {{site.data.keyword.hscrypto}} mediante programación, consulte la tabla siguiente para determinar los puntos finales de API a utilizar cuando se conecte a la [API de {{site.data.keyword.hscrypto}}](https://cloud.ibm.com/apidocs/hs-crypto):

<table>
    <tr>
        <th>Nombre de región</th>
        <th>Ubicación geográfica</th>
        <th>Punto final de API de servicio</th>
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
        <td>EE.UU. sur</td>
        <td>Dallas, EE.UU.</td>
        <td>
            <code>us-south.hs-crypto.cloud.ibm.com</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">Tabla 1. Muestra el punto final disponible para la API de {{site.data.keyword.hscrypto}}}</caption>
</table>

<!--For {{site.data.keyword.hscrypto}} service instances that exist within a Cloud Foundry org or space, use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} API.
{: tip}-->

Para obtener más información sobre la autenticación con {{site.data.keyword.hscrypto}}, consulte [Acceso a la API](/docs/services/hs-crypto/access-api.html).
