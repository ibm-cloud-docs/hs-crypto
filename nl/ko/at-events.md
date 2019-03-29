---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: Activity Tracker events, List of events

subcollection: hs-crypto

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.cloudaccesstrailshort}} 이벤트
{: #at-events}

사용자 및 애플리케이션이 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}와 상호작용하는 방법을 추적하려면 {{site.data.keyword.cloudaccesstrailfull}} 서비스를 사용하십시오.
{: shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 서비스는 {{site.data.keyword.cloud_notm}}에 있는 서비스의 상태를 변경하는 사용자 시작 활동을 기록합니다.

자세한 정보는 [{{site.data.keyword.cloudaccesstrailshort}} 문서](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla)를 참조하십시오.

## 이벤트 목록
{: #events}

다음 표에는 이벤트를 생성하는 조치가 나열되어 있습니다.

<table>
    <tr>
        <th>조치</th>
        <th>설명</th>
    </tr>
    <tr>
        <td>hs-crypto.secrets.create</td>
        <td>키 작성</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.read</td>
        <td>ID별로 키 검색</td>
    </tr>
   <tr>
        <td>hs-crypto.secrets.delete</td>
        <td>ID별로 키 삭제</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.list</td>
        <td>키 목록 검색</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.head</td>
        <td>키의 수 검색</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.wrap</td>
        <td>키 랩핑</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.unwrap</td>
        <td>키 랩핑 해제</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.rotate</td>
        <td>키 순환</td>
    </tr>
    <caption style="caption-side:bottom;">표 1. {{site.data.keyword.cloudaccesstrailfull_notm}} 이벤트를 생성하는 조치</caption>
</table>

## 이벤트 확인 위치
{: #gui}

<!-- Option 2: Add the following sentence if your service sends events to the account domain. -->

{{site.data.keyword.cloudaccesstrailshort}} 이벤트는 이벤트가 생성된 {{site.data.keyword.cloud_notm}} 지역에서 사용 가능한 {{site.data.keyword.cloudaccesstrailshort}} **계정 도메인**에서 사용할 수 있습니다.

예를 들어, {{site.data.keyword.hscrypto}}에서 키 작성, 가져오기, 삭제 또는 읽기를 수행할 때 {{site.data.keyword.cloudaccesstrailshort}} 이벤트가 생성됩니다. 이러한 이벤트는 {{site.data.keyword.hscrypto}} 서비스가 프로비저닝된 지역과 동일한 지역의 {{site.data.keyword.cloudaccesstrailshort}} 서비스에 자동으로 전달됩니다.

API 활동을 모니터하려면 {{site.data.keyword.hscrypto}} 서비스가 프로비저닝된 지역과 동일한 지역에서 사용 가능한 영역에 {{site.data.keyword.cloudaccesstrailshort}} 서비스를 프로비저닝해야 합니다. 그런 다음, Lite 플랜이 있는 경우 {{site.data.keyword.cloudaccesstrailshort}} UI에서 계정 보기를 통해 이벤트를 보고 프리미엄 플랜이 있는 경우 Kibana를 통해 이벤트를 볼 수 있습니다.

## 추가 정보
{: #info}

암호화 키에 대한 정보의 민감도로 인해 {{site.data.keyword.hscrypto}}에 대한 API 호출의 결과로 이벤트가 생성될 때 생성된 이벤트에는 키에 대한 자세한 정보가 포함되지 않습니다. 이 이벤트에는 클라우드 환경에서 내부적으로 키를 식별하는 데 사용할 수 있는 상관 ID가 포함됩니다. 상관 ID는 `responseHeader.content` 필드의 일부로 리턴되는 필드입니다. 이 정보를 사용하여 {{site.data.keyword.cloudaccesstrailshort}} 이벤트를 통해 보고되는 조치의 정보와 {{site.data.keyword.hscrypto}} 키를 상관시킬 수 있습니다.
