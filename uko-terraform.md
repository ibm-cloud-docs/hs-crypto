---

copyright:
  years: 2022, 2023
lastupdated: "2023-02-08"

keywords: terraform, set up terraform, automate set up

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Setting up Terraform for {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}
{: #uko-terraform-setup-for-hpcs}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multitiered cloud environments following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.hscrypto}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud_notm}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud_notm}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud_notm}} catalog.

Before you begin, make sure that you have the [required access](/docs/hs-crypto?topic=hs-crypto-uko-manage-access) to create and work with {{site.data.keyword.hscrypto}} resources.

## Example: Provisioning and initializing service instances by using Terraform
{: #uko-terraform-provision-initialize-instance-hpcs}

Complete the following steps to create and initialize a {{site.data.keyword.hscrypto}} instance by using Terraform:

1. Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform by following the [Terraform on {{site.data.keyword.cloud_notm}} getting started tutorial](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started).

    The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to provision, update, or delete {{site.data.keyword.hscrypto}} service instances and resources. The preferred Terraform versions are 0.13.x, 0.14.x, and 0.15.x. In the `versions.tf` file, you need to specify the `version` parameter to `1.29.0`.

2. Set up crypto unit administrator signature keys. You can select one of the following ways to create administrator signature keys:

    - Using the {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) CLI plug-in

      After you install and configure the TKE CLI plug-in by following [these instructions](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite), you can use the command `ibmcloud tke sigkey-add` to create administrator signature keys. The signature keys are stored in files that are protected by passwords on your local workstation. The file path is specified by the environment variable `CLOUDTKEFILES`.

    - Using a third-party signing service

      A third-party signing service can be used to create, store, and access the signature keys that are used by both the TKE CLI plug-in and Terraform. To [enable the signing service in the TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-signing-service-signature-key), you need to set the `TKE_SIGNSERV_URL` environment variable on the local workstation to the URL and port number where the signing service is running. To enable the signing service in Terraform, you need to set the `signature_server_url` parameter in the resource block to the same value.

3. Create a Terraform configuration file `main.tf` in the same folder as `versions.tf`. In this file, you add the configurations to perform the corresponding actions.

    The following template is an example configuration file to provision a {{site.data.keyword.hscrypto}} instance with 2 operational crypto units in the `us-south` region. This instance is charged according to the {{site.data.keyword.uko_full_notm}} pricing plan and is initialized with 2 administrators. The master key is automatically generated in recovery crypto units that are assigned to the instance. The signature keys are created by using the TKE CLI plug-in and stored in local protected files.

    As recovery crypto units are currently available only in the `us-south` and `us-east` regions, using Terraform to initialize {{site.data.keyword.hscrypto}} instances is supported only in these two regions. For more information about manual initialization, see [Introducing service instance initialization approaches](/docs/hs-crypto?topic=hs-crypto-uko-initialize-instance-mode).
    {: note}

    ```terraform
    resource ibm_hpcs hpcs {
       location             = "us-south"
       name                 = "test-hpcs"
       plan                 = "hpcs-hourly-uko"
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

    resource "ibm_iam_user_policy" "policy" {
       ibm_id = "user@ibm.com"
       roles  = ["Manager"]

       resources {
         service              = "test-hpcs"
         resource_instance_id = element(split(":", ibm_resource_instance.hpcs.id), 7)
       }
    }
    ```
    {: codeblock}

    In production environments, it is suggested to provide the passwords for the signature key files or the tokens for the signing service during the process of applying Terraform instead of writing it in plaintext in the configuration file. In that case, you are prompted to enter the authentication passwords or tokens when you run Terraform commands. After the instance initialization, the values that you enter for the passwords or tokens are stored in a `.tfstate` file. For more information about securing sensitive data in Terraform, see [Sensitive Data in State](https://www.terraform.io/docs/language/state/sensitive-data.html){: external}.
    {: important}

    The following table lists supported parameters when you create and initialize a service instance with Terraform:

    | Parameter | Description |
    | --- | --- |
    | `name` | **Required**. The name of your {{site.data.keyword.hscrypto}} instance. |
    | `location` | **Required**. The region abbreviation, such as `us-south`, that represents the geographic area where the operational crypto units of your service instance are located. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions). As recovery crypto units are available only in `us-south` and `us-east`, only these two regions are supported if you want to use Terraform for instance initialization. |
    | `plan` | **Required**. The pricing plan for your service instance. |
    | `units` | **Required**. The number of operational crypto units for your service instance. Valid values are 2 or 3. |
    | `failover_units` | **Not applicable**. Cross-region high availability is not currently supported for {{site.data.keyword.uko_full_notm}}. |
    | `service_endpoints` | **Not applicable**. The default setting is `public-and-private`. |
    | `tags` | **Optional**. Tags that are associated with your instance are used to organize your resources. For more information about tags, see [Working with tags](/docs/account?topic=account-tag). |
    | `resource_group_id` | **Optional**. The resource group where you want to organize and manage your service instance. If you do not specify the value, the default resource group is `Default`. |
    | `signature_threshold` | **Required**. The number of administrator signatures that is required to execute administrative commands. The valid value is in the range 1 - 8. You need to set it to at least 2 to enable quorum authentication. |
    | `revocation_threshold` | **Required**. The number of administrator signatures that is required to remove an administrator after you leave imprint mode. The valid value is in the range 1 - 8. |
    | `admins` | **Required**. The list of administrators for the instance crypto units. You can set up to eight administrators and the number needs to be equal to or greater than the thresholds that you specify. The following values need to be set for each administrator: \n \n **name:** \n The name of the administrator. It needs to be no more than 30 characters in length. \n \n **key:** \n * If you are using signature key files on the local workstation that are created by the TKE CLI plug-in and are not using a third-party signing service, specify the absolute path and file name of the signature key file that is to be used. \n * If you are using a signing service to provide signature keys, specify the name of the signature key depending on the signing service definition. The character string for the key name is appended to a URI that is sent to the signing service and must contain only unreserved characters as defined by section 2.3 of [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986). \n \n **token:** \n * If you are using signature key files on the local workstation that are created by the TKE CLI plug-in and are not using a third-party signing service, specify the administrator password to access the corresponding signature key file. \n * If you are using a signing service to provide signature keys, specify the token that authorizes use of the signature key depending on the signing service definition. \n \n **Note:** The token parameter is optional. If you don't specify the token, you are prompted to enter the token value when you run Terraform commands. After the instance initialization, the value that you enter for the token parameter is stored in a `.tfstate` file. For more information about securing sensitive data in Terraform, see [Sensitive Data in State](https://www.terraform.io/docs/language/state/sensitive-data.html). |
    | `signature_server_url` | **Optional**. The URL and port number where the signing service is running. If you are using a third-party signing service to provide administrator signature keys, you need to specify this parameter. |
    {: caption="Table 1. Supported parameters for provisioning a service instance with Terraform" caption-side="bottom"}

    If you manage multiple service instances in the `main.tf` file, make sure to set the same `signature_server_url` parameter for each instance. Otherwise, you will not be able to perform the actions successfully.
    {: important}

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
{: #uko-terraform-setup-hpcs-next}

For more information about using Terraform to manage {{site.data.keyword.hscrypto}} instances with {{site.data.keyword.uko_full_notm}}, see the following Terraform documentation:

- [Managing keys](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/hpcs_managed_key){: external}
- [Managing keystores](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/hpcs_keystore){: external}
- [Managing key templates](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/hpcs_key_template){: external}
- [Managing vaults](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/hpcs_vault){: external}



