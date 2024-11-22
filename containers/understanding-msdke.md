

# Understanding Microsoft Double Key Encryption services
{: #understanding-msdke}

What is Double Key Encryption (DKE)? As the name suggests, DKE enables customers to protect their data with two keys. In order to access the ocntent, you need to have access to both keys. One of the keys is in the customer's control while the other key resies in Microsoft Azure.  

It enables administrators to enable a consistent labeling experience across their entire data state. By using DKE, customers prevent any third party access to their content. Microsoft never has access to their data either, since one of the keys always stays under the control of the customer. You can configure {{site.data.keyword.uko_full_notm}} to provide this DKE encryption service to manage user acces to your key and DKE-encrypted content. 

## Encryption/ Decryption Workflow
{: #understanding-msdke-overview}

Content is encrypted with an individual symmetric key on a per-document basis. This symmetric key is placed in the metadata of the document and first encrypted with a key from the DKE encryption service and after that wrapped again with an Azure Information Protection key. 

For decryption, the Microsoft Office clients will first send the metadata portion of that file to the Azure Information Protection service and then to the DKE Encryption service to retrieve the symmetric key and be able to decrypt the document. For a detailed description of the DKE encryption workflow, refer to [Microsoft DKE documentation](https://learn.microsoft.com/en-us/purview/double-key-encryption#dke-encryption-workflow).

## Startup and configuration
{: #understanding-msdke-startup}

During startup of the service, each MSDKE HTTP Service gets its configuration from the  MSDKE Crypto Service. The one crypto service, that is connected th the MSDKE keystore, will get its information from the connected database. 

![MSDKE startup](../images/msdke-startup.png "Startup of the MSDKE service"){: caption="Startup of the MSDKE service"}

Afterwards, the following configurations are in place: 

![MSDKE configuration](../images/msdke-configuration.png "Configuration of the MSDKE service"){: caption="Configuration of the MSDKE service"}

## Key creation in {{site.data.keyword.uko_short}} 
{: #understanding-msdke-key-creation}

Before MSDKE keys can be created, an RSA KEK must be available. This key is created in {{site.data.keyword.uko_short}} and in addition to the {{site.data.keyword.uko_short}} repository, it gets distributed to all the local keystores where the MSDKE Crypto service is running. The name of this key is specified in the {{site.data.keyword.uko_short}} configuration. 

![RSA KEK installation](../images/msdke-kek-creation.png "Creation of the RSA KEK"){: caption="Creation of the RSA KEK"}

Afterwards, an MSDKE key can be created, which involves the following events: 
* The key is stored in both, in the local UKO repository as well as the local MSDKE keystore. 
* {{site.data.keyword.uko_short}} publishes the key to the MSDKE HTTP Service (via rabbitMQ)
* Each MSDKE Crypto Service verifies the key by executing the following steps: 
    * Unwrap the key using the RSA KEK
    * Encrypt random plain text
    * Decrypt cipher text
    * Compare to plain text

Note: At least one of the MSDKE Crypto services needs read access to the MSDKE keystore. 

![MSDKE key installation](../images/msdke-key-creation.png "Creation of the MSDKE key"){: caption="Creation of the MSDKE key"}

## Encryption
{: #understanding-msdke-encrypt}

1. Office user gets list of sensitivity labels and the MSDKE label URL from Microsoft
2. Office user gets the public key from msdke-http-service HTTP Handler
3. msdke-http-service HTTP Handler gets public key by name using Queue from Queueing Mechanism (RabbitMQ)
4. msdke-crypto-service Crypto Handler responds to RabbitMQ to get public key by name, return public key and key ID

![Encryption](../images/msdke-encrypt.png "Encryption"){: caption="Encryption"}

## Decryption
{: #understanding-msdke-decrypt}

1. Office user Decrypt using stored key ID URL to msdke-http-service HTTP Handler
2. Handler sends Decrypt using specific key ID request to rabbit
3. msdke-crypto-service Validate access based on user's JWT and local configuration
4. msdke-crypto-service Decrypt using key from configuration
5. msdke-crypto-service Respond with decrypted data
6. msdke-crypto-service Integrate the updated configuration into local Config Update Queue

![Decryption](../images/msdke-decrypt.png "Decryption"){: caption="Decryption"}
