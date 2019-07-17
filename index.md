---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-10"

Keywords: dedicated key management service, IBM Key, Key storage

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:external: target="_blank" .external}

# Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #get-started}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} for short) is a key management and cloud hardware security module (HSM). It is designed to enable you to take control of your cloud data encryption keys and cloud hardware security models, and is the only service in the industry built on FIPS 140-2 Level 4-certified hardware.
{:shortdesc}

{{site.data.keyword.hscrypto}} integrates with {{site.data.keyword.keymanagementservicefull_notm}} APIs to generate and encrypt keys. The Keep Your Own Keys (KYOK) function is also enabled by {{site.data.keyword.hscrypto}} to provide access to cryptographic hardware that is FIPS 140-2 Level 4 certified technology, the highest level attainable of security. {{site.data.keyword.hscrypto}} offers network addressable HSMs. <!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on. You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.--> For more information about {{site.data.keyword.hscrypto}}, see [{{site.data.keyword.hscrypto}} overview](/docs/services/hs-crypto/overview.html). For more information about security requirements for cryptographic modules, see [the specification of the NIST for FIPS 140-2 Level ![External link icon](image/external_link.svg "External link icon")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}.

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-platform/index.html){:new_window}. -->

This tutorial guides you how to set up your service instance by managing your master keys, and create and add existing cryptographic keys by using the {{site.data.keyword.hscrypto}} dashboard.


## Step 1: Provision the service
{: #provision-service}

Before you begin, you must create an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console. For detailed steps, see [Provisioning the service](/docs/services/hs-crypto/provision.html).

## Step 2: Initialize your service instance
{: #initialize-crypto}

To manage your keys, you need to initialize your service instance first. For a quick getting-started tutorial, see [Getting started with service instance initialization](/docs/services/hs-crypto/get_started_hsm.html). For detailed steps and best practices, see [Initializing service instances to protect key storage](/docs/services/hs-crypto/initialize_hsm.html).

## Step 3: Manage your keys
{: #manage-keys}

From the {{site.data.keyword.hscrypto}} dashboard, you can create new root keys or standard keys for cryptography, or you can import your existing keys. For more information on root keys and standard keys, see [Introduction to keys](/docs/services/hs-crypto/keys_intro.html).

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
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Description of the <b>Create a key</b> settings</caption>
    </table>

3. When you are finished filling out the key's details, click **Create key** to confirm.

Keys that are created in the service are symmetric 256-bit keys, supported by the AES-CBC algorithm. For added security, keys are generated by FIPS 140-2 Level 4 certified hardware security modules (HSMs) that are located in secure {{site.data.keyword.cloud_notm}} data centers.

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
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}.</td>
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
{: #get-started-next}

## What's next
{: #get-started-next}

You can start to use your keys to encode your apps and services. If you added a root key to the service, you might want to learn more about using the root key to protect the keys that encrypt your at-rest data. Check out [Wrapping keys](/docs/services/hs-crypto?topic=hs-crypto-wrap-keys) to get started.

- To find out more about managing and protecting your encryption keys with a root key, check out [Envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption).
- To find out more about integrating the {{site.data.keyword.hscrypto}} service with other cloud data solutions, [check out the Integrations doc](/docs/services/hs-crypto?topic=hs-crypto-integrate-services).
- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
