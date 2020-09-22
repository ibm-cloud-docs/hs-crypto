---

copyright:
  years: 2020
lastupdated: "2020-07-01"

keywords: instance settings, service settings, dual authorization

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:preview: .preview}

# Managing dual authorization for your service instance
{: #manage-dual-auth}

After you set up your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}
instance, you can manage dual authorization by using the key management API.
{: shortdesc}

## Managing dual authorization settings
{: #manage-dual-auth-instance-policy}

Dual authorization for {{site.data.keyword.hscrypto}} instances is an extra policy that helps to prevent accidental or malicious
deletion of keys. When you enable this policy at the instance level,
{{site.data.keyword.hscrypto}} requires an authorization from
two users to delete any keys that are created after the policy is enabled.

The dual authorization capability is available only through the
{{site.data.keyword.hscrypto}} key management API. To find out more about
accessing the {{site.data.keyword.hscrypto}} key management API, check out
[Setting up the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
{: preview}

Before you enable dual authorization for your service instance, keep in mind the
following considerations:

- **When you enable dual authorization for your service instance, the policy is applicable only for new keys.**
By enabling dual authorization at the instance level, any new keys that you add
to the instance will automatically inherit a dual authorization policy. Your
existing keys are not affected by the policy change and will still require a
single authorization for deletion.
- **You can always disable a dual authorization policy for your service instance.**
If you want to
[disable an existing dual authorization policy](#disable-dual-auth-instance-policy)
to allow for single authorization, keep in mind that the change is applicable
only for future keys that you add to the instance. Any existing keys that were
created under a dual authorization policy will continue to require actions from
two users before the keys can be deleted. After a key inherits a dual
authorization policy, the policy cannot be reverted.

### Enabling dual authorization for your service instance
{: #enable-dual-auth-instance-policy}

As an instance manager, enable a dual authorization policy for a
{{site.data.keyword.hscrypto}} instance by making a
`PUT` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/instance/policies?policy=dualAuthDelete
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To enable and disable dual authorization policies, you must be assigned a
    _Manager_ access policy for your service instance. To learn how IAM roles
    map to {{site.data.keyword.hscrypto}} service actions,
    check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Enable a dual authorization policy for your service instance by running the
following cURL command.

    ```cURL
    curl -X PUT \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/instance/policies?policy=dualAuthDelete' \
      -H 'accept: application/vnd.ibm.kms.policy+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
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

    Replace the variables in the example request according to the following
    table.

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>

      <tr>
        <td>
          <varname>region</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The region abbreviation, such as
            <code>us-south</code> or <code>eu-de</code>, that represents the
            geographic area where your
            {{site.data.keyword.hscrypto}} instance
            resides.
          </p>
          <p>
            For more information, see
            [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints).
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}}
            access token. Include the full contents of the <code>IAM</code>
            token, including the Bearer value, in the cURL request.
          </p>
          <p>
            For more information, see
            [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token).
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>instance_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier that is assigned to
            your {{site.data.keyword.hscrypto}} service
            instance.
          </p>
          <p>
            For more information, see
            [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
          </p>
        </td>
      </tr>

      <caption style="caption-side:bottom;">
        Table 1. Describes the variables that are needed to enable dual
        authorization at the instance level.
      </caption>
    </table>

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
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/instance/policies?policy=dualAuthDelete' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'accept: application/vnd.ibm.kms.policy+json'
    ```
    {: codeblock}

### Disabling dual authorization for your service instance
{: #disable-dual-auth-instance-policy}

As an instance manager, disable an existing dual authorization policy for a
{{site.data.keyword.hscrypto}} instance by making a
`PUT` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/instance/policies?policy=dualAuthDelete
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To enable and disable dual authorization policies, you must be assigned a
    _Manager_ access policy for your service instance. To learn how IAM roles
    map to {{site.data.keyword.hscrypto}} service actions,
    check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Disable an existing dual authorization policy for your service instance by
running the following cURL command.

    ```cURL
    curl -X PUT \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/instance/policies?policy=dualAuthDelete' \
      -H 'accept: application/vnd.ibm.kms.policy+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
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

    Replace the variables in the example request according to the following
    table.

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>

      <tr>
        <td>
          <varname>region</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The region abbreviation, such as
            <code>us-south</code> or <code>eu-de</code>, that represents the
            geographic area where your
            {{site.data.keyword.hscrypto}} instance
            resides.
          </p>
          <p>
            For more information, see
            [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints).
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}}
            access token. Include the full contents of the <code>IAM</code>
            token, including the Bearer value, in the cURL request.
          </p>
          <p>
            For more information, see
            [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token).
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>instance_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier that is assigned to
            your {{site.data.keyword.hscrypto}} service
            instance.
          </p>
          <p>
            For more information, see
            [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
          </p>
        </td>
      </tr>

      <caption style="caption-side:bottom;">
        Table 1. Describes the variables that are needed to enable dual
        authorization at the instance level.
      </caption>
    </table>

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
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/instance/policies?policy=dualAuthDelete' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'accept: application/vnd.ibm.kms.policy+json'
    ```
    {: codeblock}
