---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

Keywords: release note, new

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 새로운 기능
{: #what-new}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}에 사용 가능한 새 기능을 최신 상태로 유지하십시오.
{: shortdesc}

## 2019년 3월
{: #March-2019}

### {{site.data.keyword.hscrypto}}가 GA(Generally Available)됨
신규 기준일: 2019년 3월 29일

{{site.data.keyword.hscrypto}} 오퍼링에 대한 자세한 정보는 [{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 홈 페이지 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/cloud/hyper-protect-crypto){:new_window}를 참조하십시오.

### 고가용성 및 재해 복구
신규 기준일: 2019년 3월 29일

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}는 애플리케이션을 안전하고 작동 가능한 상태로 유지하는 데 도움이 되는 자동 기능을 갖춘 고가용성의 지역 서비스입니다.

{{site.data.keyword.hscrypto}} 요청이 처리되는 지리적 영역을 나타내는 지원되는 [{{site.data.keyword.cloud_notm}} 지역](/docs/services/hs-crypto/regions.html)에서 {{site.data.keyword.hscrypto}} 리소스를 작성할 수 있습니다. 지역에 대한 로컬 액세스, 짧은 대기 시간 및 보안 요구사항을 충족하기 위해 각 {{site.data.keyword.cloud_notm}} 지역에는 [여러 가용성 구역 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/)이 포함되어 있습니다.

자세한 정보는 [고가용성 및 재해 복구](/docs/services/hs-crypto/ha-dr.html)를 참조하십시오.

## 2019년 2월
{: #Feb-2019}

### {{site.data.keyword.hscrypto}} 베타가 사용 가능함
신규 기준일: 2019년 2월 5일

{{site.data.keyword.hscrypto}} 베타 버전이 릴리스되었습니다. 이제 직접 **카탈로그** > **보안 및 ID**를 통해 {{site.data.keyword.hscrypto}} 서비스에 액세스할 수 있습니다.

2019년 2월 5일부터 새 Hyper Protect Crypto Services 시범 인스턴스를 더 이상 프로비저닝할 수 없습니다. 기존 인스턴스는 시범 지원 날짜(2019년 3월 5일) 종료 시까지 지원됩니다.

## 2018년 12월
{: #Dec-2018}

### 추가됨: KYOK를 사용한 HSM 관리에 대한 지원
신규 기준일: 2018년 12월 19일

이제 {{site.data.keyword.hscrypto}}는 보존, 제어 및 관리할 수 있는 암호화 키를 사용하여 데이터에 대한 제어 및 권한을 더 강화할 수 있도록 KYOK(Keep Your Own Key)를 지원합니다. {{site.data.keyword.cloud}} 명령행 인터페이스(CLI)를 사용하여 암호화 인스턴스(HSM)를 초기화하고 관리할 수 있습니다.

자세한 정보는 [키 스토리지를 보호하기 위해 암호화 인스턴스 초기화](/docs/services/hs-crypto/initialize_hsm.html)를 참조하십시오.

### 추가됨: {{site.data.keyword.keymanagementserviceshort}} API 통합
신규 기준일: 2018년 12월 19일

이제 키를 생성하고 보호하기 위해 {{site.data.keyword.keymanagementserviceshort}} API가 Hyper Protect Crypto Services와 통합됩니다. {{site.data.keyword.hscrypto}}를 통해 직접 {{site.data.keyword.keymanagementserviceshort}} API를 호출할 수 있습니다.

자세한 정보는 [API에 액세스](/docs/services/hs-crypto/access-api.html) 및 [{{site.data.keyword.hscrypto}} API ![외부 링크 아이콘](image/external_link.svg "외부 링크 아이콘")](https://cloud.ibm.com/apidocs/hs-crypto){:new_window}를 참조하십시오.

### 더 이상 사용되지 않음: ACSP를 통해 {{site.data.keyword.hscrypto}}에 액세스하는 기능
신규 기준일: 2018년 12월 19일

현재 단계에서 ACSP(Advanced Cryptography Service Provider) 클라이언트를 통한 {{site.data.keyword.hscrypto}} 액세스는 더 이상 지원되지 않습니다. 이전 서비스 인스턴스를 사용 중인 경우 여전히 ACSP를 사용하여 {{site.data.keyword.hscrypto}}를 탐색할 수 있습니다.
