---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: standard keys, import keys, encryption keys, Hyper Protect Crypto Services GUI

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 표준 키 가져오기
{: #import-standard-keys}

{{site.data.keyword.hscrypto}} GUI를 사용하거나 프로그래밍 방식으로 {{site.data.keyword.hscrypto}} API를 사용하여 기존 암호화 키를 추가할 수 있습니다.

## GUI를 사용하여 표준 키 가져오기
{: #import-standard-key-gui}

[서비스의 인스턴스를 작성한 후](/docs/services/hs-crypto/provision.html), 다음 단계를 완료하여 {{site.data.keyword.hscrypto}} GUI로 기존 표준 키를 입력하십시오.

1. [{{site.data.keyword.cloud_notm}} 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")에 로그인하십시오.](https://cloud.ibm.com/){: new_window}
2. **메뉴** &gt; **리소스 목록**으로 이동하여 리소스 목록을 보십시오.
3. {{site.data.keyword.cloud_notm}} 리소스 목록에서 {{site.data.keyword.hscrypto}}의 프로비저닝된 인스턴스를 선택하십시오.
4. 새 키를 가져오려면 **키 추가**를 클릭하고 **고유 키 가져오기** 창을 선택하십시오.

    키의 세부사항을 지정하십시오.

    <table>
      <tr>
        <th>설정</th>
        <th>설명</th>
      </tr>
      <tr>
        <td>이름</td>
        <td>
          <p>키를 쉽게 식별할 수 있도록 해 주는 사용자가 읽을 수 있는 고유 별명입니다.</p>
          <p>개인정보를 보호하려면 키 이름에 사용자 이름 또는 위치와 같은 PII(Personally Identifiable Information)가 포함되지 않았는지 확인하십시오.</p>
        </td>
      </tr>
      <tr>
        <td>키 유형</td>
        <td>{{site.data.keyword.hscrypto}}에서 관리할 <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">키의 유형</a>입니다. 키 유형 목록에서 <b>표준 키</b>를 선택하십시오.</td>
      </tr>
      <tr>
        <td>키 자료</td>
        <td>
          <p>서비스에서 관리할 base64로 인코딩된 키 자료입니다(예: 대칭 키).</p>
          <p>키 자료가 다음 요구사항을 충족시키는지 확인하십시오.</p>
          <p><ul>
              <li>키의 크기는 최대 10,000바이트일 수 있습니다.</li>
              <li>데이터의 바이트는 base64로 인코딩되어야 합니다.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">표 1. <b>새 키 생성</b> 설정에 대한 설명</caption>
    </table>

5. 키의 세부사항 채우기를 완료한 후 확인하려면 **키 가져오기**를 클릭하십시오.

## API로 표준 키 작성
{: #create-standard-key-api}

다음 엔드포인트에 대한 `POST` 호출을 작성하여 표준 키를 작성하십시오.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [서비스 및 인증 인증 정보를 검색하여 서비스에서 키에 대한 작업을 수행하십시오](/docs/services/hs-crypto/access-api.html).

1. 다음 cURL 명령을 사용하여 [{{site.data.keyword.hscrypto}} API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/hs-crypto){: new_window}를 호출하십시오.

    ```cURL
    curl -X POST \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
     "resources": [
       {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<key_material>",
       "extractable": <key_type>
       }
     ]
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
        <td>{{site.data.keyword.hscrypto}} 서비스 인스턴스가 상주하는 지리적 영역을 표시하는 지역 약어(예: <code>us-south</code> 또는 <code>eu-gb</code>)입니다. 자세한 정보는 <a href="/docs/services/hs-crypto/regions.html#endpoints">지역 서비스 엔드포인트</a>를 참조하십시오.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>사용자의 {{site.data.keyword.cloud_notm}} 액세스 토큰입니다. cURL 요청에 Bearer 값 등 <code>IAM</code> 토큰의 전체 컨텐츠를 포함하십시오. 자세한 정보는 <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">액세스 토큰 검색</a>을 참조하십시오.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>{{site.data.keyword.hscrypto}} 서비스 인스턴스에 지정된 고유 ID입니다. 자세한 정보는 <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">인스턴스 ID 검색</a>을 참조하십시오.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>트랜잭션을 추적하고 상관시키는 데 사용되는 고유 ID입니다.</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>선택사항: <code>POST</code> 및 <code>DELETE</code> 오퍼레이션에 대한 서버 작동을 변경하는 헤더입니다.</p><p><em>return_preference</em> 변수를 <code>return=minimal</code>로 설정하면 서비스가 응답 엔티티-본문에 키 이름 및 ID 값과 같은 키 메타데이터만 리턴합니다. 변수를 <code>return=representation</code>으로 설정하면 서비스가 키 자료와 키 메타데이터를 둘 다 리턴합니다.</p></td>
      </tr>
      <tr>
        <td><varname>key_alias</varname></td>
        <td>
          <p>키를 쉽게 식별할 수 있도록 해 주는 사용자가 읽을 수 있는 고유 이름입니다.</p>
          <p>중요사항: 개인정보를 보호하려면 개인 데이터를 키의 메타데이터로 저장하지 마십시오.</p>
        </td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>
          <p>선택사항: 키에 대한 자세한 설명입니다.</p>
          <p>중요사항: 개인정보를 보호하려면 개인 데이터를 키의 메타데이터로 저장하지 마십시오.</p>
        </td>
      </tr>
      <tr>
        <td><varname>YYYY-MM-DD</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>선택사항: 시스템에서 키가 만료되는 날짜 및 시간입니다(RFC 3339 형식).  <code>expirationDate</code> 속성이 생략되면 키가 만료되지 않습니다. </td>
      </tr>
      <tr>
        <td><varname>key_material</varname></td>
        <td>
          <p>서비스에서 관리할 base64로 인코딩된 키 자료입니다(예: 대칭 키).</p>
          <p>키 자료가 다음 요구사항을 충족시키는지 확인하십시오.</p>
          <p><ul>
              <li>키의 크기는 최대 10,000바이트일 수 있습니다.</li>
              <li>데이터의 바이트는 base64로 인코딩되어야 합니다.</li>
            </ul>
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>키 자료 서비스를 중단할지 여부를 판별하는 부울 값입니다.</p>
          <p><code>extractable</code> 속성을 <code>true</code>로 설정하면 서비스가 키를 앱 또는 서비스에 저장할 수 있는 표준 키로 지정합니다.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">표 2. {{site.data.keyword.hscrypto}} API를 통해 표준 키를 추가하는 데 필요한 변수에 대한 설명</caption>
    </table>

    개인 데이터의 기밀성을 보호하려면 서비스에 키를 추가할 때 사용자 이름 또는 위치와 같은 PII(Personally Identifiable Information)를 입력하지 않도록 하십시오. PII에 대한 추가 예제는 [NIST Special Publication 800-122 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window}의 섹션 2.2를 참조하십시오.
    {: tip}

    성공한 `POST /v2/keys` 응답은 기타 메타데이터와 함께 키의 ID 값을 리턴합니다. ID는 키에 지정되어 있으며 {{site.data.keyword.hscrypto}} API에 대한 후속 호출에 사용되는 고유 ID입니다.

2. 선택사항: {{site.data.keyword.hscrypto}} 서비스 인스턴스에서 키를 가져오는 다음 호출을 실행하여 키가 추가되었는지 확인하십시오.

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### 다음에 수행할 작업
{: #import-standard-key-next}

프로그래밍 방식으로 키를 관리하는 방법에 대해 자세히 알아보려면 [{{site.data.keyword.hscrypto}} API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")를 확인하십시오](https://{DomainName}/apidocs/hs-crypto){: new_window}.

<!-- To see an example of how keys stored in {{site.data.keyword.hscrypto}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.  -->
