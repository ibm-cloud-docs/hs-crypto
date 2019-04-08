---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: root key, data encryption key, Hyper Protect Crypto Services

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 키 랩핑
{: #wrap-keys}

권한 있는 사용자인 경우 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} API를 사용하여 암호화 키를 관리하고 루트 키로 보호할 수 있습니다.
{: shortdesc}

루트 키로 데이터 암호화 키(DEK)를 랩핑하면 {{site.data.keyword.hscrypto}}가
여러 알고리즘의 장점을 결합하여 암호화된 데이터의 무결성과 개인정보를 보호합니다.   

키 랩핑을 통해 클라우드에서 저장 데이터의 보안을 제어하는 방법을 알아보려면 [엔벨로프 암호화](/docs/services/key-protect/concepts/envelope-encryption.html)를 참조하십시오.

## API를 사용하여 키 랩핑
{: #wrap-keys-api}

{{site.data.keyword.hscrypto}}에서 관리하는 루트 키로 지정된 데이터 암호화 키(DEK)를 보호할 수 있습니다
.

랩핑을 위해 루트 키를 제공하는 경우 랩핑 호출에 성공할 수 있도록 루트 키가 128, 192 또는 256비트인지 확인하십시오. 서비스에서 루트 키를 작성하는 경우 {{site.data.keyword.hscrypto}}가
HSM에서 256비트 키를 생성하며, 이는 AES-CBC 알고리즘에서 지원됩니다.

[서비스에서 루트 키를 지정하면](/docs/services/hs-crypto/create-root-keys.html) 다음 엔드포인트에 대한 `POST` 호출을 작성하여 고급 암호화로 DEK를 랩핑할 수 있습니다.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap
```
{: codeblock}

1. [서비스 및 인증 인증 정보를 검색하여 서비스에서 키에 대한 작업을 수행하십시오.](/docs/services/hs-crypto/access-api.html)

2. 관리하고 보호할 DEK의 키 자료를 복사하십시오.

    {{site.data.keyword.hscrypto}} 서비스 인스턴스에 대한 관리자 또는 작성자 권한이 있으면
 [`GET /v2/keys/<key_ID>` 요청을 작성하여 특정 키의 키 자료를 검색할 수 있습니다](/docs/services/hs-crypto/view-keys.html#api).

3. 랩핑에 사용할 루트 키의 ID를 복사하십시오.

4. 다음 cURL 명령을 실행하여 랩핑 오퍼레이션으로 키를 보호하십시오.

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
    }'
    ```
    {: codeblock}
    <!--    To work with keys within a Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [For more information, see the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
        {: tip} -->

    다음 표에 따라 예제 요청의 변수를 대체하십시오.

    <table>
      <tr>
        <th>변수</th>
        <th>설명</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>{{site.data.keyword.hscrypto}} 서비스 인스턴스가 상주하는 지리적 영역을 표시하는 지역 약어(예: <code>us-south</code> 또는 <code>eu-gb</code>)입니다. 
 자세한 정보는 <a href="/docs/services/hs-crypto/regions.html#endpoints">지역 서비스 엔드포인트</a>를 참조하십시오.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>랩핑에 사용할 루트 키의 고유 ID입니다.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>사용자의 {{site.data.keyword.cloud_notm}} 액세스 토큰입니다. cURL 요청에 Bearer 값 등 <code>IAM</code> 토큰의 전체 컨텐츠를 포함하십시오. 
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>{{site.data.keyword.hscrypto}} 서비스 인스턴스에 지정된 고유 ID입니다. 자세한 정보는 <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">인스턴스 ID 검색</a>을 참조하십시오.</td>
 자세한 정보는 <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">액세스 토큰 검색</a>을 참조하십시오.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>선택사항: 트랜잭션을 추적하고 상관시키는 데 사용되는 고유 ID입니다.</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p><code>POST</code> 및 <code>DELETE</code> 오퍼레이션에 대한 서버 작동을 변경하는 헤더입니다.</p><p><em>return_preference</em> 변수를 <code>return=minimal</code>로 설정하면 서비스가 응답 엔티티-본문에 키 이름 및 ID 값과 같은 키 메타데이터만 리턴합니다. 변수를 <code>return=representation</code>으로 설정하면 서비스가 키 자료와 키 메타데이터를 둘 다 리턴합니다.</p></td>
      </tr>
      <tr>
        <td><varname>data_key</varname></td>
        <td>선택사항: 관리하고 보호할 DEK의 키 자료입니다. <code>plaintext</code> 값은 base64로 인코딩되어야 합니다. 새 DEK를 생성하려면 <code>plaintext</code> 속성을 생략하십시오. 서비스가 랜덤 일반 텍스트(32바이트)를 생성하고 해당 값을 랩핑합니다.</td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>선택사항: 키를 추가로 보호하는 데 사용되는 추가 인증 데이터(AAD)입니다. 각 문자열은 최대 255자입니다. 서비스에 대한 랩핑 호출을 작성할 때 AAD를 제공한 경우 후속 랩핑 해제 호출 중에 동일한 AAD를 지정해야 합니다.<br></br>중요사항: {{site.data.keyword.hscrypto}} 
      </tr>
      <caption style="caption-side:bottom;">표 1. {{site.data.keyword.hscrypto}}에서 지정된 키를 랩핑하는 데 필요한 변수에 대한 설명</caption>
    </table>

    base64로 인코딩된 키 자료가 포함된 랩핑된 키가 응답 엔티티-본문에 리턴됩니다. 다음 JSON 오브젝트는 예제 리턴값을 표시합니다.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
