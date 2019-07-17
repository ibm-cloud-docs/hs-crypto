---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-10"

Keywords: key storage, HSM, hardware security module

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:external: target="_blank" .external}

# Initializing service instances
{: #initialize-hsm}

Before using the {{site.data.keyword.hscrypto}} instance (service instance for short), you need to load master key registers using the Trusted Key Entry CLI plug-in.
{:shortdesc}

To initialize service instances, you need to load the master key with the Trusted Key Entry plug-in to your key storage, service instance first. The Trusted Key Entry plug-in allows you to load your master key values.

For an introduction to service instance initialization and other concepts, see [Introduction to service instance initialization](/docs/services/hs-crypto?topic=hs-crypto-introduce-service#introduce-service).

The following diagram gives you an overview of steps you need to take to initialize the service instance. Click each step on the diagram for detailed instructions.

<img usemap="#home_map1" border="0" class="image" id="image_ztx_crb_f1b2" src="image/hsm_initialization_flow.png" width="750" alt="Click each step to get more details on the flow." style="width:750px;" />
<map name="home_map1" id="home_map1">
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-crypto-prerequisites" alt="Verify API endpoint" title="Verify API endpoint" shape="rect" coords="151, 20, 241, 78" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-crypto-prerequisites" alt="Set up CLI" title="Set up CLI" shape="rect" coords="276, 20, 365, 78" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-crypto-prerequisites4" alt="Install TKE plugin" title="Install TKE plugin" shape="rect" coords="401, 20, 493, 78" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-crypto-prerequisites4" alt="Set up local directory for key files" title="Set up local directory for key files" shape="rect" coords="528, 20, 619, 78" />

<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#Identify_crypto_units" alt="Display assigned crypto units" title="Display assigned crypto units" shape="rect" coords="148, 111, 241, 171" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#Identify_crypto_units1" alt="Add crypto units" title="Add crypto units" shape="rect" coords="276, 111, 366, 171" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#Identify_crypto_units2" alt="Remove crypto units" title="Remove crypto units" shape="rect" coords="402, 111, 493, 171" />

<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step1-create-signature-keys" alt="Create one or more signature keys" title="Create signature keys" shape="rect" coords="149, 206, 242, 264" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step2-load-admin" alt="Manage crypto unit administrators" title="Manage crypto unit administrators" shape="rect" coords="281, 206, 366, 264" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step2-load-admin" alt="Add one or more administrators in the target crypto unit" title="Add crypto unit administrators" shape="rect" coords="242, 296, 312, 358" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step3-exit-imprint-mode" alt="Exit imprint mode in the target crypto unit" title="Exit imprint mode" shape="rect" coords="328, 301, 396, 359" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step4-create-master-key" alt="Create a set of master key parts to use" title="Create master key parts" shape="rect" coords="401, 208, 493, 266" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step5-load-master-key" alt="Load master key registers" title="Load master key register" shape="rect" coords="525, 207, 620, 264" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step5-load-master-key" alt="Load new master key registers" title="Load new master key register" shape="rect" coords="455, 297, 525, 358" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step6-commit-master-key" alt="Commit the new master key register" title="Commit the new master key register" shape="rect" coords="539, 297, 610, 358" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step7-activate-master-key" alt="Activate the master key" title="Activate master key register" shape="rect" coords="619, 297, 689, 358" />
</map>

*Figure 1. Task flow of service instance initialization*

It might take 20-30 minutes for you to complete this task.

## Before you begin
{: #initialize-crypto-prerequisites}

1. Run the following command to make sure that you are logged in to the correct API endpoint:

  ```
  ibmcloud target -r <region>
  ```
  {: pre}

  To find out the regions that {{site.data.keyword.hscrypto}} supports, see [Regions and locations](/docs/services/hs-crypto?topic=hs-crypto-regions).

2. [Install the {{site.data.keyword.keymanagementservicefull}} plug-in](/docs/services/key-protect?topic=key-protect-set-up-cli#install-cli). After installation, see [Setting up the CLI](/docs/services/hs-crypto?topic=hs-crypto-set-up-cli) for detailed configuration steps. When you log in to the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started#overview), you're notified when updates are available. Be sure to keep your {{site.data.keyword.keymanagementservicefull}} plug-in up-to-date so that you can use the commands and flags that are available for the Trusted Key Entry CLI plug-in.
{: #initialize-crypto-prerequisites2}

3. Install the latest Trusted Key Entry plug-in with the following command:
{: #initialize-crypto-prerequisites3}

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

<!-- **Important:** If you are using the Beta instance of ({{site.data.keyword.hscrypto}}, run the `ibmcloud plugin install tke -v 0.0.4` to get the latest beta version of the Trusted Key Entry plug-in. Do not install later versions of the Trusted Key Entry plug-in. -->

4. Set the environment variable CLOUDTKEFILES on your workstation. Specify a directory where you want master key part files and signature key part files to be created and saved. Create the directory if it does not already exist.
{: #initialize-crypto-prerequisites4}

  * On Linux or MacOS, add the following line to the `.bash_profile` file:
     ```
     export CLOUDTKEFILES=<path>
     ```
     {: pre}
     For example, you can specify the *path* to `/Users/tke-files`.
  * On Windows, in **Control Panel**, type `environment variable` in the search box to locate the Environment Variables window. Create a CLOUDTKEFILES environment variable and set the value to the path to the key files. For example, `C:\users\tke-files`.

## Adding or removing crypto units that are assigned to a user account
{: #Identify_crypto_units}

Crypto units that are assigned to an {{site.data.keyword.cloud_notm}} user account are in a group known as *a service instance*. A service instance can have up to six crypto units. All crypto units in a service instance should be configured the same. If one part of the {{site.data.keyword.cloud_notm}} cannot be accessed, the crypto units in a service instance can be used interchangeably for load balancing or for availability.

Crypto units that are assigned to an {{site.data.keyword.cloud_notm}} user start in a cleared state known as *imprint mode*.

The master key registers in all crypto units in a single service instance must be set the same. The same set of administrators must be added in all crypto units, and all crypto units must exit imprint mode at the same time.

* To display the service instances and crypto units assigned to a user account, use the following command:
  {: #Identify_crypto_units1}
  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

  The following is a sample output that is displayed. The SELECTED column in the output table identifies the crypto units that are targeted by subsequent administrative commands that are issued by the Trusted Key Entry plug-in.

  ```
  SERVICE INSTANCE: 482cf2ce-a06c-4265-9819-0b4acf54f2ba
  CRYPTO UNIT NUM   SELECTED   LOCATION
  1                 true       [us-south].[AZ3-CS3].[02].[03]
  2                 true       [us-south].[AZ2-CS2].[02].[03]

  SERVICE INSTANCE: 96fe3f8d-9792-45bc-a9fb-2594222deaf2
  CRYPTO UNIT NUM   SELECTED   LOCATION
  3                 true       [us-south].[AZ1-CS4].[00].[03]
  4                 true       [us-south].[AZ2-CS5].[03].[03]
  ```
  {: screen}

* To add additional crypto units to the selected crypto unit list, use the following command:
  {: #Identify_crypto_units2}
  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  A list of the crypto units that are assigned to the current user account is displayed. When prompted, enter a list of crypto unit numbers to be added to the selected crypto unit list.

* To remove crypto units from the selected crypto unit list, use the following command:
  {: #Identify_crypto_units3}
  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  A list of crypto units that are assigned to the current user account is displayed. When prompted, enter a list of crypto unit numbers to be removed from the selected crypto unit list.

  **Tip:** In general, either all crypto units or none of the crypto units in a service instance are selected. This causes subsequent administrative commands to update all crypto units of a service instance consistently. However, if the crypto units of a service instance become configured differently, you need to select and work with crypto units individually to restore a consistent configuration to all crypto units in a service instance.

  You can compare the configuration settings of the selected crypto units with the following command:
  ```
  ibmcloud tke cryptounit-compare
  ```
  {: pre}

## Loading master keys
{: #load-master-keys}

<!-- A service instance is implemented as one or more crypto units on IBM cryptographic coprocessors. -->

Before the new master key register can be loaded, add one or more administrators in the target crypto units and exit imprint mode.

To load the new master key register, complete the following tasks using the {{site.data.keyword.cloud_notm}} CLI plug-in:

### Step 1: Create one or more signature keys
{: #step1-create-signature-keys}

To load the new master key register, A crypto unit administrator must sign the command with a unique signature key. The first step is to create one or more signature key files that contain signature keys on your workstation. <!-- The private part of the signature key file is used to create signatures. The public part is placed in a certificate that is installed in a target crypto unit to define a crypto unit administrator. -->

**Important**: For security considerations, the signature key owner can be a different person from the master key part owners. The signature key owner should be the only person who knows the password associated with the signature key file.

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

  When prompted, enter an administrator name and a password to protect the signature key file. You must remember the password. If the password is lost, the signature key cannot be used.

* To select the administrator to sign future commands, use the command:
  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  A list of signature key files found on the workstation is displayed. When prompted, enter the key number of the signature key file to select for signing subsequent administrative commands. And then enter the password for the signature key file. <!--If a signature key file is already selected for signing administrative commands, this is indicated when the list of signature key files is displayed. -->

  <!-- **Tip**: Before you run the `cryptounit-exit-impr` command to exit imprint mode, the command needs to be signed by a crypto unit administrator using the signature key. After the crypto unit exits imprint mode, all commands to the crypto unit must be signed. -->

### Step 2: Add one or more administrators in the target crypto unit
{: #step2-load-admin}

<!-- After a crypto unit exits imprint mode, all administrative commands sent to the crypto unit must be signed by an administrator that is added to the crypto unit. -->

* To display the existing administrators for a crypto unit, use the following command:
  ```
  ibmcloud tke cryptounit-admins
  ```
  {: pre}

* To add a new administrator, use the following command:
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  A list of the signature key files that are found on the workstation is displayed.

  When prompted, select the signature key file that is associated with the crypto unit administrator to be added. And then enter the password for the selected signature key file.

  You can repeat the command to add additional crypto unit administrators if needed. Any administrator can independently run commands in the crypto unit.

  In imprint mode, the command to add a crypto unit administrator does not need to be signed. After leaving imprint mode, to add crypto unit administrators, the command to be used must be signed by a crypto unit administrator that is already added in the crypto unit.

### Step 3: Exit imprint mode in the target crypto unit
{: #step3-exit-imprint-mode}

A crypto unit in imprint mode is not considered secure. You cannot run most of the administrative commands, such as loading the new master key register, in imprint mode.

After you add one or more crypto unit administrators, exit imprint mode by using the command:

  ```
  ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

  When prompted, enter the password for the current signature key file.

  ** Important:** The command to exit imprint mode must be signed by one of the added crypto unit administrators using the signature key. After the crypto unit exits imprint mode, all commands to the crypto unit must be signed.

### Step 4: Create a set of master key parts to use
{: #step4-create-master-key}

Each master key part is saved in a password-protected file on the workstation.

**Important**: You must create at least two master key parts. For security considerations, three master key parts can be used and each key part can be owned by a different person. The key part owner should be the only person who knows the password associated with the key part file.

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

  When prompted, enter a description for the key part and a password to protect the key part file. You must remember the password. If the password is lost, you cannot use the key part.

* To enter a known key part value and save it in a file on the workstation, use the following command:
  ```
  ibmcloud tke mk-add --value
  ```
  {: pre}

  When prompted, enter the key part value as a hexadecimal string for the 32-byte key part. And then enter a description for the key part and a password to protect the key part file.

### Step 5: Load the new master key register
{: #step5-load-master-key}

**Important**: To load a master key register, all master key part files and the signature key file must be present on a common workstation. If the files were created on separate workstations, make sure that the file names are different to avoid collision. The master key part file owners and the signature key file owner need to enter the file passwords when the master key register is loaded on the common workstation.

For information on how the master key is loaded, see the detailed illustrations at [Master key registers](/docs/services/hs-crypto?topic=hs-crypto-introduce-service#introduce-key-registers).

To load the new master key register, use the following command:
```
ibmcloud tke cryptounit-mk-load
```
{: pre}

A list of the master key parts that are found on the workstation is displayed.

When prompted, enter the key parts to be loaded into the new master key register, the password for the current signature key file, and password for each selected key part file sequentially.

### Step 6: Commit the new master key register
{: #step6-commit-master-key}

Loading the new master key register places the new master key register in the full uncommitted state. Before you can use the new master key register to initialize or re-encipher key storage, place the new master key register in the committed state. For information on how the master key is loaded, see the detailed illustrations at [Master key registers](/docs/services/hs-crypto?topic=hs-crypto-introduce-service#introduce-key-registers).

To commit the new master key register, use the following command:
```
ibmcloud tke cryptounit-mk-commit
```
{: pre}

When prompted, enter the password for the current signature key file.

### Step 7: Activate the master key
{: #step7-activate-master-key}

Activate the master key by moving the master key to the current master key register with the following command:

```
ibmcloud tke cryptounit-mk-setimm
```
{: pre}

A message is displayed asking whether to accept the new master key.

Consider the following before taking actions:
* If it is your first time to initialize the service instance, you can ignore this message and type `y` to continue.
* If you have started managing keys with the service instance and want to reload the same master key that was used before, ensure that no key management actions are in progress and type `y` to continue.
* If you have started managing keys with the service instance and want to load a new master key, type `N` to cancel. Loading a new master key is currently not supported. By doing so, all your managed keys will be unusable.
{: tip}

## What's next
{: #initialize-crypto-next}

Go to the **Manage** tab of your managed {{site.data.keyword.hscrypto}} dashboard to manage root keys and standard keys.

For more details on other options of the Trusted Key Entry plug-in commands, run the following command in the CLI:

```
ibmcloud tke help
```
{: pre}
