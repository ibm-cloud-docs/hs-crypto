---

copyright:
  years: 2021
lastupdated: "2021-06-02"

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

## Example: Provisioning service instances by using Terraform
{: #terraform-provisioning-instance-hpcs}

Complete the following steps to create a {{site.data.keyword.hscrypto}} instance by using Terraform:

1. Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform by following the [Terraform on {{site.data.keyword.cloud_notm}} getting started tutorial](/docs/ibm-cloud-provider-for-terraform). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to provision, update, or delete {{site.data.keyword.hscrypto}} service instances and resources.
2. Create a Terraform configuration file that is named `main.tf`. In this file, you add the configurations to perform the corresponding actions. The following example configures the file to createa a {{site.data.keyword.hscrypto}} instance and to assign a user an access policy in Identity and Access Management (IAM) for that instance by using HashiCorp Configuration Language (HCL). For more information, see the [Terraform documentation](https://www.terraform.io/docs/language/index.html){: external}.

  The {{site.data.keyword.hscrypto}} instance in this example is named `hpcsservice` and is created with the standard pricing plan in the `us-south` region. The instance has two operational crypto units. The `user@ibm.com` is assigned the `Manager` role in the IAM access policy. For other supported regions, see [Regions and endpoints](/docs/hs-crypto?topic=hs-crypto-regions).

  ```terraform
  resource "ibm_resource_instance" "hpcs" {
     name     = "hpcsservice"
     service  = "hs-crypto"
     plan     = "standard"
     location = "us-south"
     parameters = {
         units = 2
    }
  }

  resource "ibm_iam_user_policy" "policy" {
     ibm_id = "user@ibm.com"
     roles  = ["Manager"]

     resources {
       service              = "hs-crypto"
       resource_instance_id = element(split(":", ibm_resource_instance.hpcs.id), 7)
    }
  }
  ```
  {: codeblock}

  The following table lists supported parameters when you create a service instance with Terraform:

  <table>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>units</td>
      <td>The number of operational crypto units for your service instance. Valid values are 2 and 3. If you do not specify the number, 2 crypto units are assigned by default.</td>
    </tr>
    <tr>
      <td>allowed_network</td>
      <td>The network access to your service instance. Valid values are `public and private` and `private-only`. If you do not specify the value, the default setting is `public and private`.</td>
    </tr>
    <caption>Table 1. Supported parameters for provisioning a service instance with Terraform</caption>
  </table>
3. Initialize your service instance. Before you can manage your keys, you need to initialize your service instance first by using one of the following approaches:

  - [Initializing service instances with smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities)
  - [Initializing service instances by using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)
  - [Initializing service instances by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit)

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

6. Create the {{site.data.keyword.hscrypto}} instance and IAM access policy in {{site.data.keyword.cloud_notm}} by applying Terraform.

  ```
  terraform apply
  ```
  {: pre}

7. From the [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources){: external}, select the {{site.data.keyword.hscrypto}} instance that you create and note the instance ID.
8. Verify that the access policy is successfully assigned. For more information, see [Reviewing assigned access in the console](/docs/account?topic=account-assign-access-resources#review-your-access-console).

## What's next?
{: #terraform-setup-hpcs-next}

For other task examples with Terraform such as creating keys and setting policies, see the [Terraform documentation - Key Management Service](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key). The documentation also lists the complete argument and attribute reference.
