---

copyright:
  years: 2018, 2019
lastupdated: "2019-33-22"

Keywords: frequently asked questions, critical security parameters, cryptographic module, Security Level

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# FAQ
{: #faqs}

다음 FAQ를 사용하여 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}에 대한 도움을 받을 수 있습니다.

## HSM 인증
{: #HSM-certifications}

### IBM Crypto Card(HSM)가 FIPS 140-2 레벨 4를 충족하는 것으로 유효성 검증되었는지 어떻게 확인할 수 있습니까?
{: #FIPS-L4}

FIPS 140-2 레벨 4는 마켓플레이스에서 널리 사용되지 않는 매우 높은 보호 레벨입니다. IBM은 최고 레벨의 인증된 HSM을 제공하는 선도적인 공급업체이며 모든 차세대 카드에 대한 이러한 유효성 검증을 유지하기 위해 크게 투자해 왔습니다. 상위 레벨의 보증에 대한 요구사항은 정부 요구사항에서 수집되었습니다. 인증은 NIST 홈 페이지에 공개되어 있으므로 인증의 유효성을 검증하려면 이 페이지로 이동합니다.

### FIPS 140-2 레벨 2, 3 및 레벨 4의 차이점은 무엇입니까?
{: #FIPS-levels}

* FIPS 140-2 레벨 2: 이동식 덮개 및 도어에서 봉인, 열림 방지 잠금으로 수행되는 잠금 변조 증거에 대한 요구사항입니다. 모듈 내의 일반 텍스트 암호화 키 및 핵심 보안 매개변수(CSP)에 물리적으로 액세스하려면 코팅 또는 봉인을 제거해야 하도록 변조 증거 코팅 또는 봉인이 암호화 모듈에 배치됩니다. 보안 레벨 2에는 최소한 역할 기반 인증이 필요합니다. 역할 기반 인증에서는 암호화 모듈이 특정 역할을 수행하고 해당 서비스 세트를 수행할 수 있도록 운영자의 권한을 인증합니다.
 
* FIPS 140-2 레벨 3: 보안 레벨 3에서 필요한 물리적 보안 메커니즘은 암호화 모듈의 물리적 액세스, 사용 또는 수정 시도를 발견하고 응답할 가능성이 높이기 위한 것입니다. 보안 레벨 3에는 ID 기반 인증 메커니즘이 필요하며, 보안 레벨 2에 대해 지정된 역할 기반 인증 메커니즘에서 제공되는 보안을 강화합니다.

* FIPS 140-2 레벨 4: 이 보안 레벨에서 물리적 보안 메커니즘은 물리적 액세스 시 권한 없는 모든 시도를 발견하고 이에 응답할 목적으로 암호화 모듈 주위에 완벽한 보호 엔벨로프를 제공합니다. 어떠한 방향에서든 암호화 모듈 엔클로저를 침투하면 발견된 가능성이 매우 높고 모든 일반 텍스트 핵심 보안 매개변수(CSP)가 즉시 제로화됩니다. 보안 레벨 4 암호화 모듈은 물리적으로 보호되지 않은 환경에서 작동하는 데 유용합니다. 또한 보안 레벨 4는 모듈의 전압 및 온도가 정상 작동 범위를 벗어나는 환경 조건 또는 변동으로 인한 보안 위협으로부터 암호화 모듈을 보호합니다. 공격자가 암호화 모듈의 방어를 저지하기 위해 의도적으로 정상 작동 범위를 벗어날 수 있습니다.

## 키 관리
{: #key-management}

### {{site.data.keyword.hscrypto}}를 {{site.data.keyword.keymanagementserviceshort}} 서비스와 결합하여 사용할 수 있습니까?

 {{site.data.keyword.hscrypto}}는 Key Protect와 동일한 사용자 경험을 가지는 완전히 호환 가능한 {{site.data.keyword.keymanagementserviceshort}} API와 함께 제공되는 관리 암호화 서비스입니다. 주요 차이점은 {{site.data.keyword.hscrypto}}가 FIPS 140-2 레벨 4로 인증된 HSM에 의존한다는 점입니다. 또한 고객이 관리하는 HSM 마스터 키를 통해 완벽한 제어를 제공합니다(KYOK). {{site.data.keyword.keymanagementserviceshort}}에 대한 멀티 테넌트 설정과 비교하여 인스턴스별로 전용 서비스가 제공됩니다. 또한 {{site.data.keyword.hscrypto}}는 서명/확인, 키 생성, 암호화 해싱, 암호화/복호화 및 랩핑/랩핑 해제와 같은 암호화 오퍼레이션에 대한 HSM 기능을 제공합니다.

### 키 이름의 길이는 얼마입니까?
{: #key_names}

최대 50자 길이의 키 이름을 사용할 수 있습니다.

### 언어 문자를 키 이름의 일부로 사용할 수 있습니까?
{: #key_chars}

언어 문자(예: 중국어 문자)는 키 이름의 일부로 사용할 수 없습니다.

### 키를 삭제하면 어떻게 됩니까?
{: #key_destruction}

키를 삭제하면 해당 컨텐츠 및 연관된 데이터가 영구 삭제됩니다. 키로 암호화된 데이터에 더 이상 액세스할 수 없습니다.

키를 삭제하기 전에 키와 연관된 데이터에 더 이상 액세스할 필요가 없는지 확인하십시오.

<!-- ## Pricing
{: #pricing}

### Where can I find the detailed pricing information?
{: #pricing_info}

You can refer to the **Pricing** tab on the [{{site.data.keyword.hscrypto}} home page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/hyper-protect-crypto){: new_window} for details.

### Is there a pricing example I can refer to?
{: #pricing_example}

Here is one. If you have a requirement of 5000 keys to be crypto-processed, for high availability, you need to set up two crypto units. The amount is $3140 ($1570 per crypto unit) per month. The first 1,000,000 API calls are free of charge. However, if you perform 2,000,000 API calls per month, you will be charged additional $1 ($0.01 per 10,000 API calls over 1,000,000 API calls). In total, there will be a monthly charge of $3141 ($3140 for the crypto units and $1 for the additional API calls) for your service instance.

The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Crypto unit 1 | $1570 |
| Crypto unit 2 | $1570 |
| First 1,000,000 API calls | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) | $1 ($0.01 x 100) |
| End of month charge | $3141  |

*Table 1. Charge of two crypto units with a monthly API calls of 2,000,000* -->
