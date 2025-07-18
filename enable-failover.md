---

copyright:
  years: 2021, 2025
lastupdated: "2025-07-11"

keywords: failover crypto unit, add failover crypto units, enable failover, enable cross-region recovery

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Enabling or adding failover crypto units after you provision a service instance
{: #enable-add-failover}

Failover crypto units back up the operational crypto units and keystores in another region. If a regional disaster occurs, you can use failover crypto units to automatically restore your data, which can reduce the downtime and data loss. You can either enable failover crypto unit [when you provision a service instance](/docs/hs-crypto?topic=hs-crypto-provision) or after you provision a service instance. This topic guides you through enabling or adding failover crypto units after you provision a service instance.
{: shortdesc}

If you have a service instance in the `us-south`, `us-east`, or `eu-es` region, you can enable failover crypto units for your instance with the {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) CLI plug-in or the Management Utilities. If failover crypto units are already assigned to your service instance, you can still add extra ones. After you add failover crypto units, make sure to raise a support ticket to repair the instance and enable the failover units.

You can specify a total number of failover crypto units that are equal to or less than the number of operational crypto units. However, to meet high availability, at least two failover crypto units need to be assigned. Failover crypto units are also charged. For the detailed pricing information, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing).
{: tip}

## Step 1: Add failover crypto units
{: #add-failover-cu}

You can enable or add failover crypto units either by using the {{site.data.keyword.cloud_notm}} CLI or the Management Utilities.

### Using the {{site.data.keyword.cloud_notm}} CLI
{: #enable-add-failover-cli}

To enable or add failover crypto units by using the {{site.data.keyword.cloud_notm}} CLI, follow these steps:

1. Check and make sure that you install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli) and the latest TKE CLI plug-in with the following command:

    ```
    ibmcloud plugin install tke
    ```
    {: pre}

    If you have installed the TKE CLI plug-in, make sure to update your plug-in to the latest version with the following command:

    ```
    ibmcloud plugin update tke
    ```
    {: pre}

2. Log in to {{site.data.keyword.cloud_notm}} with the CLI.

    If you have multiple accounts, select the account that your service instance is created with. Make sure that you're logged in to the correct region and resource group where the service instance locates with the following command:

    ```
    ibmcloud target -r <region> -g <resource_group>
    ```
    {: pre}

3. To enable or add failover crypto units, run the following command:

    ```
    ibmcloud tke failover-enable
    ```
    {: pre}

    Before you can run this command, make sure that you select all the crypto units for the target instance by using the `ibmcloud tke cryptounit-add` command.
    {: note}

    This command walks you through the procedure to enable or add failover crypto units. Follow the prompts to complete the following steps:

    1. Enter the total number of failover crypto units that you want to assign to your service instance.

        For a service instance with 3 operational crypto units, specify 2 or 3 failover crypto units. For a service instance with 2 operational crypto units, specify 2 failover crypto units.

        The following output is a sample display:

        ```
        You currently have 0 failover crypto unit(s) for the selected instance 00000a09-0563-4e00-b259-06a4edfc4cba
        Since you have 2 operational crypto units for this instance, you can have up to 2 failover crypto units
        Enter the total number of failover crypto units you would like (max 2):
        > 2

        You will now have 2 failover crypto units. This will affect your billing. For more information, see https://cloud.ibm.com/docs/hs-crypto?topic=hs-crypto-faq-pricing

        Would you like to continue? [y/n]:
        > y
        ```
        {: screen}

        If your instance already has a certain number of failover crypto units assigned, you can also use this command and follow the same procedure to add more failover crypto units.
        {: tip}

    2. Type `y` to confirm the action. The failover crypto units are assigned in the target failover region.

        Failover crypto units are now available in `us-south`, `us-east`, and `eu-es`.

        The following output is a sample display:

        ```
        Instance 00000a09-0563-4e00-b259-06a4edfc4cba targeting backup region us-south
        2 failover crypto units have been assigned.
        Getting crypto unit info... this may take a moment

        API endpoint:    https://cloud.ibm.com
        Region:          us-south
        User:            user@ibm.com
        Account:         user-account (8230.....a255)
        Resource group:  Default

        SERVICE INSTANCE: 00000a09-0563-4e00-b259-06a4edfc4cba
        CRYPTO UNIT NUM   SELECTED   TYPE           LOCATION
        1                 true       OPERATIONAL    [us-east].[AZ3-CS3].[02].[03]
        2                 true       OPERATIONAL    [us-east].[AZ2-CS2].[02].[03]
        3                 true       RECOVERY       [us-east].[AZ2-CS4].[03].[06]
        4                 true       RECOVERY       [us-south].[AZ3-CS2].[03].[20]
        5                 false      FAILOVER       [us-south].[AZ2-CS2].[03].[04]
        6                 false      FAILOVER       [us-south].[AZ3-CS3].[01].[07]

        Note: all operational crypto units in a service instance must be configured the same.
        Use 'ibmcloud tke cryptounit-compare' to check how crypto units are configured.
        You should initialize your failover crypto units now to be prepared for a failover event.
        ```
        {: screen}

4. Initialize failover crypto units by using the same master key for the operational crypto units initialization and the same initialization approach:

    - [Initializing service instances with smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities)
    - [Initializing service instances by using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)
    
    To initialize your service instances by using recovery crypto units, you need to install administrators, set the signature thresholds, and load the current master key register. Select the failover crypto units to be initialized, and use the following TKE plug-in commands:

    - Add administrators: `ibmcloud tke cryptounit-admin-add`.
    - Set the signature thresholds: `ibmcloud tke cryptounit-thrhld-set`.
    - Transfer the master key value in a recovery crypto unit to the failover crypto units: `ibmcloud tke auto-mk-recover`. 

    You need to initialize failover crypto units before you use them for a regional disaster recovery. It is suggested you initialize the failover crypto units right after you enable them for your service instance.
    {: note}

### Using the Management Utilities
{: #enable-add-failover-management-utilities}

To enable or add failover crypto units by using the Management Utilities, follow these steps:

1. Check and make sure that you complete the prerequisites:

    1. [Set up the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities), and plug the two smart card readers into the USB ports of your workstation.
    
    2. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli) and the latest TKE CLI plug-in with the following command:

        ```
        ibmcloud plugin install tke
        ```
        {: pre}

        If you have installed the TKE CLI plug-in, make sure to update your plug-in to the latest version with the following command:

        ```
        ibmcloud plugin update tke
        ```
         {: pre}

    3. Log in to {{site.data.keyword.cloud_notm}} with the CLI.

        If you have multiple accounts, select the account that your service instance is created with. Make sure that you're logged in to the correct region and resource group where the service instance locates with the following command:

        ```
        ibmcloud target -r <region> -g <resource_group>
        ```
        {: pre}

2. Start the Trusted Key Entry application by changing to the subdirectory where you install the Management Utilities applications and running the following command:

    ```
    ./tke
    ```
    {: pre}

    When the Trusted Key Entry application is started, the account and resource group that you selected when you logged in to IBM Cloud are displayed.

3. To enable or add failover crypto units, on the **Crypto units** tab, perform the following steps:

    1. Click **Add crypto units**. In the dialog box that is displayed, enter the numbers of all crypto units in the service instance that is separated by a space.

    2. Click **Failover enable**, and click **Yes** to continue. 

    3. If the service instance has three operational crypto units, you are prompted to enter the number of failover crypto units based on your need. Either `2` or `3` failover crypto units are supported. 

        For a service instance with only two operational crypto units, two failover crypto units are assigned automatically. You don't need to take any actions in this case.
        
    4. Click **Yes** to confirm the action. The failover crypto units are assigned in the target failover region.

        Failover crypto units are now available in `us-south`, `us-east`, and `eu-es`. 

4. Initialize failover crypto units by using the same master key for the operational crypto units initialization and the same initialization approach:

    - [Initializing service instances with smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities)
    - [Initializing service instances by using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)

    You need to initialize failover crypto units before you use them for a regional disaster recovery. It is suggested you initialize the failover crypto units right after you enable them for your service instance.
    {: note}

## Step 2: Raise a support ticket
{: #raise-support-ticket}

After you add the failover crypto units, you need to let IBM Support know about this change by raising a support ticket, so that they can enable the added failover crypto units for you.

1. In your {{site.data.keyword.cloud_notm}} dashboard, click the **Help** icon ![Help icon](../icons/help.svg "Help") > **Support center** from the UI menu bar to enter the Support Center. Click **View all** in the **Recent support cases** panel and click **Create new case**. Or, you can directly go to the [Manage cases page](https://cloud.ibm.com/unifiedsupport/cases){: external} and click **Create new case**.
2. On the **Create a case** page displayed, select the offering {{site.data.keyword.hscrypto}}, and then specify the following values:

    | Field name | Action |
    | --- | --- |
    | Subject | Enter **Enable failover crypto units**. |
    | Description | Enter your [service instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID), the region that your service instance resides in, and the number of failover crypto units that you add. |
    | Selected resources | Select your {{site.data.keyword.hscrypto}} service instance. |
    {: caption="Describes the fields that are required to enable failover crypto units" caption-side="bottom"}

3. Check the **Email me updates about this issue** box, and click **Continue to review > Create case**.

    After the operation is completed successfully, you will get an email notification. You can also check the state in the Support Center by clicking the **Help** icon ![Help icon](../icons/help.svg "Help") > **Support center** from the UI menu bar.

## What's next
{: #enable-add-failover-next}

If a regional disaster occurs, you can use failover crypto units for automatic data restoration. For more information, see [Cross-region disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr#cross-region-disaster-recovery) and [Restoring your data from another region](/docs/hs-crypto?topic=hs-crypto-restore-data).
