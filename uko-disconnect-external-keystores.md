---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-01"

keywords: Unified Key Orchestrator, UKO keystore, disconnect keystore, external keystore, KMS keystore

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}





# Disconnecting from external keystores
{: #disconnect-external-keystores}


You can disconnect from keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault, Amazon Web Services (AWS) Key Management Service (KMS), and Google Cloud KMS. After you disconnect from an external keystore, all the managed keys in this keystore are unlinked and resources that are managed are not accessible.
{: shortdesc}

 
If you want to disconnect from an external keystore, delete all active keys in this keystore first. In other words, all keys with this keystore as a target are in Pre-active or Destroyed state. For more information about deleting keys, see [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys). However, if the keystore is still on the distribution list of any key templates, you can still disconnect the keystore.
{: note}


## Disconnecting from external keystores with the UI
{: #disconnect-external-keystores-ui}
{: ui}

To disconnect from an external keystore by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Keystores** from the navigation to view all the available keystores.
3. Click the keystore that you want to disconnect. The Details side panel is displayed.
4. Click **Disconnect** to disconnect the keystore and remove it from the keystore list. 
5. Click **Disconnect keystore** to confirm.

The external keystore has been disconnected with all the managed keys and key templates unlinked. You will no longer be able to access any metadata associated with the keystore. 

 
After you disconnect from an external keystore, you can reconnect to the keystores at any time. For more instructions, see [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).
{: tip}

## Disconnecting from external keystores with the API
{: #disconnect-external-keystores-api}
{: api}

To disconnect from an external keystore through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keystores in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Disconnect from an external keystore by making a `DELETE` call to the following endpoint.

    

    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/keystores/<id>
    
    ```
    {: codeblock}

    Replace `<id>` with the ID of your keystore.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#delete-keystore){: external}.



## What's next
{: #disconnect-external-keystores-next}

- To find out how to update the connection to an external keystore, check out [Editing connection to external keystores](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection).
  
- To find out instructions on adding a keystore, check out [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).

