---

copyright:
  years: 2021, 2024
lastupdated: "2024-10-09"

keywords: create key alias, key alias, delete key alias, add key alias, retrieve encryption key by alias, create alias API examples

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Managing key aliases
{: #manage-key-alias}

You can use {{site.data.keyword.hscrypto}} to manage key aliases with the {{site.data.keyword.hscrypto}} API.
{: shortdesc}

Key aliases are unique human-readable names that can be used to identify a key. Aliases enable your service to refer to a key by recognizable custom names, rather than the auto-generated identifier provided by {{site.data.keyword.hscrypto}}. Assume that you
create a key that has the ID `02fd6835-6001-4482-a892-13bd2085f75d` and it is aliased as `US-South-Test-Key`. You can use `US-South-Test-Key` to refer to your key when you make calls to the {{site.data.keyword.hscrypto}} API to [retrieve a key](/docs/hs-crypto?topic=hs-crypto-retrieve-key).

Before you manage key alias for keys in {{site.data.keyword.hscrypto}}, keep in mind the following considerations:

- An alias is independent from a key.

    An alias is its own resource and any actions that are taken on it do not affect the associated key. For example, deleting an alias does not delete the associated key.

- An alias can be associated with only one key at a time.

    An alias can be associated with only one key that is located in the same instance and region. If you want to change the key that the alias is associated with, you need to perform the following steps:

    1. Delete the alias.
    2. Wait up to 10 minutes.
    3. Re-create the alias and map it to the key.

- You can create an alias with the same name in a different instance or region.

    Each alias is associated with a different key in each instance or region, with which, your service's application code can be reusable in different instances or regions. For example, if you name an alias `Application Key` in both the `us-south` and `us-east` regions, with each linked to a different key.

## Creating key aliases
{: #create-key-alias}

To create a key alias for a key, you can use either the UI or the key management service API.

Each key can have up to five aliases. It is limited to 1,000 aliases per instance.
{: note}

### Creating key alias with the UI
{: #create-key-alias-ui}
{: ui}

Create a key alias with the UI by completing the following steps:

1. [Log in to the UI](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. Select the **KMS keys** tab in the side menu and find the key that you want to create key aliases for.
5. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open the list of options for the key and click **Edit key aliases**.
6. Enter key aliases separated by a comma. You can add up to five aliases for a key.

    Each alias must be alphanumeric, case-sensitive, and cannot contain spaces or special characters other than dashes (-) or underscores (_). The alias cannot be a version 4 UUID and must not be a {{site.data.keyword.hscrypto}} reserved name: `allowed_ip`, `key`, `keys`, `metadata`, `policy`, `policies`, `registration`, `registrations`, `ring`, `rings`, `rotate`, `wrap`, `unwrap`, `rewrap`, `version`, `versions`. Alias size can be 2 - 90 characters (inclusive).

7. Click **Save**.

### Creating key aliases with the API
{: #create-key-alias-api}
{: api}

Create a key alias by making a `POST` call to the following endpoint.

 

```
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>/aliases/<alias>
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

   To create a key alias, you must be assigned a _Manager_ or _Writer_ service access role. To learn how IAM roles map to
   {{site.data.keyword.hscrypto}} service actions, check out [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
   {: note}

2. Create a key alias by running the following `curl` command.

    ```sh
    $ curl -X POST \
        "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>/aliases/<key_alias>" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>" \
        -H "content-type: application/vnd.ibm.kms.key+json" \
        -H "correlation-id: <correlation_ID>"
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `key_ID` | **Required.** The identifier for the key that you would like to associate with an alias. To retrieve a key ID, see the [list keys API](/docs/hs-crypto?topic=hs-crypto-view-keys#retrieve-keys-api). |
    | `key_alias` | **Required.** A unique, human-readable name for easy identification of your key. Each alias must be alphanumeric, case-sensitive, and cannot contain spaces or special characters other than dashes (-) or underscores (_). The alias cannot be a version 4 UUID and must not be a {{site.data.keyword.hscrypto}} reserved name: `allowed_ip`, `key`, `keys`, `metadata`, `policy`, `policies`, `registration`, `registrations`, `ring`, `rings`, `rotate`, `wrap`, `unwrap`, `rewrap`, `version`, `versions`. Alias size can be 2 - 90 characters (inclusive). \n \n **Note:** You cannot have duplicate alias names in your {{site.data.keyword.hscrypto}} instance. |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the `curl` request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `correlation_ID` | The unique identifier that is used to track and correlate transactions. |
    {: caption="Describes the variables needed to create a key alias with the {{site.data.keyword.hscrypto}} API" caption-side="bottom"}

    To protect the confidentiality of your personal data, avoid entering personally identifiable information (PII), such as your name or location, when you create a key alias. For more examples of PII, see section 2.2 of the [NIST Special Publication 800-122](https://www.nist.gov/publications/guide-protecting-confidentiality-personally-identifiable-information-pii){: external}.
    {: important}

    A successful `POST api/v2/keys/<key_ID>/aliases/<key_alias>` response returns the alias for your key, along with other metadata. The alias is a unique name that is assigned to your key and can be used for to retrieve more information about the associated key.

    ```json
    {
        "metadata": {
            "collectionType": "application/vnd.ibm.kms.key+json",
            "collectionTotal": 1
        },
        "resources": [
            {
                "keyId": "02fd6835-6001-4482-a892-13bd2085f75d",
                "alias": "test-alias",
                "creationDate": "2020-03-12T03:37:32Z",
                "createdBy": "..."
            }
        ]
    }
    ```
    {: screen}

    For a detailed description of the response parameters, see the {{site.data.keyword.hscrypto}} [REST API reference doc](/apidocs/hs-crypto){: external}.
    {: tip}

## Deleting key aliases
{: #delete-key-alias}

To remove a key alias for a key, you can use either the UI or the key management service API.

### Deleting key aliases with the UI
{: #delete-key-alias-ui}
{: ui}

Delete a key alias with the UI by completing the following steps:

1. [Log in to the UI](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. Select the **KMS keys** tab in the side menu and find the key that you want to create key aliases for.
5. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open the list of options for the key and click **Edit key aliases**.
6. Delete the key alias that you want to remove and click **Save**.

### Deleting key aliases with the API
{: #delete-key-alias-api}
{: api}

Delete a key alias by making a `DELETE` call to the following endpoint.

```plaintext
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>/aliases/<alias>
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
2. Delete a key alias by running the following `curl` command.

    ```sh
    $ curl -X DELETE \
        "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>/aliases/<key_alias>" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>" \
        -H "content-type: application/vnd.ibm.kms.key+json" \
        -H "correlation-id: <correlation_ID>"
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `key_ID` | **Required.** The unique identifier for the key. |
    | `key_alias` | **Required.** The unique, human-readable name that identifies your key. |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the `curl` request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `correlation_ID` | The unique identifier that is used to track and correlate transactions. |
    {: caption="Describes the variables needed to delete a key alias with the {{site.data.keyword.hscrypto}} API" caption-side="bottom"}

    A successful `DELETE api/v2/keys/<key_ID>/aliases/<key_alias>` request returns an HTTP `204 No Content` response, which indicates that the alias associated with your key was deleted.

    It takes up to 10 minutes for an alias to be deleted from the service.
    {: important}

## APIs that use key alias
{: #key-alias-apis}
{: api}

The following table lists the APIs where you can use key alias.

| API | Key Alias Impact |
| --- | ---------------- |
| [Create Root Keys.](/docs/hs-crypto?topic=hs-crypto-create-root-keys) | You can create up to five aliases while you create a root key. |
| [Create Standard Keys.](/docs/hs-crypto?topic=hs-crypto-create-standard-keys) | You can create up to five aliases while you create a standard key. |
| [Retrieve a key.](/docs/hs-crypto?topic=hs-crypto-retrieve-key) | You can retrieve a key by ID or alias. |
| [View key metadata](/docs/hs-crypto?topic=hs-crypto-view-key-details) | You can retrieve the metadata of a key by ID or alias. |
{: caption="Describes the variables that are APIs that use key alias." caption-side="top"}
