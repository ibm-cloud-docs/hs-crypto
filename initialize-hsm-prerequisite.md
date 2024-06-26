---

copyright:
  years: 2021, 2024
lastupdated: "2024-05-30"

keywords: initialize service, key ceremony, hsm, load master key, key ceremony preparation

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# Before you begin
{: #initialize-hsm-prerequisite}

Before you can initialize your service instance, make sure that you have done the following:
{: shortdesc}

1. Install the latest version of [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli){: external}.

2. Install the latest Trusted Key Entry (TKE) CLI plug-in with the following command:

    ```
    ibmcloud plugin install tke
    ```
    {: pre}

    If you have installed the TKE CLI plug-in, make sure to update your plug-in to the latest version with the following command:

    ```
    ibmcloud plugin update tke
    ```
    {: pre}

3. Set the environment variable `CLOUDTKEFILES` on your workstation to specify the directory where you want to save master key part files and signature key files. The signature keys are used to sign TKE administrative commands. Make sure that the directory exists before you set the environment variable.

    - On the [Linux]{: tag-linux} operating system or [macOS]{: tag-macos}, add the following line to the `.bash_profile` file:

        ```
        export CLOUDTKEFILES=<path>
        ```
        {: pre}

        For example, you can specify the *path* to `/Users/tke-files`.

     - On [Windows]{: tag-windows}, in **Control Panel**, type `environment variable` in the search box to locate the Environment Variables window. Create a `CLOUDTKEFILES` environment variable, set the value to the path for storing key files (For example, `C:\users\tke-files`), and restart your computer.

    The TKE_PRIVATE_ADDR environment variable is used to set the API endpoint URL both for public endpoint and private endpoint. If you want to use the public endpoint, unset the TKE_PRIVATE_ADDR environment variable or set the TKE_PRIVATE_ADDR environment variable as the public endpoint URL: `https://tke.<region>.hs-crypto.cloud.ibm.com`.
    {: important}

4. Log in to {{site.data.keyword.cloud_notm}} with the CLI with the following command:
    
    ```
    ibmcloud login
    ```
    {: pre}

    If you have multiple accounts, select the account that your service instance is created with. Make sure that you're logged in to the correct region and resource group where the service instance locates with the following command:

    ```
    ibmcloud target -r <region> -g <resource_group>
    ```
    {: pre}

    To find out the regions that {{site.data.keyword.hscrypto}} supports, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## What's next
{: #initialize-hsm-prerequisite-whats-next}

Depending on your business needs and security requirements, {{site.data.keyword.hscrypto}} provides you with three options to initialize your service instance. For detailed operation steps, see:
- [Initializing service instances by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit)
- [Initializing service instances by using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)
- [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities)
