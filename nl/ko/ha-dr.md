---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: disaster recovery, High availability, HA, DR

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 고가용성 및 재해 복구
{: #ha-dr}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}는 애플리케이션을 안전하고 작동 가능한 상태로 유지하는 데 도움이 되는 자동 기능을 갖춘 고가용성의 지역 서비스입니다.
{: shortdesc}

이 페이지를 사용하여 {{site.data.keyword.hscrypto}}의 가용성 및 재해 복구 전략에 대해 자세히 알아볼 수 있습니다.

## 위치, 테넌시 및 가용성
{: #availability}

{{site.data.keyword.hscrypto}}는 멀티 테넌트 지역 서비스입니다.

{{site.data.keyword.hscrypto}} 요청이 처리되는 지리적 영역을 나타내는 지원되는 [{{site.data.keyword.cloud_notm}} 지역](/docs/services/hs-crypto/regions.html) 중 하나에서 {{site.data.keyword.hscrypto}} 리소스를 작성할 수 있습니다. 지역에 대한 로컬 액세스, 짧은 대기 시간 및 보안 요구사항을 충족하기 위해 각 {{site.data.keyword.cloud_notm}} 지역에는 [여러 가용성 구역 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/)이 포함되어 있습니다.

{{site.data.keyword.cloud_notm}}에서 저장 데이터 암호화 전략을 계획할 때 가장 가까운 지역에서 {{site.data.keyword.hscrypto}}를 프로비저닝하면 {{site.data.keyword.hscrypto}} API와 상호작용할 때 더 빠르고 신뢰할 수 있는 연결이 발생할 가능성이 높아집니다. {{site.data.keyword.hscrypto}} 리소스에 의존하는 사용자, 앱 또는 서비스가 지리적으로 집중되어 있는 경우 특정 지역을 선택하십시오. 지역에서 멀리 떨어진 사용자 및 서비스는 더 높은 대기 시간을 경험할 수 있습니다.

암호화 키는 이를 작성한 지역으로 한정됩니다. {{site.data.keyword.hscrypto}}는 암호화 키를 복사하거나 다른 지역으로 내보내지 않습니다.
{: note}

## 재해 복구
{: #disaster-recovery}

{{site.data.keyword.hscrypto}}에는 RTO(Recovery Time Objective)가 1시간인 재해 복구 기능이 있습니다. 이 서비스는 계획 및 재해 이벤트로부터의 복구를 위해 {{site.data.keyword.cloud_notm}} 요구사항을 따릅니다. 자세한 정보는 [재해 복구](/docs/overview/zero_downtime.html#disaster-recovery)를 참조하십시오.
