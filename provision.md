---

copyright:
  years: 2018, 2024
lastupdated: "2024-06-25"

keywords: provision, crypto unit, service instance, create service instance, kms service instance, cloud hsm service instance, hpcs cli

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Provisioning service instances
{: #provision}

You can create an instance of {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} by using the UI or the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

You can automate the instance creation by using Terraform. For more information, see [Setting up Terraform for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs).
{: tip}


{{site.data.keyword.hscrypto}} offers the following pricing plans. You can find the detailed pricing plans on the [service creation page](/catalog/services/hyper-protect-crypto-services){: external}. 

* [A standard plan with the Keep Your Own Key capability](/docs/hs-crypto?topic=hs-crypto-overview)
* [An extended plan with both the Keep Your Own Key and {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-overview)


[Pricing samples](/docs/hs-crypto?topic=hs-crypto-faq-pricing) for these two plans are also available for your reference.

## Before you begin
{: #provision-prerequisites}

In order to provision a {{site.data.keyword.hscrypto}} instance, make sure that you have a [Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account](/docs/account?topic=account-accounts).

1. To check your account type, go to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/login){: external} and click **Management** > **Account** > **Account settings**.
2. If you have a Lite account and want to use {{site.data.keyword.hscrypto}}, [upgrade your account](/docs/account?topic=account-upgrading-account) to a Pay-As-You-Go or Subscription account. You can also [apply your promo code](/docs/billing-usage?topic=billing-usage-applying-promo-codes) if you have one.

## Provisioning an instance of {{site.data.keyword.hscrypto}} Standard Plan
{: #provision-standard}

You can provision an instance of {{site.data.keyword.hscrypto}} Standard Plan from either the UI or CLI.

### Using the UI
{: #provision-gui}
{: ui}

To provision an instance of {{site.data.keyword.hscrypto}} Standard Plan from the UI, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click **Create resource** to view the list of services that are available on {{site.data.keyword.cloud_notm}}.
3. Under **Category**, select **Security**.
4. From the list of services displayed, click the **{{site.data.keyword.hscrypto}}** tile.
5. On the service page, select the **Standard** pricing plan.  
5. Fill in the form with the details that are required.

    - Under **Region**, select a [region](/docs/hs-crypto?topic=hs-crypto-regions) that you want to create your {{site.data.keyword.hscrypto}} resources in.

      Currently, supported regions other than Madrid (`eu-es`) are enabled with recovery crypto units by default, which means, when a service instance is provisioned in any supported regions, you are by default enabled with the option to back up your master keys in the recovery crypto units located in the disaster recovery region. For more information, see [Introducing service instance initialization modes](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-recovery-crypto-unit).

    - Under **Service name**, enter a name for your service instance.
    - Under **Select a resource group**, select the resource group where you want to organize and manage your service instance. You can select the initial resource group that is named `Default` or other groups that you create. For more information, see [Creating and managing resource groups](/docs/account?topic=account-rgs).
    - (Optional) Under **Tags**, add tags to organize your resources. If your tags are billing related, consider writing tags as `key: value` pairs to help with grouping, such as `costctr:124`. For more information about tags, see [Working with tags](/docs/account?topic=account-tag).
    - Under **Access management tags** (Optional), add tags to resources to help organize access control relationships in the `project:analysis` format. For more information, see [Controlling access to resources by using tags](/docs/account?topic=account-access-tags-tutorial).
    - Under **Number of crypto units**, select the number of [crypto units](#x9860404){: term} that meets your performance needs. At least two crypto units are to be enabled for high availability. These crypto units are distributed among different supported availability zones in the selected region.
    - Under **Number of cross-region failover crypto units**, select whether to enable failover crypto units that are used for an automatic restoration in case of a regional disaster.

      If you enable failover crypto units, set the number of failover crypto units equal to or less than the number of operational crypto units. However, to meet high availability, you need to specify at least two failover crypto units. Each failover crypto unit [is also charged](/docs/hs-crypto?topic=hs-crypto-faq-pricing). Failover crypto units are now available in Dallas (`us-south`) and Washington DC (`us-east`), so if you create your instance in other regions such as Frankfurt (`eu-de`), this option is automatically disabled.

      After you provision the service instance, you can still [enable or add failover crypto units](/docs/hs-crypto?topic=hs-crypto-enable-add-failover).
      {: tip}

    - **Failover region** shows the region where the failover crypto units are located.

      Available failover regions now are Dallas (`us-south`) and Washington DC (`us-east`). If you create your instance in either of the two regions, the failover region is automatically set to the other region.

    - Under **Allowed network**, choose the network access to your service instance:

        - **Public and private**: Manage your instance through both public and private network using the UI, CLI, or API. This is the default option.
        - **Private only**: Access your service instance only through private network using CLI or API. The UI is not available for the private-only network access.

        A private instance accepts API requests through only the private endpoints. The private endpoints are only accessible when your {{site.data.keyword.cloud_notm}} account, along with all associated resources, is enabled with [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint). You cannot access your private only instance through the CLI or API if your server or machine is outside the {{site.data.keyword.cloud_notm}} network.
        {: important}

    After you provision the service instance, you can still [update the network access policy](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies).
    {: tip}

    - Under **HSM connection**, choose whether you use IBM-provided cloud HSMs or your own on-premises HSMs.

        - **Standard cloud HSM**: Use FIPS 140-2 level 4 certified HSMs that IBM Cloud provides for key generation and management. You take the full ownership of the HSM by [initializing your service instance](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite) after the provision.
        - **Bring Your Own HSM**: Use your own on-premises HSMs to retain physical control over your encryption keys to meet the data sovereignty regulations. Before you can enable this function, you need to prepare and set up on-premises HSMs. For more information, see [Introducing Bring Your Own HSM](/docs/hs-crypto?topic=hs-crypto-introduce-bring-your-own-hsm) and [Setting up BYOHSM](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm).

            After you select this option, the **HSM connector ID** field is displayed. You need to provide the HSM connector ID that you get from IBM. For more information, see [Contact IBM to get the required information](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm&interface=ui#tutorial-byohsm-step3).
   
6. Click **Create** to provision an instance of {{site.data.keyword.hscrypto}} in the account, region, and resource group where you are logged in.

### Using the {{site.data.keyword.cloud_notm}} CLI
{: #provision-cli}
{: cli}

To provision an instance of {{site.data.keyword.hscrypto}} Standard Plan with the {{site.data.keyword.cloud_notm}} CLI, complete the following steps:

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started){: external}.
2. Log in to {{site.data.keyword.cloud_notm}} through the {{site.data.keyword.cloud_notm}} CLI with the following command:

    ```sh
    ibmcloud login
    ```
    {: pre}

    If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.
    {: tip}

3. Select the region and resource group where you want to create a {{site.data.keyword.hscrypto}} service instance. You can use the following command to set your target region and resource group.

    ```sh
    ibmcloud target -r <region_name> -g <resource_group_name>
    ```
    {: pre}

    Replace the variables in the sample command according to the following table.

    | Variables | Description |
    | --- | --- |
    | `region_name` | The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions). |
    | `resource_group_name` | The resource group where you organize and manage the instance. You can select the initial resource group that is named `Default` or other groups that you create. For more information, see [Creating and managing resource groups](/docs/account?topic=account-rgs). |
    {: caption="Table 1. Describes command variables to set the target region and resource group" caption-side="bottom"}

4. Run the following command to create a {{site.data.keyword.hscrypto}} instance:

    ```sh
    ibmcloud resource service-instance-create <instance_name> hs-crypto standard <region_name> [-p '{"units": <number_of_operational_crypto_units>, "allowed_network": "<network_access>", "failover_units": <number_of_failover_crypto_units>}']
    ```
    {: pre}

    Replace the variables in the example command according to the following table.

    | Variables | Description |
    | --- | --- |
    | `instance_name` | **Required**. The name of your {{site.data.keyword.hscrypto}} service instance. |
    | `region_name` | **Required**. The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions). \n \n Currently, service instances in the `eu-es` region don't support recovery crypto units, which means, when a service instance is provisioned in any supported regions, you are by default enabled with the option to back up your master keys in the recovery crypto units located in the disaster recovery region. For more information, see [Introducing service instance initialization modes](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-recovery-crypto-unit). |
    | `number_of_operational_crypto_units` | **Optional**. Multiple crypto units are distributed among different supported availability zones in the selected region to increase availability. At least two crypto units are to be enabled for high availability. If you do not specify the number of crypto units, two crypto units are assigned by default. |
    | `network_access` | **Optional**. Use this parameter to specify the network access to your service instance. The default setting is **public and private**, which means you can manage your instance through both public and private network using the UI, CLI, or API. \n \n If you set the value to **private-only**, you can access your service instance only through private network using CLI or API. The UI is not available for the private-only network access. After you provision the service instance, you can still [update the network access policy](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies). |
    | `number_of_failover_crypto_units` | **Optional**. Use this parameter to specify the number of failover crypto units to enable automatic cross-region recovery. \n \n Set the number of failover crypto units equal to or less than the number of operational crypto units. However, to meet high availability, you need to specify at least two failover crypto units. Each failover crypto unit [is also charged](/docs/hs-crypto?topic=hs-crypto-faq-pricing). Failover crypto units are now available in Dallas (`us-south`) and Washington DC (`us-east`). If you do not specify the number of failover crypto units, this feature is disabled by default. After you provision the service instance, you can still [enable or add failover crypto units](/docs/hs-crypto?topic=hs-crypto-enable-add-failover). |
    {: caption="Table 2. Describes command variables to create a {{site.data.keyword.hscrypto}} service instance" caption-side="bottom"}

    A private instance accepts API requests through only the private endpoints. The private endpoints are only accessible when your {{site.data.keyword.cloud_notm}} account, along with all associated resources, is enabled with [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint). You cannot access your private only instance through the CLI or API if your server or machine is outside the {{site.data.keyword.cloud_notm}} network.
    {: important}

5. Verify that the service instance is created successfully. Run the following command to get all the service instances that you create. Check whether the {{site.data.keyword.hscrypto}} service instance is among the list.

    ```sh
    ibmcloud resource service-instances
    ```
    {: pre}


## Provisioning an instance of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} 
{: #provision-uko}

You can provision an instance of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} from either the UI or CLI.

### Using the UI
{: #provision-uko-gui}
{: ui}

To provision an instance of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} from the UI, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click **Create resource** to view the list of services that are available on {{site.data.keyword.cloud_notm}}.
3. Under **Category**, select **Security**.
4. From the list of services displayed, click the **{{site.data.keyword.hscrypto}}** tile.
5. On the service page, select the **With {{site.data.keyword.uko_full_notm}}** pricing plan.  
5. Fill in the form with the details that are required.

    - Under **Region**, select a [region](/docs/hs-crypto?topic=hs-crypto-regions) that you want to create your {{site.data.keyword.hscrypto}} resources in.

      Currently, service instances in the `eu-es` region don't support recovery crypto units. When a service instance is provisioned in other supported regions, you are by default enabled with the option to back up your master keys in the recovery crypto units located in the disaster recovery region. For details, see [Introducing service instance initialization modes](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-recovery-crypto-unit).

    - Under **Service name**, enter a name for your service instance.
    - Under **Select a resource group**, select the resource group where you want to organize and manage your service instance. You can select the initial resource group that is named `Default` or other groups that you create. For more information, see [Creating and managing resource groups](/docs/account?topic=account-rgs).
    - Under **Tags** (Optional), add tags to organize your resources. If your tags are billing related, consider writing tags as `key: value` pairs to help group-related tags, such as `costctr:124`. For more information about tags, see [Working with tags](/docs/account?topic=account-tag).
    - Under **Access management tags** (Optional), add tags to resources to help organize access control relationships in the `project:analysis` format. For more information, see [Controlling access to resources by using tags](/docs/account?topic=account-access-tags-tutorial).
    - Under **Number of crypto units**, select the number of [crypto units](#x9860404){: term} that meets your performance needs. At least two crypto units are to be enabled for high availability. These crypto units are distributed among different supported availability zones in the selected region.
    - Under **Number of cross-region failover crypto units**, select whether to enable failover crypto units that are used for an automatic restoration in case of a regional disaster.

      If you enable failover crypto units, set the number of failover crypto units equal to or less than the number of operational crypto units. However, to meet high availability, you need to specify at least two failover crypto units. Each failover crypto unit [is also charged](/docs/hs-crypto?topic=hs-crypto-faq-pricing). Failover crypto units are now available in Dallas (`us-south`) and Washington DC (`us-east`), so if you create your instance in other regions such as Frankfurt (`eu-de`), this option is automatically disabled.

      After you provision the service instance, you can still [enable or add failover crypto units](/docs/hs-crypto?topic=hs-crypto-enable-add-failover).
      {: tip}

    - **Failover region** shows the region where the failover crypto units are located.

      Available failover regions now are Dallas (`us-south`) and Washington DC (`us-east`). If you create your instance in either of the two regions, the failover region is automatically set to the other region.
 
6. Click **Create** to provision an instance of {{site.data.keyword.hscrypto}} in the account, region, and resource group where you are logged in.

### Using the {{site.data.keyword.cloud_notm}} CLI
{: #provision-uko-cli}
{: cli}

To provision an instance of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} from the {{site.data.keyword.cloud_notm}} CLI, complete the following steps:

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started){: external}.
2. Log in to {{site.data.keyword.cloud_notm}} through the {{site.data.keyword.cloud_notm}} CLI with the following command:

    ```sh
    ibmcloud login
    ```
    {: pre}

    If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.
    {: tip}

3. Select the region and resource group where you want to create a {{site.data.keyword.hscrypto}} service instance. You can use the following command to set your target region and resource group.

    ```sh
    ibmcloud target -r <region_name> -g <resource_group_name>
    ```
    {: pre}

    Replace the variables in the sample command according to the following table.

    | Variables | Description |
    | --- | --- |
    | `region_name` | The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions). |
    | `resource_group_name` | The resource group where you organize and manage the instance. You can select the initial resource group that is named `Default` or other groups that you create. For more information, see [Creating and managing resource groups](/docs/account?topic=account-rgs). |
    {: caption="Table 3. Describes command variables to set the target region and resource group for a {{site.data.keyword.hscrypto}} instance with {{site.data.keyword.uko_full_notm}}" caption-side="bottom"}

4. Run the following command to create a {{site.data.keyword.hscrypto}} instance:

    ```sh
    ibmcloud resource service-instance-create <instance_name> hs-crypto hpcs-hourly-uko <region_name> [-p '{"units": <number_of_operational_crypto_units>']
    ```
    {: pre}

    Replace the variables in the example command according to the following table.

    | Variables | Description |
    | --- | --- |
    | `instance_name` | **Required**. The name of your {{site.data.keyword.hscrypto}} service instance. |
    | `region_name` | **Required**. The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions). \n Currently, service instances in the `eu-es` region don't support recovery crypto units, which means, when a service instance is provisioned in any supported regions, you are by default enabled with the option to back up your master keys in the recovery crypto units located in the disaster recovery region. For details, see [Introducing service instance initialization modes](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-recovery-crypto-unit). |
    | `number_of_operational_crypto_units` | **Optional**. Multiple crypto units are distributed among different supported availability zones in the selected region to increase availability. At least two crypto units are to be enabled for high availability. If you do not specify the number of crypto units, two crypto units are assigned by default. | 
    {: caption="Table 4. Describes command variables to create a {{site.data.keyword.hscrypto}} instance with {{site.data.keyword.uko_full_notm}}" caption-side="bottom"}

5. Verify that the service instance is created successfully. Run the following command to get all the service instances that you create. Check whether the {{site.data.keyword.hscrypto}} service instance is among the list.

    ```sh
    ibmcloud resource service-instances
    ```
    {: pre}


## What's next
{: #provision-next}

* As a security officer, auditor, or manager, you can use the {{site.data.keyword.at_full_notm}} service to monitor the status of your instance and how administrators, users, and applications interact with {{site.data.keyword.hscrypto}}. To enable {{site.data.keyword.at_full_notm}} for your {{site.data.keyword.hscrypto}} instance, you need to provision an instance of {{site.data.keyword.at_full_notm}} in the same region where your {{site.data.keyword.hscrypto}} instance is located. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).
* Initialize your service instance with the [{{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) or the [{{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) so that {{site.data.keyword.hscrypto}} can provide key management and data management functions.
* To find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} key management service API reference doc](/apidocs/hs-crypto){: external} or [{{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko){: external}.
* To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
* If you need to delete your service instance, see [Deleting service instances](/docs/hs-crypto?topic=hs-crypto-delete-instance) for instructions.
