---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-15"

Keywords: key storage, service instance, HSM, hardware security module

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}  
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# 서비스 인스턴스 초기화 시작하기
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> 이 튜토리얼에서는 Trusted Key Entry 플러그인으로 키 스토리지를 보호하기 위해 마스터 키를 로드하여 서비스 인스턴스를 초기화하는 방법을 보여줍니다. 서비스 인스턴스를 초기화한 후 루트 키 관리를 시작할 수 있습니다.   
{:shortdesc}

## 전제조건
{: #get-started-hsm-prerequisite}

시작하기 전에 다음 단계를 수행하십시오.

1. {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} 인스턴스(줄여서 서비스 인스턴스)를 프로비저닝하십시오. 자세한 단계는 [{{site.data.keyword.hscrypto}} 프로비저닝](/docs/services/hs-crypto/provision.html)을 참조하십시오.

2. 다음 명령을 실행하여 올바른 API 엔드포인트에 로그인했는지 확인하십시오.

  ```
  ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

3. 다음 명령을 사용하여 {{site.data.keyword.cloud_notm}} 명령행 인터페이스(CLI)를 통해 최신 Trusted Key Entry 플러그인을 설치하십시오.

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  CLI 플러그인을 설치하려면 [{{site.data.keyword.cloud_notm}} CLI 시작하기](/docs/cli/index.html)를 참조하십시오.
  {: tip}

4. 키 파트 및 서명 키를 저장할 서브디렉토리를 표시하도록 환경 변수 CLOUDTKEFILES를 설정하십시오.

##  1단계: 마스터 키 파트 및 서명 키 파일 작성
{: #hsm-step1}

1. 랜덤 마스터 키 파트를 작성하거나 알려진 값으로 마스터 키 파트를 작성하십시오.

  * 랜덤 마스터 키 파트를 작성하려면 다음 명령을 사용하십시오.

    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    프롬프트가 표시되면 키 파트에 대한 설명과 키 파트 파일의 비밀번호를 입력하십시오.

  * 알려진 값으로 마스터 키 파트를 작성하려면 다음 명령을 사용하십시오.

    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    프롬프트가 표시되면 알려진 키 파트 값을 16진 문자열로 입력한 후 키 파트 파일에 대한 설명과 비밀번호를 입력하십시오.

  추가 키 파트를 작성하려면 두 명령 중 하나를 반복하십시오.

2. 다음 명령을 사용하여 서명 키를 작성하십시오.
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  프롬프트가 표시되면 서명 키 파일의 관리자 이름과 비밀번호를 입력하십시오.

## 2단계: 작업할 암호화 단위 선택
{: #hsm-step2}

서비스 인스턴스의 모든 암호화 단위를 동일하게 구성해야 합니다.

1. 다음 명령을 사용하여 IBM Cloud 계정에 지정된 서비스 인스턴스 및 암호화 단위를 표시할 수 있습니다.

  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

2. 작업할 추가 암호화 단위를 선택하려면 다음 명령을 사용하십시오.

  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  프롬프트가 표시되면 작업할 추가 암호화 단위를 입력하십시오.

3. 작업할 세트에서 암호화 단위를 제거하려면 다음 명령을 사용하십시오.

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  프롬프트가 표시되면 제거할 암호화 단위를 입력하십시오.

## 3단계: 암호화 단위 관리자 추가 및 임프린트 모드 종료
{: #hsm-step3}

암호화 단위에 마스터 키를 로드하기 전에 하나 이상의 암호화 단위 관리자를 작성하고 임프린트 모드를 종료해야 합니다.

1. 암호화 단위 관리자를 로드하십시오. 암호화 단위 관리자를 작성하려면 다음 명령을 사용하십시오.
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  프롬프트가 표시되면 서명 키 파일의 관리자 및 비밀번호에 사용될 서명 키의 KEYNUM을 입력하십시오.

2. 다음 명령을 사용하여 명령에 서명하는 데 사용할 서명 키를 선택하십시오.

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  프롬프트가 표시되면 명령에 서명하는 데 사용할 서명 키의 KEYNUM을 입력하십시오.

  이는 3.1단계에서 암호화 단위 관리자를 로드하는 데 사용되는 서명 키 중 하나와 동일해야 합니다.
  {: tip}

3. 다음 명령을 사용하여 임프린트 모드를 종료하십시오.

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

암호화 단위 관리자를 로드하고 임프린트 모드를 종료한 후 다음 명령을 사용하여 암호화 단위의 상태를 확인할 수 있습니다.
{: tip}

```
 ibmcloud tke cryptounit-compare
```
{: pre}

## 4단계: 마스터 키 레지스터 로드
{: #hsm-step4}

마스터 키 레지스터를 로드하려면 하나 이상의 암호화 단위 관리자가 정의되야 하고 암호화 단위가 임프린트 모드를 종료해야 합니다.

1. 다음 명령을 사용하여 새 마스터 키 레지스터를 로드하십시오.

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  프롬프트가 표시되면 로드할 키 파트의 KEYNUM, 서명 키 파일의 비밀번호 및 각각의 선택한 키 파트의 비밀번호를 입력하십시오.

2. 다음 명령을 사용하여 새 마스터 키 레지스터를 커미트하십시오.

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  프롬프트가 표시되면 서명 키 파일의 비밀번호를 입력하십시오.

3. 다음 명령을 사용하여 마스터 키를 현재 마스터 키 레지스터로 이동하십시오.

  ```
  ibmcloud tke cryptounit-mk-setimm
  ```
  {: pre}

  프롬프트가 표시되면 서명 키 파일의 비밀번호를 입력하십시오.

## 다음에 수행할 작업
{: #hsm-next}

이제 서비스 인스턴스를 사용할 수 있습니다. 프로덕션 환경에서 프로시저를 구현하는 방법에 대한 세부사항은 [암호화 인스턴스를 초기화하여 키 스토리지 보호](/docs/services/hs-crypto/initialize_hsm.html)를 참조하십시오.
