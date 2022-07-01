---

copyright:
  years: 2018, 2022
lastupdated: "2022-07-01"

keywords: hsm, hardware security module, key ceremony, master key, signature key, signature threshold, imprint mode, load master key, master key register, initialize service, trusted key entry cli plug-in, tke cli, cloudtkefiles

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}
{:video: .video}


# Initializing service instances using key part files
{: #initialize-hsm}

Before you can use your {{site.data.keyword.hscrypto}} instance, you need to first initialize your service instance by loading the master key. This topic guides you through the steps to initialize your service instance by using key part files through {{site.data.keyword.cloud_notm}} TKE CLI plug-in.
{: shortdesc}

For an introduction to the approaches of service instance initialization and the related fundamental concepts, see [Initializing service instances](/docs/hs-crypto?topic=hs-crypto-introduce-service) and [Introducing service instance initialization approaches](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode).

The following diagram gives you an overview of steps you need to take to initialize the service instance using master key parts stored in files. Click each step on the diagram for detailed instructions.

<figure>
    <img usemap="#home_map1" border="0" class="image" id="image_ztx_crb_f1b2" src="/images/hsm-initialization-flow.svg" width="750" alt="Click each step to get more details on the flow." />
    <figcaption>Figure 1. Task flow of service instance initialization with the TKE CLI plug-in</figcaption>
</figure>

<map name="home_map1" id="home_map1">
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite" alt="Install IBM Cloud CLI" title="Install IBM Cloud CLI" shape="rect" coords="126, 32, 226, 82" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite" alt="Log in to IBM Cloud" title="Log in to IBM Cloud" shape="rect" coords="260, 32, 360, 82" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite" alt="Install TKE CLI plug-in" title="Install TKE CLI plug-in" shape="rect" coords="394, 32, 494, 82" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite" alt="Set up local directory for key files" title="Set up local directory for key files" shape="rect" coords="528, 32, 628, 82" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#identify_crypto_units" alt="Display assigned crypto units" title="Display assigned crypto units" shape="rect" coords="126, 123, 226, 173" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#identify_crypto_units2" alt="Add crypto units" title="Add crypto units" shape="rect" coords="260, 123, 360, 173" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#step1-create-signature-keys" alt="Create one or more signature keys" title="Create signature keys" shape="rect" coords="126, 214, 226, 264" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#step2-load-admin" alt="Manage crypto unit administrators" title="Manage crypto unit administrators" shape="rect" coords="260, 214, 360, 264" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#step2-load-admin" alt="Add one or more administrators in the target crypto unit" title="Add crypto unit administrators" shape="rect" coords="158, 290, 238, 340" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#step3-exit-imprint-mode" alt="Set quorum authentication thresholds to exit imprint mode in the target crypto unit" title="Set quorum authentication thresholds to exit imprint mode in the target crypto unit" shape="rect" coords="260, 290, 398, 340" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#step4-create-master-key" alt="Create a set of master key parts to use" title="Create master key parts" shape="rect" coords="394, 214, 494, 264" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#step5-load-master-key" alt="Load master key registers" title="Load master key register" shape="rect" coords="528, 214, 628, 264" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#step5-load-master-key" alt="Load new master key registers" title="Load new master key register" shape="rect" coords="440, 290, 520, 340" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#step6-commit-master-key" alt="Commit the new master key register" title="Commit the new master key register" shape="rect" coords="539, 290, 619, 340" />
    <area href="/docs/hs-crypto?topic=hs-crypto-initialize-hsm#step7-activate-master-key" alt="Activate the master key" title="Activate master key register" shape="rect" coords="638, 290, 718, 340" />
</map>

You can also watch the following video to learn how to initialize {{site.data.keyword.hscrypto}} instances with {{site.data.keyword.cloud_notm}} TKE CLI plug-in:

![Initialize Hyper Protect Crypto Services with IBM Cloud TKE CLI](https://www.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/27941801/partner_id/1773841?iframeembed=true&entry_id=1_9mybz1cr
){: video output="iframe" data-script="none" id="mediacenterplayer" frameborder="0" width="560" height="315" allowfullscreen webkitallowfullscreen mozAllowFullScreen} 

Before you start the instance initialization, make sure that you complete [the prerequisite steps](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite). It might take 20 - 30 minutes for you to complete this task.
{: #initialize-crypto-prerequisites}

## Adding or removing crypto units that are assigned to service instances
{: #identify_crypto_units}

Crypto units that are assigned to an {{site.data.keyword.cloud_notm}} user account are in groups that are known as service instances. A service instance can have up to six [operational crypto units](/docs/hs-crypto?topic=hs-crypto-understand-concepts#crypto-unit-concept). All crypto units in a service instance need to be configured the same. If one availability zone in the region where your instance is located can't be accessed, the operational crypto units can be used interchangeably for load balancing or for high availability.

Crypto units that are assigned to an {{site.data.keyword.cloud_notm}} user start in a cleared state that is known as [imprint mode](#x9860399){: term}.

The master key registers in all crypto units in a single service instance must be set the same. The same set of administrators must be added in all crypto units, and all crypto units must exit imprint mode at the same time.

* To display the service instances and crypto units in the target resource group under the current user account, use the following command:

    ```
    ibmcloud tke cryptounits
    ```
    {: pre}

    The following output is an example that is displayed. The SELECTED column in the output table identifies the crypto units that are targeted by later administrative commands that are issued by the TKE CLI plug-in.

    ```
    SERVICE INSTANCE: 482cf2ce-a06c-4265-9819-0b4acf54f2ba
    CRYPTO UNIT NUM   SELECTED   TYPE           LOCATION
    1                 false      OPERATIONAL    [us-south].[AZ3-CS3].[02].[03]
    2                 false      OPERATIONAL    [us-south].[AZ2-CS2].[02].[03]
    3                 false      FAILOVER       [us-east].[AZ2-CS2].[03].[04]
    4                 false      FAILOVER       [us-east].[AZ3-CS3].[01].[07]

    SERVICE INSTANCE: 96fe3f8d-9792-45bc-a9fb-2594222deaf2
    CRYPTO UNIT NUM   SELECTED   TYPE           LOCATION
    5                 false      OPERATIONAL    [us-south].[AZ1-CS4].[00].[03]
    6                 false      OPERATIONAL    [us-south].[AZ2-CS5].[03].[03]
    ```
    {: screen}

* To add extra crypto units to the selected crypto unit list, use the following command:{: #identify_crypto_units2}

    ```
    ibmcloud tke cryptounit-add
    ```
    {: pre}

    A list of the crypto units in the target resource group under the current user account is displayed. When prompted, enter a list of crypto unit numbers to be added to the selected crypto unit list.

    If you enable cross-region high availability with [failover crypto units](/docs/hs-crypto?topic=hs-crypto-understand-concepts#crypto-unit-concept), make sure that you add all the failover crypto units to the selected list for instance initialization.

    If you don't initialize and configure failover crypto units the same as the operational crypto units, you are not able to use the failover crypto units for automatic data restoration when a regional disaster happens. For more information about cross-region disaster recovery, see [High availability and disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr).
    {: important}

    If you are using a public network, crypto units that are associated with service instances with the network policy set to `private-only` are not to be listed. You can access private-only crypto units only through a private network. For more information about setting up a private-only connection, see [Target the private endpoint for the TKE plug-in](/docs/hs-crypto?topic=hs-crypto-secure-connection#target-tke-private-endpoint).
    {: note}

* To remove crypto units from the selected crypto unit list, use the following command:

    ```
    ibmcloud tke cryptounit-rm
    ```
    {: pre}

    A list of the crypto units in the target resource group under the current user account is displayed. When prompted, enter a list of crypto unit numbers to be removed from the selected crypto unit list.

    In general, either all crypto units or none of the crypto units in a service instance are selected. This operation causes later administrative commands to update all crypto units of a service instance consistently. However, if the crypto units of a service instance become configured differently, you need to select and work with crypto units individually to restore a consistent configuration to all crypto units in a service instance.
    {: tip}

    You can compare the configuration settings of the selected crypto units with the following command:

    ```
    ibmcloud tke cryptounit-compare
    ```
    {: pre}

## Loading master keys
{: #load-master-keys}

Before the new master key register can be loaded, add one or more administrators in the target crypto units and exit imprint mode.

To load the new master key register, complete the following tasks with the {{site.data.keyword.cloud_notm}} CLI plug-in:

### Step 1: Create one or more signature keys
{: #step1-create-signature-keys}

To load the new master key register, A crypto unit administrator must sign the command with a unique signature key. The first step is to create one or more signature key files that contain signature keys on your workstation. 

For security considerations, the signature key owners can be different people from the master key part owners. The signature key owner needs to be the only person who knows the password that is associated with the signature key file.
{: important}

* To display the existing signature keys on the workstation, use the following command:

    ```
    ibmcloud tke sigkeys
    ```
    {: pre}

* To create and save a new signature key on the workstation, use the following command:

    ```
    ibmcloud tke sigkey-add
    ```
    {: pre}

    When prompted, enter an administrator name and a password to protect the signature key file. You must remember the password. If the password is lost, the signature key can't be used.

    Repeat the command to create multiple signature keys if needed.

* To select the administrators to sign future commands, use the command:

    ```
    ibmcloud tke sigkey-sel
    ```
    {: pre}

    A list of signature keys that are found on the workstation is displayed. When prompted, enter the key numbers of the signature key files to select for signing future administrative commands. When prompted, enter the passwords for the signature key files.

    This command determines what signature keys are allowed to sign future commands. There is no limit to the number of signature key files that you can select. If you select more signature keys than required to sign a command, the actual signature keys that are used will be determined at the time the command is executed.

    You can also use a third-party signing service to provide signature keys. For more information, see [Using a signing service to manage signature keys for instance initialization](/docs/hs-crypto?topic=hs-crypto-signing-service-signature-key).
    {: tip}

### Step 2: Add one or more administrators in the target crypto unit
{: #step2-load-admin}



* To display the existing administrators for a crypto unit, use the following command:

    ```
    ibmcloud tke cryptounit-admins
    ```
    {: pre}

* To add an administrator, use the following command:

    ```
    ibmcloud tke cryptounit-admin-add
    ```
    {: pre}

    A list of the signature key files that are found on the workstation is displayed.

    When prompted, select the signature key file that is associated with the crypto unit administrator to be added. And then enter the password for the selected signature key file.

    You can repeat the command to add extra crypto unit administrators if needed.

    The number of administrators that you add to a crypto unit needs to be equal to or greater than the signature threshold value and the revocation signature threshold value that you intend to set in [Step 3](#step3-exit-imprint-mode). For example, if you are about to set the signature threshold or revocation signature threshold value to two, you need to add at least two administrators to the crypto unit. You can add up to eight administrators to a crypto unit.
    {: tip}

    Do not remove the administrator signature key files from your workstation. Otherwise, you are not able to perform TKE actions that need to be signed, such as zeroizing crypto units and rotating master keys.
    {: important}

    In imprint mode, the command to add a crypto unit administrator doesn't need to be signed. After the crypto unit leaves imprint mode, the signature threshold value for the crypto unit determines how many crypto unit administrators must sign the command.

    For security and compliance reasons, the administrator name of the crypto unit might be shown up in logs for auditing purposes.
    {: note}

### Step 3: Set the quorum authentication thresholds to exit imprint mode in the target crypto unit
{: #step3-exit-imprint-mode}

A crypto unit in imprint mode isn't considered secure. You can't run most of the administrative commands, such as loading the new master key register, in imprint mode.

After you add one or more crypto unit administrators, exit imprint mode by using the command:

```
ibmcloud tke cryptounit-thrhld-set
```
{: pre}

When prompted, enter values for the signature threshold and revocation signature threshold. The signature threshold controls how many signatures are required to execute most administrative commands. The revocation signature threshold controls how many signatures are required to remove an administrator after you have left imprint mode. Some commands require only one signature, regardless of how the signature threshold is set.

The signature threshold values must be numbers between one and eight. The signature threshold and revocation signature threshold can be different. Setting the signature thresholds to a value greater than one is a way to enforce [quorum authentication](/docs/hs-crypto?topic=hs-crypto-understand-concepts#quorum-authenticaion-concept) for sensitive operations.

The command to exit imprint mode must be signed by as many administrators as specified by the new signature threshold value. After crypto units leave imprint mode, all commands to the crypto unit must be signed. After the crypto unit exits imprint mode, you can still change the signature thresholds on the crypto unit by using the `cryptounit-thrhld-set` command. To display the current signature threshold values, run the `ibmcloud tke cryptounit-thrhlds` command.
{: important}

### Step 4: Create a set of master key parts to use
{: #step4-create-master-key}

Each master key part is saved in a password-protected file on the workstation.

You must create at least two master key parts. For security considerations, a maximum of three master key parts can be used and each key part can be owned by a different person. The key part owner needs to be the only person who knows the password that is associated with the key part file.
{: important}

* To display the existing master key parts on the workstation, use the following command:

    ```
    ibmcloud tke mks
    ```
    {: pre}

* To create and save a random master key part on the workstation, use the command:

    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    When prompted, enter a description for the key part and a password to protect the key part file. You must remember the password. If the password is lost, you can't use the key part.

* To enter a known key part value and save it in a file on the workstation, use the following command:

    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    When prompted, enter the key part value as a hexadecimal string for the 32-byte key part. And then enter a description for the key part and a password to protect the key part file.

### Step 5: Load the new master key register
{: #step5-load-master-key}

To load a master key register, all master key part files and signature key files to be used must be present on a common workstation. If the files were created on separate workstations, make sure that the file names are different to avoid collision. The master key part file owners and the signature key file owners need to enter the file passwords when the master key register is loaded on the common workstation.
{: important}

For information about how the master key is loaded, see the detailed illustrations at [Master key registers](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-key-ceremony).

To load the new master key register, use the following command:

```
ibmcloud tke cryptounit-mk-load
```
{: pre}

A list of the master key parts that are found on the workstation is displayed.

When prompted, enter the key parts to be loaded into the new master key register, the password for the signature key file to be used, and password for each selected key part file. For this command, only one signature key is needed.

### Step 6: Commit the new master key register
{: #step6-commit-master-key}

Loading the new master key register places the new master key register in the full uncommitted state. Before you can use the new master key register to initialize or reencipher key storage, place the new master key register in the committed state. For information about how the master key is loaded, see the detailed illustrations at [Master key registers](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-key-ceremony).

To commit the new master key register, use the following command:

```
ibmcloud tke cryptounit-mk-commit
```
{: pre}

When prompted, enter the passwords for the signature key files to be used.

### Step 7: Activate the master key
{: #step7-activate-master-key}

Activate the master key by moving the master key to the current master key register with the following command:

```
ibmcloud tke cryptounit-mk-setimm
```
{: pre}

A message is displayed asking whether to accept the new master key.

Consider the following before you take actions:
* If it is your first time to initialize the service instance, you can ignore this message and type `y` to continue.
* If you have started managing keys with the service instance and want to reload the same master key that was used before, ensure that no key management actions are in progress and type `y` to continue.
* If you have started managing keys with the service instance and want to load a new master key, type `N` to cancel. For more information about rotating the master key, see [Rotating master keys](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part).

When prompted, enter the password for the signature key file to be used. For this command, only one signature key is needed.

## What's next
{: #initialize-crypto-cli-next}

- For more details on other options of the TKE CLI plug-in commands, run the following command in the CLI:

    ```
    ibmcloud tke help
    ```
    {: pre}

- Go to the **KMS keys** tab of your instance dashboard to [manage root keys and standard keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-keys). To find out more about programmatically managing your keys, check out the {{site.data.keyword.hscrypto}} [key management service API reference doc](/apidocs/hs-crypto){: external}.
- To learn more about performing cryptographic operations with the cloud HSM, see [Introducing cloud HSM](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm).
- Use {{site.data.keyword.hscrypto}} as the root key provider for other {{site.data.keyword.cloud_notm}} services. For more information about integrating {{site.data.keyword.hscrypto}}, check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- For information on how to rotate the master key, see [Rotating master keys by using key part files](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part).
