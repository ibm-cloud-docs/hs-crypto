---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: dedicated key management service, IBM Key, Own Keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} 시작하기
{: #get-started}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}(줄여서 {{site.data.keyword.hscrypto}})는 키 관리 및 클라우드 하드웨어 보안 모듈(HSM)입니다. 클라우드 데이터 암호화 키 및 클라우드 하드웨어 보안 모델을 제어할 수 있도록 디자인되었으며 FIPS 140-2 레벨 4로 인증된 하드웨어를 기반으로 빌드된 업계의 유일한 서비스입니다.
{:shortdesc}

키를 생성하고 암호화하기 위해 {{site.data.keyword.hscrypto}}가 {{site.data.keyword.keymanagementservicefull_notm}} API와 통합됩니다. 또한 {{site.data.keyword.hscrypto}}에서 KYOK(Keep Your Own Key) 기능이 사용되어 달성 가능한 가장 높은 보안 레벨인 FIPS 140-2 레벨 4로 인증된 기술인 암호화 하드웨어에 대한 액세스를 제공할 수 있습니다. {{site.data.keyword.hscrypto}}는 네트워크 주소 지정 가능 HSM을 제공합니다. <!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on-->.  <!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.--> {{site.data.keyword.hscrypto}}에 대한 자세한 정보는 [{{site.data.keyword.hscrypto}} 개요](/docs/services/hs-crypto/overview.html)를 참조하십시오. 암호화 모듈의 보안 요구사항에 대한 자세한 정보는 [FIPS 140-2 레벨에 대한 NIST의 스펙 ![외부 링크 아이콘](image/external_link.svg "외부 링크 아이콘")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}을 참조하십시오.

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-platform/index.html){:new_window}. -->

이 튜토리얼은 {{site.data.keyword.hscrypto}} 대시보드를 통해 마스터 키를 관리하고 기존 암호화 키를 작성 및 추가하여 서비스 인스턴스를 설정하는 방법을 안내합니다.


## 1단계: 서비스 프로비저닝
{: #provision-service}

시작하기 전에 {{site.data.keyword.cloud_notm}} 콘솔에서 {{site.data.keyword.hscrypto}}의 인스턴스를 작성해야 합니다. 자세한 단계는 [서비스 프로비저닝](/docs/services/hs-crypto/provision.html)을 참조하십시오.

## 2단계: 서비스 인스턴스 초기화
{: #initialize-crypto}

키를 관리하려면 서비스 인스턴스를 초기화해야 합니다. 빠른 시작 튜토리얼은 [서비스 인스턴스 초기화 시작하기](/docs/services/hs-crypto/get_started_hsm.html)를 참조하십시오. 자세한 단계와 우수 사례는 [키 스토리지를 보호하기 위해 서비스 인스턴스 초기화](/docs/services/hs-crypto/initialize_hsm.html)를 참조하십시오.

## 3단계: 키 관리
{: #manage-keys}

{{site.data.keyword.hscrypto}} 대시보드에서 암호화를 위해 새 루트 키 또는 표준 키를 작성하거나 기존 키를 가져올 수 있습니다. 루트 키 및 표준 키에 대한 자세한 정보는 [키 소개](/docs/services/hs-crypto/keys_intro.html)를 참조하십시오.

### 키 새로 작성
{: #create-keys}

다음 단계를 완료하여 첫 암호화 키를 작성하십시오.

1. {{site.data.keyword.hscrypto}} 대시보드에서 **관리** &gt; **키 추가**를 클릭하십시오.
2. 키를 새로 작성하려면 **키 생성** 창을 선택하십시오.

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
        <td>{{site.data.keyword.hscrypto}}에서 관리할 <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">키의 유형</a>입니다.</td>
      </tr>
      <caption style="caption-side:bottom;">표 1. <b>키 작성</b> 설정에 대한 설명</caption>
    </table>

3. 키의 세부사항 채우기를 완료한 후 확인하려면 **키 작성**을 클릭하십시오.

서비스에서 작성된 키는 대칭 256비트 키이며, AES-CBC 알고리즘으로 지원됩니다. 보안 추가를 위해 키가 보안 {{site.data.keyword.cloud_notm}} 데이터 센터에 있는 FIPS 140-2 레벨 4 인증 HSM(Hardware Security Module)에서 생성됩니다.

### 고유 키 가져오기
{: #import-keys}

서비스에 기존 키를 도입하고 기존 키를 관리하여 KYOK(Keep Your Own Key)의 보안 이점을 사용할 수 있습니다.

다음 단계를 완료하여 기존 키를 추가하십시오.

1. {{site.data.keyword.hscrypto}} 대시보드에서 **관리** &gt; **키 추가**를 클릭하십시오.
2. 기존 키를 업로드하려면 **고유 키 가져오기** 창을 선택하십시오.

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
        <td>{{site.data.keyword.hscrypto}}에서 관리할 <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">키의 유형</a>입니다.</td>
      </tr>
      <tr>
        <td>키 자료</td>
        <td>{{site.data.keyword.hscrypto}} 서비스에 저장할 키 자료입니다(예: 대칭 키). 제공하는 키는 base64로 인코딩되어야 합니다.</td>
      </tr>
      <caption style="caption-side:bottom;">표 2. <b>고유 키 가져오기</b> 설정에 대한 설명</caption>
    </table>

3. 키의 세부사항 채우기를 완료한 후 확인하려면 **키 가져오기**를 클릭하십시오.

{{site.data.keyword.hscrypto}} 대시보드에서 새 키의 일반 특성을 검사할 수 있습니다.

## 다음에 수행할 작업
{: #get-started-next}

이제 키를 사용하여 앱과 서비스를 코딩할 수 있습니다. 서비스에 루트 키를 추가한 경우 루트 키를 사용하여 저장 데이터를 암호화하는 키를 보호하는 방법에 대해 자세히 알아보십시오. 시작하려면 [키 랩핑](/docs/services/hs-crypto/wrap-keys.html)을 확인하십시오.

- 루트 키를 사용한 암호화 키 관리 및 보호에 대해 알아보려면 [엔벨로프 암호화](/docs/services/key-protect/concepts/envelope-encryption.html)를 확인하십시오.
<!-- - To find out more about integrating the {{site.data.keyword.hscrypto}} service with other cloud data solutions, [check out the Integrations doc](/docs/services/key-protect/integrations/integrate-services.html). -->
- 프로그래밍 방식으로 키를 관리하는 방법에 대해 자세히 알아보려면 [{{site.data.keyword.hscrypto}} API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")를 확인하십시오](https://{DomainName}/apidocs/hs-crypto){: new_window}.

<!-- Complete the following steps to provision {{site.data.keyword.hscrypto}}:
1. Log in to your [IBM Cloud account ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/){:new_window}.
2. Visit [{{site.data.keyword.cloud_notm}} Experimental Services ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/catalog/labs/){:new_window} to see the list of services in experimental phase.
3. From the **All Categories** navigation pane on the left, click the **Security** category under **Platform**.
4. From the list of services, click the **{{site.data.keyword.hscrypto}}** tile.
5. Select the **{{site.data.keyword.hscrypto}} Lite Plan**, and click **Create** to provision an instance of {{site.data.keyword.IBM_notm}} CloudCrypto in the account, region, and resource group where you log in.-->

<!-- ## Installing ACSP client libraries -->

<!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client. Complete the following steps to install the ACSP client libraries in your local environment. -->

<!-- 1. Download the installation package from the [GitHub repository ![External link icon](image/external_link.svg "External link icon")](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto){:new_window}. In the **packages** folder, choose the installation package file that is suitable for your operation system and CPU architecture. For example, for Ubuntu on x86, choose `acsp-pkcs11-client_1.5-3.5_amd64.deb`.
2. Install the package to install the ACSP client libraries with the `dpkg` command. For example, `dpkg -i acsp-pkcs11-client_1.5-3.5_amd64.deb`. -->



<!-- ## Configuring ACSP client -->

<!-- At the current stage, {{site.data.keyword.hscrypto}} provides only self-signed certificates.

You need to configure the ACSP client to enable a proper secure communication channel (mutual TLS) to your service instance in the cloud. -->

<!-- 1. In your {{site.data.keyword.hscrypto}} service instance in {{site.data.keyword.cloud_notm}}, select **Manage** from the left navigator.
2. On the "Manage" screen, click the **Download Config** button to download the `acsp_client_credentials.uue` file.
3. Copy the `acsp_client_credentials.uue` file to the `/opt/ibm/acsp-pkcs11-client/config` directory in your local environment.
4. In the `/opt/ibm/acsp-pkcs11-client/config` directory, decode the file with the following command:
       `base64 --decode acsp_client_credentials.uue > acsp_client_credentials.tar`
5. Extract the client credentials file with the following command:
       `tar xf acsp_client_credentials.tar`
6. Move the `server-config` files into the default place with the following command:
       `mv server-config/* ./`
7. Rename the client credentials file with the following command:
       `mv acsp.properties.client acsp.properties`
8. (Optional:) Change group ID of the files with the following command:
       `chown root.pkcs11 *`
9. Enable ACSP to use the proper config for the service instance in the cloud:
       `export ACSP_P11=/opt/ibm/acsp-pkcs11-client/config/acsp.properties` -->

<!-- Now your ACSP client is operational and your {{site.data.keyword.hscrypto}} is ready to use!

For more information about ACSP client installation and configuration, see [ACSP Client Installation and Configuration Guide ![External link icon](image/external_link.svg "External link icon")](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/blob/master/doc/ACSP-client-config-guide.pdf){:new_window}. -->
