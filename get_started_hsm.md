---

copyright:
  years: 2018, 2021
lastupdated: "2021-04-26"

keywords: key storage, key ceremony, initialize service instance, hsm, hardware security module, cloud hsm

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:external: target="_blank" .external}
{:term: .term}

# Getting started with service instance initialization
{: #get-started-hsm}

This tutorial shows you how to initialize the service instance by loading the [master key](#x2908413){: term} to protect your key storage with the Trusted Key Entry (TKE) command-line interface (CLI) plug-in. After you initialize the service instance, you can start managing your keys.
{:shortdesc}

## Prerequisite
{: #get-started-hsm-prerequisite}

Before you start, perform the following steps:

1. Provision the {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} instance (service instance for short). For detailed steps, see [Provisioning {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-provision).
2. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started#step1-install-idt){:external} and [log in to {{site.data.keyword.cloud_notm}} with the CLI](/docs/cli?topic=cli-getting-started#step3-configure-idt-env){: external}. Make sure that you are logged in to the correct region and resource group with the right account.
3. Install the latest TKE CLI plug-in with the following command:

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

4. Set the environment variable CLOUDTKEFILES to indicate the subdirectory where you want to store reference files on your workstation.



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

2. Create a [signature key](#x8250375){: term} with the following command:
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  When prompted, enter an administrator name and a password for the signature key file.

## Step 2: Select the crypto units that you want to work with
{: #hsm-step2}

All [crypto units](#x9860404){: term} in a service instance must be configured the same.

1. You can display the service instances and crypto units that are assigned to your IBM Cloud account by using the following command:

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

3. To remove crypto units from the set to work with, use the command:

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  When prompted, enter the crypto units that you want to remove.

## Step 3: Add crypto unit administrators and exit imprint mode
{: #hsm-step3}

Before you can load the master keys in a crypto unit, you must create one or more crypto unit administrators and exit [imprint mode](#x9860399){: term}.

1. Load a crypto unit administrator. To create a crypto unit administrator, use the command:
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  When prompted, enter the KEYNUM of the signature key to be used for the administrator and the password for the signature key file.

2. Select the signature key to use for signing commands by using the command:

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  When prompted, enter the KEYNUM of the signature key to use for signing commands.

  The signature key that you select must be the same as one of the signature keys that are used to load a crypto unit administrator in step 3.1.
  {: tip}

3. Exit imprint mode by using the following command:

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

  After you load a crypto unit administrator and exit imprint mode, you can check the state of your crypto units by using the command:
  {: tip}

  ```
  ibmcloud tke cryptounit-compare
  ```
  {: pre}

## Step 4: Load the master key register
{: #hsm-step4}

To load the master key register, one or more crypto unit administrators must be defined and the crypto unit must have left imprint mode.

1. Load the new master key register by using the following command:

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

- You can also initialize service instances by using smart cards and the Management Utilities. To get a better understanding of the two options and the associated concepts, see [Introduction to service instance initialization](/docs/hs-crypto?topic=hs-crypto-introduce-service).
- For detailed instructions and best practices on using the TKE CLI plug-in, see [Initializing service instances with the {{site.data.keyword.cloud_notm}} Trusted Key Entry CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)
- For detailed instructions and best practices on using the Management Utilities, see [Setting up smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities) and [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).
