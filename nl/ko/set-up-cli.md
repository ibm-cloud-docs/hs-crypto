---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: IBM Cloud CLI plug-in, ibmcloud commands, IBM Cloud command-line interface

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# CLI 설정
{: #set-up-cli}

{{site.data.keyword.keymanagementservicelong_notm}} CLI 플러그인을 사용하여 암호화 루트 키 및 표준 키를 작성하고, 가져오고, 관리할 수 있도록 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}가 {{site.data.keyword.keymanagementservicelong_notm}} CLI 플러그인과 통합되었습니다.

- CLI 사용에 대해 자세히 알아보려면 [{{site.data.keyword.keymanagementserviceshort}} CLI 참조 문서](/docs/services/key-protect/cli-reference.html)를 확인하십시오.
- CLI 액세스에 대해 자세히 알아보려면 [{{site.data.keyword.keymanagementserviceshort}} CLI 설정](/docs/services/key-protect/set-up-cli.html)을 확인하십시오.

{{site.data.keyword.hscrypto}} 인스턴스에서 {{site.data.keyword.keymanagementserviceshort}} CLI 플러그인을 사용하기 전에 먼저 다음 명령을 실행하십시오.

```
export KP_PRIVATE_ADDR=<URL>
```
{: pre}

이 명령에서 *URL*은 사용자 인터페이스의 **관리** 페이지에 표시되는 엔드포인트입니다. 또는 API를 통해 엔드포인트 URL을 검색할 수 있습니다. 예를 들어, 다음과 같습니다.

```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
```
{: pre}

세부사항은 [{{site.data.keyword.hscrypto}} API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")를 참조](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}하십시오.
