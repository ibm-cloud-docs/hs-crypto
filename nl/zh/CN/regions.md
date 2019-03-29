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

# 区域和位置
{: #regions}

您可以通过指定区域服务端点来连接应用程序和 {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}。
{: shortdesc}

<!-- ## Available regions
{: #regions}

{{site.data.keyword.hscrypto}} is available in the following regions and locations: -->


## 服务端点
{: #endpoints}

如果是以编程方式管理 {{site.data.keyword.hscrypto}} 资源，请参阅下表以确定连接到 [{{site.data.keyword.hscrypto}} API](https://cloud.ibm.com/apidocs/hs-crypto) 时要使用的 API 端点：

<table>
    <tr>
        <th>区域名称</th>
        <th>地理位置
</th>
        <th>服务 API 端点</th>
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
        <td>美国南部</td>
        <td>美国达拉斯</td>
        <td>
            <code>us-south.hs-crypto.cloud.ibm.com</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">表 1. 显示 {{site.data.keyword.hscrypto}} API 的可用端点</caption>
</table>

<!--For {{site.data.keyword.hscrypto}} service instances that exist within a Cloud Foundry org or space, use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} API.
{: tip}-->

有关向 {{site.data.keyword.hscrypto}} 进行认证的更多信息，请参阅[访问 API](/docs/services/hs-crypto/access-api.html)。
