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

# {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} の概説
{: #get-started}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} (略して {{site.data.keyword.hscrypto}}) は、鍵管理とクラウドのハードウェア・セキュリティー・モジュール (HSM) です。これはクラウド・データ暗号鍵とクラウド・ハードウェア・セキュリティー・モデルを制御できるように設計されており、FIPS 140-2 レベル 4 認証のハードウェアに基づいて構築された業界で無二のサービスです。
{:shortdesc}

{{site.data.keyword.hscrypto}} は、{{site.data.keyword.keymanagementservicefull_notm}} API と統合して鍵の生成と暗号化を行います。 {{site.data.keyword.hscrypto}} によって Keep Your Own Keys (KYOK: 自分の鍵の保持) 機能を使用できるので、達成可能なセキュリティーの最高レベルである FIPS 140-2 レベル 4 認証テクノロジーの暗号化ハードウェアにアクセスできます。 {{site.data.keyword.hscrypto}} は、ネットワーク・アドレス可能な HSM を備えています。
<!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on-->.  <!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.--> {{site.data.keyword.hscrypto}} について詳しくは、[{{site.data.keyword.hscrypto}} の概要](/docs/services/hs-crypto/overview.html)を参照してください。 暗号モジュールのセキュリティー要件について詳しくは、[FIPS 140-2 レベルの NIST の仕様 ![外部リンク・アイコン](image/external_link.svg "外部リンク・アイコン")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window} を参照してください。

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-platform/index.html){:new_window}. -->

このチュートリアルでは、マスター鍵を管理することによってサービス・インスタンスをセットアップする方法と、{{site.data.keyword.hscrypto}} ダッシュボードを使用して既存の暗号鍵を作成および追加する方法を説明します。


## ステップ 1: サービスのプロビジョン
{: #provision-service}

開始する前に、{{site.data.keyword.cloud_notm}} コンソールから {{site.data.keyword.hscrypto}} のインスタンスを作成する必要があります。 詳細なステップについては、[サービスのプロビジョニング](/docs/services/hs-crypto/provision.html)を参照してください。

## ステップ 2: サービス・インスタンスの初期化
{: #initialize-crypto}

鍵を管理するために、まずサービス・インスタンスを初期化する必要があります。 概要のクイック・チュートリアルについては、[サービス・インスタンス初期化の概要](/docs/services/hs-crypto/get_started_hsm.html)を参照してください。 詳細なステップとベスト・プラクティスについては、[鍵ストレージを保護するためのサービス・インスタンスの初期化](/docs/services/hs-crypto/initialize_hsm.html)を参照してください。

## ステップ 3: 鍵の管理
{: #manage-keys}

{{site.data.keyword.hscrypto}} ダッシュボードでは、暗号化用の新しいルート鍵または標準鍵を作成したり、既存の鍵をインポートしたりすることができます。 ルート鍵および標準鍵について詳しくは、[鍵の概要](/docs/services/hs-crypto/keys_intro.html)を参照してください。

### 新しい鍵の作成
{: #create-keys}

最初の暗号鍵を作成するには、以下の手順を実行します。

1. {{site.data.keyword.hscrypto}} ダッシュボードで、**「管理」** &gt; **「鍵の追加」**をクリックします。
2. 新しい鍵を作成するには、**「鍵の作成 (Create a key)」**ウィンドウを選択します。

    鍵の詳細を以下のように指定します。

    <table>
      <tr>
        <th>設定</th>
        <th>説明</th>
      </tr>
      <tr>
        <td>名前</td>
        <td>
          <p>鍵を簡単に識別するための、人間が理解できる固有の別名。</p>
          <p>プライバシーを保護するため、鍵の名前には、個人の名前や場所などの個人情報 (PII) を含めないように注意してください。</p>
        </td>
      </tr>
      <tr>
        <td>鍵のタイプ</td>
        <td>{{site.data.keyword.hscrypto}} で管理する<a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">鍵のタイプ</a>。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. <b>「鍵の作成 (Create a key)」</b>の設定の説明</caption>
    </table>

3. 鍵の詳細の記入が完了したら、**「鍵の作成 (Create key)」**をクリックして確認します。

サービス内で作成される鍵は、AES-CBC アルゴリズムによってサポートされている、対称 256 ビット鍵です。 セキュリティーを強化するために、鍵はセキュアな {{site.data.keyword.cloud_notm}} データ・センターにある FIPS 140-2 レベル 4 認証ハードウェア・セキュリティー・モジュール (HSM) で生成されます。

### 独自の鍵のインポート
{: #import-keys}

自分が所有する既存の鍵をサービスに導入して既存の鍵を管理することにより、Keep Your Own Key (KYOK) によるセキュリティー上の利点を活用できます。

既存の鍵を追加するには、以下の手順を実行します。

1. {{site.data.keyword.hscrypto}} ダッシュボードで、**「管理」** &gt; **「鍵の追加」**をクリックします。
2. 既存の鍵をアップロードするには、**「独自の鍵をインポート (Import your own key)」**ウィンドウを選択します。

    鍵の詳細を以下のように指定します。

    <table>
      <tr>
        <th>設定</th>
        <th>説明</th>
      </tr>
      <tr>
        <td>名前</td>
        <td>
          <p>鍵を簡単に識別するための、人間が理解できる固有の別名。</p>
          <p>プライバシーを保護するため、鍵の名前には、個人の名前や場所などの個人情報 (PII) を含めないように注意してください。</p>
        </td>
      </tr>
      <tr>
        <td>鍵のタイプ</td>
        <td>{{site.data.keyword.hscrypto}} で管理する<a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">鍵のタイプ</a>。</td>
      </tr>
      <tr>
        <td>鍵の素材</td>
        <td>{{site.data.keyword.hscrypto}} サービスで保管する鍵の素材 (対称鍵など)。 提供する鍵は、base64 エンコードでなければなりません。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. <b>「独自の鍵をインポート (Import your own key)」</b>の設定の説明</caption>
    </table>

3. 鍵の詳細の記入が完了したら、**「鍵のインポート (Import key)」**をクリックして確認します。

{{site.data.keyword.hscrypto}} ダッシュボードで、新しい鍵の一般特性を検査できます。

## 次に行うこと
{: #get-started-next}

これで、鍵を使用してアプリやサービスをコーディングできるようになりました。 ルート鍵をサービスに追加した場合、ルート鍵を使用して、保存データを暗号化する鍵を保護する方法についての詳細を確認することをお勧めします。 [鍵のラッピング](/docs/services/hs-crypto/wrap-keys.html)を確認して開始してください。

- ルート鍵を使用した暗号鍵の管理および保護について詳しくは、[エンベロープ暗号化](/docs/services/key-protect/concepts/envelope-encryption.html)を確認してください。
<!-- - To find out more about integrating the {{site.data.keyword.hscrypto}} service with other cloud data solutions, [check out the Integrations doc](/docs/services/key-protect/integrations/integrate-services.html). -->
- プログラムでの鍵の管理について詳しくは、[{{site.data.keyword.hscrypto}} API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/hs-crypto){: new_window} を確認してください。

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
