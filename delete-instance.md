---

copyright:
  years: 2018, 2023
lastupdated: "2023-09-27"

keywords: delete, delete service instance, crypto unit, ibm cloud cli, clear crypto unit, uninstall

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}

# Deleting service instances
{: #delete-instance}

You can delete your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance with the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} CLI. To do so, you need to set all the [crypto units](#x9860404){: term} of the service instance back to the [imprint mode](#x9860399){: term} by zeroizing the crypto units.
{: shortdesc}

## Before you begin
{: #delete-instance-prerequisite}

1. Follow [these instructions](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite) to set the environment variable `CLOUDTKEFILES` on your workstation to specify the directory where you saved the master key part files and signature key files you created when you initialized your service instance.
2. Log in to {{site.data.keyword.cloud_notm}} also by following [these instructions](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite). 


## Step 1: Delete keys 
{: #delete-all-key-step}

To delete keys in the service instance, you need to delete root keys with the standard plan and managed keys with the {{site.data.keyword.uko_full_notm}} plan through the {{site.data.keyword.cloud_notm}} console or the CLI.

### Deleting root keys from the {{site.data.keyword.cloud_notm}} console - Standard plan
{: delete-root-key-gui}
{: ui}

You can delete root keys of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console resources page by completing the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **KMS keys** page, use the **Keys** table to browse the keys in your service.
5. Select the key that you want to delete and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key.
6. From the options menu, click **Delete key**, enter the key name to confirm the key to be deleted, and click **Delete key**.

### Deleting managed keys from the {{site.data.keyword.cloud_notm}} console - {{site.data.keyword.uko_full_notm}} plan
{: delete-managed-key-gui}
{: ui}

You can delete managed keys of {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} from the {{site.data.keyword.cloud_notm}} console resources page by completing the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. If the managed key that you want to delete is in Active state, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Deactivated** to deactivate the key first.
4. To destroy a Pre-active or Deactivated key, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Destroyed**.
5. Click **Destroy key** to confirm.
6. To remove the key and the metadata from the vault, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Remove from vault**.

### Deleting roots keys from the {{site.data.keyword.cloud_notm}} CLI - Standard plan
{: delete-root-key-cli}
{: cli}

You can delete root keys of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} CLI by running the following command:

```
ibmcloud kp key delete KEY_ID_OR_ALIAS
        -i, --instance-id INSTANCE_ID
    [--key-ring          KEY_RING_ID]
    [-f, --force]
    [-o, --output      OUTPUT]
```
{: codeblock}

- *Key_ID_OR_ALIAS* is the v4 UUID or alias of the key that you want to delete. 
- *-i, --instance-id* is your [service instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).



### Deleting managed keys from the {{site.data.keyword.cloud_notm}} CLI - {{site.data.keyword.uko_full_notm}} plan
{: delete-managed-key-cli}
{: cli}

You can delete managed keys of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} CLI by running the following command:

```
ibmcloud hpcs uko managed-key-delete --id ID --uko-vault UKO-VAULT --if-match IF-MATCH
```
{: codeblock}

- *ID* is the UUID of the key, which you can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.
- *UKO-VAULT* is the UUID of the vault, which you can use the `ibmcloud hpcs uko vaults` command to retrieve the vault UUID. 
- *IF-MATCH* is value of the ETag from the header on a GET request, which you can use the `ibmcloud hpcs uko managed-key` command to retrieve the ETag.

## Step 2: Select the crypto units to be deleted 
{: #select-crypto-unit-step}

1. To select the administrators to sign TKE commands, use the following command:

    ```
    ibmcloud tke sigkey-sel
    ```
    {: pre}

    A list of signature keys that are found on the workstation is displayed. When prompted, enter the key numbers of the signature key files to select for signing future administrative commands. When prompted, enter the passwords for the signature key files.

2. To list the numbers of crypto units in the target resource group under the current user account, run the following command:

    ```
    ibmcloud tke cryptounits
    ```
    {: pre}

3. Check whether the crypto units that you want to zeroize are marked as `true`. If not, add the crypto units by running the following command:
    
    ```
    ibmcloud tke cryptounit-add
    ```
    {: pre}

    A list of the crypto units in the target resource group under the current user account is displayed. When prompted, enter crypto unit numbers to be zeroized to the selected crypto unit list.

## Step 3: Zeroize crypto units
{: #zeroize-crypto-unit-step}

If you initialize your service instance and load the [master key](#x2908413){: term} to the service instance, you need to set the crypto units back to imprint mode with the following steps:

1. Clear all crypto unit administrators and the master key registers with one of the following options:

    -  If you initialize your service instance through {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) command-line interface (CLI) plug-in, run the following command to zeroize the crypto units in the TKE CLI plug-in:

        ```
        ibmcloud tke cryptounit-zeroize
        ```
        {: pre}

    -  If you initialize your service instance through the Management Utilities, in the user interface of the TKE application, select **Imprint mode** &gt; **Zeroize crypto unit**.

2. To zeroize the crypto units, enter the password for the administrator signature key to be used when prompted. Make sure that your signature key files are properly saved either on your workstation or on your smart cards. Otherwise, you are not able to perform this action.

After you zeroize the crypto unit, the administrator [signature keys](#x8250375){: term} and the master key are cleared from the crypto unit, which means you are not able to access keys that are protected by the master key. Any resources that are associated with the root keys cannot be accessed. However, you might still be charged for the resources, such as the [Immutable Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-immutable), as long as the policy is enforced. 
{: important}

## Step 4: Optional - Uninstall the {{site.data.keyword.hscrypto}} utilities
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



- [Linux]{: tag-linux} operating system

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

## Step 5: Delete your service instance
{: #delete-instance-step}

After you set the crypto units to imprint mode, you can choose to delete your service instance through the {{site.data.keyword.cloud_notm}} console resources page, the instance details page, or the CLI.

### Deleting instances from the {{site.data.keyword.cloud_notm}} console resources page
{: #delete-gui-resource}
{: ui}

You can delete an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console resources page by completing the following steps:

1. From the {{site.data.keyword.cloud_notm}} console, click **Resource list** from the navigation.
2. Find the {{site.data.keyword.hscrypto}} service instance that you want to delete under the **Services** section.
3. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open the actions menu.
4. Click **Delete**.

### Deleting instances from the {{site.data.keyword.cloud_notm}} console instance details page
{: #delete-gui-detail}
{: ui}

You can delete an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console instance details page by completing the following steps:

1. From the {{site.data.keyword.cloud_notm}} console, click **Resource list** from the navigation.
2. Find the {{site.data.keyword.hscrypto}} service instance that you want to delete under the **Services** section and click the instance name to open the instance details page.
3. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open the service instance actions menu.
4. Click **Delete service**.

### Deleting instances from the {{site.data.keyword.cloud_notm}} CLI
{: #delete-cli}
{: cli}

You can delete an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} CLI by running the following command:

```
ibmcloud resource service-instance-delete <instance_name|instance_ID>
```
{: pre}

Replace *instance_name* with your instance name and *instance_ID* with your [service instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). You can use either the instance name or the service instance ID to run the command.
