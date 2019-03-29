---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: IBM Cloud CLI plug-in, ibmcloud commands, IBM Cloud command-line interface

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Accessing {{site.data.keyword.keymanagementserviceshort}} CLI on a {{site.data.keyword.hscrypto}} instance
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is integrated with {{site.data.keyword.keymanagementservicelong_notm}} CLI plug-in, so that you can use the {{site.data.keyword.keymanagementservicelong_notm}} CLI plug-in to create, import, and manage encryption root keys and standard keys.

Before you are able to use the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in on a {{site.data.keyword.hscrypto}} instance (service instance for short), you need to set the KP_KP_PRIVATE_ADDR environment variable on you workstation:

* On Linux or MacOS, run the following command:

  ```
  export KP_PRIVATE_ADDR=<URL>
  ```
  {: pre}

  In this command, the *URL* is the endpoint that is displayed on the **Manage** tab of your provisioned {{site.data.keyword.hscrypto}} dashboard. For example:

  ```
  export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
  ```
  {: pre}

* On Windows, in **Control Panel**, type `environment variable` in the search box to locate the Environment Variables window. Create a KP_PRIVATE_ADDR environment variable and set the value to the endpoint that is displayed on the **Manage** tab of your provisioned {{site.data.keyword.hscrypto}} dashboard. For example, `https://us-south.hs-crypto.cloud.ibm.com:<port>`.

You can also retrieve the endpoint URL through the API. For details, [check out the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

- To find out more about using the CLI, check out the [{{site.data.keyword.keymanagementserviceshort}} CLI reference doc](/docs/services/key-protect/cli-reference.html).
- To find out about accessing the CLI, check out [Setting up the {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/services/key-protect/set-up-cli.html).
