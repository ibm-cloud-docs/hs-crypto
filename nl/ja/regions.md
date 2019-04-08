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

# 地域とロケーション
{: #regions}

地域のサービス・エンドポイントを指定することによって、アプリケーションを {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} に接続できます。
{: shortdesc}

<!-- ## Available regions
{: #available-regions}

{{site.data.keyword.hscrypto}} is available in the following regions and locations: -->


## サービス・エンドポイント
{: #endpoints}

{{site.data.keyword.hscrypto}} リソースをプログラムで管理している場合は、次の表を参照して、[{{site.data.keyword.hscrypto}} API](https://{DomainName}/apidocs/hs-crypto) への接続時に使用する API エンドポイントを判断してください。

<table>
    <tr>
        <th>地域名</th>
        <th>地理的位置</th>
        <th>サービス API エンドポイント</th>
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
        <td>米国南部</td>
        <td>米国のダラス</td>
        <td>
            <code>us-south.hs-crypto.cloud.ibm.com</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">表 1. {{site.data.keyword.hscrypto}} API の使用可能なエンドポイント</caption>
</table>

<!--For {{site.data.keyword.hscrypto}} service instances that exist within a Cloud Foundry org or space, use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} API.
{: tip}-->

{{site.data.keyword.hscrypto}} での認証について詳しくは、[API へのアクセス](/docs/services/hs-crypto/access-api.html)を参照してください。
