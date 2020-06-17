---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-17"

keywords: initialize service, key ceremony, hsm, tke, tke cli, management utilities, imprint mode, smart card, master key, key part, load master key

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}

# Initializing your service instance
{: #introduce-service}

Before you start initializing the service instance of {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, you might want to understand the process logic first.
{:shortdesc}

A {{site.data.keyword.hscrypto}} instance (service instance for short) is a group of [crypto units](#x9860404){: term} that are assigned to an {{site.data.keyword.cloud_notm}} user account. Crypto units contain [master keys](#x2908413){: term} that encrypt the contents of key storage. With the Keep You Own Keys technology, the service instance administrators are the only person who can access the master key.

The following diagram illustrates a services instance with two crypto units.

![Service instance components](/image/kms_service.svg "Service instance components"){: caption="Figure 1. Service instance components" caption-side="bottom"}

To initialize the service instance, you need to create administrator [signature keys](#x8250375){: term}, exit the [imprint mode](#x9860399){: term}, and load the master key to the instance. To meet your various security requirements, IBM offers you the following options to load the master key:

- Using the Management Utilities

  For the highest level of security, use the {{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Management Utilities to initialize the service instance. This solution uses smart cards to store signature keys and master key parts. Signature keys and master key parts never appear in the clear outside the smart card. For more information, see [Understanding the Management Utilities](#understand-management-utilities).

- Using the {{site.data.keyword.cloud_notm}} Trusted Key Entry CLI plug-in

  For a solution that does not require the purchase of smart card readers and smart cards, use the Trusted Key Entry (TKE) CLI plug-in to initialize the service instance. This solution uses workstation files encrypted with a key that is derived from a file password to store signature keys and master key parts. When the keys are used, file contents are decrypted and appear temporarily in the clear in workstation memory. For more information, see [Understanding the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](#understand-tke-plugin).

## Understanding crypto units
{: #understand-crypto-unit}

A single unit that is composed of a [hardware security module (HSM)](#x6704988){: term} and the corresponding software stack that is dedicated to HSM is referred to as a *crypto unit*. Each crypto unit can manage up to 5000 digital keys. If you're setting up a production environment, it is suggested to assign at least two crypto units per service instance for high availability. The crypto units are located in different availability zones within the region that you select when you create the service instance. All crypto units in a service instance need to be configured the same. If one part of the IBM Cloud can't be accessed, the crypto units in a service instance can be used interchangeably.

## Understanding imprint mode and signature keys
{: #understand-imprint-mode}

To initialize a {{site.data.keyword.hscrypto}} service instance, the crypto units need to start in a clear state that is known as *Imprint Mode*. A crypto unit in imprint mode is not secure because actions towards a crypto unit in imprint mode don't need to be signed with any administrator signature keys. However, you need to set up crypto unit administrators and create administrator signature keys in imprint mode.

The following flow chart shows how the signature keys are being created and assigned on a service instance with two crypto units.

![Creating and assigning signature keys](/image/sigkey_flow.svg "How to create and assign signature keys"){: caption="Figure 3. Creating and assigning signature keys" caption-side="bottom"}

Signature keys are created and assigned by following this procedure:

1. The administrator creates the signature key pairs.
  The private and public key parts are stored on local workstation or smart card.
2. The administrator is added by assigning the public signature key part to the crypto unit.
  The public key part is placed in a certificate that is installed in a target crypto unit to define a crypto unit administrator.
3. The crypto unit exits imprint mode.

You need to keep in mind of the following items when you initialize the service instance:

- The command to exit imprint mode must be signed by one of the added crypto unit administrators by using the signature key.
- After the crypto unit exits imprint mode, the administrators need to sign any commands with their own signature keys.
- The master key can be loaded only after the crypto unit exits imprint mode.

## Understanding master keys and master key parts
{: #understand-master-keys}

A master key is used to encrypt data in a service instance. With the master key, you own the root of trust that encrypts the entire key hierarchy, including root keys and standard keys. Each service instance has only one master key.

A master key is composed of at least two master key parts. For security considerations, each key part is owned by a different key owner. The key owner need to be the only person who knows the password that is associated with the key part file.

{{site.data.keyword.IBM_notm}} does not back up or touch the master key, and has no way to copy it or restore it to a different machine or data center. If you delete the master key of the service instance, you can effectively crypto-shred all data that was encrypted with the keys that are managed in the service.

To use {{site.data.keyword.hscrypto}} to protect your keys and data, you need to first initialize your service instance by loading master key parts to the service instance from the smart cards with the TKE application or from the workstation with the TKE CLI plug-in.

## Understanding the Management Utilities
{: #understand-management-utilities}

The Management Utilities are two applications that use smart cards to configure service instances. The Smart Card Utility Program sets up and manages the smart cards used. The Trusted Key Entry (TKE) application uses those smart cards to configure service instances.

To use the Management Utilities, you need to order IBM-supported smart cards and smart card readers.

The following diagram illustrates the relationship between various components when you use the Management Utilities to initialize a service instance.

![The architecture of using the Management Utilities](/image/tke_application_architecture.svg "Using the Management Utilities"){: caption="Figure 4. Using the Management Utilities to initialize service instances" caption-side="bottom"}

### Understanding smart cards
{: #understand-smart-cards}

A smart card looks like a credit card with an embedded chip. The chip can perform a limited set of cryptographic operations and is loaded with custom software. In the Management Utilities, the Smart Card Utility Program loads custom software on the smart card to create two types of smart cards:

- Certificate authority smart cards

  The Certificate authority smart cards establish a set of smart cards that can work together, called *a smart card zone*.

- EP11 smart cards

  Enterprise PKCS #11 (EP11) smart cards hold an administrator signature key and up to 85 master key parts. The custom software on an EP11 smart card includes functions for signing a command by using a private signature key that is stored on the smart card and for encrypting a master key part for delivery to a crypto unit.

Smart cards are protected by a personal identification number (PIN) that must be entered on a smart card reader PIN pad before the smart card performs the operations. The EP11 smart card has a single PIN. The certificate authority smart card has two PINs and both must be entered to enable operations.

On an EP11 smart card, if an incorrect PIN is entered three times, the smart card becomes blocked and can't be used for operations that require PIN entry. An EP11 smart card can be unblocked by using the Smart Card Utility Program. You need the certificate authority smart card that is used to initialize the EP11 smart card to unblock an EP11 smart card. To unblock an EP11 smart card, select **EP11 Smart Card** > **Unblock EP11 smart card** from the menu, and follow the prompts.

A certificate authority smart card becomes blocked if an incorrect PIN is entered five times. If a certificate authority smart card becomes blocked, it can't be unblocked.

#### Smart card setup recommendations
{: #smart-card-considerations}

Because smart cards are the only place where signature keys and master key parts are saved, it is suggested that you prepare a backup copy of all smart cards. A backup certificate authority smart card can be created by using the Smart Card Utility Program. Select **CA Smart Card** > **Backup CA smart card** from the menu, and follow the prompts.

The contents of an EP11 smart card can be copied to another EP11 smart card that was created in the same smart card zone by using the Trusted Key Entry application. On the **Smart card** tab, click **Copy smart card**, and follow the prompts.

It is suggested that each master key part is created on a separate EP11 smart card and be assigned to a different person. Backup copies of all smart cards need to be created and stored in a safe place. It is suggested that you buy eight or 10 smart cards and initialize them this way:

- Create a certificate authority smart card and a backup certificate authority smart card.
- Create two EP11 smart cards to hold an administrator signature key. Generate the administrator signature key on one EP11 smart card and copy it to the other.
- Create four or six EP11 smart cards to hold master key parts. Generate an EP11 master key part on two or three of the smart cards, depending on whether you want to use two or three key parts when you load your master key. Copy each key part value to a backup EP11 smart card.

For greater security, you can generate administrator signature keys on additional EP11 smart cards and set the signature thresholds in your crypto units to a value greater than one. You can install up to eight administrators in your crypto units and specify that up to eight signatures are required for some administrative commands.

### Understanding smart card readers
{: #understand-smart-card-reader}

A smart card reader is a device that attaches to a workstation and allows the workstation to communicate with a smart card. To access a smart card, the smart card must be inserted in the smart card reader. Most smart card operations require the smart card PIN to be entered on the smart card reader PIN pad.

A driver for the smart card reader must be installed on the workstation before the smart card reader can be used. For more information, see [Installing the smart card reader driver](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#install-smart-card-reader-driver).

The Trusted Key Entry application uses smart card reader 1 to hold a smart card with a signature key, and uses smart card reader 2 to hold smart cards that contain master key parts.

After a smart card that contains a valid signature key is inserted in smart card reader 1 and the PIN is entered, the smart card can be used to sign multiple commands, without needing to enter the PIN again. If the smart card is removed from the reader and reinserted, the PIN must be reentered on the smart card reader PIN pad before extra commands can be signed.

### Understanding the Smart Card Utility Program
{: #understand-smart-card-application}

The Smart Card Utility Program is one of the two applications that are installed as part of the Management Utilities. It sets up and manages the smart cards that are used by the Trusted Key Entry application.

### Understanding the Trusted Key Entry application
{: #understand-tke-application}

The Trusted Key Entry application is one of the two applications that are installed as part of the Management Utilities. It uses smart cards to load master keys in service instances and perform other configuration tasks for service instances.

## Understanding the {{site.data.keyword.cloud_notm}} TKE CLI plug-in
{: #understand-tke-plugin}

When you choose to store the signature key and master key parts on your workstation, use the {{site.data.keyword.cloud_notm}} TKE CLI plug-in to load the master key. With the TKE CLI plug-in, you can load the master key by issuing corresponding commands. No additional hardware is needed. However, as master key parts are stored on your local workstation, the TKE CLI plug-in provides a comparatively lower level of security.

For the complete command reference, see [Trusted Key Entry CLI plug-in reference]((/docs/hs-crypto-cli-plugin/hs-crypto-cli-plugin-tke_cli_plugin)). For detailed instructions, see [Initializing service instances with {{site.data.keyword.cloud_notm}} Trusted Key Entry CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

## Understanding how master key is loaded
{: #understand-key-ceremony}

After the crypto unit exits imprint mode, you need to create at least two master key parts to be used to build your master key. In a production environment, it is suggested to create at least three key parts that are owned by different administrators for security considerations.

After you create the required number of master key parts to use, you can load your master key. The following steps are used to create and run the load key command. A command is needed for every crypto unit that is being updated.

Each crypto unit has two master key registers: a new master key register and a current master key register. The value in the current master key register encrypts the contents of the user's key storage. The new master key register is used to change the value in the current master key register. When you change the value in the current master key register, the contents of key storage need to be reenciphered with the new master key value. Both the current master key value and the new master key value are needed. Key values in key storage are deciphered by using the value in the current master key register and then reenciphered by using the value in the new master key register. The reenciphering takes place inside the HSM, so it's secure. After the full contents of key storage are reenciphered, the value in the new master key register can be moved into the current master key register.

The following flow chart illustrates how the master key register state changes, and how the master key is loaded.

![Loading master keys](/image/master_key_register.svg "How to load a master key"){: caption="Figure 5. Loading master key" caption-side="bottom"}

In the following chart, each crypto unit loads the master key with the following steps:

1. Load the New Master Key Register with the master key. After the master key is loaded, the New Master Key Register is in FULL UNCOMMITTED state.
2. Commit the New Master Key Register. After it is committed, the New Master Key Register is in FULL COMMITTED state.
3. Activate the Current Master Key Register. By doing so, the New Master Key Register value is copied into the Current Master Key Register, and the New Master Key Register is cleared.
