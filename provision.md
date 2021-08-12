---

copyright:
  years: 2018, 2021
lastupdated: "2021-08-12"

keywords: provision, crypto unit, service instance, create service instance, kms service instance, cloud hsm service instance, hpcs cli

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}

# Provisioning service instances
{: #provision}

You can create an instance of {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} by using the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

You can automate the instance creation by using Terraform. For more information, see [Setting up Terraform for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs).
{: tip}

## Before you begin
{: #provision-prerequisites}

In order to provision a {{site.data.keyword.hscrypto}} instance, make sure that you have a [Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account](/docs/account?topic=account-accounts).

1. To check your account type, go to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/login){: external} and click **Management** > **Account** > **Account settings**.

2. If you have a Lite account and want to use {{site.data.keyword.hscrypto}}, [upgrade your account to a Pay-As-You-Go or Subscription account](/docs/account?topic=account-upgrading-account). You can also [apply your promo code](/docs/billing-usage?topic=billing-usage-applying-promo-codes) if you have one.

## Provisioning from the {{site.data.keyword.cloud_notm}} console
{: #provision-gui}

To provision an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click **Catalog** to view the list of services that are available on {{site.data.keyword.cloud_notm}}.
3. From the Catalog navigation pane, click **Services**. And then, under **Category**, select **Security**.
4. From the list of services displayed, click the **{{site.data.keyword.hscrypto}}** tile.
5. Fill in the form with the details that are required.

    - Under **Region**, select a [region](/docs/hs-crypto?topic=hs-crypto-regions) that you want to create your {{site.data.keyword.hscrypto}} resources in.

      Currently, the `us-south` and `us-east` regions are enabled with recovery crypto units by default, which means, when a service instance is provisioned in either regions, you are enabled with the option to back up your master keys in the recovery crypto units located in both regions. For details, see [Introducing service instance initialization modes](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-recovery-crypto-unit).

    - Under **Service name**, enter a name for your service instance.
    - Under **Select a resource group**, select the resource group where you want to organize and manage your service intance. You can select the initial resource group that is named `Default` or other groups that you create. For more information, see [Creating and managing resource groups](/docs/account?topic=account-rgs).
    - Under **Tags** (Optional), add tags to organize your resources. If your tags are billing related, consider writing tags as `key: value` pairs to help group-related tags, such as `costctr:124`. For more information about tags, see [Working with tags](/docs/account?topic=account-tag).
    - Under **Number of operational crypto units**, select the number of [crypto units](#x9860404){: term} that meets your performance needs. At least two crypto units are to be enabled for high availability. These crypto units are distributed among different supported availability zones in the selected region.
    - Under **Number of cross-region failover crypto units**, select whether to enable failover crypto units that are used for an automatic restoration in case of a regional disaster.

      If you enable failover crypto units, set the number of failover crypto units equal to or less than the number of operational crypto units. However, to meet high availability, you need to specify at least two failover crypto units. Each failover crypto unit [is also charged](/docs/hs-crypto?topic=hs-crypto-faq-pricing). Failover crypto units are now available in Dallas (`us-south`) and Washington DC (`us-east`), so if you create your instance in other regions such as Frankfurt (`eu-de`), this option is automatically disabled.

      After you provision the service instance, you can still [enable or add failover crypto units by using the {{site.data.keyword.cloud_notm}} CLI](/docs/hs-crypto?topic=hs-crypto-enable-add-failover).
      {: tip}

    - **Failover region** shows the region where the failover crypto units are located.

      Available failover regions now are Dallas (`us-south`) and Washington DC (`us-east`). If you create your instance in either of the two regions, the failover region is automatically set to the other region.

    - Under **Allowed network**, choose the network access to your service instance:

        - **Public and private**: Manage your instance through both public and private network using the {{site.data.keyword.cloud_notm}} console, CLI, or API. This is the default option.
        - **Private only**: Access your service instance only through private network using CLI or API. The {{site.data.keyword.cloud_notm}} console is not available for the private-only network access.

        A private instance accepts API requests through only the private endpoints. The private endpoints are only accessible when your {{site.data.keyword.cloud_notm}} account, along with all associated resources, is enabled with [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint). You cannot access your private only instance through the CLI or API if your server or machine is outside the {{site.data.keyword.cloud_notm}} network.
        {: important}

    After you provision the service instance, you can still [update the network access policy](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies).
    {: tip}

6. Click **Create** to provision an instance of {{site.data.keyword.hscrypto}} in the account, region, and resource group where you are logged in.

## Provisioning from the {{site.data.keyword.cloud_notm}} CLI
{: #provision-cli}

To provision an instance of {{site.data.keyword.hscrypto}} with the {{site.data.keyword.cloud_notm}} CLI, complete the following steps:

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

    <table>
      <tr>
        <th>Variables</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>region_name</td>
        <td>The region abbreviation, such as <code>us-south</code> or <code>au-syd</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td>resource_group_name</td>
        <td>The resource group where you organize and manage the instance. You can select the initial resource group that is named <code>Default</code> or other groups that you create. For more information, see <a href="/docs/account?topic=account-rgs">Creating and managing resource groups</a>.</td>
      </tr>
      <caption>Table 1. Describes command variables to set the target region and resource group</caption>
    </table>

4. Run the following command to create a {{site.data.keyword.hscrypto}} instance:

    ```sh
    ibmcloud resource service-instance-create <instance_name> hs-crypto standard <region_name> [-p '{"units": <number_of_operational_crypto_units>, "allowed_network": "<network_access>", "failover_units": <number_of_failover_crypto_units>}']
    ```
    {: pre}

    Replace the variables in the example command according to the following table.

    <table>
      <tr>
        <th>Variables</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>instance_name</td>
        <td>Mandatory. The name of your {{site.data.keyword.hscrypto}} service instance.</td>
      </tr>
      <tr>
        <td>region_name</td>
        <td><p>Mandatory. The region abbreviation, such as <code>us-south</code> or <code>au-syd</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions">Regional service endpoints</a>.</p>
        <p>Currently, the <code>us-south</code> and <code>us-east</code> regions are enabled with recovery crypto units by default, which means, when a service instance is provisioned in either regions, you are enabled with the option to back up your master keys in the recovery crypto units located in both regions. For details, see <a href="/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-recovery-crypto-unit">Introducing service instance initialization modes</a>.</p></td>
      </tr>
      <tr>
        <td>number_of_operational_crypto_units</td>
        <td><p>Optional. Multiple crypto units are distributed among different supported availability zones in the selected region to increase availability.</p>
        <p>At least two crypto units are to be enabled for high availability. If you do not specify the number of crypto units, two crypto units are assigned by default.</p></td>
      </tr>
      <tr>
        <td>network_access</td>
        <td><p>Optional. Use this parameter to specify the network access to your service instance.</p>
        <p>The default setting is <strong>public and private</strong>, which means you can manage your instance through both public and private network using the {{site.data.keyword.cloud_notm}} console, CLI, or API.</p>
        <p>If you set the value to <strong>private-only</strong>, you can access your service instance only through private network using CLI or API. The {{site.data.keyword.cloud_notm}} console is not available for the private-only network access.</p>
        <p>After you provision the service instance, you can still <a href="/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies">update the network access policy</a>.</p></td>
      </tr>
      <tr>
        <td>number_of_failover_crypto_units</td>
        <td><p>Optional. Use this parameter to specify the number of failover crypto units to enable automatic cross-region recovery.</p>
        <p>Set the number of failover crypto units equal to or less than the number of operational crypto units. However, to meet high availability, you need to specify at least two failover crypto units. Each failover crypto unit <a href="/docs/hs-crypto?topic=hs-crypto-faq-pricing">is also charged</a>. Failover crypto units are now available in Dallas (<code>us-south</code>) and Washington DC (<code>us-east</code>). If you do not specify the number of failover crypto units, this feature is disabled by default.</p>
        <p>After you provision the service instance, you can still <a href="/docs/hs-crypto?topic=hs-crypto-enable-add-failover">enable or add failover crypto units by using the {{site.data.keyword.cloud_notm}} CLI</a>.</p></td>
      </tr>
      <caption>Table 2. Describes command variables to create a {{site.data.keyword.hscrypto}} service instance</caption>
    </table>

    A private instance accepts API requests through only the private endpoints. The private endpoints are only accessible when your {{site.data.keyword.cloud_notm}} account, along with all associated resources, is enabled with [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint). You cannot access your private only instance through the CLI or API if your server or machine is outside the {{site.data.keyword.cloud_notm}} network.
    {: important}

5. Verify that the service instance is created successfully. Run the following command to get all the service instances that you create. Check whether the {{site.data.keyword.hscrypto}} service instance is among the list.

    ```sh
    ibmcloud resource service-instances
    ```
    {: pre}

## What's next
{: #provision-next}

* Initialize your service instance with the [{{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) or the [{{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) so that {{site.data.keyword.hscrypto}} can provide key management and data management functions.
* To find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](/apidocs/hs-crypto){: external}.
* To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
* If you need to delete your service instance, see [Deleting service instances](/docs/hs-crypto?topic=hs-crypto-delete-instance) for instructions.
