---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: troubleshoot, problems, known issues

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}

# 문제점 해결
{: #troubleshooting}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 사용과 관련된 일반 문제점에는 API와 상호작용할 때 올바른 헤더 또는 인증 정보를 제공하는 것이 포함될 수 있습니다. 대부분 몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다.
{: shortdesc}

## 초기화된 {{site.data.keyword.hscrypto}} 인스턴스 삭제 시 오류 발생

초기화된 {{site.data.keyword.hscrypto}} 인스턴스를 삭제할 때 다음과 유사한 오류가 수신될 수 있습니다.

```
FAILED
Error response from server. Status code: 400; description: 400 DELETE https://zCryptoBroker.mybluemix.net/v2/service_instances/ failed with error status 409. Conflict.
```
{: codeblock}
{: tsSymptoms}

인스턴스를 삭제하기 전에 초기화된 {{site.data.keyword.hscrypto}} 인스턴스를 지우지(제로화) 않았습니다.
{: tsCauses}

인스턴스를 삭제하기 전에 다음 명령을 실행하십시오.
{: tsResolve}

```
ibmcloud tke cryptounit-zeroize
```
{: codeblock}

## Trusted Key Entry 플러그인과 관련된 명령을 실행한 후 권한 없는 토큰

`tke` CLI 명령을 실행한 후 다음과 유사한 메시지를 수신할 수 있습니다.

```
ibmcloud tke cryptounits
FAILED
Error querying crypto instances.
Status code: 401
Message: Unauthorized
Your access token is invalid, expired, or does not have the necessary permissions to access this instance.`
```
{: codeblock}
{: tsSymptoms}

토큰이 새로 고쳐지지 않습니다.
{: tsCauses}

`ibmcloud login` 명령으로 {{site.data.keyword.cloud_notm}}에 다시 로그인하여 토큰을 새로 고치십시오.
{: tsResolve}

## CLI 또는 API 사용 시 `CKR_IBM_WK_NOT_INITIALIZED` 오류 발생

CLI 또는 API를 사용할 때 다음과 유사한 오류 메시지가 표시될 수 있습니다.

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

`ibmcloud tke cryptounit-compare` 명령을 실행했을 때 현재 마스터 키 레지스터에 대해 `Valid` 확인을 얻지 못했습니다.
{: tsCauses}

HSM 마스터 키가 올바르게 설정되었는지 확인하십시오.
{: tsResolve}

## 키를 작성하거나 삭제할 수 없음
{: #unable-to-create-keys}

{{site.data.keyword.hscrypto}} 사용자 인터페이스에 액세스할 때 키를 추가하거나 삭제하는 옵션이 표시되지 않습니다.

{{site.data.keyword.cloud_notm}} 대시보드에서 {{site.data.keyword.hscrypto}} 서비스의 인스턴스를 선택합니다.
{: tsSymptoms}

키 목록을 볼 수 있지만 키를 추가하거나 삭제하는 옵션이 표시되지 않습니다.

{{site.data.keyword.hscrypto}} 조치를 수행할 수 있는 올바른 권한이 없습니다.
{: tsCauses}

적용 가능한 리소스 그룹 또는 서비스 인스턴스에서 사용자에게 올바른 역할이 지정되었는지 관리자에게 확인하십시오. 역할에 대한 자세한 정보는 [역할 및 권한](/docs/services/key-protect/manage-access.html#roles)을 참조하십시오.
{: tsResolve}

## 도움 및 지원 받기
{: #getting-help}

{{site.data.keyword.hscrypto}} 사용 시에 문제점이나 질문이 있는 경우 {{site.data.keyword.cloud_notm}}를 확인하거나, 정보를 검색하거나 포럼을 통해 질문하여 도움을 받을 수 있습니다. 또한 지원 티켓을 열 수도 있습니다.
{: shortdesc}

[상태 페이지 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/status?tags=platform,runtimes,services)로 이동하여 {{site.data.keyword.cloud_notm}}가 사용 가능한지 여부를 확인할 수 있습니다.

포럼을 검토하여 다른 사용자에게 동일한 문제점이 발생했는지 확인할 수 있습니다. 포럼을 사용하여 질문하는 경우에는 {{site.data.keyword.cloud_notm}} 개발 팀이 볼 수 있도록 질문에 태그를 지정하십시오.

- {{site.data.keyword.hscrypto}}에 대한 기술적 질문이 있는 경우 [Stack Overflow ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://stackoverflow.com/){: new_window}에 질문을 게시하고 질문에 "ibm-cloud" 및 "hyperprotect-crypto" 태그를 지정하십시오.
- 서비스 및 시작하기 지시사항에 대한 질문이 있는 경우 [IBM developerWorks dW Answers ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/answers/index.html){: new_window} 포럼을 활용하십시오. "ibm-cloud" 및 "hyperprotect-crypto" 태그를 포함하십시오.

포럼 활용에 대한 세부사항은 [도움 받기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/docs/support/index.html#getting-help){: new_window}를 참조하십시오.

{{site.data.keyword.IBM_notm}} 지원 티켓 열기 또는 지원 레벨과 티켓 심각도에 대한 자세한 정보는 [지원 문의 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/docs/support/index.html#contacting-support){: new_window}를 참조하십시오.
