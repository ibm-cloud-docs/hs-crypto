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

# 地區及位置
{: #regions}

您可以指定地區服務端點，將應用程式與 {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} 連接。
{: shortdesc}

<!-- ## Available regions
{: #available-regions}

{{site.data.keyword.hscrypto}} is available in the following regions and locations: -->


## 服務端點
{: #endpoints}

如果您要以程式設計方式管理 {{site.data.keyword.hscrypto}} 資源，請參閱下表，以決定要在連接至 [{{site.data.keyword.hscrypto}} API](https://{DomainName}/apidocs/hs-crypto) 時使用的 API 端點：

<table>
    <tr>
        <th>地區名稱</th>
        <th>地理位置</th>
        <th>服務 API 端點</th>
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
        <td>美國南部</td>
        <td>美國達拉斯</td>
        <td>
            <code>us-south.hs-crypto.cloud.ibm.com</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">表 1. 顯示 {{site.data.keyword.hscrypto}} API 的可用端點</caption>
</table>

<!--For {{site.data.keyword.hscrypto}} service instances that exist within a Cloud Foundry org or space, use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} API.
{: tip}-->

如需向 {{site.data.keyword.hscrypto}} 進行鑑別的相關資訊，請參閱[存取 API](/docs/services/hs-crypto/access-api.html)。
