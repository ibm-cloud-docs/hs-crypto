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

# Regiões e locais
{: #regions}

É possível conectar seus aplicativos ao {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} especificando um terminal em serviço regional.
{: shortdesc}

<!-- ## Available regions
{: #regions}

{{site.data.keyword.hscrypto}} is available in the following regions and locations: -->


## Terminais de serviço
{: #endpoints}

Se você estiver gerenciando seus recursos do {{site.data.keyword.hscrypto}} programaticamente, consulte a tabela a seguir para determinar os terminais de API a serem usados ao se conectar à [API do {{site.data.keyword.hscrypto}}](https://cloud.ibm.com/apidocs/hs-crypto):

<table>
    <tr>
        <th>Nome da região</th>
        <th>Localização geográfica</th>
        <th>Serviço de API</th>
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
        <td>Sul dos EUA</td>
        <td>Dallas, EUA</td>
        <td>
            <code>us-south.hs-crypto.cloud.ibm.com</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">Tabela 1. Mostra o terminal disponível para a API do {{site.data.keyword.hscrypto}}</caption>
</table>

<!--For {{site.data.keyword.hscrypto}} service instances that exist within a Cloud Foundry org or space, use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} API.
{: tip}-->

Para obter mais informações sobre a autenticação com o {{site.data.keyword.hscrypto}}, veja [Acessando a API](/docs/services/hs-crypto/access-api.html).
