---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# Getting started with crypto instance initialization
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> This tutorial shows you how to initialize the crypto instance by loading the master keys to protect your key storage with the Trusted Key Entry plug-in. After you initialize the crypto instance, you can start managing your root keys.   
{:shortdesc}

## Prerequisite

Before you start, perform the following steps:

1. Provision the {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} service. For detailed steps, see [Provisioning {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/provision.html).

2. Install the latest Trusted Key Entry plug-in through {{site.data.keyword.cloud_notm}} command-line interface (CLI) with the following command:

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  To install the CLI plug-in, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html).
  {: tip}

3. Set the environment variable CLOUDTKEFILES to indicate the subdirectory where you want to store the key parts and signature keys

## 1. Create your master key parts and signature key files

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

## 2. Select the domains you want to work with

All domains in a crypto instance must be configured the same.

1. You can display the crypto instances and domains assigned to your IBM Cloud account using the following command:

  ```
  ibmcloud tke domains
  ```
  {: pre}

2. To select additional domains to work with, use the command:

  ```
  ibmcloud tke domain-add
  ```
  {: pre}

  When prompted, enter the additional domains to work with.

3. To remove domains from the set you will work with, use the command:

  ```
  ibmcloud tke domain-rm
  ```
  {: pre}

  When prompted, enter the domains you want to remove.

## 3. Add domain administrators and exit imprint mode

Before you can load the master keys in a domain, you must create one or more domain administrators and exit imprint mode.

1. Load a domain administrator. To create a domain administrator, use the command:
  ```
  ibmcloud tke domain-admin-add
  ```
  {: pre}

  When prompted, enter the KEYNUM of the signature key to be used for the administrator and the password for the signature key file.

2. Select the signature key to use for signing commands using the command:

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  When prompted, enter the KEYNUM of the signature key to use for signing commands.

  This must be the same as one of the signature keys used to load a domain administrator in step 3.1.
  {: tip}

3. Exit imprint mode using the following command:

  ```
   ibmcloud tke domain-exit-impr
  ```
  {: pre}

After you load a domain administrator and exit imprint mode, you can check the state of your domains using the command:

{: tip}
```
 ibmcloud tke domain-compare
```
{: pre}

## 4. Load the master key register

To load the master key register, one or more domain administrators must be defined and the domain must have left imprint mode.

1. Load the new master key register using the following command:

  ```
  ibmcloud tke domain-mk-load
  ```
  {: pre}

  When prompted, enter the KEYNUM of the key parts to be loaded, the password for the signature key file, and the passwords for each selected key part.

2. Commit the new master key register with the following command:

  ```
  ibmcloud tke domain-mk-commit
  ```
  {: pre}

  When prompted, enter the password for the signature key file.

3. Move the master key to the current master key register with the following command:

  ```
  ibmcloud tke domain-mk-setimm
  ```
  {: pre}

  When prompted, enter the password for the signature key file.

## What's next

Now you can start using your crypto instance. For details on implementing the procedure in a production environment, see [Protecting key storage by initializing crypto instances](/docs/services/hs-crypto/initialize_hsm.html).
