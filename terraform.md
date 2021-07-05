---

copyright:
  years: 2021
lastupdated: "2021-07-05"

keywords: terraform, set up terraform, automate set up

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Setting up Terraform for {{site.data.keyword.hscrypto}}
{: #terraform-setup-for-hpcs}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multi-tier cloud environments following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.hscrypto}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud_notm}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud_notm}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud_notm}} catalog.
{: tip}

Before you begin, make sure that you have the [required access](/docs/hs-crypto?topic=hs-crypto-manage-access) to create and work with {{site.data.keyword.hscrypto}} resources.

## Example: Provisioning and initializing service instances by using Terraform
{: #terraform-provision-initialize-instance-hpcs}

Complete the following steps to create and initialize a {{site.data.keyword.hscrypto}} instance by using Terraform:

1. Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform by following the [Terraform on {{site.data.keyword.cloud_notm}} getting started tutorial](/docs/ibm-cloud-provider-for-terraform).

  The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to provision, update, or delete {{site.data.keyword.hscrypto}} service instances and resources. The preferred Terraform versions are 0.13.x, 0.14.x, and 0.15.x. In the `versions.tf` file, you need to specify the `version` parameter to `1.26.3`.

2. Set up the crypto unit administrators. You can select one of the following ways to create administrator signature keys:

  - Using the {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) CLI plug-in

    After you install and configure the TKE CLI plug-in by following [the instruction](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite), you can use the command `ibmcloud tke sigkey-add` to create administrator sinature keys. The signature keys are stored in files that are protected by passwords on your local workstation. The file path is specified by the environments variable `CLOUDTKEFILES`.

  - Using the third-party signing service

    **Need further input**
    
3. Create a Terraform configuration file `main.tf` in the same folder as `versions.tf`. In this file, you add the configurations to perform the corresponding actions.

  The following template is an example configuration file to provision a {{site.data.keyword.hscrypto}} instance with 2 operational crypto units in the `us-south` region. This instance is charged according to the standard pricing plan and is initialized with 2 administrators. The master key is automatically generated in recovery crypto units that are assigned to the instance.

  As recovery crypto units are currently available only in the `us-south` and `us-east` regions, using Terraform to initialize {{site.data.keyword.hscrypto}} instances is supported only in these two regions. For more information about manual initialization, see [Introducing service instance initialization approaches](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode).
  {: note}

  ```terraform
  resource ibm_hpcs hpcs {
     location             = "us-south"
     name                 = "test-hpcs"
     plan                 = "standard"
     units                = 2
     signature_threshold  = 1
     revocation_threshold = 1
     admins {
       name  = "admin1"
       key   = "/cloudTKE/1.sigkey"
       token = "sensitive1234"
     }
     admins {
       name  = "admin2"
       key   = "/cloudTKE/2.sigkey"
       token = "sensitive1234"
     }
  }
  ```
  {: codeblock}

  In production environments, it is suggested to provide the passwords for the signature key files or the tokens for the signing service during the process of applying Terraform instead of writing it in plaintext in the configuration file. After the instance intialization, the passwords are stored in a `.tfstate` file. For more information about securing sensitive data in Terraform, see [Sensitive Data in State](https://www.terraform.io/docs/language/state/sensitive-data.html){: external}.
  {: important}

  The following table lists supported parameters when you create and initialize a service instance with Terraform:

  <table>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>name</td>
      <td>**Required**. The name of your {{site.data.keyword.hscrypto}} instance.</td>
    </tr>
    <tr>
      <td>location</td>
      <td>**Required**. The region abbreviation, such as `us-south`, that represents the geographic area where the operational crypto units of your service instance are located. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions). As recovery crypto units are available only in `us-south` and `us-east`, only these two regions are supported if you want to use Terraform for instance initialization.</td>
    </tr>
    <tr>
      <td>plan</td>
      <td>**Required**. The pricing plan for your service instance. Currently, only the `standard` plan is supportd. </td>
    </tr>
    <tr>
      <td>units</td>
      <td>**Required**. The number of operational crypto units for your service instance. Valid values are 2 and 3.</td>
    </tr>
    <tr>
      <td>service_endpoints</td>
      <td>**Optional**. The network access to your service instance. Valid values are `public and private` and `private-only`. If you do not specify the value, the default setting is `public and private`.</td>
    </tr>
    <tr>
      <td>tags</td>
      <td>**Optional**. Tags that are associated with your instance are used to organize your resources. For more information about tags, see [Working with tags](/docs/account?topic=account-tag).</td>
    </tr>
    <tr>
      <td>resource_group_id</td>
      <td>**Optional**. The resource group where you want to organize and manage your service intance.</td>
    </tr>
    <tr>
      <td>signature_threshold</td>
      <td>**Required**. The number of administrator signatures that is required to execute administrative commands. The valid value is between 1 and 8. You need to set it to at least 2 to enable quorum authentication.</td>
    </tr>
    <tr>
      <td>revocation_threshold</td>
      <td>**Required**. The number of administrator signatures that is required to remove an administrator after you leave the imprint mode. The valid value is between 1 and 8.</td>
    </tr>
    <tr>
      <td>admins</td>
      <td>**Required**. The list of administrators for the instance crypto units. You can set up to 8 administrators and the number needs to be equal to or greater than the thresholds that you specify. The following values need to be set for each administrator:
      <ul>
      <li>name: The name of the administrator.</li>
      <li>key: The path in your local workstation where you store the administrator signature file.</li>
      <li>token: The administrator password to access the corresponding signature file.</li>
      </ul>
      </td>
    </tr>
    <tr>
      <td>signature_server_url</td>
      <td>**Optional**. The URL of the signing service. If you use a third-party signing service to provide administrator signature keys, you need to specify the URL.</td>
    </tr>
    <caption>Table 1. Supported parameters for provisioning a service instance with Terraform</caption>
  </table>

4. Initialize the Terraform CLI with the following command.

  ```
  terraform init
  ```
  {: pre}

5. Create a Terraform execution plan with the following command. The Terraform execution plan summarizes all the actions that need to be run to create the {{site.data.keyword.hscrypto}} instance in your account.

  ```
  terraform plan
  ```
  {: pre}

6. Create and initialize the {{site.data.keyword.hscrypto}} instance by applying Terraform.

  ```
  terraform apply
  ```
  {: pre}

7. Check whether the {{site.data.keyword.hscrypto}} instance is created and initialized from the [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources){: external}.
8. Verify that the access policy is successfully assigned. For more information, see [Reviewing assigned access in the console](/docs/account?topic=account-assign-access-resources#review-your-access-console).

## What's next?
{: #terraform-setup-hpcs-next}

For other task examples with Terraform such as creating keys and setting policies, see the [Terraform documentation - Key Management Service](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key). The documentation also lists the complete argument and attribute reference.
