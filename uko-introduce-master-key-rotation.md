---
copyright:
  years: 2022, 2024
lastupdated: "2024-10-09"

keywords: uko, rotate, rotate master key, rotate encryption key, rotate keys automatically, key rotation, rewrap data

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Master key rotation - {{site.data.keyword.uko_full_notm}} Plan
{: #uko-master-key-rotation-intro}

After you load a master key to your {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} instance, you can rotate the master key on demand to meet industry standards and cryptographic best practices.
{: shortdesc}

A master key is used to wrap encryption keys that are managed in the service instance. With the master key rotation, you retire the original master key and load a new master key that reencrypts the entire key storage.


When the master key is being rotated, you can still perform some KMS key actions such as listing keys, retrieving key metadata, or deleting keys, but you cannot create or rotate keys. You cannot call either the PKCS #11 API or GREP11 API during the master key rotation.
{: note}


## How master key rotation works
{: #uko-how-master-key-rotation-works}

Master key rotation works by securely transferring the value between two types of master key registers in crypto units: new master key register and current master key register. Depending on [the approach that you use to initialize your service instance](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode), the rotation process is slightly different.


Key objects in the in-memory keystore are not automatically rotated after the master key rotation. If PKCS #11 keystores are enabled in your service instance, you need to restart all active PKCS #11 applications to clear the in-memory keystore after the master key rotation is complete. For detailed information, see [PKCS #11 implementation components](/docs/hs-crypto?topic=hs-crypto-uko-pkcs11-intro#uko-pkcs11-components).
{: important}


The following chart illustrates how the master key register state changes during the master key rotation. 

![How master key register state changes during master key rotation](/images/rotate-master-key.svg "How master key register state changes during master key rotation"){: caption="How master key register state changes during master key rotation" caption-side="bottom"}

### Rotating master keys by using smart cards and Management Utilities
{: #uko-how-master-key-rotation-works-smard-cards}

Master keys that are created with the Management Utilities can be rotated by using the smart cards, where master key parts are stored. Before you rotate the master key, you need to create the key parts that you are going to use.

You can create a new master key value using either 2 or 3 key parts. To be able to rotate the master key, the current master key registers must be in `Valid` state with the same verification pattern, and the new master key registers must be `Empty`.

You can rotate the master key using the Management Utilities regardless of whether your service instance has recovery crypto units assigned to it or not.

The following flow shows how master key rotation works in this mode:

1. Load the new master key register by clicking the **Load** button in the Trusted Key Entry application. The state of the new master key register is changed from `Empty` to `Full uncommitted`.
2. Commit the new master key value by clicking the **Commit** button in the Trusted Key Entry application. The new master key register state is changed to `Full committed`.
3. Reencrypt key storage and activate the new master key by clicking the **Rotate** button in the Trusted Key Entry application:
    1. Encryption keys in key storage are decrypted by using the value in the current master key register and then reencrypted by using the value in the new master key register. The rewrapping takes place inside the hardware security module (HSM), so it's secure.
    2. The new master key is activated and loaded to the current master key register in `Valid` state, and the new master key register is cleared and back to `Empty` state.

For detailed instructions, see [Rotating master keys by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-smart-cards).

### Rotating master keys by using recovery crypto units
{: #uko-how-master-key-rotation-works-recovery-crypto-unit}

If your service instance has recovery crypto units assigned to it, apart from using workstation files, you can also rotate the master keys using the `ibmcloud tke auto-mk-rotate` command. With this command, a random new master key value is generated in one of the recovery crypto units for the service instance and securely moved to the other crypto units in the service instance.

You don't need to prepare a new master key before the master key rotation. Before you can rotate the master key with the {{site.data.keyword.IBM_notm}} TKE CLI plug-in, all the current master key registers in both [operational crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#understand-operational-crypto-unit) and [recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#understand-recovery-crypto-unit) need to be in `Valid` state with the current master key loaded and all the new master key registers needs to be empty.

Comparing to the option where you load a new master key value from your local workstation files, the main difference in this mode is that a new master key value is first randomly generated within a recovery crypto unit and then exported to other crypto units.

The following flow shows how master key rotation works in this mode:

1. A new random master key value is generated in the new master key register of a recovery crypto unit assigned to the service instance. The state of the new master key register is changed from `Empty` to `Full uncommitted`.
2. The new master key value is copied to the new master key registers of the crypto units that are assigned to the service instance and other recovery crypto units for the service instance. All the new master key registers now are in `Full uncommitted` state.
3. The new master key is committed, and all the new master key registers state are changed to `Full committed`.
4. Key storage is reencrypted. Encryption keys that are managed in the service instance are decrypted using the current master key in the current master key registers and reencrypted using the new master key in the new master key registers.
5. The new master key is loaded to the current master key registers of the operational and recovery crypto units for the service instance in `Valid` state, and the new master key registers are cleared and back to `Empty` state.

For detailed instructions on how to rotate master keys by using recovery crypto units, see [Rotating master keys by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit).

### Rotating master keys by using workstation files
{: #uko-how-master-key-rotation-works-use-key-part-files}

Master keys that are created from workstation files can be rotated by using TKE CLI plug-in. When master keys are rotated, master key parts are stored in files on the local workstation. 

Similar to using the Management Utilities, you need to first create the 2 or 3 key parts that you are going to use. To be able to rotate the master key, the current master key registers must be in `Valid` state with the same verification pattern and the new master key registers must be `Empty`.

You can rotate the master key using TKE CLI plug-in regardless of whether your service instance has recovery crypto units assigned to it or not.

The following flow shows how master key rotation works in this mode:

1. Load the new master key register by using the `cryptounit-mk-load` command. The state of the new master key register is changed from `Empty` to `Full uncommitted`.
2. Commit the new master key value by using the `cryptounit-mk-commit` command. The new master key register state is changed to `Full committed`.
3. Reencrypt key storage and activate the new master key by using the `cryptounit-mk-rotate` command:
    1. Encryption keys in key storage are decrypted by using the value in the current master key register and then reencrypted by using the value in the new master key register. The rewrapping takes place inside the HSM, so it's secure.
    2. The new master key is activated and loaded to the current master key register in `Valid` state, and the new master key register is cleared and back to `Empty` state.

## How keys are protected during master key rotation
{: #uko-how-master-key-protect-rotation}

In the {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} plan, managed keys are protected in different ways: 
- Internal KMS keys that are activated in internal KMS keystores are encrypted by the master key directly. 
- External keys are wrapped by one or more key-encryption keys with advanced encryption. The key-encryption keys are encrypted by the master key. 

If you want to create a managed key or a vault during master key rotation, keep in mind the following considerations: 
- You can still create or activate internal KMS keys. However, an **Out of sync** flag can be displayed. To sync each of these keys, after the master key rotation is complete, select **Show details** on the Actions  ![Actions icon](../icons/action-menu-icon.svg "Actions")  menu and then click **Sync key**.  
- You can create external keys with no restrictions.  
- You can create vaults only after the master key rotation process is complete.


## How the UI reflects master key rotation
{: #uko-how-console-display-progress}

The following flow shows how master key rotation progress is displayed in the UI:

1. Master key rotation process starts

    After you start the master key rotation process by using one of the approaches introduced in [Master key rotation introduction](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro&interface=ui), you can go back to the UI to view the progress. 

2. Key rewrapping starts

    After the new master key register is loaded, all managed keys are to be rewrapped by the new master key. If the key-rewrapping progress is failed or the master key rotation is manuallly cancelled, a corresponding notification is displayed in the UI. Under **Overview** from the navigation, you can view the key progress indicators under **Crypto units** during the key rewrapping process. Three types of keys progress indicators are displayed:


    * **System internal keys**: Displays the rewrapping progress of any system internal keys that are not accessible by the user, such as the key-encryption keys.
    * **{{site.data.keyword.cloud_notm}} KMS keys**: Displays the rewrapping progress of KMS keys that are stored in the internal KMS keystores.
    

    If the only rewrapped keys are System internal keys, you can view the progress in the form of a percentage indicator under **Crypto units**. If multiple types of keys that need to be rewrapped, you can view the latest key-rewrapping progress by clicking the refresh button next to **Crypto units** or reloading the web page.
    {: tip}

3. Key rewrapping is complete

    After the key rewrapping process is complete, a notification is displayed in the UI. Then, you can continue to commit and activate the new master key using the approach that you choose. 

4. Master key rotation is complete

    After the master key rotation process is complete, a notification is displayed in the UI. Under **Overview** from the navigation, you can also find the timestamp of the key updates under **Crypto units**.



## What's next
{: #uko-master-key-rotation-next}

For more detailed instructions on options to rotate master keys, see:
- [Rotating master keys by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-smart-cards).
- [Rotating master keys by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit).
- [Rotating master keys by using workstation files](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part).
