---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

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

# 開始使用 {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #get-started}

<!-- {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is in the BETA phase and is for tryout and test purpose only. To prevent data loss, use only test data in the current service. This restriction also applies to using {{site.data.keyword.hscrypto}} with other  {{site.data.keyword.cloud_notm}} services.
{:important} -->

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}（簡稱 {{site.data.keyword.hscrypto}}）提供用於專用金鑰管理服務的雲端硬體安全模組 (HSM)。{{site.data.keyword.hscrypto}} 可協助您以便利且具成本競爭力的方式，以 IBM Z 加密的安全層次將資料加密。
{:shortdesc}

{{site.data.keyword.hscrypto}} 可與 {{site.data.keyword.keymanagementservicefull_notm}} API 整合以產生及加密金鑰。{{site.data.keyword.hscrypto}} 還啟用了「自行保管金鑰 (KYOK)」功能，用來存取採用 FIPS 140-2 Level 4 認證技術的加密硬體，這是可達到的最高安全層次。{{site.data.keyword.hscrypto}} 提供網路可定址的硬體安全模組 (HSM)<!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on-->。<!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.-->如需 {{site.data.keyword.hscrypto}} 的相關資訊，請參閱 [{{site.data.keyword.hscrypto}} 概觀](/docs/services/hs-crypto/overview.html)。如需加密模組之安全需求的相關資訊，請參閱 [NIST 對於 FIPS 140-2 層次的規格 ![外部鏈結圖示](image/external_link.svg "外部鏈結圖示")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}。

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-platform/index.html){:new_window}. -->

本指導教學將教導您如何管理主要金鑰來設定加密實例，以及使用 {{site.data.keyword.hscrypto}} 儀表板建立並新增現有的加密金鑰。


## 步驟 1：佈建服務
{: #provision}

開始之前，您必須從 {{site.data.keyword.cloud_notm}} 主控台建立 {{site.data.keyword.hscrypto}} 的實例。如需詳細步驟，請參閱[佈建服務](/docs/services/hs-crypto/provision.html)。

## 步驟 2：起始設定加密實例

若要管理金鑰，您必須先起始設定加密 (HSM) 實例。如需快速開始使用的指導教學，請參閱[開始使用加密實例起始設定](/docs/services/hs-crypto/get_started_hsm.html)。如需詳細步驟及最佳作法，請參閱[起始設定加密實例來保護金鑰儲存空間](/docs/services/hs-crypto/initialize_hsm.html)。

## 步驟 3：管理金鑰
{: #manage-keys}

從 {{site.data.keyword.hscrypto}} 儀表板，您可以建立用於加密的新根金鑰或標準金鑰，也可以匯入現有金鑰。如需根金鑰及標準金鑰的相關資訊，請參閱[金鑰簡介](/docs/services/hs-crypto/keys_intro.html)。

### 建立新金鑰
{: #create-keys}

請完成下列步驟，以建立第一個加密金鑰。

1. 從 {{site.data.keyword.hscrypto}} 儀表板中，按一下**管理** &gt; **新增金鑰**。
2. 若要建立新的金鑰，請選取**建立金鑰**視窗。

    指定金鑰的詳細資料：

    <table>
      <tr>
        <th>設定</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>
          <p>方便識別金鑰且人類可閱讀的唯一別名。</p>
          <p>若要保護您的隱私權，請確定金鑰名稱未包含個人識別資訊 (PII)（例如您的姓名或位置）。</p>
        </td>
      </tr>
      <tr>
        <td>金鑰類型</td>
        <td>您要在 {{site.data.keyword.hscrypto}} 中管理的<a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">金鑰類型</a>。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. <b>建立金鑰</b>設定的說明</caption>
    </table>

3. 當您填寫完金鑰的詳細資料時，請按一下**建立金鑰**以便確認。

在服務中所建立的金鑰是 AES-GCM 演算法所支援的對稱 256 位元金鑰。為了加強安全，金鑰是由位於安全 {{site.data.keyword.cloud_notm}} 資料中心的 FIPS 140-2 Level 4 認證硬體安全模組 (HSM) 所產生。

### 匯入自己的金鑰
{: #import-keys}

您可以將現有金鑰引入服務並管理您的現有金鑰，來獲得「自行保管金鑰 (KYOK)」的安全好處。

請完成下列步驟，以新增現有金鑰。

1. 從 {{site.data.keyword.hscrypto}} 儀表板中，按一下**管理** &gt; **新增金鑰**。
2. 若要上傳現有的金鑰，請選取**匯入自己的金鑰**視窗。

    指定金鑰的詳細資料：

    <table>
      <tr>
        <th>設定</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>
          <p>方便識別金鑰且人類可閱讀的唯一別名。</p>
          <p>若要保護您的隱私權，請確定金鑰名稱未包含個人識別資訊 (PII)（例如您的姓名或位置）。</p>
        </td>
      </tr>
      <tr>
        <td>金鑰類型</td>
        <td>您要在 {{site.data.keyword.hscrypto}} 中管理的<a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">金鑰類型</a>。</td>
      </tr>
      <tr>
        <td>金鑰資料</td>
        <td>您要在 {{site.data.keyword.hscrypto}} 服務中儲存的金鑰資料（例如對稱金鑰）。您提供的金鑰必須以 base64 編碼。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. <b>匯入自己的金鑰</b>設定的說明</caption>
    </table>

3. 當您填寫完金鑰的詳細資料時，請按一下**匯入金鑰**以便確認。

從 {{site.data.keyword.hscrypto}} 儀表板中，您可以檢查新金鑰的一般特徵。

## 下一步為何？

現在，您可以使用金鑰來撰寫應用程式及服務的程式碼。如果您新增了根金鑰給服務，建議您進一步瞭解如何使用根金鑰來保護將靜態資料加密的金鑰。請參閱[包裝金鑰](/docs/services/hs-crypto/wrap-keys.html)以便開始。

- 若要進一步瞭解如何使用根金鑰管理和保護您的加密金鑰，請參閱[封套加密](/docs/services/key-protect/concepts/envelope-encryption.html)。
- 若要進一步瞭解如何整合 {{site.data.keyword.hscrypto}} 服務與其他雲端資料解決方案，[請參閱整合文件](/docs/services/key-protect/integrations/integrate-services.html)。
- 若要進一步瞭解如何以程式設計方式管理您的金鑰，[請參閱 {{site.data.keyword.hscrypto}} API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}。

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
