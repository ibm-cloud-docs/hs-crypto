---

copyright:
  years: 2018
lastupdated: "2018-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Protecting your keys

> _**Disclaimer: {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is still in experimental phase and it might change at anytime.**_

You can binds {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} and the {{site.data.keyword.keymanagementservicefull_notm}} to manage and secure your keys by FIPS 140-2 Level 4 certified hardware security modules (HSMs).
{:shortdesc}

## About {{site.data.keyword.keymanagementserviceshort}}
{: #key_protect}

{{site.data.keyword.keymanagementserviceshort}} generates and manages encryption keys for apps across {{site.data.keyword.cloud_notm}} services. You can create new keys for cryptography or you can import your existing keys.

You can use different keys to encrypt different data. {{site.data.keyword.keymanagementserviceshort}} helps you manage the lifecycle of these keys. You can wrap your encryption keys with a root key, which guarantees the privacy and the integrity of your encrypted data.

For more information about the {{site.data.keyword.keymanagementserviceshort}} service, see [About {{site.data.keyword.keymanagementserviceshort}} ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/keymgmt/keyprotect_about.html){:new_window}.


## How it works
{: #how_it_works}

{{site.data.keyword.hscrypto}} provisions z HSMs in {{site.data.keyword.cloud_notm}} and serves as the key store for {{site.data.keyword.keymanagementserviceshort}}. Key processing and storage happens within z HSMs, which offers higher assurance on key management.

The following list describes the basic steps to set up the hyper secure evironment for your keys with {{site.data.keyword.hscrypto}} and {{site.data.keyword.keymanagementserviceshort}} services.

1. Provision an instance of {{site.data.keyword.hscrypto}}. For more information, see [Provisioning a {{site.data.keyword.hscrypto}} instance](overview.html#provision).
2. Retrieve the instance ID of your {{site.data.keyword.hscrypto}} instance with the [bluemix resource service-instance ![External link icon](image/external_link.svg "External link icon")](){:new_window} command.
3. Retrieve connection information of your {{site.data.keyword.hscrypto}} instance by calling the {{site.data.keyword.hscrypto}} API with the instance ID and your IAM token.  For example:
    
    ```cURL
    curl -X GET \
        https://zcryptobroker.bluemix.net/crypto_v1/instances/<instance_ID> \
        -H 'Authorization: <IAM_token>' \
    ```
    {: codeblock}
4. Provision an instance of {{site.data.keyword.keymanagementserviceshort}} with the connection information. For more information, see [Provisioning a {{site.data.keyword.keymanagementserviceshort}} instance ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/keymgmt/keyprotect_provision.html){:new_window}.
5. Grant access between the two service instances with Identity and Access Management (IAM). For more information, see [Granting access between services ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/iam/authorizations.html){:new_window}.

