---

copyright:
  years: 2018
lastupdated: "2018-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Protecting your keys

***NOTE: Need to verify whether this topic is still needed in Beta. ***

You can bind {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} and the {{site.data.keyword.keymanagementservicefull_notm}} to manage and protect your keys with hardware security modules (HSMs) using FIPS 140-2 Level 4 certified technology.
{:shortdesc}

## About {{site.data.keyword.keymanagementserviceshort}}
{: #key_protect}

{{site.data.keyword.keymanagementserviceshort}} generates and manages encryption keys for apps across {{site.data.keyword.cloud_notm}} services. You can create new keys for cryptography or you can import your existing keys.

You can use different keys to encrypt different data. {{site.data.keyword.keymanagementserviceshort}} helps you manage the lifecycle of these keys. You can wrap your encryption keys with a root key, which guarantees the privacy and the integrity of your encrypted data.

For more information about the {{site.data.keyword.keymanagementserviceshort}} service, see [About {{site.data.keyword.keymanagementserviceshort}} ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/keymgmt/keyprotect_about.html){:new_window}.


## How it works
{: #how_it_works}

{{site.data.keyword.hscrypto}} provisions z HSMs in {{site.data.keyword.cloud_notm}} and serves as the key store for {{site.data.keyword.keymanagementserviceshort}}. Key processing and storage happens within z HSMs, which offers higher assurance on key management.

The following list describes the basic steps to set up the hyper protected environment for your keys with {{site.data.keyword.hscrypto}} and {{site.data.keyword.keymanagementserviceshort}} services.

1. Provision an instance of {{site.data.keyword.hscrypto}}. For more information, see [Provisioning a {{site.data.keyword.hscrypto}} instance](index.html#provision).
2. Retrieve the instance ID of your {{site.data.keyword.hscrypto}} instance with the [bluemix resource service-instance ![External link icon](image/external_link.svg "External link icon")](){:new_window} command.
3. Retrieve connection information of your {{site.data.keyword.hscrypto}} instance by calling the {{site.data.keyword.hscrypto}} API with the instance ID and your IAM token.  For example:
    ```cURL
    curl -X GET \
        https://hpcs.cloud.ibm.com/crypto_v1/instances/<instance_ID> \
        -H 'Authorization: <IAM_token>' \
    ```
    {: codeblock}
4. Provision an instance of {{site.data.keyword.keymanagementserviceshort}} with the connection information. For more information, see [Provisioning a {{site.data.keyword.keymanagementserviceshort}} instance ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/keymgmt/keyprotect_provision.html){:new_window}.
5. Grant access between the two service instances with Identity and Access Management (IAM). For more information, see [Granting access between services ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/iam/authorizations.html){:new_window}.

<!--
You need to provision instances for both {{site.data.keyword.hscrypto}} and {{site.data.keyword.keymanagementserviceshort}} services. For more information, see [Provisioning a {{site.data.keyword.hscrypto}} instance](overview.html#provision) and [Provisioning a {{site.data.keyword.keymanagementserviceshort}} instance](https://console.bluemix.net/docs/services/keymgmt/keyprotect_provision.html).
After you have both service instances, grant access between them.  When you need to grant access between {{site.data.keyword.hscrypto}} and {{site.data.keyword.keymanagementserviceshort}} service instances, you can set authorizations by using the {{site.data.keyword.iamlong}} dashboard. Authorizations enable service to service access policies, so you can associate your storage buckets in COS with root keys provisioned in {{site.data.keyword.keymanagementserviceshort}}.
Complete the following steps to create an authorization:
1. From the {{site.data.keyword.cloud_notm}} menu bar, click **Manage** &gt; **Account** &gt; **Identity and Access**, and then select **Authorizations**.
2. Click **Create authorization**.
3. Select a source and target for the authorization.
    a. For **Source service**, select **{{site.data.keyword.keymanagementservicelong_notm}}**.
    b. For **Target service**, select **{{site.data.keyword.hscrypto}}**.
4. To grant read-only access between the services, select the **Reader** check box.
    With _Reader_ permissions, your instance of {{site.data.keyword.keymanagementservicelong_notm}} can browse the root keys that are provisioned in the specified instance of {{site.data.keyword.hscrypto}}. During bucket creation, you can associate your bucket with a {{site.data.keyword.hscrypto}} root key that you specify.
5. Click **Authorize**.
To learn more about service authorizations, see the [IAM documentation](/docs/iam/authorizations.html#serviceauth).
-->
