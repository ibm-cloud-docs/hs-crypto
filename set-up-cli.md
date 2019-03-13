---

copyright:
  years: 2018
lastupdated: "2018-12-20"

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

- To find out more about using the CLI, check out the [{{site.data.keyword.keymanagementserviceshort}} CLI reference doc](/docs/services/key-protect/cli-reference.html).
- To find out about accessing the CLI, check out [Setting up the {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/services/key-protect/set-up-cli.html).

Before you are able to use the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in on a {{site.data.keyword.hscrypto}} instance, run the following command first:

```
export KP_PRIVATE_ADDR=<URL>
```
{: pre}

In this command, the *URL* is the endpoint that is displayed on the **Manage** page of the user interface. Or, you can retrieve the endpoint URL through the API. For example:

```
export KP_PRIVATE_ADDR="https://us-south.hpcs.cloud.ibm.com:<port>"
```
{: pre}

For details, [check out the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/hp-crypto){: new_window}.
