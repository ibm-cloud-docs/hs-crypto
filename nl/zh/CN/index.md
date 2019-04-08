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

# {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} 入门
{: #get-started}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}（简称 {{site.data.keyword.hscrypto}}）是密钥管理和云硬件安全模块 (HSM)。它旨在让您能够控制云数据加密密钥和云硬件安全模型，并且是行业中唯一构建于 FIPS 140-2 4 级认证硬件上的服务。
{:shortdesc}

{{site.data.keyword.hscrypto}} 与 {{site.data.keyword.keymanagementservicefull_notm}} API 集成以生成并加密密钥。{{site.data.keyword.hscrypto}} 也支持使用“保管自己的密钥”(KYOK) 功能来访问加密硬件，这是 FIPS 140-2 4 级认证的技术，是可实现的最高级别安全性。{{site.data.keyword.hscrypto}} 提供网络可寻址 HSM。<!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on-->.  <!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.--> 有关 {{site.data.keyword.hscrypto}} 的更多信息，请参阅 [{{site.data.keyword.hscrypto}} 概述](/docs/services/hs-crypto/overview.html)。有关加密模块的安全性需求的更多信息，请参阅 [ FIPS 140-2 级别的 NIST 规范 ![外部链接图标](image/external_link.svg "外部链接图标")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}。

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-platform/index.html){:new_window}. -->

本教程会引导您逐步通过管理主密钥来设置服务实例，并使用 {{site.data.keyword.hscrypto}} 仪表板来创建密钥和添加现有密钥。


## 第 1 步：供应服务
{: #provision-service}

在开始之前，必须从 {{site.data.keyword.cloud_notm}} 控制台创建 {{site.data.keyword.hscrypto}} 的实例。有关详细步骤，请参阅[供应服务](/docs/services/hs-crypto/provision.html)。

## 第 2 步：初始化服务实例
{: #initialize-crypto}

要管理密钥，您需要先初始化服务实例。有关快速入门教程，请参阅[服务实例初始化入门](/docs/services/hs-crypto/get_started_hsm.html)。有关详细步骤和最佳实践，请参阅[初始化服务实例以保护密钥存储器](/docs/services/hs-crypto/initialize_hsm.html)。

## 第 3 步：管理密钥
{: #manage-keys}

在 {{site.data.keyword.hscrypto}} 仪表板中，可以创建用于加密的新根密钥或标准密钥，也可以导入现有密钥。有关根密钥和标准密钥的更多信息，请参阅[密钥简介](/docs/services/hs-crypto/keys_intro.html)。

### 创建新密钥
{: #create-keys}

要创建第一个密钥，请完成以下步骤。

1. 在 {{site.data.keyword.hscrypto}} 仪表板中，单击**管理** &gt; **添加密钥**。
2. 要创建新密钥，请选择**创建密钥**窗口。

    指定密钥的详细信息：

    <table>
      <tr>
        <th>设置</th>
        <th>描述</th>
      </tr>
      <tr>
        <td>名称</td>
        <td>
          <p>密钥的人类可读的唯一别名，以便可轻松识别密钥。</p>
          <p>为保护隐私，请确保密钥名称不包含个人可标识信息 (PII)，例如，姓名或位置。</p>
        </td>
      </tr>
      <tr>
        <td>密钥类型</td>
        <td>要在 {{site.data.keyword.hscrypto}} 中管理的<a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">密钥类型</a>。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述<b>创建密钥</b>设置</caption>
    </table>

3. 填写完密钥详细信息后，单击**创建密钥**以进行确认。

服务中创建的密钥是 AES-CBC 算法支持的 256 位对称密钥。为了提高安全性，密钥通过位于安全 {{site.data.keyword.cloud_notm}} 数据中心且通过 FIPS 140-2 4 级认证的硬件安全模块 (HSM) 生成。

### 导入自己的密钥
{: #import-keys}

可以通过将现有密钥引入服务并管理现有密钥来利用“保管自己的密钥”(KYOK) 的安全优势。

要添加现有密钥，请完成以下步骤。

1. 在 {{site.data.keyword.hscrypto}} 仪表板中，单击**管理** &gt; **添加密钥**。
2. 要上传现有密钥，请选择**导入自己的密钥**窗口。

    指定密钥的详细信息：

    <table>
      <tr>
        <th>设置</th>
        <th>描述</th>
      </tr>
      <tr>
        <td>名称</td>
        <td>
          <p>密钥的人类可读的唯一别名，以便可轻松识别密钥。</p>
          <p>为保护隐私，请确保密钥名称不包含个人可标识信息 (PII)，例如，姓名或位置。</p>
        </td>
      </tr>
      <tr>
        <td>密钥类型</td>
        <td>要在 {{site.data.keyword.hscrypto}} 中管理的<a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">密钥类型</a>。</td>
      </tr>
      <tr>
        <td>密钥资料</td>
        <td>要在 {{site.data.keyword.hscrypto}} 服务中存储的密钥资料，例如，对称密钥。提供的密钥必须采用 Base64 编码。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. 描述<b>导入自己的密钥</b>设置</caption>
    </table>

3. 填写完密钥详细信息后，单击**导入密钥**以进行确认。

在 {{site.data.keyword.hscrypto}} 仪表板中，可以检查新密钥的常规特征。

## 后续工作
{: #get-started-next}

现在，可使用密钥对应用程序和服务进行编码。如果向服务添加了根密钥，那么可能要了解有关使用根密钥来保护用于加密静态数据的密钥的更多信息。请查看[打包密钥](/docs/services/hs-crypto/wrap-keys.html)以开始。

- 要查找有关使用根密钥来管理和保护加密密钥的更多信息，请查看[包络加密](/docs/services/key-protect/concepts/envelope-encryption.html)。
<!-- - To find out more about integrating the {{site.data.keyword.hscrypto}} service with other cloud data solutions, [check out the Integrations doc](/docs/services/key-protect/integrations/integrate-services.html). -->
- 要了解有关以编程方式管理密钥的更多信息，请[查看 {{site.data.keyword.hscrypto}} API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto){: new_window}。

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
