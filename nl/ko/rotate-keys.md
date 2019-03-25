---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: root keys, Rotate key, key rotation

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# 키 순환
{: #rotating-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}를 사용하여 요청 시 루트 키를 순환할 수 있습니다.
{: shortdesc}

현재 마스터 키 순환은 지원되지 않습니다.
{: important}

루트 키를 순환하는 경우 키의 수명이 줄어들고 해당 키로 보호되는 정보의 양이 제한됩니다.   

키 순환을 통해 산업 표준 및 암호화 우수 사례를 충족시키는 방법을 알아보려면 [키 순환](/docs/services/key-protect/concepts/key-rotation.html)을 참조하십시오.

순환은 루트 키에만 사용 가능합니다.
{: tip}

## GUI로 루트 키 순환
{: #gui}

그래픽 인터페이스를 사용한 루트 키 순환을 원하는 경우 {{site.data.keyword.hscrypto}} GUI를 사용할 수 있습니다.

[키를 새로 작성하거나 기존 루트 키를 서비스로 가져온 후](/docs/services/hs-crypto/create-root-keys.html) 다음 단계를 완료하여 키를 순환하십시오.

1. [{{site.data.keyword.cloud_notm}} 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")에 로그인하십시오.](https://cloud.ibm.com/){: new_window}
2. {{site.data.keyword.cloud_notm}} 대시보드에서 {{site.data.keyword.hscrypto}}의 프로비저닝된 인스턴스를 선택하십시오.
3. **키** 테이블을 사용하여 서비스에서 키를 찾아보십시오.
4. ⋮ 아이콘을 클릭하여 순환할 키에 대한 옵션 목록을 여십시오.
5. 옵션 메뉴에서 **키 삭제**를 클릭한 후 다음 화면에서 순환을 확인하십시오.

처음에 루트 키를 가져온 경우 키를 순환하여면 base64로 인코딩된 새 키 자료를 제공해야 합니다. 자세한 정보는 [GUI를 사용하여 루트 키 가져오기](/docs/services/hs-crypto/import-root-keys.html#gui)를 참조하십시오.
{: tip}

## API를 사용하여 루트 키 순환
{: #api}

[서비스에서 루트 키를 지정하면](/docs/services/hs-crypto/create-root-keys.html) 다음 엔드포인트에 대한 `POST` 호출을 작성하여 키를 순환할 수 있습니다.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate
```
{: codeblock}

1. [서비스 및 인증 인증 정보를 검색하여 서비스에서 키에 대한 작업을 수행하십시오.](/docs/services/hs-crypto/access-api.html)

2. 순환할 루트 키의 ID를 복사하십시오.

4. 다음 cURL 명령을 실행하여 키를 새 키 자료로 바꾸십시오.

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -d '{
        'payload: <key_material>'
      }'
    ```
    {: codeblock}

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
        <td><varname>key_ID</varname></td>
        <td>순환할 루트 키의 고유 ID입니다.</td>
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
        <td><varname>key_material</varname></td>
        <td>
          <p>서비스에 저장하고 관리할 base64로 인코딩된 키 자료입니다. 이 값은 키를 서비스에 추가할 때 초기에 키 자료를 가져온 경우 필수입니다.</p>
          <p>{{site.data.keyword.hscrypto}}로 초기에 생성된 키를 순환하려면 <code>payload</code> 속성을 생략하고 비어 있는 요청 엔티티-본문을 전달하십시오. 가져온 키를 순환하려면 다음 요구사항을 충족시키는 키 자료를 제공하십시오.</p>
          <p>
            <ul>
              <li>키가 256, 384 또는 512비트여야 합니다.</li>
              <li>base64 인코딩을 사용하여 데이터 바이트(예: 256비트의 경우 32바이트)를 인코딩해야 합니다.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">표 1. {{site.data.keyword.hscrypto}}에서 지정된 키를 순환하는 데 필요한 변수에 대한 설명</caption>
    </table>

    성공한 순환 요청은 루트 키가 새 키 자료로 바뀌었음을 표시하는 HTTP `204 No Content` 응답을 리턴합니다.

4. 선택사항: {{site.data.keyword.hscrypto}} 서비스 인스턴스에서 키를 찾아보는 다음 호출을 실행하여 키가 순환되었는지 확인하십시오.

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    ```
    {: codeblock}

    응답 엔티티-본문에 있는 `lastRotateDate` 값을 검토하여 키가 마지막으로 순환된 날짜 및 시간을 검사하십시오.
