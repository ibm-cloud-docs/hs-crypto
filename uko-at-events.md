---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-14"

keywords: event, security, monitor event, audit event, activity tracker, activity tracker event, Unified Key Orchestrator, UKO events

subcollection: hs-crypto

---


{{site.data.keyword.attribute-definition-list}}



# Auditing events for {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}
{: #uko-at-events}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.at_full}} service to monitor how users and applications interact with {{site.data.keyword.cloud_notm}} with {{site.data.keyword.uko_full_notm}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard.

To enable {{site.data.keyword.at_full_notm}} for your {{site.data.keyword.hscrypto}} instance, you need to provision an instance of the {{site.data.keyword.at_full_notm}} service in the same region where your {{site.data.keyword.hscrypto}} instance is located. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

To see which requests correlate to the following actions, check out the [{{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko){: external} and [TKE CLI reference](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#tke-cli-plugin){: external}.

## Supported events
{: #uko-at-supported-events}

### Key events
{: #uko-key-actions}

The following table lists the key actions that generate an event.

| Action                            | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| `hs-crypto.managed-keys.write`              | Create or update a managed key.                          |
| `hs-crypto.managed-keys.list`                | Get a list of managed keys.                             |
| `hs-crypto.managed-keys.read`                |Retrieve information about a managed key.                |
| `hs-crypto.managed-keys.delete`              | Delete a managed key.   |
{: caption="Table 1. Managed key actions" caption-side="bottom"}

### Keystore events
{: #uko-keystore-actions}

The following table lists the key actions that generate an event.

| Action                            | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| `hs-crypto.target-keystores.write`               | Create or update a target keystore.   |
| `hs-crypto.target-keystores.list `         | Get a list of target keystores.               |
| `hs-crypto.target-keystores.read`         | Retrieve information about a target keystore.     |
| `hs-crypto.target-keystores.delete`              | Delete a target keystore.                |
{: caption="Table 2. Target keystore actions" caption-side="bottom"}

### Vault events
{: #uko-vault-actions}

The following table lists the key actions that generate an event.

| Action                            | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| `hs-crypto.vaults.list`             | Get a list of vaults.                                    |
| `hs-crypto.vaults.write`             | Create or update a vault.                                    |
| `hs-crypto.vaults.read`             | Retrieve information about a vault.                                    |
| `hs-crypto.vaults.delete`             | Delete a vault.                                    |
{: caption="Table 3. Vault actions" caption-side="bottom"}

### Template events
{: #uko-template-actions}

The following table lists the key actions that generate an event.

| Action                            | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| `hs-crypto.key-templates.write`             | Create or update a template.                                    |
| `hs-crypto.key-templates.read`             | Retrieve template information.                                    |
| `hs-crypto.key-templates.delete`             | Delete a template.                                    |
| `hs-crypto.key-templates.list`             | List all key templates.                                    |
{: caption="Table 4. Template actions" caption-side="bottom"}

### Registration events
{: #uko-registration-actions}

The following table lists the registration actions that generate an event.




| Action                                  | Description                                              |
| --------------------------------------- | -------------------------------------------------------- |
| `hs-crypto.registrations.list`          | List registrations for any key.                           |
| `hs-crypto.registrations.default`       | Invalid registration request event.                       |
{: caption="Table 5. Registration actions" caption-side="bottom"}




### Trusted Key Entry events
{: #uko-tke-actions}

The following table lists the Trusted Key Entry (TKE) actions that generate an event.

| Action                         | Description                                  |
| ------------------------------ | -------------------------------------------- |
| `hs-crypto.tke-cryptounit-admin.add` | Add a crypto unit administrator to the selected crypto units.  |
| `hs-crypto.tke-cryptounit-admin.remove`  | Remove a crypto unit administrator from the selected crypto units. |
| `hs-crypto.tke-cryptounit-threshold.set` | Set the signature thresholds for the selected crypto units. |
| `hs-crypto.tke-cryptounit-master-key-register.add` | Load the new master key register. |
| `hs-crypto.tke-cryptounit-master-key-register.commit`   | Commit the new master key register.  |
| `hs-crypto.tke-cryptounit-master-key-register.activate` | Activate the current master key register.  |
| `hs-crypto.tke-cryptounit-new-master-key-register.clear` | Clear the new master key register. |
| `hs-crypto.tke-cryptounit-current-master-key-register.clear` | Clear the current master key register. |
| `hs-crypto.tke-cryptounit.reset`   | Zeroize and reset the selected crypto units |
{: caption="Table 6. Trusted Key Entry actions" caption-side="bottom"}

### Certificate manager events
{: #uko-mtlscert-mgr-actions}

The following table lists the certificate manager actions that generate an event.

| Action                         | Description                                  |
| ------------------------------ | -------------------------------------------- |
| `hs-crypto.mtlscert-admin-key.create` | Create the administrator signature key for the certificate administrator to connect to the certificate manager server.  |
| `hs-crypto.mtlscert-admin-key.update`  | Refresh and update the administrator signature key for the certificate administrator. |
| `hs-crypto.mtlscert-admin-key.read` | Get the administrator signature key of the certificate administrator. |
| `hs-crypto.mtlscert-admin-key.delete` | Delete the administrator signature key of the certificate administrator.|
| `hs-crypto.mtlscert-cert.set`   | Create or update certificates by the certificate administrator.  |
| `hs-crypto.mtlscert-cert.list` | List all certificates that are managed by the certificate administrator.  |
| `hs-crypto.mtlscert-cert.read` | Get certificates by the certificate administrator.|
| `hs-crypto.mtlscert-cert.delete` | Delete certificates by the certificate administrator. |
{: caption="Table 7. Certificate manager actions" caption-side="bottom"}

### KMIP for VMware events
{: #uko-at-events-kmip}

When you manage keys for the KMIP for VMware® service, an event is generated.

The following table provides the actions that generate and send events for KMIP for VMware. These actions are performed by an initiator from VMware vCenter Server® and do not include the initiator's IP address. The requests for these actions run from within the {{site.data.keyword.cloud_notm}} private network.

The initiator ID is derived from the TLS (Transport Layer Security) certificate of the vCenter Server that is used to authenticate the connection to the KMIP server. The initiator ID is in the format `CertificateID-<value>`, where the value matches the fingerprint of the corresponding TLS certificate. Using the fingerprint, you can identify the vCenter Server that triggered the action.

| Action                                      | Description                               |
|--------------------------------------------|------------------------------------------|
| `hs-crypto.kmip-key.create` | A KMIP key is created. |
| `hs-crypto.kmip-key.read` | A KMIP key is retrieved. |
| `hs-crypto.kmip-key-attributes.retrieve` | A KMIP key's attributes are retrieved. |
| `hs-crypto.kmip-key.activate` | A KMIP key is activated. |
| `hs-crypto.kmip-key.revoke` | A KMIP key is revoked. |
| `hs-crypto.kmip-key.destroy` | A KMIP key is destroyed. |
{: caption="Table 8. Description of actions that generate events for the KMIP for VMware service" caption-side="top"}

### EP11 keystore events
{: uko-ep11-keystore-events}

The following table lists the Enterprise PKCS #11 (EP11) keystore actions that generate an event: 
| Action                                      | Description                               |
|--------------------------------------------|------------------------------------------|
| `hs-crypto.keystore.createkeystore` | Create an EP11 keystore. |
| `hs-crypto.keystore.deletekey` | Delete an EP11 key. |
| `hs-crypto.keystore.deletekeystore`| Delete an EP11 keystore. |
| `hs-crypto.keystore.listkeysbyattributes` |	View EP11 keys. |
| `hs-crypto.keystore.listkeysbyids` |	View EP11 keys. |
| `hs-crypto.keystore.listkeystoresbyattributes` |	View EP11 keystores. |
| `hs-crypto.keystore.listkeystoresbyids` |View EP11 keystores. |
| `hs-crypto.keystore.storenewkey` | Store an EP11 key. |
| `hs-crypto.keystore.updatekey` | Update an EP11 key. |
{: caption="Table 9. EP11 keystore actions" caption-side="top"}

### EP11 crypto events
{: uko-ep11-crypto-events}

The following table lists the EP11 crypto actions that generate an event:
| Action                                      | Description                               |
|--------------------------------------------|------------------------------------------|
| `hs-crypto.ep11.use` |	Cryptographic operation |
{: caption="Table 10. EP11 crypto actions" caption-side="top"} 


## Viewing events
{: #uko-at-ui}

Events that are generated by an instance of {{site.data.keyword.hscrypto}} are automatically forwarded to the
{{site.data.keyword.at_full_notm}} service instance that is available in the same location.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the
{{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information,
see [Launching the web UI through the IBM Cloud UI](/docs/activity-tracker?topic=activity-tracker-launch#launch_cloud_ui).

| Deployment region         | Activity Tracker region                         |
| ------------------------- | ----------------------------------------------- |
| `au-syd`                  | `au-syd`                                        |
| `br-sao`                  | `br-sao`                                        |
| `ca-tor`                  | `ca-tor`                                        |
| `eu-de`                   | `eu-de`                                         |
| `eu-gb`                   | `eu-gb`                                         |
| `jp-tok`                  | `jp-tok`                                        |
| `us-east`                 | `us-east`                                       |
| `us-south`                | `us-south`                                      |
{: caption="Table 11. Activity Tracker regions" caption-side="bottom"}

## Analyzing successful events
{: #uko-at-events-analyze}

Most successful requests have unique `requestData` and `responseData` associated with each related event. In `requestData` and `responseData` properties there are available full payloads from requests and responses except sensitive data. The list of field, endpoints, and payloads is available in API docs.

Fields are not guaranteed to appear unless the request is successful.
{: note}

The list of sensitive field values that are hidden using the `[redacted]` placeholder:
* service_principal_password
* secret_access_key
* access_key_id
* api_key

### Common fields
{: #uko-at-common fields}

Some common fields are available for {{site.data.keyword.hscrypto}} to use outside of the CADF event model to provide more insight into your data.

| Field | Description |
| --- | --- |
| `requestData.requestURI` | The URI of the API request that was made. |
| `requestData.instanceID` | The unique identifier of your {{site.data.keyword.hscrypto}} service instance. |
{: caption="Table 12. Common fields in Activity Tracker events for {{site.data.keyword.hscrypto}} service actions" caption-side="bottom"}

For more information about the event fields in the Cloud Auditing Data Federation (CADF) event model, see [Event Fields](/docs/activity-tracker?topic=activity-tracker-event){: external}.

While `initiator.host.address` is a field that is part of the Cloud Auditing Data Federation model, the host address field is not shown for requests made through private networks.
{: important}

### Registration events
{: #uko-registration-events}

#### List registrations
{: #uko-list-registration-success}

The following field includes extra information:

- The `responseData.totalResources` field includes the total number of registrations that are returned in the response.


### Trusted Key Entry events
{: #uko-tke-events-success}

The following table lists the returned values that indicate a successful TKE event.

| Field name | Returned value |
| -------- | ----------- |
|`outcome` | `success`  |
| `reason.reasonCode`  | `200`  |
| `reason.reasonType`  |`OK`  |
{: caption="Table 13. Returned values of a successful TKE event" caption-side="bottom"}

The following common fields for TKE events include extra information:

- The `requestData.location` field includes the specific location of the crypto unit. The location follows this format:

    *\[region\].\[availability zone\].\[hardware security module (HSM) module index\].\[HSM domain index\]*.

    For example, if you provision your instance in the `us-east` region, the value that is returned is similar to `[us-east].[AZ2-CSSTAG2].[03].[22]`.
- The `target.id` field includes the [Cloud Resource Name (CRN)](/docs/account?topic=account-crn) of the crypto unit.
- The `target.name` field also includes the location of the crypto unit.
- The `target.typeURI` field includes the URI of the object that the action is targeting at. For example, if you perform the `hs-crypto.tke-cryptounit-master-key-register.add` action, the value that is returned is `hs-crypto/tke-cryptounit/master-key-register`.

For the following TKE events, some specific fields indicate more information.

#### Add a crypto unit administrator
{: #uko-tke-add-admin-success}

- The `requestData.adminId` field includes the SHA-256 hash of the signature key file that is associated with the administrator to be added.
- The `responseData.adminIds` field lists the SHA-256 hashes of the signature key files associated with all the administrators that are added to the crypto unit.


#### Remove a crypto unit administrator
{: #uko-tke-remove-admin-success}

- The `requestData.adminId` field includes the SHA-256 hash of the signature key file that is associated with the administrator to be removed.
- The `responseData.adminIds` field lists the SHA-256 hashes of the signature key files associated with all the administrators that are   added to the crypto unit.


#### Set the signature thresholds
{: #uko-tke-set-threshold-success}

- The `requestData.signatureThreshold` field includes the [main signature threshold](/docs/hs-crypto?topic=hs-crypto-uko-understand-concepts#uko-signature-thresholds-concept) that you set on the crypto unit.
- The `requestData.revocationSignatureThreshold` field includes the [revocation signature threshold](/docs/hs-crypto?topic=hs-crypto-uko-understand-concepts#uko-signature-thresholds-concept) that you set on the crypto unit.
- The `responseData.signatureThreshold` field includes the [main signature threshold](/docs/hs-crypto?topic=hs-crypto-uko-understand-concepts#uko-signature-thresholds-concept) that is successfully set on the crypto unit.
- The `responseData.revocationSignatureThreshold` field includes the [revocation signature threshold](/docs/hs-crypto?topic=hs-crypto-uko-understand-concepts#uko-signature-thresholds-concept) that is successfully set on the crypto unit.

#### Load the new master key register
{: #uko-tke-load-new-master-success}

- The `requestData.masterKeyIds` field lists the SHA-256 hashes of all the master key parts files that you select to load to the crypto unit.
- The `responseData.verificationPattern` field includes the SHA-256 hash of the master key that is composed of the selected master key parts and is loaded to the new master key register.


#### Commit the new master key register
{: #uko-tke-commit-new-master-success}

- The `requestData.verificationPattern` field includes the SHA-256 hash of the master key that is loaded to the new master key register.
- The `responseData.masterKeyIds` field lists the SHA-256 hashes of all the master key parts files that compose the master key.


#### Activate the current master key register
{: #uko-tke-activate-current-master-success}

- The `requestData.verificationPattern` field includes the SHA-256 hash of the master key that is loaded and committed to the new master key register.
- The `responseData.verificationPattern` field includes the SHA-256 hash of the master key that is activated.


### Certificate manager events
{: #uko-mgr-events-success}

The following table lists the returned values that indicate a successful certificate manager event.

| Field name | Returned value |
| -------- | ----------- |
|`outcome` | `success`  |
| `reason.reasonCode`  | `200`  |
| `reason.reasonType`  |`OK`  |
{: caption="Table 14. Returned values of a successful mTLS certificate manager event" caption-side="bottom"}

The following common fields for certificate manager events include extra information:

- The `target.id` field includes the [Cloud Resource Name (CRN)](/docs/account?topic=account-crn) of the event.
- The `target.name` field indicates the target name of the event, such as "mtlscert-admin-key" or "mtlscert-cert".
- The `target.typeURI` field includes the URI of the object that the action is targeting at. For example, if you perform the `hs-crypto.mtlscert-admin-key.create` action, the value that is returned is `hs-crypto/mtlscert-admin-key`.

The specified fields of the following certificate manager events can indicate more information.

#### Create the administrator signature key for the certificate administrator
{: #uko-cert-mgr-create-adminkey-success}

The following fields include extra information:

- The `requestData.accountId` field includes the current user ID.
- The `responseData.action` field includes the action details of the current user.


#### Update the administrator signature key for the certificate administrator
{: #uko-cert-mgr-update-adminkey-success}

The following fields include extra information:

- The `requestData.accountId` field includes the current user ID.
- The `responseData.action` field includes the action details of the current user.


#### Remove the administrator signature key of the certificate administrator
{: #uko-cert-mgr-delete-adminkey-success}

The following fields include extra information:

- The `requestData.accountId` field includes the current user ID.
- The `responseData.action` field includes the action details of the current user.


#### Get the administrator signature key of the certificate administrator
{: #uko-cert-mgr-read-adminkey-success}

The following fields include extra information:

- The `requestData.accountId` field includes the current user ID.
- The `responseData.action` field includes the action details of the current user.


#### Create or updating certificates by the certificate administrator
{: #uko-cert-mgr-set-cert-success}

The following fields include extra information:

- The `requestData.certificateId` field indicates the target certificate.
- The `responseData.action` field indicates that the certificate is to be created or updated.


#### List certificates by the certificate administrator
{: #uko-cert-mgr-list-cert-success}

The following field includes extra information:

- The `responseData.action` field indicates all certificates that are managed by current administrator are to be listed.


#### Get certificates by the certificate administrator
{: #uko-cert-mgr-read-cert-success}

The following fields include extra information:

- The `requestData.certificateId` field indicates the target certificate.
- The `responseData.action` field indicates that the certificate is to be fetched and displayed.


#### Remove certificates by the certificate administrator
{: #uko-cert-mgr-delete-cert-success}

The following fields include extra information:

- The `requestData.certificateId` field indicates the target mTLS certificate.
- The `responseData.action` field indicates that the certificate is to be deleted.

### EP11 keystore events
{: uko-ep11-keystore}

The following table lists the returned values that indicate a successful EP11 keystore event:

| Field name | Returned value |
| --- | --- |
| outcome | success |
| reason.reasonCode	| 200 |
| reason.reasonType	| OK |

{: caption="Table 15. Returned values of a successful EP11 keystore event" caption-side="bottom"}

The following common fields for EP11 keystore events include extra information:
- The `target.name` field includes the IDs of the keystore or key.

### EP11 crypto events
{: uko-ep11-crypto}

The following table lists the returned values that indicate a successful EP11 crypto event:

| Field name | Returned value |
| --- | --- |
| outcome | success |
| reason.reasonCode	| 200 |
| reason.reasonType	| OK |
{: caption="Table 16. Returned values of a successful EP11 crypto event" caption-side="bottom"}


## Analyzing failed events
{: #uko-at-events-analyze-failed}

All failed events contain the `message` field with detailed description of the problem.

### Lifecycle action on a key with registrations did not complete
{: #uko-protected-resource-key-failure}

The `responseData.reasonForFailure` and `responseData.resourceCRN` fields contain information about why the action wasn't able to
be completed.

If the event has a `reason.reasonCode` of `409`, the action cannot be completed due to the adopting service's key state
conflicting with the key state that {{site.data.keyword.hscrypto}} has.

If the event has a `reason.reasonCode` of `408`, the action cannot be completed because
{{site.data.keyword.hscrypto}} was not notified that all appropriate actions were taken within 4 hours of the
action request.

### Unable to perform Trusted Key Entry actions
{: #uko-tke-actions-failure}

Failed TKE events have an `outcome` of `failure`. The `reason.reasonType` and `reason.reasonForFailure` fields contain information about why the action wasn't able to be completed.

If the event has a `reason.reasonCode` of `400`, the action cannot be completed because the operation to the crypto units is not supported or is not valid. Check whether the TKE command that you use is valid by referring to the [TKE CLI reference](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#tke-cli-plugin){: external}.

If the event has a `reason.reasonCode` of `401` or `403`, the action cannot be completed because your access token is not valid or does not have the necessary permissions to access this instance. [Refresh your access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token) and check whether you have [appropriate permissions](/docs/hs-crypto?topic=hs-crypto-uko-manage-access) to perform the corresponding actions.

If the event has a `reason.reasonCode` of `500`, check out the value of `reason.reasonForFailure` to identify the reasons of failure and the corresponding actions that you need to take.

## Event severity
{: #uko-event-severity}


The severity for all Activity Tracker events with
{{site.data.keyword.hscrypto}} is based on the type of request
that was made, then status code. For example, you might request to create a key
with an invalid key and are not authenticated in the service instance. The unauthentication takes precedence and
the event is evaluated as a `401` bad request call with a severity of
`critical`.

The severity level for all TKE events is `critical` due to the sensitivity of the actions.
{: important}

The following table lists the actions that are associated with each severity level.

| Severity | Actions |
| --- | --- |
| Critical | `hs-crypto.target-keystores.delete` \n \n `hs-crypto.managed-keys.delete` \n \n `hs-crypto.vaults.delete` \n \n `hs-crypto.registrations.delete` \n \n `hs-crypto.tke-cryptounit-admin.add` \n \n `hs-crypto.tke-cryptounit-admin.remove` \n \n `hs-crypto.tke-cryptounit-current-master-key-register.clear` \n \n `hs-crypto.tke-cryptounit-new-master-key-register.clear` \n \n `hs-crypto.tke-cryptounit-master-key-register.add` \n \n `hs-crypto.tke-cryptounit-master-key-register.commit` \n \n `hs-crypto.tke-cryptounit-master-key-register.activate` \n \n `hs-crypto.tke-cryptounit-threshold.set` \n \n `hs-crypto.tke-cryptounit.reset` \n \n `hs-crypto.mtlscert-admin-key.create` \n \n `hs-crypto.mtlscert-admin-key.update` \n \n `hs-crypto.mtlscert-admin-key.delete` \n \n `hs-crypto.mtlscert-cert.set` \n \n `hs-crypto.mtlscert-cert.set` \n \n `hs-crypto.keystore.deletekey` \n \n `hs-crypto.keystore.deletekeystore` \n \n `hs-crypto.keystore.updatekey` |
| Warning | `hs-crypto.managed-keys.write` \n \n Note that when this event is triggered to change the key state to `destroyed`, the severity level is `Critical` instead of `Warning`. |
| Normal | `hs-crypto.managed-keys.list` \n \n `hs-crypto.managed-keys.read` \n \n `hs-crypto.target-keystores.write` \n \n `hs-crypto.target-keystores.list` \n \n `hs-crypto.target-keystores.read` \n \n `hs-crypto.vaults.list` \n \n `hs-crypto.vaults.write` \n \n `hs-crypto.vaults.read` \n \n `hs-crypto.keystore.createkeystore` \n \n `hs-crypto.keystore.listkeysbyattributes` \n \n `hs-crypto.keystore.listkeysbyids` \n \n `hs-crypto.keystore.listkeystoresbyattributes` \n \n `hs-crypto.keystore.listkeystoresbyids` \n \n `hs-crypto.keystore.storenewkey` \n \n `hs-crypto.ep11.use` |
{: caption="Table 17. Severity level for {{site.data.keyword.hscrypto}} service actions" caption-side="bottom"}

The following table lists the status codes that are associated with each severity level.

| Severity | Status code |
| -------- | ----------- |
| Critical | `400` (For TKE events only), `401`, `403`, `500`, `503`, `507`  |
| Warning  | `400`, `409`, `424`, `502`, `504`, `505`  |
{: caption="Table 18. Severity level for {{site.data.keyword.hscrypto}} response status codes" caption-side="bottom"}

