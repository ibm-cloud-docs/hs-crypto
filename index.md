---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}

***Disclaimer: {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is in the BETA phase and is for tryout and test purpose only. To prevent data loss, use only test data in the current service. This restriction also applies to using {{site.data.keyword.hscrypto}} with other  {{site.data.keyword.cloud_notm}} services. ***

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} for short) provides a cloud hardware security module (HSM) for a dedicated key management service. {{site.data.keyword.hscrypto}} helps you encrypt your data at the safety and security level of IBM Z cryptography in a convenient and cost competitive manner.
{:shortdesc}

{{site.data.keyword.hscrypto}} integrates with {{site.data.keyword.keymanagementservicefull_notm}} APIs to generate and encrypt keys. The Keep Your Own Keys (KYOK) function is also enabled by {{site.data.keyword.hscrypto}} to provide access to cryptographic hardware that is FIPS 140-2 Level 4 certified technology, the highest level attainable of security. {{site.data.keyword.hscrypto}} offers network addressable hardware security modules (HSMs)<!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on-->.  <!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.--> For more information about {{site.data.keyword.hscrypto}}, see [{{site.data.keyword.hscrypto}} overview](overview.html). For more information about security requirements for cryptographic modules, see [the specification of the NIST for FIPS 140-2 Level![External link icon](image/external_link.svg "External link icon")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}].

{{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/hypersecure-platform/index.html){:new_window}.

This tutorial guides you how to set up your crypto instance by managing your master keys, and create and add existing cryptographic keys by using the {{site.data.keyword.hscrypto}} dashboard.


## 1. Provision the service
{: #provision}

Before you begin, you must create an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console. For detailed steps, see [Provisioning the service](provision.html).

## 2. Initialize your crypto instance

To manage your keys, you need to initialize your crypto (HSM) instance first. For a quick getting-started tutorial, see [Getting started with crypto instance initialization](get_started_hsm.html). For detailed steps and best practices, see [Initializing crypto instances to protect key storage](initialize_hsm.html).

## 3. Manage your keys
{: #manage-keys}

From the {{site.data.keyword.hscrypto}} dashboard, you can create new root keys or standard keys for cryptography, or you can import your existing keys. For more information on root keys and standard keys, see [Introduction to keys](keys_intro.html).

### Creating new keys
{: #create-keys}

Complete the following steps to create your first cryptographic key.

1. From the {{site.data.keyword.hscrypto}} dashboard, click **Manage** &gt; **Add key**.
2. To create a new key, select the **Create a key** window.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>
          <p>A unique, human-readable alias for easy identification of your key.</p>
          <p>To protect your privacy, ensure that the key name does not contain personally identifiable information (PII), such as your name or location.</p>
        </td>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">type of key</a> that you would like to manage in {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Description of the <b>Create a key</b> settings</caption>
    </table>

3. When you are finished filling out the key's details, click **Create key** to confirm.

Keys that are created in the service are symmetric 256-bit keys, supported by the AES-GCM algorithm. For added security, keys are generated by FIPS 140-2 Level 4 certified hardware security modules (HSMs) that are located in secure {{site.data.keyword.cloud_notm}} data centers.

### Importing your own keys
{: #import-keys}

You can enable the security benefits of Keep Your Own Key (KYOK) by introducing your existing keys to the service and managing your existing keys.

Complete the following steps to add an existing key.

1. From the {{site.data.keyword.hscrypto}} dashboard, click **Manage** &gt; **Add key**.
2. To upload an existing key, select the **Import your own key** window.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>
          <p>A unique, human-readable alias for easy identification of your key.</p>
          <p>To protect your privacy, ensure that the key name does not contain personally identifiable information (PII), such as your name or location.</p>
        </td>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">type of key</a> that you would like to manage in {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <tr>
        <td>Key material</td>
        <td>The key material, such as a symmetric key, that you want to store in the {{site.data.keyword.hscrypto}} service. The key that you provide must be base64 encoded.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 2. Description of the <b>Import your own key</b> settings</caption>
    </table>

3. When you are finished filling out the key's details, click **Import key** to confirm.

From the {{site.data.keyword.hscrypto}} dashboard, you can inspect the general characteristics of your new keys.

## What's next

Now you can use your keys to code your apps and services. If you added a root key to the service, you might want to learn more about using the root key to protect the keys that encrypt your at-rest data. Check out [Wrapping keys](/docs/services/hs-crypto/wrap-keys.html) to get started.

- To find out more about managing and protecting your encryption keys with a root key, check out [Envelope encryption](/docs/services/key-protect/concepts/envelope-encryption.html).
- To find out more about integrating the {{site.data.keyword.hscrypto}} service with other cloud data solutions, [check out the Integrations doc](/docs/services/key-protect/integrations/integrate-services.html).
- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/hp-crypto){: new_window}.

<!-- Complete the following steps to provision {{site.data.keyword.hscrypto}}:
1. Log in to your [IBM Cloud account ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/){:new_window}.
2. Visit [{{site.data.keyword.cloud_notm}} Experimental Services ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/catalog/labs/){:new_window} to see the list of services in experimental phase.
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

For more information about ACSP client installation and configureation, see [ACSP Client Installation and Configuration Guide ![External link icon](image/external_link.svg "External link icon")](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/blob/master/doc/ACSP-client-config-guide.pdf){:new_window}. -->
