---

copyright:
  years: 2020, 2021
lastupdated: "2021-05-07"

keywords: rotate, rotate master key, master key rotation, master key rolling, rewrap root key, reencrypt root key

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}
{:term: .term}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}


# Rotating master keys by using key part files
{: #rotate-master-key-cli-key-part}

You need to rotate the master key for your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance regularly to meet industry standards and cryptographic best practices. To rotate the master key using master key part files on your local workstation, follow these steps.
{: shortdesc}

Rotating the master key reencrypts the keys in key storage using the new master key value. After the keys in key storage are reencrypted, the value in the new master key register is promoted to the current master key register. Before you start rotating the master key, you need to do the following steps:

- Understand {{site.data.keyword.hscrypto}} concepts, such as [master keys](/docs/hs-crypto?topic=hs-crypto-understand-concepts#master-key-concept), [master key parts](/docs/hs-crypto?topic=hs-crypto-understand-concepts#master-key-part-concept), and [signature keys](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-key-concept), and understand [how a master key is rotated](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro).
- Assign the **Manager** or **Crypto unit administrator** service access role to perform TKE CLI operations. For more information about the access management, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).
- Configure all crypto units in the service instance the same.

You can rotate your master key only when PKCS #11 keystores are not enabled in your service instance.
{: important}

## Before you begin
{: #rotate-master-key-cli-key-part-prerequisites}

Before you start, make sure to do the following steps:

1. Complete the [steps to set up the IBM Cloud CLI with TKE plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite).
2. Check and make sure that the current master key register is in `Valid` state with [the current master key loaded](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#load-master-keys), the new master key register is empty, and the crypto units of the service instance are not in [imprint mode](/docs/hs-crypto?topic=hs-crypto-understand-concepts#imprint-mode-concept) by running the following command:

  ```
  ibmcloud tke cryptounit-compare
  ```
  {: pre}
3. The new master key parts are prepared for rotation. For more information about how to create a new master key part, see [Create a set of master key parts to use](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#step4-create-master-key).

## Rotating master keys by using key part files
{: #rotate-master-key-cli-key-part-steps}
{: help}
{: support}

To rotate the master key by using key part files on your workstation, follow these steps:

1. Load the new master key parts to the new master key register with the following command:

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  To load a master key register, all master key part files and signature key files to be used must be present on a common workstation. If the files were created on separate workstations, make sure that the file names are different to avoid collision. The master key part file owners and signature key file owners need to enter the file passwords when the master key register is loaded on the common workstation.

  A list of the master key parts that are found on the workstation is displayed.

  When prompted, enter the master key parts to be loaded into the new master key register, the password for the signature key file to be used, and password for each selected key part file sequentially.

  The new master key is now in `Full uncommited` state in the new master key register.

  To load a new master key, you need to enter at least two master key parts. Make sure that at least one master key part is not used for the current master key. Otherwise, the same master key is generated and you are not able to load it to the new master key register.
  {: important}

2. Commit the new master key with the following command:

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  When prompted, enter the passwords for the signature key files to be used.

  The new master key is now in `Full commited` state in the new master key register.

3. If you have any encryption keys that are encrypted with the current master key using the GREP11 API and are not stored in the {{site.data.keyword.hscrypto}} keystore, call the [RewrapKeyBlob GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-rewrapKeyBlob) to reencrypt the keys with the new master key.

  Make sure to perform this step before you rotate the master key. Otherwise, your keys that are encrypted with the current master key cannot be reencrypted and used.
  {: important}

  For an introduction to the GREP11 API, see [Introducing EP11 over gRPC](/docs/hs-crypto?topic=hs-crypto-grep11_intro). You can also find code examples that are written in [Golang](https://github.com/IBM-Cloud/hpcs-grep11-go){: external} and [JavaScript](https://github.com/IBM-Cloud/hpcs-grep11-js) on the GREP11 API usage.

4. Rotate the current master key with the new master key and reencrypt the root keys that are managed by performing the following steps:

  1. Start master key rotation by running the following command:

    ```
    ibmcloud tke cryptounit-mk-rotate
    ```
    {: pre}

  2. When prompted, type `y` to proceed with the pre-check.

    The following settings are checked:
    * Only one service instance is selected and all crypto units from that service instance are select.
    * All selected crypto units have left imprint mode and have the same signature threshold.
    * The selected administrators match the administrators that are installed in the crypto units.
    * All crypto units have the new and current key registers configured correctly.

  3. To rotate the master key and activate the new master key, enter the password for the signature key file to be used when prompted.

    It might take approximately 60 seconds to reencrypt 3000 root keys. When the master key is being rotated, you cannot perform any key-related actions except for deleting keys.
    {: note}

    A success message is displayed when the master key rotation is completed.

    The new master key is now in `Valid` state in the current master key register. Check out [Master key rotation](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro) for more information about how the key states change.

Your root keys and encryption keys are now protected by the new master key.

If an error occurs during master key rotation, see [Why can't I rotate master keys by using key part files](/docs/hs-crypto?topic=hs-crypto-troubleshoot-master-key-rotation-key-part-files).

## What's next
{: #rotate-master-key-cli-key-part-next}

- To learn more about master key rotation, check out [Master key rotation introduction](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro).
- Go to the **Key management service keys** tab of your instance dashboard to [manage root keys and standard keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-keys). To find out more about programmatically managing your keys, check out the {{site.data.keyword.hscrypto}} [key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
- To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
