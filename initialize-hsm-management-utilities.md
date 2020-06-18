---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-18"

keywords: key storage, hsm, hardware security module, key ceremony, master key, signature key, signature threshold, imprint mode, load master key, master key register, key part, initialize service, smart card, trusted key entry application, tke application, management utilities, cloudtkefiles

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


# Loading master keys with the Management Utilities
{: #initialize-hsm-management-utilities}

Before you can use a service instance, you need to load the [master keys](#x2908413){: term}. You can load master keys with either the {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) CLI plug-in or the {{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Management Utilities. To load the master keys with the Management Utilities, follow these steps.
{: shortdesc}

The [Management Utilities](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-management-utilities) use smart cards to hold [signature keys](#x8250375){: term} and master key parts. You need to complete the tasks in [Setting up the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities) before you can complete the steps in this task.

You can also watch the following video to learn how to initialize {{site.data.keyword.hscrypto}} instances with the Management Utilities:

<iframe class="embed-responsive-item" id="youtubeplayer" title="Initialize Hyper Protect Crypto Services with IBM Cloud TKE CLI" type="text/html" width="640" height="390" src="//www.youtube.com/embed/VTkGd_mcwyI?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Before you begin
{: #initialize-crypto-utilities-prerequisites}

1. Make sure that you've [provisioned a {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-provision), and [installed the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities).

2. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started#step1-install-idt){:external} and [log in to {{site.data.keyword.cloud_notm}} with the CLI](/docs/cli?topic=cloud-cli-getting-started#step3-configure-idt-env){: external}. If you've multiple accounts, select the account that your service instance is created with. Select the region and resource group where the service instance is located with the following command:

  ```
  ibmcloud target -r <region> -g <resource_group>
  ```
  {: pre}

  To find out the regions that {{site.data.keyword.hscrypto}} supports, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

3. Install the latest TKE CLI plug-in with the following command. The minimum required TKE CLI plug-in level is 0.0.11:

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

4. Set the environment variable CLOUDTKEFILES on your workstation. Specify a directory for storing reference files that the TKE application uses. Create the directory if it doesn't exist. Currently, only the Linux&reg; operating system is supported to use the TKE application.

  <!--
Currently, only the Windows&reg; 10 and Linux operating systems are supported to use the TKE application.

  - On Windows, in **Control Panel**, type `environment variable` in the search box to locate the Environment Variables window. Create a CLOUDTKEFILES environment variable and set the value to the path for storing reference files. For example, `C:\users\tke-files`.
  -->

  - On the Linux operating system, add the following line to the `.bash_profile` file:

    ```
    export CLOUDTKEFILES=<path>
    ```
    {: pre}

    For example, you can specify the *path* to `/Users/tke-files`.

5. Plug the two smart card readers into the USB ports of your workstation.

6. Start the Trusted Key Entry application by changing to the subdirectory where you install the Management Utilities applications and running the following command:
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

  When prompted, insert an [EP11 smart card](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-smart-cards) in smart card reader 2, enter a name for the administrator, and enter the personal identification number (PIN) for the smart card on the smart card reader PIN pad.

  An administrator signature key is generated and stored on the smart card. Repeat this step to create multiple signature keys if needed.

  Each smart card can contain only one signature key. If you want to set up multiple administrators, repeat this step by using different EP11 smart cards.
  {: tip}

2. To generate the master key parts for service instance initialization, on the **Smart card** tab, click **Generate key part**.

  If prompted, insert an EP11 smart card in smart card reader 2 and enter the smart card PIN. Enter a description for the key part.

  A random master key part is generated and stored on the smart card.

  To create more master key parts, repeat this step.<!-- You can create up to 85 master key parts on an EP11 smart card.-->

  You need to generate at least two master key parts to load a master key. For added security, it is recommended to generate three master key parts. To improve security, you can choose to generate signature keys and master key parts on separate smart cards and assign each smart card to a different person. For more information, see [Smart card considerations](/docs/hs-crypto?topic=hs-crypto-introduce-service#smart-card-considerations).
  {: important}

3. (Optional) If you want to create a backup copy of an EP11 smart card, click **Copy smart card** on the **Smart card** tab and follow the prompts.
4. (Optional) The signature keys and master key parts that are created with the TKE CLI plug-in and saved in a workstation file can be copied to a smart card. To do this, on the **Smart card** tab, click **Copy signature key file** or **Copy key part file** and follow the instructions. To copy the signature key or key part to a smart card, you need to provide the password for the file.

### Step 2: Select the crypto units where the master key is to be loaded
{: #step2-select-crypto-units-management-utilities}

Select the **Crypto units** tab. A list of [crypto units](#x9860404){: term} that are assigned to your user account is displayed. The SELECTED column shows what crypto units you're going to work with in later commands.

- To select extra crypto units to work with, click **Add crypto units** and enter the CRYPTO UNIT NUM (crypto unit numbers) of the extra crypto units you want to work with. You can enter multiple crypto unit numbers, which are separated by a space.
- To remove crypto units from the set you're going to work with, click **Remove crypto units** and enter the CRYPTO UNIT NUM of the crypto units you want to remove. You can enter multiple crypto unit numbers, which are separated by a space.

When the operations are done, `true` is displayed in the SELECTED column for each crypto unit that is to be affected by later commands. Note that if more than one crypto unit is assigned to a service instance, all crypto units in the service instance must be configured the same.

### Step 3: Add administrators to the selected crypto units
{: #step3-add-administrator-management-utilities}

The command to load a master key must be signed by an administrator that is predefined to the crypto unit. This step predefines an administrator.

1. Select the **Administrators** tab. This tab displays a list of administrators that are allowed to sign commands to the crypto unit.
2. Click **Add administrator**.
3. When prompted, insert the EP11 smart card that holds that administrator signature key in smart card reader 1, and enter the PIN on the smart card reader PIN pad.

The public signature key and administrator name are read from the smart card and installed in the crypto unit. When the operation is done, the administrator's name is displayed in the ADMIN NAME field of the selected crypto units.

For security and compliance reasons, the administrator name of the crypto unit might be shown up in logs for auditing purposes.
{: note}

Repeat this step if you want to add multiple administrators. You must add at least as many administrators to a crypto unit as the larger of the signature threshold value and the revocation signature threshold value you intend to set in Step 4.

### Step 4: Set the signature thresholds to exit imprint mode in the selected crypto units
{: #step4-exit-imprint-mode-management-utilities}

When crypto units in service instances are assigned to a user, they begin in a cleared state that is called imprint mode. In imprint mode, most operations on the crypto unit are disabled. To load the master key in a crypto unit, you must first exit imprint mode by setting the signature thresholds to a value greater than zero.

1. To set the signature thresholds, select the **Signature thresholds** tab and click **Change signature thresholds**.
2. When prompted, enter the new signature threshold value and the new revocation signature threshold value. 
  The values must be numbers between one and eight and do not need to be the same. The signature threshold controls how many signatures are needed to run most administrative commands. The revocation signature threshold controls how many signatures are needed to remove an administrator after you leave imprint mode. Some commands need only one signature, regardless of how the signature threshold is set.
3. If prompted, insert an EP11 smart card with an administrator signature key that is defined to the selected crypto units in smart card reader 1 and enter the smart card PIN on the smart card reader PIN pad. Repeat this operation if prompted for additional EP11 smart cards with signature keys. When exiting imprint mode, the number of signatures needed for this command is the new signature threshold value. 

After the signature threshold values are set, the new values are displayed on the **Signature thresholds** page. Setting the signature thresholds to a value greater than one enables [quorum authentication](/docs/hs-crypto?topic=hs-crypto-understand-concepts#quorum-authenticaion-concept) from multiple administrators for sensitive operations.

When an EP11 smart card with a valid administrator signature key is inserted in smart card reader 1 and its PIN is entered, the smart card can be used to sign multiple commands. In the following Step 5, if the reader already contains an EP11 smart card with a valid signature key and the PIN is entered, you're not prompted to insert an EP11 smart card with a signature key in smart card reader 1.
{: tip}

### Step 5: Load the master key
{: #step5-load-master-key-management-utilities}

#### Load the new master key register
{: #step5-load-new-register-management-utilities}

1. Select the **Master keys** tab and click **Load**.
2. If prompted, insert an EP11 smart card with an administrator signature key that is defined to the selected crypto units in smart card reader 1, and enter the smart card PIN on the smart card reader PIN pad.
3. When prompted, enter the number of master key parts to be loaded. Only 2 or 3 master key parts are accepted.
4. When prompted, insert the EP11 smart card that contains the first master key part in smart card reader 2 and enter the smart card PIN on the smart card reader PIN pad.
5. Select the master key part to be loaded from the list of master key parts on the smart card.
6. Repeat substep 4 and 5 for each master key part to be loaded.
7. If prompted, in smart card reader 1, insert the EP11 smart card with an administrator signature key that is defined to the selected crypto units, and enter the smart card PIN on the smart card reader PIN pad.

After all master key parts are loaded, the New Master Key Register is in Full Uncommitted state. For more information about the state transition of the master key register, see [Understanding how master key is loaded](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-key-ceremony).

#### Commit the new master key register
{: #step5-commit-new-register-management-utilities}

1. Click **Commit** to move the master key to the Full Committed state.
2. If prompted, in smart card reader 1, insert an EP11 smart card with an administrator signature key that is defined to the selected crypto units and enter the smart card PIN on the smart card reader PIN pad. Repeat this operation if prompted for additional EP11 smart cards with signature keys.

After the process is complete, the New Master Key Register is in Full Committed state.

#### Activate the master key
{: #step5-activate-master-key-management-utilities}

Perform this step only when you're setting up a service instance for the first time and the service instance doesn't have key storage that contains keys. If the service instance has key storage that contains keys, this command changes the value of the Current Master Key Register and the keys in key storage become unusable.
{: important}

1. Click **Set immediate** to move the value of the New Master Key Register to the Current Master Key Register and clear the New Master Key Register.
2. Click **Yes** if you are ready to move the master key to the current master key register. This action can't be reversed.
3. If prompted, insert an EP11 smart card with an administrator signature key that is defined to the selected crypto units in smart card reader 1, and enter the smart card PIN on the smart card reader PIN pad.

The crypto units in the Current Master Key Register is now in `Valid` status, which indicates that your master key is loaded to your service instance.

## What's next
{: #initialize-crypto-utilities-management-utilities-next}

- Go to the **Manage** tab of your instance dashboard to [manage root keys and standard keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-keys). To find out more about programmatically managing your keys, check out the {{site.data.keyword.hscrypto}} [key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
- To learn more about using Enterprise PKCS #11 APIs to perform cryptographic operations for your applications, check out [Encrypt your data with Cloud HSM](/docs/hs-crypto?topic=hs-crypto-get-started#encrypt-data-hsm) and the [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
- Use {{site.data.keyword.hscrypto}} as the root key provider for other {{site.data.keyword.cloud_notm}} services. For more information about integrating {{site.data.keyword.hscrypto}}, check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
