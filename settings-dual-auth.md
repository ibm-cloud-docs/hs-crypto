---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-09"

keywords: instance settings, service settings, dual authorization

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Managing dual authorization of your service instance
{: #manage-dual-auth}

After you set up your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}
instance, you can manage dual authorization by using the key management service API.
{: shortdesc}

This policy only applies to key management service keys and related operations.
{: important}

## Understanding dual authorization of your service instance
{: #understand-daul-auth-policy}

Dual authorization for {{site.data.keyword.hscrypto}} instances is an extra policy that helps to prevent accidental or malicious
deletion of keys. When you enable this policy at the instance level,
{{site.data.keyword.hscrypto}} requires an authorization from
two users to delete any keys that are created after the policy is enabled.

Before you enable dual authorization for your service instance, keep in mind the
following considerations:

- **When you enable dual authorization for your service instance, the policy is applicable only for new keys.** By enabling dual authorization at the instance level, any new keys that you add to the instance will automatically inherit a dual authorization policy. Your existing keys are not affected by the policy change and will still require a single authorization for deletion.
- **You can always disable a dual authorization policy for your service instance.** If you want to disable an existing dual authorization policy to allow for single authorization, keep in mind that the change is applicable only for future keys that you add to the instance. Any existing keys that were created under a dual authorization policy will continue to require actions from two users before the keys can be deleted. After a key inherits a dual authorization policy, the policy cannot be reverted.

## Enabling dual authorization for your service instance with the UI
{: #enable-dual-auth-instance-policy-ui}
{: ui}

As an instance manager, if you prefer to enable a dual authorization policy on your instance by using a graphical interface, you can use the UI.

After creating a service instance, complete the following steps to create a dual authorization policy:

1. [Log in to the UI](https://{DomainName}/){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. In the UI of the selected service instance, select the **Instance policies** tab in the side menu.
5. In the **Dual authorization deletion** section, check the box for `Require two users to approve key deletions`, and click **Save policy**.

## Enabling dual authorization for your service instance with the API
{: #enable-dual-auth-instance-policy-api}
{: api}

As an instance manager, enable a dual authorization policy for a
{{site.data.keyword.hscrypto}} instance by making a
`PUT` call to the following endpoint.

 

```
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=dualAuthDelete
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To enable and disable dual authorization policy, you must be assigned a
    _Manager_ access policy for your service instance. To learn how IAM roles
    map to {{site.data.keyword.hscrypto}} service actions,
    check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Enable a dual authorization policy for your service instance by running the following cURL command.

    ```sh
    curl -X PUT \
      'https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=dualAuthDelete' \
      -H 'accept: application/vnd.ibm.kms.policy+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'x-kms-key-ring: <key_ring_ID>' \
      -H 'content-type: application/vnd.ibm.kms.policy+json' \
      -d '{
        "metadata": {
          "collectionType": "application/vnd.ibm.kms.policy+json",
          "collectionTotal": 1
        },
        "resources": [
          {
            "policy_type": "dualAuthDelete",
            "policy_data": {
              "enabled": true
            }
          }
        ]
      }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south` or `eu-de`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `key_ring_ID` | **Optional.** The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} will search for the key in every key ring that is associated with the specified instance. Therefore, it is suggested to specify the key ring ID for a more optimized request. \n \n Note: The key ring ID of keys that are created without an `x-kms-key-ring` header is: default. For more information, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    {: caption="Describes the variables needed to enable dual authorization at the instance level" caption-side="bottom"}

    A successful request returns an HTTP `204 No Content` response, which
    indicates that your service instance is now enabled for dual authorization.
    Keys that you create or import to the service now require two authorizations
    before they can be deleted. For more information, see
    [Deleting keys](/docs/hs-crypto?topic=hs-crypto-delete-keys).

    This new policy does not affect existing keys in your instance. If you need
    to enable dual authorization for an existing key, see
    [Creating a dual authorization policy for a key](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy#create-dual-auth-key-policy-api).
    {: note}

3. Optional: Verify that the dual authorization policy was created by browsing
the policies that are available for your
{{site.data.keyword.hscrypto}} instance.

    ```cURL
    curl -X GET \
      'https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=dualAuthDelete' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'accept: application/vnd.ibm.kms.policy+json'
    ```
    {: codeblock}

## Disabling dual authorization for your service instance with the UI
{: #disable-dual-auth-instance-policy-ui}
{: ui}

As an instance manager, if you prefer to disable a dual authorization policy on your instance by using a graphical interface, you can use the UI.

After creating a service instance, complete the following steps to create a dual authorization policy:

1. [Log in to the UI](https://{DomainName}/){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. In the UI of the selected service instance, select the **Instance policies** tab in the side menu.
5. In the **Dual authorization deletion** section, clear the box for `Require two users to approve key deletions`, and click **Save policy**.

## Disabling dual authorization for your service instance with the key management service API
{: #disable-dual-auth-instance-policy-api}
{: api}

As an instance manager, disable an existing dual authorization policy for a
{{site.data.keyword.hscrypto}} instance by making a
`PUT` call to the following endpoint.

```
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=dualAuthDelete
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To enable and disable dual authorization policy, you must be assigned a
    _Manager_ access policy for your service instance. To learn how IAM roles
    map to {{site.data.keyword.hscrypto}} service actions,
    check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Disable an existing dual authorization policy for your service instance by running the following cURL command.

    ```cURL
    curl -X PUT \
      'https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=dualAuthDelete' \
      -H 'accept: application/vnd.ibm.kms.policy+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'x-kms-key-ring: <key_ring_ID>' \
      -H 'content-type: application/vnd.ibm.kms.policy+json' \
      -d '{
        "metadata": {
          "collectionType": "application/vnd.ibm.kms.policy+json",
          "collectionTotal": 1
        },
        "resources": [
          {
            "type": "application/vnd.ibm.kms.policy+json",
            "dualAuthDelete": {
              "enabled": false
            }
          }
        ]
      }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south` or `eu-de`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `key_ring_ID` | **Optional.** The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} will search for the key in every key ring that is associated with the specified instance. Therefore, it is suggested to specify the key ring ID for a more optimized request. \n \n Note: The key ring ID of keys that are created without an `x-kms-key-ring` header is: default. For more information, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    {: caption="Describes the variables needed to enable dual authorization at the instance level" caption-side="bottom"}

    A successful request returns an HTTP `204 No Content` response, which
    indicates that the dual authorization policy was updated for your service
    instance. Keys that you create or import to the service now require only one
    authorization before they can be deleted. For more information, see
    [Deleting keys](/docs/hs-crypto?topic=hs-crypto-delete-keys).

3. Optional: Verify that the dual authorization policy was updated by browsing
the policies that are available for your
{{site.data.keyword.hscrypto}} instance.

    ```cURL
    curl -X GET \
      'https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=dualAuthDelete' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'accept: application/vnd.ibm.kms.policy+json'
    ```
    {: codeblock}
