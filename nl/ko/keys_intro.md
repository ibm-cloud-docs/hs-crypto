---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: root keys, master keys, standard keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# 키 소개
{: #introduce-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}는 루트 키, 표준 키 및 마스터 키를 포함하여 여러 키 유형을 지원합니다.
{:shortdesc}

## 루트 키

*루트 키*는 {{site.data.keyword.hscrypto}}에서 완전히 관리하는 대칭 키-랩핑 키입니다. 루트 키를 사용하여 고급 암호화를 통해 다른 암호화 키를 보호할 수 있습니다. 자세히 알아보려면 <a href="/docs/services/key-protect/concepts/envelope-encryption.html">엔벨로프 암호화</a>를 참조하십시오.

[키 관리](/docs/services/hs-crypto/index.html#manage-keys)의 단계에 따라 루트 키를 관리할 수 있습니다.

## 표준 키

*표준 키*는 암호화에 사용되는 대칭 키입니다. 표준 키를 사용하여 데이터를 직접 암호화하고 복호화할 수 있습니다.

[키 관리](/docs/services/hs-crypto/index.html#manage-keys)의 단계에 따라 표준 키를 관리할 수 있습니다.

## 마스터 키

*마스터 키*는 루트 키 및 표준 키를 암호화 처리하고 관리하는 암호화 인스턴스(HSM)를 암호화하는 데 사용됩니다. 마스터 키가 있으면 루트 키 및 표준 키를 포함하여 키의 전체 체인을 암호화하는 신뢰점을 소유합니다.

암호화 인스턴스(HSM)에 대해 설정된 엔드-투-엔드 보안 채널로 인해 {{site.data.keyword.hscrypto}} 인스턴스의 관리자만 마스터 키를 설정하고 관리할 수 있습니다. IBM에서는 마스터 키를 백업하거나 수정하지 않으며 마스터 키를 복사하거나 다른 시스템 또는 데이터 센터에 복원할 방법이 없습니다.

하나의 암호화 인스턴스(HSM)에는 하나의 마스터 키만 있을 수 있습니다. {{site.data.keyword.hscrypto}} 인스턴스의 마스터 키를 삭제하면 서비스에서 관리되는 키로 암호화된 모든 데이터의 암호를 효과적으로 제거할 수 있습니다.

[키 스토리지를 보호하기 위해 암호화 인스턴스를 초기화](/docs/services/hs-crypto/initialize_hsm.html)할 때 마스터 키를 관리할 수 있습니다.

현재 단계에서는 마스터 키 순환이 지원되지 않습니다.
{:important}
