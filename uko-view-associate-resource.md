---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-29"

keywords: associate resource, key associated resource

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Viewing resources associated with managed keys
{: #uko-view-associated-resource}

You can view other {{site.data.keyword.cloud}} resources that are protected by managed keys with [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) by using the UI, or programmatically with the {{site.data.keyword.uko_full_notm}}.
{: shortdesc}


Currently, envelope encryption applies to IBM Cloud KMS keys and IBM Key Protect keys. Therefore, you can view resources that are associated with these keys only.
{: note}

## Viewing associated resources with the UI
{: #uko-view-associated-resource-ui}
{: ui}

To view the associated resources by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the key that you want to view, and choose **Show details**.
4. Click the **Associated resources** tab to view the details of resources that are protected by this key. 
    
    |       Column	     |                         Description                       |
    |--------------------|-----------------------------------------------------------|
    | Resource name      | The name of the cloud resource that is associated with the key.|
    | Service name       | The name of the cloud service, such as `cloud-object-storage` for {{site.data.keyword.cos_full_notm}}. |
    | Retention policy   | Indicates whether the cloud resource can be erased. If the value is `Enabled`, the cloud resource cannot be erased, and the key that is associated with the cloud resource cannot be deleted. If the value is `Disabled`, the cloud resource can be erased. You can delete the key that is associated with the cloud resource if needed. |
    {: caption="Associated resources properties" caption-side="bottom"} 

## Viewing associated resources with the API
{: #uko-view-associated-resource-api}
{: api}

To view the associated resources through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. View the associated resources by making a `GET` call to the following endpoint.

    

    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/managed_keys/{id}/associated_resources
    
    ```
    {: codeblock}

    Replace `<id>` with the ID of your managed key.

3. If you want to view the resources that are associated with all keys in a keystore, make a `GET` call to the following endpoint.

    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/keystores/{id}/associated_resources
    
    ```
    {: codeblock}

    Replace `<id>` with the ID of the keystore.

For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko){: external}. 


## What's next
{: #uko-view-associated-resource-next}

- For more information about envelope encryption, see [Protecting your data with envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).
- For a list of cloud services that supports envelope encryption, see [Integrating {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-integrate-services). 
