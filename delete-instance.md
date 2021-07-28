---

copyright:
  years: 2018, 2021
lastupdated: "2021-07-26"

keywords: delete, delete service instance, crypto unit, ibm cloud cli, clear crypto unit, uninstall

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}

# Deleting service instances
{: #delete-instance}

You can delete your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance with the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} CLI. To do so, you need to set all the [crypto units](#x9860404){: term} of the service instance back to the [imprint mode](#x9860399){: term} by zeroizing the crypto units.
{: shortdesc}

## Step 1: Zeroize crypto units
{: #zeroize-crypto-unit-step}

If you initialize your service instance and load the [master key](#x2908413){: term} to the service instance, you need to set the crypto units back to imprint mode. You can clear all crypto unit administrators and the master key registers with one of the following options:

-  If you initialize your service instance through {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) command-line interface (CLI) plug-in, run the following command to zeroize the crypto units in the TKE CLI plug-in:

    ```
    ibmcloud tke cryptounit-zeroize
    ```
    {: pre}

-  If you initialize your service instance through the Management Utilities, in the user interface of the TKE application, select **Imprint mode** &gt; **Zeroize crypto unit**.

To zeroize the crypto units, enter the password for the administrator signature key to be used when prompted. Make sure that your signature key files are properly saved either on your workstation or on your smart cards. Otherwise, you are not able to perform this action.

After you zeroize the crypto unit, the administrator [signature keys](#x8250375){: term} and the master key are cleared from the crypto unit, which means you are not able to access any data that is protected by the master key, such as the [root keys](#x6946961){: term} and standard keys.
{: important}

## Step 2: Optional - Uninstall the {{site.data.keyword.hscrypto}} utilities
{: #uninstall-utilities-step}

Before you delete the service instance, you might want to uninstall the utilities that are associated with {{site.data.keyword.hscrypto}} first.

### Uninstall the TKE CLI plug-in
{: #uninstall-tke-cli-plugin}

If you initialize your service instance by loading master key parts from your workstation, uninstall the TKE CLI plug-in with the following command:

```
ibmcloud plugin uninstall tke
```
{: pre}

If you want to uninstall the entire {{site.data.keyword.cloud_notm}} CLI, see [Uninstalling the stand-alone {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-uninstall-ibmcloud-cli).

### Uninstall the Management Utilities
{: #uninstall-management-utilities}

If you initialize your service instance by loading master key parts from smart cards, follow these steps to uninstall the {{site.data.keyword.hscrypto}} Management Utilities.



- Linux&reg; operating system

  1. From the command line, enter the directory where the Management Utilities are installed with the following command:
    ```
    cd <management_utilities_directory>
    ```
    {: pre}
  2. Enter the `_installation` subdirectory with the following command:
    ```
    cd _installation
    ```
    {: pre}
  3. To uninstall the Management Utilities, run the following command:
    ```
    ./uninstall
    ```
    {: pre}

## Step 3: Delete your service instance
{: #delete-instance-step}

After you set the crypto units to imprint mode, you can choose to delete your service instance through the {{site.data.keyword.cloud_notm}} console resources page, the instance details page, or the CLI.

### Deleting instances from the {{site.data.keyword.cloud_notm}} console resources page
{: #delete-gui-resource}

You can delete an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console resources page by completing the following steps:

1. From the {{site.data.keyword.cloud_notm}} console, click **Resource List** on the left navigation menu.
2. Find the {{site.data.keyword.hscrypto}} service instance that you want to delete under the **Services** section.
3. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open the actions menu.
4. Click **Delete**.

### Deleting instances from the {{site.data.keyword.cloud_notm}} console instance details page
{: #delete-gui-detail}

You can delete an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console instance details page by completing the following steps:

1. From the {{site.data.keyword.cloud_notm}} console, click **Resource List** on the left navigation menu.
2. Find the {{site.data.keyword.hscrypto}} service instance that you want to delete under the **Services** section and click the instance name to open the instance details page.
3. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open the service instance actions menu.
4. Click **Delete service**.

### Deleting instances from the {{site.data.keyword.cloud_notm}} CLI
{: #delete-cli}

You can delete an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} CLI by running the following command:

```
ibmcloud resource service-instance-delete <instance_name|instance_ID>
```
{: pre}

Replace *instance_name* with your instance name and *instance_ID* with your [service instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). You can use either the instance name or the service instance ID to run the command.
