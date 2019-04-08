---

copyright:
years: 2018, 2019
lastupdated: "2019-03-26"

Keywords: root keys, standard keys, migration, transition, beta

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# 베타 서비스 인스턴스에서 키 마이그레이션
{: #migrate-keys}

베타 서비스 인스턴스를 사용하고 관리한 루트 키와 표준 키를 {{site.data.keyword.hscrypto}} 프로덕션 서비스 인스턴스로 마이그레이션하려면 다음 프로시저를 수행해야 합니다.
{: shortdesc}

마스터 키는 암호화 단위에서 추출할 수 없으므로 IBM Cloud 관리자는 마스터 키를 마이그레이션할 수 없습니다. 마스터 키를 사용하여 프로덕션 서비스 인스턴스를 초기화해야 합니다.
{:important}  

## 시작하기 전에
{: #migrate-prerequisites}

1. Hyper Protect Crypto Services 플랜으로 [서비스 인스턴스를 작성](/docs/services/hs-crypto/provision.html)하십시오.

2. Trusted Key Entry 플러그인을 사용하여 [서비스 인스턴스를 초기화](/docs/services/hs-crypto/initialize_hsm.html)하십시오.

## 키 마이그레이션
{: #migrate-keys-steps}  

루트 키와 표준 키를 프로덕션 환경으로 마이그레이션하려면 다음 단계를 완료하십시오.

1. GUI 또는 API를 통해 [루트 키를 가져오십시오](/docs/services/hs-crypto/import-root-keys.html).

  가져온 루트 키를 베타 서비스 인스턴스에서 프로덕션 서비스 인스턴스로 마이그레이션할 수 있습니다.
  {:tip}

2. 데이터 암호화 키(DEK)를 베타 서비스 인스턴스에서 랩핑 해제하고 프로덕션 서비스 인스턴스에서 DEK를 랩핑하십시오.

  1. [invoke-an-action-on-a-key API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: new_window}를 사용하여 베타 서비스 인스턴스에서 [데이터 암호화 키(DEK)를 랩핑 해제하십시오](/docs/services/hs-crypto/unwrap-keys.html).

  2. [invoke-an-action-on-a-key API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key{: new_window})를 사용하여 프로덕션 서비스 인스턴스에서 [DEK를 랩핑하십시오](/docs/services/hs-crypto/wrap-keys.html).

3. 다음 단계를 따라 표준 키를 재작성하십시오.

  1. [retrieve-key-by-id API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/hs-crypto#retrieve-a-key-by-id){: new_window}를 사용하여 [표준 키를 검색하십시오](/docs/services/hs-crypto?topic=hs-crypto-view-keys#retrieve-key-api). 그러면 베타 인스턴스에서 키를 작성하는 데 사용되는 페이로드가 리턴됩니다.

  2. GUI 또는 [create-a-new-key API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/hs-crypto#create-a-new-key){: new_window}를 통해 이전 단계에서 검색된 정보를 사용하여 새 서비스 인스턴스에서 [표준 키를 작성하십시오](/docs/services/hs-crypto/create-standard-keys.html).

## 다음에 수행할 작업
{: #migration-next}

프로그래밍 방식으로 키를 관리하는 방법에 대해 자세히 알아보려면 [{{site.data.keyword.hscrypto}} API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")를 확인하십시오](https://{DomainName}/apidocs/hs-crypto){: new_window}.
