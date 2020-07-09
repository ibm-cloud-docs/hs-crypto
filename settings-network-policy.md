---

copyright:
  years: 2020
lastupdated: "2020-07-01"

keywords: instance settings, service settings, network access policies

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

# Managing network access policies for your service instance
{: #managing-network-access-policies}

After you set up your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}
instance, you manage network access policies by using the key management API.
{: shortdesc}

## Managing network access policy settings
{: #managing-network-access-policy-settings}

A network access policy for {{site.data.keyword.hscrypto}} instances is an extra policy that you can use to block a {{site.data.keyword.hscrypto}} instance from getting API requests from public or private networks.

The network access policy applies to newly provisioned and existing instances. For existing instances the network access policy is enforced after it is set.

The network access policy capability is available only through the {{site.data.keyword.hscrypto}} key management API. To find out more about
accessing the {{site.data.keyword.hscrypto}} APIs, check out [Setting up the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api). {: preview}

### Understanding network access policies
{: #understanding-network-access-policies}

Two options control network access to
{{site.data.keyword.hscrypto}} instances:

* Public and private network access - this is the default
* Private network access only

#### Public and private network access
{: #public-and-private}

The {{site.data.keyword.hscrypto}} instance accepts API
requests from both `public and private` endpoints.

Public and private network access is the default setting and is used if a policy
is not set.

For example, multiple teams are testing a solution that uses
{{site.data.keyword.hscrypto}} instances. Development and test
teams issue API requests from both outside (public endpoints) and inside
(private endpoints) the {{site.data.keyword.cloud_notm}}. You allow public and private API requests to
ensure each team has access to {{site.data.keyword.hscrypto}}
instances during this phase of the project.

#### Private network access only
{: #private-only}

The {{site.data.keyword.hscrypto}} instance accepts API
requests from only `private` endpoints.

For example, development and testing is complete and the solution that uses
{{site.data.keyword.hscrypto}} instances is in production. You
want to limit API requests to private networks for security reasons. All
{{site.data.keyword.hscrypto}} API requests must originate from
within the {{site.data.keyword.cloud_notm}}.

In the `Regions and endpoints` section there is a section that explains how to
[enable private endpoints](/docs/hs-crypto?topic=hs-crypto-regions#connectivity-options).

After the network access policy is set to `private-only` you cannot make any
{{site.data.keyword.hscrypto}} key management API calls from the public
network, including the API to change the policy. Make sure the private
environment is set up before setting the network access policy to
`private-only`. See
[using private endpoints](/docs/hs-crypto?topic=hs-crypto-private-endpoints).
{: note}

Before you set the network policy for your service instance, keep in mind the
following considerations:

* The network access policy is not enforced when a request for a {{site.data.keyword.hscrypto}} instance is deprovisioned.
* Setting and retrieving the network access policy is only supported through the application programming interface (API). After the network access policy is set to `private-only` the UI cannot be used for any {{site.data.keyword.hscrypto}} actions. Keys in a `private-only` instance will not be shown in the UI and any {{site.data.keyword.hscrypto}} actions in the UI will return an unauthorized error (HTTP status code 401).

### Enabling network access to your service instance
{: #enabling-network-access-to-your-service-instance}

As an admin, enable a network access policy for a {{site.data.keyword.hscrypto}} instance by making a `PUT` call to the following endpoint. See these API references to [set](/apidocs/hs-crypto#set-instance-policies){: external} and [list](/apidocs/hs-crypto#list-instance-policies){: external} instance policies.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/instance/policies?policy=allowedNetwork
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To change a network access policy, you must be assigned a _Manager_ access
    policy for your service instance. To learn how IAM (identity and access
    management) roles map to {{site.data.keyword.hscrypto}}
    service actions, check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Enable a network access policy for your service instance by running the
following cURL command.

    ```cURL
    curl -X PUT \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/instance/policies?policy=allowedNetwork' \
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
            "policy_type": "allowedNetwork",
            "policy_data": {
              "enabled": <enabled>,
              "attributes": {
                "allowed_network": "<access_type>"
              }
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

      <tr>
        <td>
          <varname>enabled</varname>
        </td>
        <td>
          <strong>Required.</strong> Set to <code>true</code> to enable a
          network access policy. Set to <code>false</code> to remove the network
          access policy, that is, the policy is not enforced.
        </td>
      </tr>

      <tr>
        <td>
          <varname>access_type</varname>
        </td>
        <td>
          <strong>Required.</strong> The network access policy to apply to your
          {{site.data.keyword.hscrypto}} instance.
          Acceptable values are <code>public-and-private</code> or
          <code>private-only</code>.
        </td>
      </tr>

      <caption style="caption-side:bottom;">
        Table 1. Describes the variables that are needed to set a network access
        policy at the instance level.
      </caption>
    </table>

    A successful request returns an HTTP `204 No Content` response, which
    indicates that your service instance now enforces a network access policy.
    API requests to the service are restricted to the policy you set.

    This policy applies to {{site.data.keyword.hscrypto}}
    instances only. The network access policy does not apply to specific keys.

3. Optional: Verify that the network access policy was created by browsing the
policies that are available for your
{{site.data.keyword.hscrypto}} instance.

    ```cURL
    curl -X GET \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/instance/policies?policy=allowedNetwork' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'accept: application/vnd.ibm.kms.policy+json'
    ```
    {: codeblock}

## What's next
{: #managing-network-access-policies-next-steps}

These are key management API references to set and list instance policies.

* [Set instance policies](/apidocs/hs-crypto#set-instance-policies){: external}
* [List instance policies](/apidocs/hs-crypto#list-instance-policies){: external}
