---

copyright:
  years: 2020, 2024
lastupdated: "2024-02-27"

keywords: key registration, register resources, service integration, protected resource, view crn, registraion api

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# Registering protected resources
{: #register-protected-resources}

Before you protect a data encryption key (DEK) with a root key, register the cloud resource with {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

When you register cloud resources with {{site.data.keyword.hscrypto}}, {{site.data.keyword.cloud_notm}} customers can:

- View how root keys map to resources across the cloud
- Understand which cloud resources are protected by root keys
- Determine the risk that is involved with destroying a root key
- Evaluate the affected range if a key becomes compromised

## Planning for registration
{: #plan-for-registration}

Registering new resources
:   When your customers create a new resource, such as a {{site.data.keyword.cos_full_notm}} bucket, they can choose to encrypt the resource with an existing root key. At resource creation, your service must [create a registration](#create-registration) between the new resource and the {{site.data.keyword.hscrypto}} key.

Registering existing resources
:   If your service is already integrated with {{site.data.keyword.hscrypto}} for enhanced security, your service must [register existing resources](#register-existing-resources) retroactively. When your service registers all existing resources, customers can see a full view of the cloud resources that are already protected by {{site.data.keyword.hscrypto}} keys.


## Registering new resources
{: #register-new-resources}

As an integrated service, you can call the registration API methods to create, replace, update, and delete registrations between a resource and a root key. The following table shows the API methods that are available for creating and modifying registrations.

| API methods | Description |
| --- | --- |
| `POST /api/v2/keys/{id}/registrations/{url_encoded_crn}` | [Create a registration](/apidocs/hs-crypto#createregistration){: external} |
| `PUT /api/v2/keys/{id}/registrations/{url_encoded_crn}` | [Replace a registration](/apidocs/hs-crypto#replaceregistration){: external} |
| `PATCH /api/v2/keys/{id}/registrations/{url_encoded_crn}` | [Update a registration](/apidocs/hs-crypto#updateregistration){: external} |
| `DELETE /api/v2/keys/{id}/registrations/{url_encoded_crn}` | [Delete a registration](/apidocs/hs-crypto#deleteregistration){: external} |
{: caption="Table 1. Lists API methods for creating and modifying registrations" caption-side="bottom"}

### Creating a registration
{: #create-registration}

To associate a resource to a root key, make a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/registrations/<url_encoded_CRN>
```

**Example request**

```cURL
curl -X POST \
  https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/registrations/<url_encoded_CRN> \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'content-type: application/json' \
  -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.registration_input+json",
      "collectionTotal": 1
    },
    "resources":[
      {
        "description": "<external_description>",
        "registrationMetadata": <internal_metadata>,
        "preventKeyDeletion": <true|false>
      }
    ]
  }'
```
{: codeblock}

Replace the variables in the example request according to the following table.

| Variable | Description |
| -------- | ----------- |
| `region` | **Required.** The region abbreviation, such as `us-south`, that represents the geographic area where the {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Service regions and locations](/docs/hs-crypto?topic=hs-crypto-regions). |
| `port`   | **Required.** The port number of the API endpoint.  |
| `key_ID` | **Required.** The unique identifier for the customer's root key that protects the cloud resource. |
| `url_encoded_CRN` | **Required.** The URL encoded [Cloud Resource Name (CRN)](/docs/account?topic=account-crn) that uniquely identifies the cloud resource. At minimum, provide a CRN that includes up to the `service-instance` segment. |
| `CRN_token` | **Required.** Your [service's CRN token](/docs/get-coding?topic=get-coding-servicetoservice#create_crn_token). Include the full contents of the token, including the Bearer value, in the cURL request. |
| `instance_ID` | **Required.** The unique identifier that is assigned to customer's {{site.data.keyword.hscrypto}} service instance.
| `description` | A meaningful description in the context of your cloud service that describes the resource that is being protected by the root key. This field is exposed to customers when they use {{site.data.keyword.hscrypto}} to review registered resources.|
| `registrationMetadata` | A text field that cloud services can use to store internal metadata about the registration. This field is not exposed to customers and is visible only by using {{site.data.keyword.cloud_notm}} service to service calls. |
| `preventKeyDeletion` | A boolean that determines whether {{site.data.keyword.hscrypto}} must prevent deletion of a root key due to a Write Once Read Many (WORM) policy set on the customer resource. \n \n If set to `true`, {{site.data.keyword.hscrypto}} prevents deletion of the root key and the associated protected resources. The system prevents the deletion of any key that has at least one registration where `preventKeyDeletion` is `true`.|
{: caption="Table 2. Lists variables for the API method to create a registration" caption-side="bottom"}

### Updating the registration
{: #update-registration}

To modify a registration, make a `PATCH` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/registrations/<url_encoded_CRN>
```

**Example request**

```cURL
curl -X PATCH \
  https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/registrations/<url_encoded_CRN> \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'content-type: application/json' \
  -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.registration_input+json",
      "collectionTotal": 1
    },
    "resources":[
      {
        "description": "<external_description>",
        "registrationMetadata": <internal_metadata>,
        "preventKeyDeletion": <true|false>
      }
    ]
  }'
```
{: codeblock}

Replace the variables in the example request according to the following table.

| Variable | Description |
| -------- | ----------- |
| `region` | **Required.** The region abbreviation, such as `us-south`, that represents the geographic area where the {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Service regions and locations](/docs/hs-crypto?topic=hs-crypto-regions). |
| `port`   | **Required.** The port number of the API endpoint.  |
| `key_ID` | **Required.** The unique identifier for the customer's root key that protects the cloud resource. |
| `url_encoded_CRN` | **Required.** The URL encoded [Cloud Resource Name (CRN)](/docs/account?topic=account-crn) that uniquely identifies the cloud resource. At minimum, provide a CRN that includes up to the `service-instance` segment. |
| `CRN_token` | **Required.** Your [service's CRN token](/docs/get-coding?topic=get-coding-servicetoservice#create_crn_token). Include the full contents of the token, including the Bearer value, in the cURL request. |
| `instance_ID` | **Required.** The unique identifier that is assigned to customer's {{site.data.keyword.hscrypto}} service instance.
| `description` | A meaningful description in the context of your cloud service that describes the resource that is being protected by the root key. This field is exposed to customers when they use {{site.data.keyword.hscrypto}} to review registered resources.|
| `registrationMetadata` | A text field that cloud services can use to store internal metadata about the registration. This field is not exposed to customers and is visible only by using {{site.data.keyword.cloud_notm}} service to service calls. |
| `preventKeyDeletion` | A boolean that determines whether {{site.data.keyword.hscrypto}} must prevent deletion of a root key due to a Write Once Read Many (WORM) policy set on the customer resource. \n \n If set to `true`, {{site.data.keyword.hscrypto}} prevents deletion of the root key and the associated protected resources. The system prevents the deletion of any key that has at least one registration where `preventKeyDeletion` is `true`.|
{: caption="Table 3. Lists variables for the API method to update a registration" caption-side="bottom"}

### Deleting the registration
{: #delete-registration}

After a resource is no longer within the cloud or protected by a root key, unregister the association with the key.

**Example request**

```cURL
curl -X DELETE \
  https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/registrations/<url_encoded_CRN> \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>'
```
{: codeblock}

Replace the variables in the example request according to the following table.

| Variable | Description |
| -------- | ----------- |
| `region` | **Required.** The region abbreviation, such as `us-south`, that represents the geographic area where the {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Service regions and locations](/docs/hs-crypto?topic=hs-crypto-regions). |
| `port`   | **Required.** The port number of the API endpoint.  |
| `key_ID` | **Required.** The unique identifier for the customer's root key that protects the cloud resource. |
| `url_encoded_CRN` | **Required.** The URL encoded [Cloud Resource Name (CRN)](/docs/account?topic=account-crn) that uniquely identifies the cloud resource. At minimum, provide a CRN that includes the `service-instance` segment. |
{: caption="Table 4. Lists variables for the API method to delete a registration" caption-side="bottom"}

## Registering existing resources
{: #register-existing-resources}

If your service has resources that are already protected by a root key, you need to create registrations for these resources retroactively.

### Identifying your protected resources
{: #identify-protected-resources}

Your service might have a place that stores root key IDs in some metadata that associates your resource to the data. Identify all the affected resources and gather the following information:

- The Cloud Resource Name (CRN) of the resource that is protected (for example, a Cloud Object Storage bucket, or a Kubernetes Service cluster).
- The description of the protected resource using a string provided by the customer that is meaningful in the context of your service. Maybe that is the description, the name, or an ID, but provide that string so that when your customer sees it, they can quickly understand what it means.
- Information about the root key, which can be found in the root key's CRN
    - The {{site.data.keyword.hscrypto}} instance GUID that contains the root key
    - The root key ID

### Creating a registration for each protected resource
{: #create-registration-existing-resource}

After your service has identified each protected resource, call the API method to [create a registration](#create-registration) for each resource.

## Retrieving Registered Resources
{: #view-registered-resources}

After you register a cloud service with {{site.data.keyword.hscrypto}}, use the {{site.data.keyword.hscrypto}} registration API methods to view the association between your cloud resource and a root key.

The following table shows the API methods that are available for listing registrations.

| API Method                            | Description                                                                                      |
|---------------------------------------|------------------------------------------------------- |
| `GET /api/v2/keys/{id}/registrations` | [List registrations for a key](/apidocs/hs-crypto#getregistrations){: external}     |
| `GET /api/v2/keys/registrations`      | [List registrations for any key](/apidocs/hs-crypto#getregistrationsallkeys){: external} |
{: caption="Table 5. Lists API methods for listing registrations" caption-side="bottom"}

### Viewing CRNs associated with a registration
{: #view-protected-resource-crn}

After your cloud resource is associated with one registration, you can view the resource CRNs by calling the API methods that are listed in Table 5. The following example shows the CRN format that uniquely identifies registrations:

| Service | CRN Format | Example |
|---------|------------|---------|
| {{site.data.keyword.cos_full_notm}} | `crn:version:cname:ctype:service-name:location:scope:service-instance:bucket:bucketname` | `crn:v1:bluemix:public:cloud-object-storage:global:a/59bcbfa6ea2f006b4ed7094c1a08dcff:76b98bfd-f730-47b8-b163-515187bbbbbb:bucket:mybucket` |
{: caption="Table 6. Lists an example of resource CRNs" caption-side="bottom"}



## Key states and service actions on a registration
{: #key-states-service-actions-registrations}

Key states affect whether an action that is performed on a registration succeeds or fails. For example, if a key is in the Destroyed state, registrations cannot be created with the key because it is previously deleted.

The following table shows how {{site.data.keyword.hscrypto}} handles service actions for registration based on the state of a key. The column headers represent the key states and the row headers represent the actions that you can perform on a registration. The **Checkmark** icon ![checkmark icon](../../icons/checkmark-icon.svg "Checkmark") indicates that the action on a registration is expected to succeed based on the key state.

| Action | Active | Suspended | Deactivated | Destroyed |
| --- | --- | --- | --- | --- |
| Create Registration  | ![Checkmark icon](../../icons/checkmark-icon.svg "Checkmark")  |   |   |   |
| Replace Registration | ![Checkmark icon](../../icons/checkmark-icon.svg "Checkmark")  |   |   |   |
| Update Registration  | ![Checkmark icon](../../icons/checkmark-icon.svg "Checkmark")  |   |   |   |
| Delete Registration  | ![Checkmark icon](../../icons/checkmark-icon.svg "Checkmark")  | ![Checkmark icon](../../icons/checkmark-icon.svg "Checkmark") |   |   |
| Get Registration  | ![Checkmark icon](../../icons/checkmark-icon.svg "Checkmark")  | ![Checkmark icon](../../icons/checkmark-icon.svg "Checkmark") |   |   |
| List Registration | ![Checkmark icon](../../icons/checkmark-icon.svg "Checkmark")  | ![Checkmark icon](../../icons/checkmark-icon.svg "Checkmark") |   |   |
{: caption="Table 7. Describes how key states affect service actions on registrations." caption-side="bottom"}

## Next steps
{: #registration-next-steps}

You have added a foundational capability that we can now build upon!

- For the full list of services supported for integration, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- You can also view associations between root keys and encrypted resources with the UI, see [Viewing protected resources with the UI](/docs/hs-crypto?topic=hs-crypto-view-protected-resources#view-protected-resources-gui) for detailed instructions.
