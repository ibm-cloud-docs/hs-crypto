---

copyright:
  years: 2018, 2021
lastupdated: "2021-06-28"

keywords: hsm, hardware security module, key ceremony, master key, signature key, signature threshold, imprint mode, load master key, master key register, initialize service, smart card, trusted key entry application, tke application, management utilities

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:note: .note}
{:hide-in-docs: .hide-in-docs}
{:hide-dashboard: .hide-dashboard}
{:external: target="_blank" .external}
{:term: .term}
{:video: .video}


# Initializing service instances with smart cards and the Management Utilities
{: #initialize-hsm-management-utilities}

Before you can use your {{site.data.keyword.hscrypto}} instance, you need to first initialize your service instance by loading the master key. Initialize your service instance by using smart cards and the {{site.data.keyword.hscrypto}} Management Utilities with the steps that are provided.
{: shortdesc}

For an introduction to the approaches of service instance initialization and the related fundamental concepts, see [Initializing service instances](/docs/hs-crypto?topic=hs-crypto-introduce-service) and [Introducing service instance initialization approaches](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode).

The {{site.data.keyword.hscrypto}} [Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#understand-management-utilities) use smart cards to hold [signature keys](#x8250375){: term} and master key parts. You need to complete the tasks in [Setting up smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities) before you can complete the steps in this task.

You can also watch the following video to learn how to initialize {{site.data.keyword.hscrypto}} instances with smart cards and the Management Utilities:

![Initialize Hyper Protect Crypto Services with smart cards and the Management Utilities](https://www.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/27941801/partner_id/1773841?iframeembed=true&entry_id=1_lo2fmwbb){: video output="iframe" data-script="none" id="mediacenterplayer" frameborder="0" width="560" height="315" allowfullscreen webkitallowfullscreen mozAllowFullScreen}

## Before you begin
{: #initialize-hsm-management-utilities-prerequisites}

1. Make sure that you [set up the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities).
2. Complete [the prerequisite steps](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite) before you initialize your service instance.
3. Plug the two smart card readers into the USB ports of your workstation.
4. Start the Trusted Key Entry application by changing to the subdirectory where you install the Management Utilities applications and running the following command:

  ```
  ./tke
  ```
  {: pre}

## Loading the master key from the smart cards
{: #load-master-key-management-utilities}

Crypto units that are assigned to an {{site.data.keyword.cloud_notm}} user start in a cleared state that is known as [imprint mode](#x9860399){: term}. To load the master key from the smart cards, complete the following steps with the Trusted Key Entry application:

### Step 1: Generate the signature keys and master key parts
{: #step1-generate-keys-management-utilities}

1. To generate a signature key for an administrator, select the **Smart card** tab, and click **Generate signature key**.

  When prompted, insert an [EP11 smart card](/docs/hs-crypto?topic=hs-crypto-understand-concepts#smart-card-concept) in smart card reader 2. Enter a name for the administrator, and enter the personal identification number (PIN) for the smart card on the smart card reader PIN pad.

  An administrator signature key is generated and stored on the smart card. Repeat this step to create multiple signature keys if needed.

  Each smart card can contain only one signature key. If you want to set up multiple administrators, repeat this step by using different EP11 smart cards.
  {: tip}

2. To generate the master key parts for service instance initialization, on the **Smart card** tab, click **Generate key part**.

  If prompted, insert an EP11 smart card in smart card reader 2 and enter the smart card PIN. Enter a description for the key part.

  A random master key part is generated and stored on the smart card.

  To create more master key parts, repeat this step.

  You need to generate at least two master key parts to load a master key. For added security, it is suggested to generate three master key parts. To improve security, you can choose to generate signature keys and master key parts on separate smart cards and assign each smart card to a different person. For more information, see [Smart card setup recommendations](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-smart-card-setup).
  {: important}

3. (Optional) If you want to create a backup copy of an EP11 smart card, click **Copy smart card** on the **Smart card** tab and follow the prompts.
4. (Optional) The signature keys and master key parts that are created with the TKE CLI plug-in and saved in a workstation file can be copied to a smart card. To do so, on the **Smart card** tab, click **Copy signature key file** or **Copy key part file** and follow the instructions. To copy the signature key or key part to a smart card, you need to provide the password for the file.

### Step 2: Select the crypto units where the master key is to be loaded
{: #step2-select-crypto-units-management-utilities}

Select the **Crypto units** tab. A list of [crypto units](#x9860404){: term} in the target resource group under the current user account is displayed. The SELECTED column shows what crypto units you're going to work with in later commands.

For more information about how to retrieve your service instance ID, see [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
{: tip}

- To select extra crypto units to work with, click **Add crypto units** and enter the CRYPTO UNIT NUM (crypto unit numbers) of the extra crypto units you want to work with. You can enter multiple crypto unit numbers, which are separated by a space.
- To remove crypto units from the set you're going to work with, click **Remove crypto units** and enter the CRYPTO UNIT NUM of the crypto units you want to remove. You can enter multiple crypto unit numbers, which are separated by a space.

When the operations are done, `true` is displayed in the SELECTED column for each crypto unit that is to be affected by later commands. If more than one crypto unit is assigned to a service instance, all crypto units in the service instance must be configured the same.



### Step 3: Add administrators to the selected crypto units
{: #step3-add-administrator-management-utilities}

The command to load a master key must be signed by an administrator that is predefined to the crypto unit. This step predefines an administrator.

1. Select the **Administrators** tab. This tab displays a list of administrators that are allowed to sign commands to the crypto unit.
2. Click **Add administrator**.
3. When prompted, insert the EP11 smart card that holds that administrator signature key in smart card reader 1, and enter the PIN on the smart card reader PIN pad.

The public signature key and administrator name are read from the smart card and installed in the crypto unit. When the operation is done, the administrator's name is displayed in the ADMIN NAME field of the selected crypto units.

For security and compliance reasons, the administrator name of the crypto unit might be shown up in logs for auditing purposes.
{: note}

Repeat this step if you want to add multiple administrators. The number of administrators that are added must be equal to or greater than the larger of the following values:
* The [signature threshold](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-thresholds-concept) value. The signature threshold controls how many signatures are needed to run most administrative commands.
* The revocation signature threshold value that you intend to set in Step 4. The revocation signature threshold controls how many signatures are needed to remove an administrator.

Do not remove the administrator signature keys from your smart cards. Otherwise, you are not able to perform TKE actions that need to be signed, such as zeroizing crypto units and rotating master keys.
{: important}

### Step 4: Set the signature thresholds to exit imprint mode in the selected crypto units
{: #step4-exit-imprint-mode-management-utilities}

When crypto units in service instances are assigned to a user, they begin in a cleared state that is called imprint mode. In imprint mode, most operations on the crypto unit are disabled. To load the master key in a crypto unit, first exit imprint mode by setting the signature thresholds to a value greater than zero.

1. To set the signature thresholds, select the **Signature thresholds** tab and click **Change signature thresholds**.
2. When prompted, enter the new signature threshold value and the new revocation signature threshold value. 
  The values must be numbers between one and eight and do not need to be the same. The signature threshold controls how many signatures are needed to run most administrative commands. The revocation signature threshold controls how many signatures are needed to remove an administrator after you leave imprint mode. Some commands need only one signature, regardless of how the signature threshold is set.
3. If prompted, insert an EP11 smart card with an administrator signature key that is defined to the selected crypto units in smart card reader 1. And then, enter the smart card PIN on the smart card reader PIN pad. Repeat this operation if prompted for more EP11 smart cards with signature keys. When the crypto unit exits imprint mode, the number of signatures that are needed for this command is the new signature threshold value. 

After the signature threshold values are set, the new values are displayed on the **Signature thresholds** page. Setting the signature thresholds to a value greater than one enables [quorum authentication](/docs/hs-crypto?topic=hs-crypto-understand-concepts#quorum-authenticaion-concept) from multiple administrators for sensitive operations.

When an EP11 smart card with a valid administrator signature key is inserted in smart card reader 1 and the PIN is entered, the smart card can be used to sign multiple commands. In Step 5, if the reader contains an EP11 smart card with a valid signature key and the PIN is entered, you're not prompted to insert an EP11 smart card with a signature key in smart card reader 1.
{: tip}

### Step 5: Load the master key
{: #step5-load-master-key-management-utilities}

For more information about the state transition of the master key register, see [Understanding how master key is loaded](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-key-ceremony).

#### Load the new master key register
{: #step5-load-new-register-management-utilities}

1. Select the **Master keys** tab and click **Load**.
2. If prompted, insert an EP11 smart card with an administrator signature key that is defined to the selected crypto units in smart card reader 1. And then, enter the smart card PIN on the smart card reader PIN pad.
3. When prompted, enter the number of master key parts to be loaded. Only 2 or 3 master key parts are accepted.
4. When prompted, insert the EP11 smart card that contains the first master key part in smart card reader 2 and enter the smart card PIN on the smart card reader PIN pad.
5. Select the master key part to be loaded from the list of master key parts on the smart card.
6. Repeat substep 4 and 5 for each master key part to be loaded.
7. If prompted, in smart card reader 1, insert the EP11 smart card with an administrator signature key that is defined to the selected crypto units, and enter the smart card PIN on the smart card reader PIN pad.

After all master key parts are loaded, the new master key register is in `Full uncommitted` state.

#### Commit the new master key register
{: #step5-commit-new-register-management-utilities}

1. Click **Commit** to move the master key to the `Full committed` state.
2. If prompted, in smart card reader 1, insert an EP11 smart card with an administrator signature key that is defined to the selected crypto units and enter the smart card PIN on the smart card reader PIN pad. Repeat this operation if prompted for more EP11 smart cards with signature keys.

After the process is complete, the new master key register is in `Full committed` state.

#### Activate the master key
{: #step5-activate-master-key-management-utilities}

Perform this step only when you are setting up a service instance for the first time and the key storage is empty. This command changes the value in the current master key register. If this command is run when key storage contains keys, and those keys are encrypted by using a master key value that is different from the value that is placed in the current master key register by this command, the keys in key storage become unusable.
{: important}

1. Click **Set immediate** to move the value of the new master key register to the current master key register and clear the new master key register.
2. Click **Yes** if you are ready to move the master key to the current master key register. This action can't be reversed.
3. If prompted, insert an EP11 smart card with an administrator signature key that is defined to the selected crypto units in smart card reader 1. And then, enter the smart card PIN on the smart card reader PIN pad.

The crypto units in the current master key register is now in `Valid` status, which indicates that your master key is loaded to your service instance.

## What's next
{: #initialize-crypto-utilities-management-utilities-next}

- Go to the **KMS keys** tab of your instance dashboard to [manage root keys and standard keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-keys). To find out more about programmatically managing your keys, check out the {{site.data.keyword.hscrypto}} [key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
- To learn more about performing cryptographic operations with the cloud HSM, see [Introducing cloud HSM](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm).
- Use {{site.data.keyword.hscrypto}} as the root key provider for other {{site.data.keyword.cloud_notm}} services. For more information about integrating {{site.data.keyword.hscrypto}}, check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
