---

copyright:
  years: 2018
lastupdated: "2018-02-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Protecting your keys

> _**Disclaimer: The {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is still in experimental phase. Therefore, this service might change anytime, including the service name, configuration steps, etc.**_

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} integrates the {{site.data.keyword.keymanagementservicefull_notm}} service to manage and secure your keys by FIPS 140-2 Level 4 certified hardware security modules (HSMs).
{:shortdesc}

## About {{site.data.keyword.keymanagementserviceshort}}
{: #key_protect}

{{site.data.keyword.keymanagementserviceshort}} generates and manages encryption keys for apps across {{site.data.keyword.cloud_notm}} services. You can create new keys for cryptography or you can import your existing keys. 

You can use different keys to encrypt different data. {{site.data.keyword.keymanagementserviceshort}} helps you manage the lifecycle of these keys. You can wrap your encryption keys with a root key, which garantee the privacy and the integrity of your encrypted data.

For more information about the {{site.data.keyword.keymanagementserviceshort}} service, see [About {{site.data.keyword.keymanagementserviceshort}} ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/keymgmt/keyprotect_about.html){:new_window}.


## How it works
{: #how_it_works}

{{site.data.keyword.hscrypto}} provisions z HSMs in {{site.data.keyword.cloud_notm}} and serves as the backend for {{site.data.keyword.keymanagementserviceshort}}. Key processing and storage happens within z HSMs, which offers higher assurance on key management. 


## Granting access between the services
{: #grant_access}

When you need to grant access between {{site.data.keyword.hscrypto}} and {{site.data.keyword.keymanagementserviceshort}} service instances, you can set authorizations by using the {{site.data.keyword.iamlong}} dashboard. Authorizations enable service to service access policies, so you can associate your storage buckets in COS with root keys provisioned in {{site.data.keyword.keymanagementserviceshort}}.

To create an authorization:

1. From the {{site.data.keyword.cloud_notm}} menu bar, click **Manage** &gt; **Account** &gt; **Identity and Access**, and then select **Authorizations**. 
2. Click **Create authorization**.
3. Select a source and target for the authorization.
    a. For **Source service**, select **{{site.data.keyword.cos_full_notm}}**.
    b. For **Target service**, select **{{site.data.keyword.keymanagementservicelong_notm}}**. 
4. To grant read-only access between the services, select the **Reader** check box.

    With _Reader_ permissions, your instance of {{site.data.keyword.cos_full_notm}} can browse the root keys that are provisioned in the specified instance of {{site.data.keyword.keymanagementserviceshort}}. During bucket creation, you can associate your bucket with a {{site.data.keyword.keymanagementserviceshort}} root key that you specify.
5. Click **Authorize**.

To learn more about service authorizations, see the [IAM documentation](/docs/iam/authorizations.html#serviceauth). 

