---

copyright:
  years: 2018, 2021
lastupdated: "2021-04-26"

keywords: event, security, monitor event, audit event, activity tracker, activity tracker event

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:table: .aria-labeledby="caption"}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:external: target="_blank" .external}

# Auditing events for {{site.data.keyword.hscrypto}}
{: #at-events}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.at_full}} service to monitor how users and applications interact with {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard.

To enable {{site.data.keyword.at_full_notm}} for your {{site.data.keyword.hscrypto}} instance, you need to provision an instance of the {{site.data.keyword.at_full_notm}} service in the same region where your {{site.data.keyword.hscrypto}} instance is located. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started).

To see which {{site.data.keyword.hscrypto}} key management requests or Trusted Key Entry (TKE) requests correlate to the actions below, check out the [key management API reference doc](/apidocs/hs-crypto){: external} and [TKE CLI reference](/docs/hs-crypto-cli-plugin?topic=hs-crypto-cli-plugin-tke_cli_plugin){: external}.

## Supported events
{: #at-supported-events}

### Key events
{: #key-actions}

The following table lists the key actions that generate an event:




| Action                            | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| `hs-crypto.secrets.create`              | Create a key                                                 |
| `hs-crypto.secrets.delete`              | Delete a key                                                 |
| `hs-crypto.secrets.createalias`         | Create a key alias                                           |
| `hs-crypto.secrets.deletealias`         | Delete a key alias                                           |
| `hs-crypto.secrets.expire`              | Expire a key                                                 |
| `hs-crypto.secrets.read`                | Retrieve all key information                                 |
| `hs-crypto.secrets.readmetadata`        | Retrieve key metadata (excluding key payload, if applicable) |
| `hs-crypto.secrets.head`                | Retrieve key total                                           |
| `hs-crypto.secrets.list`                | List keys                                                    |
| `hs-crypto.secrets.wrap`                | Wrap a key                                                   |
| `hs-crypto.secrets.unwrap`              | Unwrap a key                                                 |
| `hs-crypto.secrets.rewrap`              | Rewrap a key                                                 |
| `hs-crypto.secrets.rotate`              | Rotate a key                                                 |
| `hs-crypto.secrets.setkeyfordeletion`   | Authorize deletion for a key with Dual Authorization policy  |
| `hs-crypto.secrets.unsetkeyfordeletion` | Cancel deletion for a key with Dual Authorization policy     |
| `hs-crypto.secrets.restore`             | Restore a key                                                |
| `hs-crypto.secrets.listkeyversions`     | List all the versions of a key                               |
| `hs-crypto.secrets.enable`              | Enable operations for a key                                  |
| `hs-crypto.secrets.disable`             | Disable operations for a key                                 |
| `hs-crypto.secrets.eventack`            | Acknowledge a lifecycle action on a key                      |
| `hs-crypto.secrets.default`             | Invalid key request event                                    |
{: caption="Table 1. Lifecycle Key Actions" caption-side="bottom"}


### Policy events
{: #policy-actions}

The following table lists the policy actions that generate an event:

| Action                         | Description                                  |
| ------------------------------ | -------------------------------------------- |
| `hs-crypto.policies.read`            | List key policies                            |
| `hs-crypto.policies.write`           | Set key policies                             |
| `hs-crypto.instancepolicies.read`    | List instance policies                       |
| `hs-crypto.instancepolicies.write`   | Set instance policies                        |
| `hs-crypto.policies.default`         | Invalid policy request event                 |
| `hs-crypto.instancepolicies.default` | Invalid policy request event                 |
{: caption="Table 2. Policy actions" caption-side="bottom"}

### Import token events
{: #import-token-actions}

The following table lists the import token actions that generate an event:

| Action                    | Description                            |
| ------------------------- | -------------------------------------- |
| `hs-crypto.importtoken.create`  | Create an import token                 |
| `hs-crypto.importtoken.read`    | Retrieve an import token               |
| `hs-crypto.importtoken.default` | Invalid import token request event     |
{: caption="Table 3. Import token actions" caption-side="bottom"}

### Registration events
{: #registration-actions}

The following table lists the registration actions that generate an event:




| Action                                  | Description                                              |
| --------------------------------------- | -------------------------------------------------------- |
| `hs-crypto.registrations.list`          | List registrations for any key                           |
| `hs-crypto.registrations.default`       | Invalid registration request event                       |
{: caption="Table 4. Registration actions" caption-side="bottom"}




### Trusted Key Entry events
{: #tke-actions}

The following table lists the Trusted Key Entry (TKE) actions that generate an event:

| Action                         | Description                                  |
| ------------------------------ | -------------------------------------------- |
| `hs-crypto.tke-cryptounit-admin.add` | Add a crypto unit administrator to the selected crypto units  |
| `hs-crypto.tke-cryptounit-admin.remove`  | Remove a crypto unit administrator from the selected crypto units |
| `hs-crypto.tke-cryptounit-threshold.set` | Set the signature thresholds for the selected crypto units |
| `hs-crypto.tke-cryptounit-master-key-register.add` | Load the new master key register |
| `hs-crypto.tke-cryptounit-master-key-register.commit`   | Commit the new master key register  |
| `hs-crypto.tke-cryptounit-master-key-register.activate` | Activate the current master key register  |
| `hs-crypto.tke-cryptounit-new-master-key-register.clear` | Clear the new master key register |
| `hs-crypto.tke-cryptounit-current-master-key-register.clear` | Clear the current master key register |
| `hs-crypto.tke-cryptounit.reset`   | Zeroize and reset the selected crypto units |
{: caption="Table 5. Trusted Key Entry actions" caption-side="bottom"}


### KMIP for VMware events
{: #at-events-kmip}

When you manage keys for the KMIP for VMware® service, an event is generated.

The following table provides the actions that generate and send events for KMIP for VMware. These actions are performed by an initiator from VMware vCenter Server® and do not include the initiator's IP address. The requests for these actions run from within the {{site.data.keyword.cloud_notm}} private network.

The initiator ID is derived from the TLS (Transport Layer Security) certificate of the vCenter Server that is used to authenticate the connection to the KMIP server. The initiator ID is in the format `CertificateID-<value>`, where the value matches the fingerprint of the corresponding TLS certificate. Using the fingerprint, you can identify the vCenter Server that triggered the action.

| Action                                      | Description                               |
|:--------------------------------------------|:------------------------------------------|
| `hs-crypto.kmip-key.create` | A KMIP key is created. |
| `hs-crypto.kmip-key.read` | A KMIP key is retrieved. |
| `hs-crypto.kmip-key-attributes.retrieve` | A KMIP key's attributes are retrieved. |
| `hs-crypto.kmip-key.activate` | A KMIP key is activated. |
| `hs-crypto.kmip-key.revoke` | A KMIP key is revoked. |
| `hs-crypto.kmip-key.destroy` | A KMIP key is destroyed. |
{: caption="Table 6. Description of actions that generate events for the KMIP for VMware service" caption-side="top"}

## Viewing events
{: #at-ui}

Events that are generated by an instance of {{site.data.keyword.hscrypto}} are automatically forwarded to the
{{site.data.keyword.at_full_notm}} service instance that is available in the same location.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the
{{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information,
see [Launching the web UI through the IBM Cloud UI](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-launch#launch_cloud_ui).


| Deployment Region         | Activity Tracker Region                         |
| ------------------------- | ----------------------------------------------- |
| `us-south`                | `us-south`                                      |
| `us-east`                 | `us-east`                                       |
| `eu-de`                   | `eu-de`                                         |
| `au-syd`                  | `au-syd`                                        |
{: caption="Table 7. Activity Tracker regions" caption-side="bottom"}

## Analyzing successful events
{: #at-events-analyze}

Most successful requests have unique `requestData` and `responseData`associated with each related event. The following sections describe the data of each {{site.data.keyword.hscrypto}} service action event.

Fields are not guaranteed to appear unless the request is successful.
{: note}

### Common fields
{: #at-common fields}

There are some common fields that {{site.data.keyword.hscrypto}} uses outside of the CADF event model to provide more insight into your data.

  <table>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><p><varname>`requestData.requestURI`</varname></p></td>
      <td>
        <p>The URI of the API request that was made.</p>
      </td>
    </tr>
    <tr>
      <td><p><varname>`requestData.instanceID`</varname></p></td>
      <td>
        <p>The unique identifier of your {{site.data.keyword.hscrypto}} service instance.</p>
      </td>
    </tr>
     <tr>
      <td><p><varname>`correlationId`</varname></p></td>
      <td>
        <p>The unique identifier of the API request that generated the event.</p>
        <p>Note: This field is currently not supported in TKE events.</p>
      </td>
    </tr>
    
    <caption style="caption-side:bottom;">Table 8. Describes the common fields in Activity Tracker events for {{site.data.keyword.hscrypto}} service
    actions.</caption>
  </table>

For more information on the event fields in the Cloud Auditing Data Federation (CADF) event model, see [Event Fields](https://test.cloud.ibm.com/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-event){: external}

While `initiator.host.address` is a field that is part of the Cloud Auditing Data Federation model, the host address field will not be shown for requests made through private networks.
{: important}

### Key action events
{: #key-action-events}

Because of the sensitivity of the information for an encryption key, when an event is generated as a result of an API call to the service of {{site.data.keyword.hscrypto}}, the event that is generated does not include detailed information about the key, such as the payload and encrypted nonce.

The `responseData.keyState` field is an integer and corresponds to the Pre-activation = 0, Active = 1, Suspended = 2, Deactivated = 3, and Destroyed = 5 values.
For more information on key states, see [Key states and transitions](/docs/hs-crypto?topic=hs-crypto-key-states#key-transitions).
{: note}

#### Create key
{: #create-key-success}

The following fields include extra information:

- The `requestData.keyType` field includes the type of key that was created.
- The `responseData.keyId` field includes the unique identifier associated with the key.
- The `responseData.keyVersionId` field includes the unique identifier of the current key version used to wrap input ciphertext on wrap requests.
- The `responseData.keyVersionCreationDate` field includes the date that the current version of the key was created.
- The `responseData.keyState` field includes the integer that correlates to the state of the key.

#### Delete key
{: #delete-key-success}

The following field includes extra information:

- The `responseData.keyState` field includes the integer that correlates to the state of the key.

#### Expire Key
{: #expire-key-success}

The following field includes extra information:

- The `requestData.keyType` field includes the type of key that was created.
- The `responseData.keyId` field includes the unique identifier associated with the key.
- The `requestData.expirationDate` field includes the date that the key expired on.
- The `responseData.initialValue.keyState` field includes the integer that correlates to the previous state of the key.
- The `responseData.newValue.keyState` field includes the integer that correlates to the current state of the key.

#### Wrap or unwrap key
{: #wrap-unwrap-key-success}

The following field includes extra information:

- The `responseData.keyVersionId` field includes the unique identifier of the current key version used to wrap input ciphertext on wrap requests.

#### Rewrap key
{: #rewrap-key-success}

The following field includes extra information:

- The `responseData.keyVersionId` field includes the unique identifier of the current key version used to wrap input ciphertext on wrap requests.
- The `responseData.rewrappedKeyVersionId` field includes the unique identifier of the new key version used to wrap input ciphertext on wrap requests.

#### Restore key
{: #restore-key-success}

The following field includes extra information:

- The `responseData.keyVersionId` field includes the unique identifier of the current key version used to wrap input ciphertext on wrap requests.

#### Rotate key
{: #rotate-key-success}

Rotate key doesn't have any additional fields outside of those from the [Common Fields](#at-common-fields) section
{: note}

#### Get key total
{: #list-head-success}

The following field includes extra information:

- The `responseData.totalResources` field includes the total amount of keys within the service instance.

#### List keys
{: #list-keys-success}

The following field includes extra information:

- The `responseData.totalResources` field includes the total amount of keys returned in the response.

#### Get key or key metadata
{: #get-key-success}

The following fields include extra information:

- The `requestData.keyType` field includes the type of key that was retrieved.
- The `responseData.keyState` field includes the integer that correlates to the state of the key.
- The `responseData.keyVersionId` field includes the unique identifier of the current key version used to wrap input ciphertext on wrap requests.
- The `responseData.keyVersionCreationDate` field includes the date that the current version of the key was created.



#### List key versions
{: #list-key-versions-success}

The following field includes extra information:

- The `responseData.totalResources` field includes the total amount of key versions returned in the response.

#### Set or unset key for deletion
{: #dual-auth-set-success}

The following fields include extra information:

- The `responseData.initialValue.authID` field includes the initiator ID of the person who set the dual
authorization policy.
- The `responseData.initialValue.authExpiration` field includes the expiration date for the dual
authorization policy.
- The `responseData.newValue.authID` field includes the initiator ID of the person who set the dual
authorization policy.
- The `responseData.newValue.authExpiration` field includes the expiration date for the dual authorization
policy.

`initialValue` is the initiatorID of the person who last set the dual authorization policy and `newValue` is the
new initiatorID of the person who set the dual authorization policy.
{: note}

### Policy events
{: #policy-at-events}

#### Allowed network policies
{: #allowed-network-event}

The following fields include extra information:

- The `requestData.initialValue.policyAllowedNetworkEnabled` field includes if your allowed network policy was previously enabled or disabled.
- The `requestData.initialValue.policyAllowedNetworkAttribute` field includes if your allowed network policy was previously only for public networks or both public and private networks.
- The `requestData.newValue.policyAllowedNetworkEnabled` field includes if your allowed network policy is currently enabled or disabled.
- The `requestData.newValue.policyAllowedNetworkAttribute` field includes if your allowed network policy is currently only for public networks or both public and private networks.

#### Dual auth delete policies
{: #dual-auth-event}

The following fields include extra information:

- The `requestData.initialValue.policyDualAuthDeleteEnabled` field includes if your dual auth delete policy was previously enabled or disabled.
- The `requestData.newValue.policyDualAuthDeleteEnabled` field includes if your dual auth delete policy is currently enabled or disabled.

#### Key creation and importation access policies
{: #allowed-key-creation-policy}

The following fields include extra information:

- The `requestData.initialValue.PolicyKCIAEnabled` field includes if your key creation and importation policy was previously enabled or disabled.
- The `requestData.newValue.PolicyKCIAEnabled` field includes if your key creation and importation policy is currently enabled or disabled.
- The `requestData.initialValue.PolicyKCIAAttrCRK` field includes if your key creation and importation policy previously allowed the creation of root keys.
- The `requestData.newValue.PolicyKCIAAttrCRK` field includes if your key creation and importation policy allows the creation of root keys.
- The `requestData.initialValue.PolicyKCIAAttrCSK` field includes if your key creation and importation policy previously allowed the creation of standard keys.
- The `requestData.newValue.PolicyKCIAAttrCSK` field includes if your key creation and importation policy allows the creation of standard keys.
- The `requestData.initialValue.PolicyKCIAAttrIRK` field includes if your key creation and importation policy previously allowed imported root keys.
- The `requestData.newValue.PolicyKCIAAttrIRK` field includes if your key creation and importation policy allows imported root keys.
- The `requestData.initialValue.PolicyKCIAAttrISK` field includes if your key creation and importation policy previously allowed imported standard keys.
- The `requestData.newValue.PolicyKCIAAttrISK` field includes if your key creation and importation policy allows imported standard keys.
- The `requestData.initialValue.PolicyKCIAAttrET` field includes if your key creation and importation policy previously required keys to be imported through import token.
- The `requestData.newValue.PolicyKCIAAttrET` field includes if your key creation and importation policy requires keys to be imported through import token.

### Import token events
{: #import-token-events}

#### Create import token
{: #create-import-token-success}

The following fields include extra information:

- The `responseData.expirationDate` field includes the expiration date of the import token.
- The `responseData.maxAllowedRetrievals` field includes the maximum amount of times the import token can be retrieved within its expiration time before it is no
longer accessible.

#### Retrieve import token
{: #retrieve-import-token-success}

The following fields include extra information:

- The `responseData.maxAllowedRetrievals` field includes the maximum amount of times the import token can be retrieved within its expiration time before it is no
longer accessible.
- The `responseData.remainingRetrievals` field includes the number of times the import token can be retrieved within its expiration time before it is no longer
accessible.



### Registration events
{: #registration-events}

#### List registrations
{: #list-registration-success}

The following field includes extra information:

- The `responseData.totalResources` field includes the total amount of registrations returned in the response.

### Trusted Key Entry events
{: #tke-events-success}

The following table lists the returned values that indicate a successful TKE event.

| Field name | Returned value |
| -------- | ----------- |
|`outcome` | `success`  |
| `reason.reasonCode`  | `200`  |
| `reason.reasonType`  |`OK`  |
{: caption="Table 9. Describes the returned values of a successful TKE event" caption-side="bottom"}

The following common fields for TKE events include extra information:

- The `requestData.location` field includes the specific location of the crypto unit. The location follows this format:

  *\[region\].\[availability zone\].\[hardware security module (HSM) module index\].\[HSM domain index\]*.

  For example, if you provision your instance in the `us-east` region, the value returned is similar to `[us-east].[AZ2-CSSTAG2].[03].[22]`.
- The `target.id` field includes the [Cloud Resource Name (CRN)](/docs/account?topic=account-crn) of the crypto unit.
- The `target.name` field also includes the location of the crypto unit.
- The `target.typeURI` field includes the URI of the object that the action is targeting at. For example, if you perform the `hs-crypto.tke-cryptounit-master-key-register.add` action, the value returned is `hs-crypto/tke-cryptounit/master-key-register`.

For the following TKE events, there are some specific fields that indicate more information.

#### Add a crypto unit administrator
{: #tke-add-admin-success}

- The `requestData.adminId` field includes the SHA-256 hash of the signature key file associated with the administrator to be added.
- The `responseData.adminIds` field lists the SHA-256 hashes of the signature key files associated with all the administrators that are currently added to the crypto unit.

#### Remove a crypto unit administrator
{: #tke-remove-admin-success}

- The `requestData.adminId` field includes the SHA-256 hash of the signature key file associated with the administrator to be removed.
- The `responseData.adminIds` field lists the SHA-256 hashes of the signature key files associated with all the administrators that are currently added to the crypto unit.

#### Set the signature thresholds
{: #tke-set-threshold-success}

- The `requestData.signatureThreshold` field includes the [main signature threshold](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-thresholds-concept) that you set on the crypto unit.
- The `requestData.revocationSignatureThreshold` field includes the [revocation signature threshold](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-thresholds-concept) that you set on the crypto unit.
- The `responseData.signatureThreshold` field includes the [main signature threshold](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-thresholds-concept) that is successfully set on the crypto unit.
- The `responseData.revocationSignatureThreshold` field includes the [revocation signature threshold](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-thresholds-concept) that is successfully set on the crypto unit.

#### Load the new master key register
{: #tke-load-new-master-success}

- The `requestData.masterKeyIds` field lists the SHA-256 hashes of all the master key parts files that you select to load to the crypto unit.
- The `responseData.verificationPattern` field includes the SHA-256 hash of the master key that is composed of the selected master key parts and is loaded to the new master key register.

#### Commit the new master key register
{: #tke-commit-new-master-success}

- The `requestData.verificationPattern` field includes the SHA-256 hash of the master key that is loaded to the new master key register.
- The `responseData.masterKeyIds` field lists the SHA-256 hashes of all the master key parts files that compose the master key.

#### Activate the current master key register
{: #tke-activate-current-master-success}

- The `requestData.verificationPattern` field includes the SHA-256 hash of the master key that is loaded and committed to the new master key register.
- The `responseData.verificationPattern` field includes the SHA-256 hash of the master key that is activated.

## Analyzing failed events
{: #at-events-analyze-failed}

### Unable to delete a key
{: #delete-key-failure}

If the delete key event has a `reason.reasonCode`of `409`, the key cannot be deleted because it is possibly protecting one or more cloud resources that have a retention
policy. Make a GET request to `/keys/{id}/registrations` to learn which resources this key is associated with. A registration with `"preventKeyDeletion": true`
indicates that the associated resource has a retention policy. To enable deletion, contact an account owner to remove the retention policy on each resource
that is associated with this key.

A delete key event might also receive a `reason.reasonCode` of `409` due to a dual auth deletion policy on the key. Make a GET request to `/api/v2/keys/{id}/policies` to see if there is a dual authorization policy associated with your key. If there is a policy set, contact the other authorized user to delete the key.

### Unable to authenticate while make a request
{: #authenticate-failure}

If the event has a `reason.reasonCode` of `401`, you might not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions in the specified service instance. Verify with an
administrator that you are assigned the correct platform and service access roles in the applicable service instance. For more
information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access).

Check that you are using a valid token that is associated with an account authorized to perform the service action.
{: note}

### Unable to view or list keys in a service instance
{: #list-keys-failure}

If you make a call to `GET api/v2/keys` to list the keys that are available in
your service instance and `responseData.totalResources` is 0, you might need to query for keys in
the deleted state using the `state` parameter or adjust the `offset` and `limit` parameters in
your request.

### Lifecycle action on a key with registrations did not complete
{: #protected-resource-key-failure}

The `responseData.reasonForFailure` and `responseData.resourceCRN` fields contain information on why the action wasn't able to
be completed.

If the event has a `reason.reasonCode` of `409`, the action cannot be completed due to the adopting service's key state
conflicting with the key state that {{site.data.keyword.hscrypto}} has.

If the event has a `reason.reasonCode` of `408`, the action cannot be completed because
{{site.data.keyword.hscrypto}} was not notified that all appropriate actions were taken within 4 hours of the
action request.

### Unable to perform Trusted Key Entry actions
{: #tke-actions-failure}

Failed TKE events have an `outcome` of `failure`. The `reason.reasonType` and `reason.reasonForFailure` fields contain information on why the action wasn't able to be completed.

If the event has a `reason.reasonCode` of `400`, the action cannot be completed because the operation to the crypto units is not supported or is not valid. Check whether the TKE command that you use is valid by referring to the [TKE CLI reference](/docs/hs-crypto-cli-plugin?topic=hs-crypto-cli-plugin-tke_cli_plugin){: external}.

If the event has a `reason.reasonCode` of `401` or `403`, the action cannot be completed because your access token is not valid or does not have the necessary permissions to access this instance. [Refresh your access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token) and check whether you have [appropriate permissions](/docs/hs-crypto?topic=hs-crypto-manage-access) to perform the corresponding actions.

If the event has a `reason.reasonCode` of `500`, check out the value of `reason.reasonForFailure` to identify the reasons of failure and the corresponding actions that you need to take.

## Event severity
{: event-severity}

The severity for all Activity Tracker events with
{{site.data.keyword.hscrypto}} is based on the type of request
that was made, then status code. For example, if you make a request to create a key
with an invalid key, but you are also unauthenticated for the service instance
that you included in the request, the unauthentication will take precedence and
the event will be evaluated as a `401` bad request call with a severity of
`critical`.

The severity level for all TKE events is `critical` due to the sensitivity of the actions.
{: important}

The following table lists the actions associated with each severity level:

<table>
    <tr>
      <th>Severity</th>
      <th>Actions</th>
    </tr>
    <tr>
      <td><p><varname>Critical</varname></p></td>
      <td>
        <p><code>hs-crypto.secrets.delete</code></p>
        <p><code>hs-crypto.registrations.delete</code></p>
        <p><code>hs-crypto.tke-cryptounit-admin.add</code></p>
        <p><code>hs-crypto.tke-cryptounit-admin.remove</code></p>
        <p><code>hs-crypto.tke-cryptounit-current-master-key-register.clear</code></p>
        <p><code>hs-crypto.tke-cryptounit-new-master-key-register.clear</code></p>
        <p><code>hs-crypto.tke-cryptounit-master-key-register.add</code></p>
        <p><code>hs-crypto.tke-cryptounit-master-key-register.commit</code></p>
        <p><code>hs-crypto.tke-cryptounit-master-key-register.activate</code></p>
        <p><code>hs-crypto.tke-cryptounit-threshold.set</code></p>
        <p><code>hs-crypto.tke-cryptounit.reset</code></p>
      </td>
    </tr>
    <tr>
      <td><p><varname>Warning</varname></p></td>
      <td>
        <p><code>hs-crypto.secrets.rotate</code>, <code>hs-crypto.secrets.restore</code></p>
        <p><code>hs-crypto.secrets.enable</code>, <code>hs-crypto.secrets.disable</code></p>
        <p><code>hs-crypto.secrets.setkeyfordeletion</code>, <code>hs-crypto.secrets.unsetkeyfordeletion</code></p>
        <p><code>hs-crypto.policies.write</code>, <code>hs-crypto.instancepolicies.write</code></p>
      </td>
    </tr>
     <tr>
      <td><p><varname>Normal</varname></p></td>
      <td>
        <p><code>hs-crypto.secrets.create</code>, <code>hs-crypto.secrets.read</code></p>
        <p><code>hs-crypto.secrets.readmetadata</code>, <code>hs-crypto.secrets.head</code></p>
        <p><code>hs-crypto.secrets.list</code>, <code>hs-crypto.secrets.wrap</code></p>
        <p><code>hs-crypto.secrets.unwrap</code>, <code>hs-crypto.secrets.rewrap</code></p>
        <p><code>hs-crypto.secrets.listkeyversions</code>, <code>hs-crypto.secrets.eventack</code></p>
        <p><code>hs-crypto.policies.read</code>, <code>hs-crypto.instancepolicies.read</code></p>
        <p><code>hs-crypto.importtoken.create</code>, <code>hs-crypto.importtoken.read</code></p>
        <p><code>hs-crypto.registrations.list</code></p>
      </td>
    </tr>
    <caption style="caption-side:bottom;">Table 10. Describes the severity level for {{site.data.keyword.hscrypto}} service actions.</caption>
  </table>

The following table lists the status codes associated with each severity level:

| Severity | Status code |
| -------- | ----------- |
| Critical | `400`[^services-1], `401`, `403`, `500`, `503`, `507`  |
| Warning  | `400`, `409`, `424`, `502`, `504`, `505`  |
{: caption="Table 11. Describes the severity level for {{site.data.keyword.hscrypto}} response status codes." caption-side="bottom"}

[^services-1]: For Trusted Key Entry events.
