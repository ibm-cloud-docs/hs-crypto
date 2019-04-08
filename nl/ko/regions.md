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

# 지역 및 위치
{: #regions}

지역 서비스 엔드포인트를 지정하여 애플리케이션을 {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}와 연결할 수 있습니다.
{: shortdesc}

<!-- ## Available regions
{: #available-regions}

{{site.data.keyword.hscrypto}} is available in the following regions and locations: -->


## 서비스 엔드포인트
{: #endpoints}

{{site.data.keyword.hscrypto}} 리소스를 프로그래밍 방식으로 관리하는 경우 [{{site.data.keyword.hscrypto}} API](https://{DomainName}/apidocs/hs-crypto)에 연결할 때 사용할 API 엔드포인트를 판별하려면 다음 표를 확인하십시오.

<table>
    <tr>
        <th>지역 이름</th>
        <th>지리적 위치</th>
        <th>서비스 API 엔드포인트</th>
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
        <td>미국 남부</td>
        <td>댈러스, 미국</td>
        <td>
            <code>us-south.hs-crypto.cloud.ibm.com</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">표 1. {{site.data.keyword.hscrypto}} API에 사용 가능한 엔드포인트를 보여줍니다.</caption>
</table>

<!--For {{site.data.keyword.hscrypto}} service instances that exist within a Cloud Foundry org or space, use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} API.
{: tip}-->

{{site.data.keyword.hscrypto}} 인증에 대한 자세한 정보는 [API에 액세스](/docs/services/hs-crypto/access-api.html)를 참조하십시오.
