---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

Keywords: instance ID, account ID, Access Management

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 키에 대한 액세스 관리
{: #manage-access-api}

{{site.data.keyword.iamlong}}를 사용하면 액세스 정책을 작성하고 수정하여 암호화 키에 대한 세부 단위의 액세스 제어를 사용할 수 있습니다.
{: shortdesc}

이 페이지에서는 [액세스 관리 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://iampap.ng.bluemix.net/v1/docs/#/Policies/post_v1_policies){: new_window}를 사용하여 암호화 키에 대한 액세스를 관리하기 위한 시나리오를 안내합니다.

## 시작하기 전에
{: #prereqs}

API에 대해 작업하려면 [액세스 토큰](/docs/services/hs-crypto/access-api.html#retrieve-token) 및 [인스턴스 ID](/docs/services/hs-crypto/access-api.html#retrieve-instance-ID)와 같은 인증 인증 정보를 생성하십시오. 액세스를 관리할 {{site.data.keyword.hscrypto}} 키의 ID도 필요합니다.

키 ID 보기에 대해 알아보려면 [키 보기](/docs/services/hs-crypto/view-keys.html)를 참조하십시오.
{: tip}

### 계정 ID 검색
{: #retrieve-account-ID}

인증 정보를 검색한 후 {{site.data.keyword.hscrypto}} 서비스 인스턴스를 포함하는 계정의 ID를 검색하여 새 액세스 정책에 대한 액세스 범위를 판별하십시오.

계정 ID를 검색하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.cloud_notm}} CLI에 로그인하십시오.
    ```sh
    ibmcloud login [--sso]
    ```
    {: codeblock}

    **참고**: 연합 ID로 로그인하는 경우 `--sso` 매개변수가 필요합니다. 이 옵션을 사용하는 경우에는 CLI 출력에 나열된 링크로 이동하여 일회성 패스코드를 생성하십시오.

    계정에 대한 식별 정보가 결과에 표시됩니다.

    ```sh
    Authenticating...
    OK

    Select an account (or press enter to skip):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Enter a number> 1
    Targeted account sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    API endpoint:   https://api.ng.bluemix.net (API version: 2.75.0)
    Region:         us-south
    User:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}

2. 계정 ID에 대한 값을 복사하십시오.

    _b6hnh3560ehqjkf89s4ba06i367801e_ 값은 계정 ID의 예입니다.

### 사용자 ID 검색
{: #retrieve-user-ID}

액세스를 수정하려는 사용자의 사용자 ID를 검색하십시오.

사용자 ID를 검색하려면 다음 단계를 완료하십시오.

1. [IAM 토큰을 제공하도록 사용자에게 요청](/docs/services/hs-crypto/access-api.html#retrieve-token)하십시오.
    IAM 토큰 구조는 다음과 같습니다.

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. 중간 값을 복사하고 다음 명령을 실행하십시오.
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    결과에 다음 예제와 유사한 JSON 오브젝트가 표시됩니다.
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. `id` 특성의 값을 복사하십시오.

## 액세스 정책 작성
{: #create-policy}

특정 키에 대한 액세스 제어를 사용하려는 경우 다음 명령을 실행하여 요청을 {{site.data.keyword.iamshort}}에 전송할 수 있습니다. 각 액세스 정책에 대해 명령을 반복하십시오.

```cURL
curl -X POST \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<account_ID>",
      "region": "<region>",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

지정된 Cloud Foundry 조직 및 영역 내의 키에 대한 액세스를 관리해야 하는 경우 `serviceInstance`를 `organizationId` 및 `spaceId`로 대체하십시오. 자세히 보려면 [액세스 관리 API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}를 참조하십시오.
{: tip}

`<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` 및 `<key_ID>`를 적절한 값으로 대체하십시오.

**선택사항:** 정책이 작성되었는지 확인하십시오.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## 액세스 정책 업데이트
{: #update-policy}

검색된 정책 ID를 사용하여 사용자에 대한 기존 정책을 수정할 수 있습니다. 다음 명령을 실행하여 {{site.data.keyword.iamshort}}에 요청을 전송하십시오.

```cURL
curl -X PUT \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'If-Match': <ETag_ID> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<account_ID>",
      "region": "<region>",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

`<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` 및 `<key_ID>`를 적절한 값으로 대체하십시오.

**선택사항:** 정책이 업데이트되었는지 확인하십시오.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## 액세스 정책 삭제
{: #delete-policy}

검색된 정책 ID를 사용하여 사용자에 대한 기존 정책을 삭제할 수 있습니다. 다음 명령을 실행하여 {{site.data.keyword.iamshort}}에 요청을 전송하십시오.

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

`<account_ID>`, `<user_ID>`, `<policy_ID>` 및 `<Admin_IAM_token>`을 적절한 값으로 대체하십시오.

**선택사항:** 정책이 삭제되었는지 확인하십시오.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}
