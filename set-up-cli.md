---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-06"

keywords: ibmcloud cli, hpcs cli, ibmcloud commands, ibm cloud command-line interface, key protect cli, kms cli

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}

# Performing key management operations with the command-line interface
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is integrated with {{site.data.keyword.keymanagementservicelong_notm}} CLI plug-in, so that you can use the {{site.data.keyword.keymanagementservicelong_notm}} CLI plug-in to create, import, and manage encryption [root keys](#x6946961){: term} and standard keys.
{: shortdesc}

Before you use the {{site.data.keyword.keymanagementserviceshort}} CLI through a {{site.data.keyword.hscrypto}} instance (service instance for short), you need to perform the following steps:

1. Install the [{{site.data.keyword.keymanagementservicelong_notm}} CLI plug-in](/docs/key-protect?topic=key-protect-set-up-cli#install-cli).

2. Set the KP_PRIVATE_ADDR environment variable on your workstation:

  * On the Linux&reg; operating system or MacOS, run the following command:

    ```
    export KP_PRIVATE_ADDR=<URL>
    ```
    {: pre}

    In this command, the *URL* is the key management endpoint URL that is displayed on the **Manage** tab of your provisioned {{site.data.keyword.hscrypto}} dashboard. For example:

    ```
    export KP_PRIVATE_ADDR="https://api.us-south.hs-crypto.cloud.ibm.com:<port>"
    ```
    {: pre}

    To find out the regions that {{site.data.keyword.hscrypto}} supports, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

  * On the Windows&reg; operating system, in **Control Panel**, type `environment variable` in the search box to locate the Environment Variables window. Create a KP_PRIVATE_ADDR environment variable and set the value to the endpoint that is displayed on the **Manage** tab of your provisioned {{site.data.keyword.hscrypto}} dashboard. For example, `https://api.us-south.hs-crypto.cloud.ibm.com:<port>`.

  You can also retrieve the endpoint URL through the API. For details, [check out the {{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.

  Depending on whether you are using public or private endpoint, choose the corresponding endpoint URL to set the value of the KP_PRIVATE_ADDR environment variable.
  {: important}

3. Set the KP_INSTANCE_ID environment variable on your workstation:

  * On the Linux operating system or MacOS, run the following command:

    ```
    export KP_INSTANCE_ID=<instance_ID>
    ```
    {: pre}

    In this command, the *instance_ID* is displayed on the **Manage** tab of your provisioned {{site.data.keyword.hscrypto}} dashboard. *instance_ID* is in a Universally Unique Identifier (UUID) format.

  * On Windows, in **Control Panel**, type `environment variable` in the search box to locate the Environment Variables window. Create a KP_INSTANCE_ID environment variable and set the value to the instance ID value that is displayed on the **Manage** tab of your provisioned {{site.data.keyword.hscrypto}} dashboard.

  Alternatively, you can use the `-i <instance_ID>` option on the `ibmcloud kp` command to set the instance ID.

4. Run the specific command to perform key management operations. For the full list of commands, check out the [key management CLI reference](/docs/key-protect?topic=key-protect-cli-reference).

5. [Upgrade the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in](/docs/key-protect?topic=key-protect-set-up-cli#update-cli) to the newest version to enable new features.

6. (Optional) If you don't need the plug-in any more, you can [uninstall the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in](/docs/key-protect?topic=key-protect-set-up-cli#uninstall-cli).

## What's next
{: #cli-next-steps}

- You can also perform key management operations with API calls, check out [Managing your keys with the key management API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
- Learn how to perform cryptographic operations with Enterprise PKCS #11 (EP11) APIs over gRPC (GREP11), refer to [Performing cryptographic operations with the GREP11 API](/docs/hs-crypto?topic=hs-crypto-set-up-grep11-api).
