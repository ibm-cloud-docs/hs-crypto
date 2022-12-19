---

copyright:
  years: 2020, 2022
lastupdated: "2022-12-19"

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Rotating master keys by using smart cards and the Management Utilities
{: #rotate-master-key-smart-cards}

You need to rotate the master key for your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance regularly to meet industry standards and cryptographic best practices. This topic guides you through the steps to rotate the master key by using smart cards and the Management Utilities.
{: shortdesc}

Master key rotation is currently supported only by the {{site.data.keyword.hscrypto}} Standard Plan.
{: note}

Rotating the master key reencrypts the keys in key storage by using the new master key value. After the keys in key storage are reencrypted, the value in the new master key register is promoted to the current master key register. Before you start rotating the master key, you need to:

- Understand {{site.data.keyword.hscrypto}} concepts, such as [master keys](/docs/hs-crypto?topic=hs-crypto-understand-concepts#master-key-concept), [master key parts](/docs/hs-crypto?topic=hs-crypto-understand-concepts#master-key-part-concept), and [signature keys](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-key-concept), and understand [how a master key is rotated](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro).
- Assign the **Manager** or **Crypto unit administrator** service access role to perform the Management Utilities operations. For more information about the access management, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).
- Configure all crypto units in the service instance the same.

You can rotate your master key only when PKCS #11 keystores are not enabled in your service instance.
{: important}

## Before you begin
{: #rotate-master-key-smart-cards-prerequisites}

Before you start, make sure that you have done the following:

1. The new master key parts are prepared for rotation. For information on how to create a new master key part, see [Generate the signature keys and master key parts](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities#step1-generate-keys-management-utilities).
2. Open the Trusted Key Entry application on your workstation and click the *Crypto units* tab. Check and make sure that `true` is displayed as the value of the SELECTED column for all crypto units in the service instance where you want to rotate the master key. If any crypto units in the service instance are not selected, select the crypto units by clicking the *Add crypto units* button and following the prompts.

    You can work with only one service instance at a time. If any crypto units in other service instances are selected, click the *Remove crypto units* button to unselect.
    {: note}

## Rotating master keys using smart cards and the Management Utilities
{: #rotate-master-key-smart-cards-steps}
{: help}
{: support}

To rotate the master key, follow these steps:

1. To load the new master key parts to the new master key register, follow these steps:

    1. Select the **Master keys** tab and click **Load**.
    2. If prompted, insert an EP11 smart card with an administrator signature key that is defined to the selected crypto units in smart card reader 1, and enter the smart card PIN on the smart card reader PIN pad.
    3. When prompted, enter the number of master key parts to be loaded. Only 2 or 3 master key parts are accepted.
    4. When prompted, insert the EP11 smart card that contains the first master key part in smart card reader 2 and enter the smart card PIN on the smart card reader PIN pad.
    5. Select the master key part to be loaded from the list of master key parts on the smart card.
    6. Repeat substep 4 and 5 for each master key part to be loaded.

    After all master key parts are loaded, the new master key register is in `Full uncommitted` state.

2. Commit the new master key by following these steps:

    1. Click **Commit** to move the master key to the `Full committed` state.
    2. If prompted, in smart card reader 1, insert an EP11 smart card with an administrator signature key that is defined to the selected crypto units and enter the smart card PIN on the smart card reader PIN pad. Repeat this operation if prompted for more EP11 smart cards with signature keys.

    After the process is complete, the new master key register is in `Full committed` state.

3. If you have any encryption keys that are encrypted with the current master key by using the GREP11 API and are stored locally, call the [RewrapKeyBlob GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-rewrapKeyBlob) to reencrypt the keys with the new master key.

    Make sure to perform this step before you rotate the master key. Otherwise, your keys that are encrypted with the current master key cannot be reencrypted and used.
    {: important}

4. To reencrypt root keys in the key management service keystore using the master key in the new master key register, click the **Rotate** button and click **Yes** on the message window.

    It might take approximately 60 seconds to reencrypt 3000 root keys. When the master key is being rotated, you cannot perform any key-related actions except for deleting keys.
    {: note}

    When you receive the following messages for system operations, click **OK** to continue:

    1. `Master key rotation started.`
    2. `MKS CRK rewrap successful, waiting on cryptounit-mk-setimm.`
    3. `Master key rotation successful.`

    The new master key is now in `Valid` state in the current master key register. Check out [Master key rotation](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro) for information on how the key states change.

You have successfully rotated the current master key with the new master key. Your root keys and encryption keys are now well protected by the new master key.

If an error occurs during master key rotation, see [Why can't I rotate master keys using smart cards](/docs/hs-crypto?topic=hs-crypto-troubleshoot-master-key-rotation-key-smart-cards).

## What's next
{: #rotate-master-key-smart-cards-next}

- To learn more about master key rotation, check out [Master key rotation introduction](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro).
- Go to the **KMS keys** tab of your instance dashboard to [manage root keys and standard keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-keys). To find out more about programmatically managing your keys, check out the {{site.data.keyword.hscrypto}} [key management service API reference doc](/apidocs/hs-crypto){: external}.
- To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
