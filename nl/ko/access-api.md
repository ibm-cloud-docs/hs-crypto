---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: REST API, RESTful API, access token, instance ID

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# API에 액세스
{: #access-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}는 키를 저장, 검색, 생성하기 위해 어떠한 프로그래밍 언어와도 함께 사용할 수 있는 {{site.data.keyword.keymanagementserviceshort}} REST API와 통합됩니다.
{: shortdesc}

API 관련 작업을 수행하려면 서비스 및 인증 인증 정보를 생성해야 합니다.

## 액세스 토큰 검색
{: #retrieve-token}

{{site.data.keyword.iamshort}}에서 액세스 토큰을 검색하여 {{site.data.keyword.hscrypto}}에 인증할 수 있습니다. [서비스 ID](/docs/iam/serviceid.html#serviceids)를 사용하면 개인 사용자 인증 정보를 공유하지 않고도 {{site.data.keyword.cloud_notm}}에서 또는 그 외부에서 서비스나 애플리케이션 대신 {{site.data.keyword.hscrypto}} API에 대한 작업을 수행할 수 있습니다.  

<!-- If you want to authenticate with your user credentials, you can retrieve your token by running `ibmcloud iam oauth-tokens` in the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview).
{: tip} -->

다음 단계를 완료하여 액세스 토큰을 검색하십시오.

1. {{site.data.keyword.cloud_notm}} 콘솔에서 **관리** &gt; **보안** &gt; **ID 및 액세스** &gt; **서비스 ID**로 이동하십시오. 프로세스에 따라 [서비스 ID를 작성](/docs/iam/serviceid.html#creating-a-service-id)하십시오.
2. **조치** 메뉴를 사용하여 [새 서비스 ID의 액세스 정책을 정의](/docs/iam/serviceidaccess.html)하십시오.

    {{site.data.keyword.hscrypto}} 리소스의 액세스 관리에 대한 자세한 정보는 [역할 및 권한](/docs/services/hs-crypto/manage-access.html#roles)을 참조하십시오.
3. **API 키** 섹션을 사용하여 [서비스 ID와 연관시킬 API 키를 작성](/docs/iam/serviceid_keys.html#serviceidapikeys)하십시오. 보안 위치로 API 키를 다운로드하여 저장하십시오.
4. {{site.data.keyword.iamshort}} API를 호출하여 액세스 토큰을 검색하십시오.

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/identity/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>" \
    ```
    {: codeblock}

    요청에서 `<API_KEY>`를 3단계에서 작성한 API로 바꾸십시오. 다음 잘린 예는 토큰 출력을 표시합니다.

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    전체 `access_token` 값(_Bearer_ 토큰 유형이 접두부임)을 사용하여 {{site.data.keyword.hscrypto}} API로 서비스의 키를 프로그래밍 방식으로 관리하십시오.

    액세스 토큰은 1시간 동안 유효하지만 필요에 따라 재생성할 수 있습니다. 서비스에 대한 액세스를 유지보수하려면 {{site.data.keyword.iamshort}} API를 호출하여 정기적으로 API 키에 대한 액세스 토큰을 새로 고치십시오.   
    {: tip }

## 인스턴스 ID 검색
{: #retrieve-instance-ID}

[{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview)를 사용하여 {{site.data.keyword.hscrypto}} 서비스 인스턴스에 대한 식별 정보를 검색할 수 잇습니다. 계정에서 {{site.data.keyword.hscrypto}}의 지정된 인스턴스 내 암호화 키를 관리하려면 인스턴스 ID를 사용하십시오.

1. [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview)를 사용하여 {{site.data.keyword.cloud_notm}}에 로그인하십시오.

    ```sh
    ibmcloud login
    ```
    {: pre}

    **참고:** 로그인에 실패하면 `ibmcloud login --sso` 명령을 실행하여 다시 시도하십시오. `--sso` 매개변수는 연합 ID로 로그인할 때 필요합니다. 이 옵션을 사용하는 경우에는 CLI 출력에 나열된 링크로 이동하여 일회성 패스코드를 생성하십시오.

2. 프로비저닝된 인스턴스가 포함된 계정을 선택하십시오.

    `ibmcloud resource service-instances`를 실행하여 계정에 프로비저닝된 모든 서비스 인스턴스를 나열할 수 있습니다.

3. {{site.data.keyword.hscrypto}} 서비스 인스턴스를 고유하게 식별하는 클라우드 리소스 이름(CRN)을 검색하십시오.

    ```sh
    ibmcloud resource service-instance <instance_name> --id
    ```
    {: pre}

    `<instance_name>`을(를) {{site.data.keyword.hscrypto}}의 인스턴스에 지정된 고유 별명으로 바꾸십시오. 다음의 잘려진 예는 CLI 출력을 표시합니다. _42454b3b-5b06-407b-a4b3-34d9ef323901_ 값은 인스턴스 ID의 예입니다.

    ```
    crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:42454b3b-5b06-407b-a4b3-34d9ef323901::
    ```
    {: screen}

## 연결 정보 검색
{: #retrieve-connection-info}

{{site.data.keyword.keymanagementserviceshort}} API를 호출하기 전에 먼저 **연결 정보 검색** API를 호출하여 연결 정보를 검색하십시오. 자세한 정보는 [{{site.data.keyword.hscrypto}} API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}를 참조하십시오.

## API 요청 구성
{: #form-api-request}

서비스에 대한 API 호출을 작성할 때 처음에 {{site.data.keyword.hscrypto}}의 인스턴스를 프로비저닝한 방법에 따라 API 요청을 구조화하십시오.

요청을 빌드하려면 [지역 서비스 엔드포인트](/docs/services/hs-crypto/regions.html)를 해당 인증 인증 정보와 쌍으로 묶으십시오. 예를 들어, `us-south` 지역의 서비스 인스턴스를 작성한 경우 다음 엔드포인트 및 API 헤더를 사용하여 서비스에서 키를 찾아보십시오.

```cURL
curl -X GET \
    https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/key \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### 다음에 수행할 작업

- 프로그래밍 방식으로 키를 관리하는 방법에 대해 자세히 알아보려면 [{{site.data.keyword.hscrypto}} API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")를 확인하십시오.](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}
- 데이터를 암호화하고 복호화하기 위해 {{site.data.keyword.hscrypto}}에 저장된 키가 작동하는 방식에 대한 예를 보려면 [GitHub에서 샘플 앱 확인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}을 수행하십시오.
