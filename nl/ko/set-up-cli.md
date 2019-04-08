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

# {{site.data.keyword.hscrypto}} 인스턴스에서 {{site.data.keyword.keymanagementserviceshort}} CLI 액세스
{: #set-up-cli}

{{site.data.keyword.keymanagementservicelong_notm}} CLI 플러그인을 사용하여 암호화 루트 키 및 표준 키를 작성하고, 가져오고, 관리할 수 있도록 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}가 {{site.data.keyword.keymanagementservicelong_notm}} CLI 플러그인과 통합되었습니다.

{{site.data.keyword.hscrypto}} 인스턴스(줄여서 서비스 인스턴스)에서 {{site.data.keyword.keymanagementserviceshort}} CLI 플러그인을 사용하기 전에 워크스테이션에 KP_KP_PRIVATE_ADDR 환경 변수를 설정해야 합니다.

* Linux 또는 MacOS에서 다음 명령을 실행하십시오.

  ```
export KP_PRIVATE_ADDR=<URL>
  ```
  {: pre}

  이 명령에서 *URL*은 프로비저닝된 {{site.data.keyword.hscrypto}} 대시보드의 **관리** 탭에 표시되는 엔드포인트입니다. 예를 들어, 다음과 같습니다.

  ```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
  ```
  {: pre}

* Windows의 경우, **제어판**에서 검색 상자에 `환경 변수`를 입력하여 환경 변수 창을 찾으십시오. KP_PRIVATE_ADDR 환경 변수를 작성하고 해당 값을 프로비저닝된 {{site.data.keyword.hscrypto}} 대시보드의 **관리** 탭에 표시되는 엔드포인트에 설정하십시오. 예: `https://us-south.hs-crypto.cloud.ibm.com:<port>`.

또는 API를 통해 엔드포인트 URL을 검색할 수도 있습니다. 세부사항은 [{{site.data.keyword.hscrypto}} API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")를 참조](https://{DomainName}/apidocs/hs-crypto){: new_window}하십시오.

- CLI 사용에 대해 자세히 알아보려면 [{{site.data.keyword.keymanagementserviceshort}} CLI 참조 문서](/docs/services/key-protect/cli-reference.html)를 확인하십시오.
- CLI 액세스에 대해 자세히 알아보려면 [{{site.data.keyword.keymanagementserviceshort}} CLI 설정](/docs/services/key-protect/set-up-cli.html)을 확인하십시오.
