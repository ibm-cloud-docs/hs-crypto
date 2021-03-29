---

copyright:
  years: 2020, 2021
lastupdated: "2021-03-11"

keywords: pkcs11 key, view ep11 key, create pkcs11 key, generate pkcs11 key, create cryptographic keys, create encryption keys, delete pkcs11 keys

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:external: target="_blank" .external}
{:term: .term}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Managing EP11 keys with the {{site.data.keyword.cloud_notm}} console
{: #manage-ep11-key-ui}

Apart from using the {{site.data.keyword.hscrypto}} [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api) to generate and use Enterprise PKCS #11 (EP11) keys, you can also use the {{site.data.keyword.cloud}} console to view, create, and delete EP11 keys.
{: shortdesc}

## Before you begin
{: #manage-ep11-key-ui-before}

Before you can manage EP11 keystores and keys with the console, complete the following steps to open your {{site.data.keyword.hscrypto}} dashboard:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}} and click the instance name.
4. Create an EP11 keystore to store the key. The keystore can be created [through the console UI](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui#create-ep11-keystore-ui) or [through the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api).

## Viewing EP11 keys
{: #view-ep11-key-ui}

For default service access roles that support viewing EP11 keys, see [service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles). If you are to create custom roles, make sure to assign the following actions to the custom role:

* `hs-crypto.keystore.listkeystoresbyids`
* `hs-crypto.keystore.listkeysbyids`

For instructions on creating custom roles, see [Creating custom roles](/docs/account?topic=account-custom-roles).

On the {{site.data.keyword.hscrypto}} dashboard, do the following to view EP11 key details:

1. To view a list of created EP11 keys, select the **Enterprise PKCS #11 keys** tab in the side menu.

  An EP11 key table is displayed with the following details.

    <table>
    <tr>
      <th>Setting</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>ID</td>
      <td>
        <p>The unique identifier that is assigned when the key is created.</p>
      </td>
    </tr>
    <tr>
      <td>Name</td>
      <td>
        <p>A human-readable alias for easy identification of your key. The value of the CKA_LABEL key attribute is displayed in this field.</p>
        <p>The key name might not be unique. You can assign multiple keys with the same name. However, it is suggested to assign a unique name to each key in the same keystore for easy identification.</p>
      </td>
    </tr>
    <tr>
      <td>Class</td>
      <td>
        <p>The class of the key. Possible values are **Public**, **Private**, and **Secret**. The value is determined by the CKA_CLASS key attribute.</p>
        <p>**Public** indicates the key is the public key of an asymmetric key pair. **Private** indicates the key is the private key of an asymmetric key pair. **Secret** indicates the key is a symmetric key.</p>
      </td>
    </tr>
    <tr>
      <td>Version</td>
      <td>
        <p>The version number of the key.</p>
        <p>When the key is first created, version 0 is assigned. The version number is increased by 1 sequentially upon each update, such as using the `C_SetAttributeValue` function to update a key attribute value.</p>
      </td>
    </tr>
    <tr>
      <td>Keystore</td>
      <td>
        <p>The unique identifier of the keystore the key is stored in. </p>
      </td>
    </tr>
    <tr>
      <td>Type</td>
      <td>The type of the EP11 key that is managed in {{site.data.keyword.hscrypto}}.</td>
    </tr>
        <caption style="caption-side:bottom;">Table 1. Describes the EP11 keys table</caption>
    </table>

2. To view details of the [key attributes](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs-attribute-list), click the overflow icon (...) of the key row, and then select **Show more details**.

  You can also identify the public key, the private key, and the symmetric key by checking the value of the CKA_CLASS attribute. `CKO_PUBLIC_KEY` indicates a public key; `CKO_PRIVATE_KEY` indicates a private key; `CKO_SECRET_KEY` indicates a symmetric key.
  {: tip}

## Creating EP11 keys
{: #create-ep11-key-ui}
{: help}
{: support}

For default service access roles that support creating EP11 keys, see [service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles). If you are to create custom roles, make sure to assign the following actions to the custom role:

* `hs-crypto.keystore.listkeystoresbyids`
* `hs-crypto.keystore.listkeysbyids`
* `hs-crypto.crypto.generatekey`
* `hs-crypto.crypto.generatekeypair`
* `hs-crypto.keystore.storenewkey`

For instructions on creating custom roles, see [Creating custom roles](/docs/account?topic=account-custom-roles).

Complete the following steps to create an EP11 key:

1. Select the **Enterprise PKCS #11 keys** tab in the side menu. You can see a list of existing EP11 keys with each having a unique ID.
2. Click **Create key**. In the **Create EP11 key** panel that is displayed, complete the following steps:

  1. Specify the following key details on the **Identifier** page:

    <table>
    <tr>
      <th>Setting</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>Key name</td>
      <td>
        <p>A human-readable alias for easy identification of your key.</p>
        <p>The key name length can be 1 to 32 characters. To protect your privacy, ensure that the key name does not contain personally identifiable information (PII), such as your name or location.</p>
        <p>The key name might not be unique. You can assign multiple keys with the same name. However, it is suggested to assign a unique name to each key in the same keystore for easy identification.</p>
      </td>
    </tr>
    <tr>
      <td>Key type</td>
      <td><p>The type of the EP11 key that you want to manage in {{site.data.keyword.hscrypto}}.</p></td>
    </tr>
    <tr>
      <td>Keystore</td>
      <td>
        <p>The unique identifier of the keystore with the keystore type appended. Choose one that you want the key to be stored in from the list. For an asymmetric key pair, you need to specify the keystore separately to store the public key and the private key.</p>
        <p>You can find all available keystores by clicking the **Enterprise PKCS #11 keystores** tab in the side menu.</p>
      </td>
    </tr>
        <caption style="caption-side:bottom;">Table 2. Describes the Identifier page</caption>
    </table>

    By default, two key IDs are automatically generated. One is for the public key, the other is for the private key. However, if you select a symmetric key type, such as an AES key, a DES key, or a Generic key, only one key ID is shown on the page.

  2. Specify key attributes by following these steps:

    * If you are creating an asymmetric key, specify key attributes on the **Public key attributes** and **Private key attributes** pages subsequently:

        1. The required attributes are listed with the default values. To modify the attribute values, click the pencil icon.
        2. To add additional attributes, click **Add public attribute** or **Add private attribute** depending on which page you are on. For a list of supported attributes, see [supported attributes table](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs-attribute-list) and [supported curve names for Elliptic Curve keys](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#supported-pkcs11-ec-curve-name).
        3. (Optional) You can delete additional attributes by clicking the trash can icon. The required attributes cannot be deleted.
        4. Click **Next** to continue.

    * If you are creating a symmetric key, such as an AES key, a DES key, and a Generic key, specify key attributes on the **Key attributes** page:

        1. The required attributes are listed with the default values. To modify the attribute values, click the pencil icon.
        2. To add additional attributes, click **Add attributes**. For a list of supported attributes, see [supported attributes table](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs-attribute-list).
        3. (Optional) You can delete additional attributes by clicking the trash can icon. The required attributes cannot be deleted.
        4. Click **Next** to continue.

  3. On the **Confirmation** page, verify the key details and click **Create key**.

    1. Verify the key details that are displayed, especially the key type, keystore, and key attributes.

      All the values cannot be modified through the console after the key is created.
      {:important}
    2. Click **Create key** to confirm the creation.

You have successfully created a EP11 key. The created key is displayed as the first row in the **Enterprise PKCS #11 keys** table.

## Deleting EP11 keys
{: #delete-ep11-key-ui}

For default service access roles that support deleting EP11 keys, see [service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles). If you are to create custom roles, make sure to assign the following actions to the custom role:

* `hs-crypto.keystore.listkeystoresbyids`
* `hs-crypto.keystore.listkeysbyids`
* `hs-crypto.keystore.deletekey`

For instructions on creating custom roles, see [Creating custom roles](/docs/account?topic=account-custom-roles).

If you want to delete an EP11 key, complete the following steps:

After you delete an EP11 key, you are not able to access the data associated with the key. This action cannot be undone.
{: important}

1. Select the **Enterprise PKCS #11 keys** tab in the side menu, and find the key that you want to delete in the list.
2. Click the overflow icon (...) in the key row, and click **Delete key**.
2. Verify the ID of the key to be deleted, and check the box to confirm the deletion.
3. Click **Delete keystore**.

## What's next
{: #manage-ep11-key-ui-next}

You can use EP11 keys for cryptographic operations with the PKCS #11 API. For more information, see [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api) and [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).
