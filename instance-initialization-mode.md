---

copyright:
  years: 2020, 2022
lastupdated: "2022-01-26"

keywords: initialize service, key ceremony, hsm, tke, cloud tke, tke cli, management utilities, imprint mode, smart card, master key, key part, load master key

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:note: .note}
{:external: target="_blank" .external}
{:term: .term}

# Introducing service instance initialization approaches
{: #initialize-instance-mode}

Depending on your business needs and security requirements, {{site.data.keyword.hscrypto}} provides you with the following three approaches to initializing your service instance.
{: shortdesc}

- [Initializing service instances by using smart cards and the {{site.data.keyword.hscrypto}} Management Utilities](#instance-initialization-management-utilities)
- [Initializing service instances by using recovery crypto units](#instance-initialization-recovery-crypto-unit)
- [Initializing service instances by using key part files](#instance-initialization-key-files)


The following table compares the three approaches:

| Approaches | Tool | Master key storage | Master key backup | Master key rotation |
| ---------- | ---- | ------------------ | ---------------- | ------------------- |
| Using smart cards and the {{site.data.keyword.hscrypto}} Management Utilities   | The Management Utilities  | The master key is composed of several master key parts that are stored on smart cards.  | You are responsible for backing up the master key using smart cards.  | You need to prepare new master key parts on your smart card before you can rotate the master key for your service instance. |
| Using recovery crypto units   | {{site.data.keyword.cloud_notm}} TKE CLI plug-in  | The master key is automatically generated and stored within the recovery crypto units of your service instance.  | The master key is automatically backed up in recovery crypto units. You can recover your master key from the backups if the master key is lost or destroyed.  | You don't need to prepare a new master key for the rotation. The new master key is automatically generated in a recovery crypto unit and then propagated to the operational crypto units and other recovery crypto units. |
| Using key part files   | {{site.data.keyword.cloud_notm}} TKE CLI plug-in  | The master key is composed of several master key parts that are stored on your local workstation files.  | The local files serve as a backup of the master key. You need to make sure that the files are properly saved and only the master key custodian knows the password. | You need to prepare new master key parts on your local workstation before you can rotate the master key for your service instance.  |
{: caption="Table 1. Comparing three approaches to initializing service instances" caption-side="bottom"}

If smart cards are used to initialize the service instance, the recovery crypto units are not applicable and can be ignored. The backup of the master key relies on the backup of the smart cards in that case.
{: note}

## Initializing service instances by using smart cards and the Management Utilities
{: #instance-initialization-management-utilities}

For the highest level of security, you can use smart cards together with the {{site.data.keyword.hscrypto}} Management Utilities to initialize the service instance. This approach uses smart cards to store signature keys and master key parts. Signature keys and master key parts never appear in the clear outside the smart card.

### Understanding the Management Utilities
{: #understand-management-utilities}

The Management Utilities are composed of two applications that use smart cards to configure service instances: the Smart Card Utility Program and the Trusted Key Entry (TKE) application. To use the Management Utilities, you need to [order IBM-supported smart cards and smart card readers](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#order-smart-card-and-reader) and follow the instructions in [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

The following diagram illustrates the relationship between various components when you use the Management Utilities to initialize a service instance.

![The architecture of using smart cards and the Management Utilities](/images/tke_application_architecture.svg "Using the Management Utilities"){: caption="Figure 1. Using smart cards and the Management Utilities to initialize service instances" caption-side="bottom"}

- The Smart Card Utility Program

    One of the two applications that are installed as part of the Management Utilities. It sets up and manages the smart cards that are used by the Trusted Key Entry application.

- The Trusted Key Entry application

    One of the two applications that are installed as part of the Management Utilities. It uses smart cards to load master keys in service instances and perform other configuration tasks for service instances.

### Understanding smart cards
{: #understand-smart-card}

A smart card looks like a credit card with an embedded chip. The chip can perform a limited set of cryptographic operations and is loaded with custom software. In the Management Utilities, the Smart Card Utility Program loads custom software on the smart card to create two types of smart cards:

- Certificate authority smart cards

    The Certificate authority smart cards establish a set of smart cards that can work together, called a smart card zone.

- EP11 smart cards

    Enterprise PKCS #11 (EP11) smart cards hold an administrator signature key and up to 85 master key parts. The custom software on an EP11 smart card includes functions for signing a command by using a private signature key that is stored on the smart card and for encrypting a master key part for delivery to a crypto unit.

Smart cards are protected by a personal identification number (PIN) that must be entered on a smart card reader PIN pad before the smart card performs the operations. The EP11 smart card has a single PIN. The certificate authority smart card has two PINs and both must be entered to enable operations.

When you use smart cards, consider the following recommendations:

- Create each master key part on a separate EP11 smart card and assign each master key part to a different person. Create backup copies of all smart cards and store them in a safe place.

- Order 8 or 10 smart cards and configure them this way:

    - Create a certificate authority smart card and a backup certificate authority smart card.

        A backup certificate authority smart card can be created by using the Smart Card Utility Program. Select **CA Smart Card** > **Backup CA smart card** from the menu, and follow the prompts.

    - Create two EP11 smart cards to hold an administrator signature key. Generate the administrator signature key on one EP11 smart card and copy it to the other.

        The contents of an EP11 smart card can be copied to another EP11 smart card that was created in the same smart card zone by using the Trusted Key Entry application. On the **Smart card** tab, click **Copy smart card**, and follow the prompts.

    - Create four or six EP11 smart cards to hold master key parts. Generate an EP11 master key part on 2 or 3 of the smart cards, depending on whether you want to use two or three key parts when you load your master key. Copy each key part value to a backup EP11 smart card.

- For greater security, generate administrator signature keys on more EP11 smart cards and set the signature thresholds in your crypto units to a value greater than one. You can install up to eight administrators in your crypto units and specify that up to eight signatures are required for some administrative commands.

### Understanding smart card readers
{: #understand-smart-card-reader}

A smart card reader is a device that attaches to a workstation and allows the workstation to communicate with a smart card. To access a smart card, the smart card must be inserted in the smart card reader. Most smart card operations require the smart card PIN to be entered on the smart card reader PIN pad.

A driver for the smart card reader must be installed on the workstation before the smart card reader can be used. For more information, see [Installing the smart card reader driver](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#install-smart-card-reader-driver).

The TKE application uses smart card reader 1 to hold a smart card with a signature key, and uses smart card reader 2 to hold smart cards that contain master key parts.

After a smart card that contains a valid signature key is inserted in smart card reader 1 and the PIN is entered, the smart card can be used to sign multiple commands, without needing to enter the PIN again. If the smart card is removed from the reader and reinserted, the PIN must be reentered on the smart card reader PIN pad before extra commands can be signed.

## Initializing service instances by using recovery crypto units
{: #instance-initialization-recovery-crypto-unit}

If one or more recovery crypto units are allocated for your service instance, you can choose this approach to initialize your service instance. In this case, a random master key value is automatically generated in a recovery crypto unit and copied to the other crypto units for the service instance. The master key value never appears in the clear outside of the HSMs. This approach is more streamlined and easier to use compared to the other two options.

Currently, only the `us-south` and `us-east` regions are enabled with the recovery crypto units. Therefore, this option is only available in these two regions. For more information about supported regions, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).
{: note}

The following diagram shows the components of an example service instance with two recovery crypto units:

![The architecture of using recovery crypto units to initialize service instances](/images/minimum_touch_architecture.svg "Using recovery crypto units to initialize service instances"){: caption="Figure 2. Initializing service instances by using recovery crypto units" caption-side="bottom"}

The following sections explain each component in detail.

### Understanding {{site.data.keyword.cloud_notm}} TKE CLI plug-in
{: #understand-tke-plugin}

The TKE CLI plug-in is an addition to the {{site.data.keyword.cloud_notm}} command-line interface (CLI). With the TKE CLI plug-in, you can send commands to the crypto units in your service instance to load the master key. The TKE CLI plug-in supports two approaches for loading the master key.

If your service instance has recovery crypto units, you can load the master key by running the `ibmcloud tke auto-init` command. This command guides you through steps to add administrators and set the signature thresholds, and then generates a random master key value in one of the recovery crypto units in your service instance and copies the value to the other crypto units. For more information about this approach, see [Initializing service instances by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit).

You can also use the TKE CLI plug-in to load the master key using key parts stored in key part files. This approach can be taken regardless of whether your service instance has any recovery crypto units. Using this approach, you run a series of commands to generate signature keys and master key parts, add administrators, set the signature thresholds, and load the master key registers. For more information, see [Initializing service instances by using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

You need to be assigned the appropriate role to perform TKE CLI plug-in operations. For more information about the available service access roles, see [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).

For a complete list of commands available in the TKE CLI plug-in, see [{{site.data.keyword.cloud_notm}} Trusted Key Entry CLI plug-in reference](/docs/hs-crypto?topic=hs-crypto-cli-plugin-hpcs-cli-plugin#tke-cli-plugin).

### Understanding operational crypto units
{: #understand-operational-crypto-unit}

Operational crypto units are used to manage encryption keys and perform cryptographic operations. Operational crypto units are the crypto units that you send API requests to. When you create a service instance, the number of crypto units that you specify is the number of operational crypto units. Operational crypto units are located in different availability zones of the same region where your instance resides.

### Understanding recovery crypto units
{: #understand-recovery-crypto-unit}

Two recovery units are automatically assigned to your service instance without extra costs. One recovery unit is allocated in the same region as the operational crypto units, and the other is allocated in a backup region. When you run the `ibmcloud tke auto-init` or `ibmcloud tke auto-mk-rotate` command, a random master key value is generated in one of the recovery crypto units and then securely exported to the other crypto units (including failover crypto units if any) for the service instance.

The sole purpose of the recovery crypto units is to save a backup copy of the master key value. The recovery crypto units are not used when running operational workloads. If the current master key value is lost or destroyed, you can recover the master key value from either of the recovery crypto units by using the `ibmcloud tke auto-mk-recover` command. This command copies the value in the current master key register of a recovery crypto unit to the current master key register of other crypto units.



Currently, only the `us-south` and `us-east` regions are enabled with the recovery crypto units, which means, when a service instance is provisioned in either region, you are by default enabled with the option to back up your master keys in the recovery crypto units located in both regions. For more information about supported regions, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).
{: note}

For detailed instructions on recovering the master key, see [Recovering a master key from a recovery crypto unit](/docs/hs-crypto?topic=hs-crypto-recover-master-key-recovery-crypto-unit).

## Initializing service instances by using key part files
{: #instance-initialization-key-files}

You can also initialize your service instance by using master key parts that you create and store in files on your local workstation. You can use this approach regardless of whether or not your service instance includes recovery crypto units. In this case, the workstation key files serve as a backup copy of your master key value. To complete the initialization in this approach, you also need to use the {{site.data.keyword.cloud_notm}} TKE CLI plug-in.

### Understanding master key parts
{: #understand-master-key-parts}

In this approach, the master key is composed of several master key parts that you need to use the TKE CLI plug-in to create. For security considerations, each key part can be owned by a different person called [master key custodian](/docs/hs-crypto?topic=hs-crypto-manage-access#roles). Key parts are stored in workstation files and are protected by password. The master key custodian needs to make sure that the key files are properly saved and no one else knows the password.

The TKE CLI plug-in provides a series of commands to complete the initialization, including creating signature keys and master key parts, adding administrators, and loading the master key. For detailed steps, see [Initializing service instances by using key part files](https://test.cloud.ibm.com/docs/hs-crypto?topic=hs-crypto-initialize-hsm).
