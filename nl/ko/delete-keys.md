---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: details of the DELETE request, delete encryption key, deleting keys, Variable Description region

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 키 삭제
{: #deleting-keys}

{{site.data.keyword.cloud_notm}} 영역 또는 {{site.data.keyword.hscrypto}} 서비스 인스턴스의 관리자인 경우에는 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}를 사용하여 암호화 키와 해당 컨텐츠를 삭제할 수 있습니다.
{: shortdesc}

**중요:** 키를 삭제하면 해당 컨텐츠 및 연관된 데이터가 영구 삭제됩니다. 이 조치는 되돌릴 수 없습니다. 프로덕션 환경의 경우에는 리소스 영구 삭제가 권장되지 않지만, 테스트나 QA 등의 임시 환경의 경우에는 유용할 수 있습니다.

## GUI로 키 삭제
{: #delete-keys-gui}

그래픽 인터페이스를 사용한 암호화 키 삭제를 원하는 경우 {{site.data.keyword.hscrypto}} GUI를 사용할 수 있습니다.

[키를 새로 작성하거나 기존 키를 서비스로 가져온 후](/docs/services/hs-crypto/create-root-keys.html) 다음 단계를 완료하여 키를 삭제하십시오.

1. [{{site.data.keyword.cloud_notm}} 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")에 로그인하십시오.](https://cloud.ibm.com/){: new_window}
2. **메뉴** &gt; **리소스 목록**으로 이동하여 리소스 목록을 보십시오.
3. {{site.data.keyword.cloud_notm}} 리소스 목록에서 {{site.data.keyword.hscrypto}}의 프로비저닝된 인스턴스를 선택하십시오.
4. **키** 테이블을 사용하여 서비스에서 키를 찾아보십시오.
5. 아이콘을 클릭하여 삭제할 키에 대한 옵션 목록을 여십시오.
6. 옵션 메뉴에서 **키 삭제**를 클릭한 후 다음 화면에서 키 삭제를 확인하십시오.

키를 삭제하면 키가 _영구 삭제됨_ 상태로 전이됩니다. 이 상태의 키는 더 이상 복구 불가능합니다. 키와 연관된 메타데이터(예: 키의 삭제 날짜)가 {{site.data.keyword.hscrypto}} 데이터베이스에 보관됩니다.

## API로 키 삭제
{: #api}

키와 해당 컨텐츠를 삭제하려면 다음 엔드포인트에 대해 `DELETE` 호출을 작성하십시오.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```

1. [서비스 및 인증 인증 정보를 검색하여 서비스에서 키에 대한 작업을 수행하십시오](/docs/services/hs-crypto/access-api.html).

2. 삭제할 키의 ID를 검색하십시오.

    `GET /v2/keys/` 요청을 작성하거나 {{site.data.keyword.hscrypto}} 대시보드에서 키를 확인하여 지정된 키의 ID를 검색할 수 있습니다.

3. 다음 cURL 명령을 실행하여 키와 해당 컨텐츠를 영구 삭제하십시오.

    ```cURL
    curl -X DELETE \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
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
        <td><varname>key_ID</varname></td>
        <td>삭제할 키의 고유 ID입니다.</td>
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
        <td><varname>return_preference</varname></td>
        <td><p><code>POST</code> 및 <code>DELETE</code> 오퍼레이션에 대한 서버 작동을 변경하는 헤더입니다.</p><p><em>return_preference</em> 변수를 <code>return=minimal</code>로 설정하면 서비스가 성공한 삭제 응답을 리턴합니다. 변수를 <code>return=representation</code>으로 설정하면 서비스가 키 자료와 키 메타데이터를 둘 다 리턴합니다.</p></td>
      </tr>
      <caption style="caption-side:bottom;">표 1. {{site.data.keyword.hscrypto}} API를 통해 키를 삭제하는 데 필요한 변수에 대한 설명</caption>
    </table>

    _return_preference_ 변수가 `return=representation`으로 설정되면 `DELETE` 요청의 세부사항이 응답 엔티티-본문에 리턴됩니다. 다음 JSON 오브젝트는 예제 리턴값을 표시합니다.
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
      },
      "resources": [
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    사용 가능한 매개변수에 대한 자세한 설명은 {{site.data.keyword.hscrypto}} [REST API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/hs-crypto){: new_window}를 참조하십시오.
