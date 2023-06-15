---

copyright:
  years: 2018, 2023
lastupdated: "2023-06-15"

keywords: ibmcloud cli, hpcs cli, ibmcloud commands, ibm cloud command-line interface, key protect cli, kms cli

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}

# Performing key management operations with the CLI - Standard Plan only
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} Standard Plan is integrated with {{site.data.keyword.keymanagementservicelong_notm}} command-line interface (CLI) plug-in, so that you can use the {{site.data.keyword.keymanagementservicelong_notm}} CLI plug-in to create, import, and manage encryption [root keys](#x6946961){: term} and standard keys.
{: shortdesc}

Currently, performing key management operations with the CLI is only supported with the Standard Plan. You can still perform key management operations for the {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} through the UI or API. 
{: note}

Before you use the {{site.data.keyword.keymanagementserviceshort}} CLI through a {{site.data.keyword.hscrypto}} instance (service instance for short), you need to perform the following steps:

1. Install the [{{site.data.keyword.keymanagementservicelong_notm}} CLI plug-in](/docs/key-protect?topic=key-protect-set-up-cli#install-cli).

2. Set the KP_PRIVATE_ADDR environment variable on your workstation:

    - On the [Linux]{: tag-linux} operating system or [macOS]{: tag-macos}, run the following command:

      ```
      export KP_PRIVATE_ADDR=<URL>
      ```
      {: pre}

      In this command, the *URL* is the `Key management endpoint URL`. You can get the endpoint from your provisioned service instance dashboard through **Overview** &gt; **Connect** &gt; **Key management endpoint URL**. Or, you can dynamically [retrieve the API endpoint URL](/apidocs/hs-crypto#getinstance){: external} with an API call. For example:

      ```
      export KP_PRIVATE_ADDR="https://api.us-south.hs-crypto.cloud.ibm.com:<port>"
      ```
      {: pre}

      To find out the regions that {{site.data.keyword.hscrypto}} supports, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

    - On the [Windows]{: tag-windows} operating system, in **Control Panel**, type `environment variable` in the search box to locate the Environment Variables window. Create a KP_PRIVATE_ADDR environment variable and set the value to the endpoint that is displayed on the **Manage** tab of your provisioned {{site.data.keyword.cloud_notm}} console. For example, `https://api.us-south.hs-crypto.cloud.ibm.com:<port>`.

    You can also retrieve the endpoint URL through the API. For details, [check out the {{site.data.keyword.hscrypto}} key management service API reference doc](/apidocs/hs-crypto){: external}.

    Depending on whether you are using public or private endpoint, choose the corresponding endpoint URL to set the value of the KP_PRIVATE_ADDR environment variable.
    {: important}

3. Set the KP_INSTANCE_ID environment variable on your workstation:

    - On the [Linux]{: tag-linux} operating system or [macOS]{: tag-macos}, run the following command:

      ```
      export KP_INSTANCE_ID=<instance_ID>
      ```
      {: pre}

      In this command, the *instance_ID* is displayed on the **Manage** tab of your provisioned {{site.data.keyword.cloud_notm}} console. *instance_ID* is in a Universally Unique Identifier (UUID) format.

    - On [Windows]{: tag-windows}, in **Control Panel**, type `environment variable` in the search box to locate the Environment Variables window. Create a KP_INSTANCE_ID environment variable and set the value to the instance ID value that is displayed on the **Manage** tab of your provisioned {{site.data.keyword.hscrypto}} dashboard.

    Alternatively, you can use the `-i <instance_ID>` option on the `ibmcloud kp` command to set the instance ID.

4. Run the specific command to perform key management operations. For the full list of commands, check out the [key management CLI reference](/docs/key-protect?topic=key-protect-cli-plugin-key-protect-cli-reference).

5. [Upgrade the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in](/docs/key-protect?topic=key-protect-set-up-cli#update-cli) to the newest version to enable new features.

6. (Optional) If you don't need the plug-in any more, you can [uninstall the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in](/docs/key-protect?topic=key-protect-set-up-cli#uninstall-cli).

## What's next
{: #cli-next-steps}

- You can also perform key management operations with API calls, check out [Managing your keys with the key management service API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
- To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
