---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-15"

Keywords: key storage, service instance, HSM, hardware security module

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}  
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# Getting started with service instance initialization
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> This tutorial shows you how to initialize the service instance by loading the master keys to protect your key storage with the Trusted Key Entry plug-in. After you initialize the service instance, you can start managing your root keys.   
{:shortdesc}

## Prerequisite
{: #get-started-hsm-prerequisite}

Before you start, perform the following steps:

1. Provision the {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} instance (service instance for short). For detailed steps, see [Provisioning {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/provision.html).

2. Run the following command to make sure that you are logged in to the correct API endpoint:

  ```
  ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

3. Install the latest Trusted Key Entry plug-in through {{site.data.keyword.cloud_notm}} command-line interface (CLI) with the following command:

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  To install the CLI plug-in, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html).
  {: tip}

4. Set the environment variable CLOUDTKEFILES to indicate the subdirectory where you want to store the key parts and signature keys

##  Step 1: Create your master key parts and signature key files
{: #hsm-step1}

1. Create a random master key part or a master key part with a known value.

  * To create a random master key part, use the following command:

    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    When prompted, enter a description for the key part and a password for the key part file.

  * To create a master key part with a known value, use the following command:

    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    When prompted, enter the known key part value as a hexadecimal string, then enter a description and a password for the key part file.

  Repeat either command to create additional key parts.

2. Create a signature key with the following command:
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  When prompted, enter an administrator name and a password for the signature key file.

## Step 2: Select the crypto units you want to work with
{: #hsm-step2}

All crypto units in a service instance must be configured the same.

1. You can display the service instances and crypto units assigned to your IBM Cloud account using the following command:

  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

2. To select additional crypto units to work with, use the command:

  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  When prompted, enter the additional crypto units to work with.

3. To remove crypto units from the set you will work with, use the command:

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  When prompted, enter the crypto units you want to remove.

## Step 3: Add crypto unit administrators and exit imprint mode
{: #hsm-step3}

Before you can load the master keys in a crypto unit, you must create one or more crypto unit administrators and exit imprint mode.

1. Load a crypto unit administrator. To create a crypto unit administrator, use the command:
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  When prompted, enter the KEYNUM of the signature key to be used for the administrator and the password for the signature key file.

2. Select the signature key to use for signing commands using the command:

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  When prompted, enter the KEYNUM of the signature key to use for signing commands.

  This must be the same as one of the signature keys used to load a crypto unit administrator in step 3.1.
  {: tip}

3. Exit imprint mode using the following command:

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

After you load a crypto unit administrator and exit imprint mode, you can check the state of your crypto units using the command:
{: tip}

```
 ibmcloud tke cryptounit-compare
```
{: pre}

## Step 4: Load the master key register
{: #hsm-step4}

To load the master key register, one or more crypto unit administrators must be defined and the crypto unit must have left imprint mode.

1. Load the new master key register using the following command:

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  When prompted, enter the KEYNUM of the key parts to be loaded, the password for the signature key file, and the passwords for each selected key part.

2. Commit the new master key register with the following command:

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  When prompted, enter the password for the signature key file.

3. Move the master key to the current master key register with the following command:

  ```
  ibmcloud tke cryptounit-mk-setimm
  ```
  {: pre}

  When prompted, enter the password for the signature key file.

## What's next
{: #hsm-next}

Now you can start using your service instance. For details on implementing the procedure in a production environment, see [Initializing service instances to protect key storage](/docs/services/hs-crypto/initialize_hsm.html).
