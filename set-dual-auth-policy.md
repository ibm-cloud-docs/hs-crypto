---

copyright:
  years: 2017, 2022
lastupdated: "2022-04-21"

keywords: set deletion policy, dual authorization, policy-based, key deletion

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
{:term: .term}
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Setting dual authorization policies for keys
{: #set-dual-auth-key-policy}

You can use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to set dual
authorization policies for individual root keys or standard keys.
{: shortdesc}

Dual authorization is an extra policy that helps to prevent accidental or
malicious deletion of encryption keys in your
{{site.data.keyword.hscrypto}} instance. When you
enable this policy at the key level,
{{site.data.keyword.hscrypto}} requires an authorization from
two users to delete an encryption key.

After you enable dual authorization at the key level, the policy that is
associated with the key can no longer be changed to allow a single authorization
to delete the encryption key.
{: important}

To enable dual authorization settings at the instance level, check out
[Managing service settings](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth).
{: tip}

## Managing dual authorization policies with the key management service API
{: #manage-dual-auth-key-policies-api}

Consider the following items before you enable dual authorization for a key:

- **Determine whether a dual authorization policy is required for the key.**
As a security admin, assess the sensitivity of your workload to determine
whether a key requires a dual authorization policy based on your requirements.
After you enable dual authorization for a key, the policy can no longer be
changed to allow a single authorization to delete the key.
- **Determine who can authorize deletion of your {{site.data.keyword.hscrypto}} resources.**
After you create a dual authorization policy for a key, the key will require
[an action from two users](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys)
before it can be deleted. Be sure to identify two distinct users with the
[appropriate levels of access](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles)
to the instance or key.

To learn how to delete a key that has a dual authorization policy, see
[Deleting keys using dual authorization](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys).

### Viewing a dual authorization policy for a key
{: #view-dual-auth-key-policy-api}

For a high-level view, you can retrieve the dual authorization policy for a
single key by making a `GET` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/policies?policy=dualAuthDelete
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To work with dual authorization policies, you must be assigned a _Manager_
    access policy for the instance or key. To learn how IAM roles map to
    {{site.data.keyword.hscrypto}} actions, check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Retrieve the dual authorization policy for a specified key by running the
following cURL command.

    ```cURL
    curl -X GET \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/policies?policy=dualAuthDelete' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'accept: application/vnd.ibm.kms.policy+json'
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
          <varname>key_ID</varname>
        </td>
        <td>
          <strong>Required.</strong> The unique identifier for the key that has
          an existing rotation policy.
        </td>
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
            your {{site.data.keyword.hscrypto}}
            instance.
          </p>
          <p>
            For more information, see
            [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
          </p>
        </td>
      </tr>

      <caption>
        Table 1. Describes the variables that are needed to view a dual
        authorization policy for a key with the
        {{site.data.keyword.hscrypto}} key management service API.
      </caption>
    </table>

    A successful request returns dual authorization policy details that are
    associated with your key. The following JSON object shows an example
    response for a key that has an existing dual authorization policy.

    ```json
    {
      "metadata": {
        "collectionTotal": 1,
        "collectionType": "application/vnd.ibm.kms.policy+json"
      },
      "resources": [
        {
          "id": "02fd6835-6001-4482-a892-13bd2085f75d",
          "crn": "crn:v1:bluemix:public:hs-crypto:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:12e8c9c2-a162-472d-b7d6-8b9a86b815a6:key:02fd6835-6001-4482-a892-13bd2085f75d",
          "dualAuthDelete": {
            "enabled": true
          },
          "createdBy": "...",
          "creationDate": "2020-03-10T20:41:27Z",
          "updatedBy": "...",
          "lastUpdateDate": "2020-03-16T20:41:27Z"
        }
      ]
    }
    ```
    {: screen}

    For keys that do not have an existing dual authorization policy, the
    following JSON shows an example response.

    ```json
    {
      "metadata": {
        "collectionTotal": 0,
        "collectionType": "application/vnd.ibm.kms.policy+json"
      }
    }
    ```
    {: screen}

### Creating a dual authorization policy for a key
{: #create-dual-auth-key-policy-api}

Create a dual authorization policy for single key by making a `PUT` call to the
following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/policies?policy=dualAuthDelete
```
{: codeblock}

After you enable a dual authorization policy for a single key, the policy cannot
be reverted.
{: important}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To work with dual authorization policies, you must be assigned a _Manager_
    access policy for the instance or key. To learn how IAM roles map to
    {{site.data.keyword.hscrypto}} actions, check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Enable dual authorization for a specified key by running the following cURL
command.

    ```cURL
    curl -X PUT \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/policies?policy=dualAuthDelete' \
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
          <varname>key_ID</varname>
        </td>
        <td>
          <strong>Required.</strong> The unique identifier for the key that you
          want to create a dual authorization policy for.
        </td>
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
            {{site.data.keyword.hscrypto}} instance resides.
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
          access token. Include the full contents of the <code>IAM</code> token,
          including the Bearer value, in the cURL request.
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
            your {{site.data.keyword.hscrypto}}
            instance.
          </p>
          <p>
            For more information, see
            [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
          </p>
        </td>
      </tr>

      <caption>
        Table 2. Describes the variables that are needed to update a dual
        authorization policy with the
        {{site.data.keyword.hscrypto}} key management service API.
      </caption>
    </table>

    A successful request returns a `200 OK` response with dual authorization
    policy details for your key. The following JSON object shows an example
    response.

    ```json
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.policy+json",
        "collectionTotal": 1
      },
      "resources": [
        {
          "id": "2291e4ae-a14c-4af9-88f0-27c0cb2739e2",
          "crn": "crn:v1:bluemix:public:hs-crypto:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:30372f20-d9f1-40b3-b486-a709e1932c9c:key:2291e4ae-a14c-4af9-88f0-27c0cb2739e2",
          "dualAuthDelete": {
            "enabled": true
          },
          "createdBy": "...",
          "creationDate": "2020-03-10T20:41:27Z",
          "updatedBy": "...",
          "lastUpdateDate": "2020-03-16T20:41:27Z"
        }
      ]
    }
    ```
    {: screen}

    The key now requires an authorization from two users before it can be
    deleted.

    For more information, see
    [Deleting keys using dual authorization](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys).
