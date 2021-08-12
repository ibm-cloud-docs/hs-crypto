---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-12"

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

# Managing the network access policy
{: #managing-network-access-policies}

After you set up your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance, you manage network access policy by using the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

Before you update the network access policy, you need to initialize the service instance first. See [Initializing service instances with the IBM Cloud TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) for instructions.
{: important}

For more information about how the network access differs, see [Understanding the network access policy](/docs/hs-crypto?topic=hs-crypto-secure-connection#understand-network-access-policies).

## Updating the network access policy for your {{site.data.keyword.hscrypto}} instance with the console
{: #update-network-access-policy-ui}

As a security administrator, if you prefer to update the network access policy for your instance by using a graphical interface, you can use the {{site.data.keyword.cloud_notm}} console.

After the network access policy is set to `private-only`, the UI cannot be used for any {{site.data.keyword.hscrypto}} actions.  Any
{{site.data.keyword.hscrypto}} operations in the UI return an unauthorized error (HTTP status code 401).
{: note}

After you create a {{site.data.keyword.hscrypto}} instance, complete the following steps to create a network access policy:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://{DomainName}/){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. In the UI of the selected service instance, select the **Instance policies** tab in the side menu.
5. In the **Allowed network** section, select the network that you want traffic to come through, and click **Save policy**. The default network policy is public and private, which allows access from both public and private networks.

    If a private-only network is enabled, you are not able to view or manage keys through the UI. However, you can still adjust the network setting later by using the API or CLI.
    {: note}

## Updating the network access policy for your {{site.data.keyword.hscrypto}} instance with the key management API
{: #update-network-access-policy-api}

As a security administrator, update the network access policy for your {{site.data.keyword.hscrypto}} instance by making a `PUT` call to the following endpoint. See these API references to [set](/apidocs/hs-crypto#putinstancepolicy){: external} and [list](/apidocs/hs-crypto#getinstancepolicy){: external} instance policies.

```
https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=allowedNetwork
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To change a network access policy, you must be assigned a _Manager_ access policy for your {{site.data.keyword.hscrypto}} instance. To learn how IAM (identity and access management) roles map to {{site.data.keyword.hscrypto}} service actions, check out [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Update the network access policy for your {{site.data.keyword.hscrypto}} instance by running the following cURL command.

    ```sh
    $ curl -X PUT \
        "https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=allowedNetwork" \
        -H "accept: application/vnd.ibm.kms.policy+json" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>" \
        -H "content-type: application/vnd.ibm.kms.policy+json" \
        -d '{
                "metadata": {
                    "collectionType": "application/vnd.ibm.kms.policy+json",
                    "collectionTotal": 1
                },
                "resources": [
                    {
                        "policy_type": "allowedNetwork",
                        "policy_data": {
                            "enabled": true,
                            "attributes": {
                                "allowed_network": "<access_type>"
                            }
                        }
                    }
                ]
            }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

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
            <strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>eu-de</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides.
          </p>
          <p>
            For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>port</varname></td>
        <td><strong>Required.</strong> The port number of the API endpoint.</td>
      </tr>
      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request.
          </p>
          <p>
            For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <varname>instance_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service
            instance.
          </p>
          <p>
            For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <varname>enabled</varname>
        </td>
        <td>
          <strong>Required.</strong> Set to <code>true</code> to enable a network access policy.
        </td>
      </tr>
      <tr>
        <td>
          <varname>access_type</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The network access policy to apply to your {{site.data.keyword.hscrypto}} instance. Acceptable values are <code>public-and-private</code> or <code>private-only</code>.
          </p>
          <p>
            After the network access policy is set to <code>private-only</code>, you cannot access your instance from the public network and cannot view or manage keys through the UI. However, you can still adjust the network setting later using the API or CLI.
          </p>
        </td>
      </tr>

      <caption>
        Table 1. Describes the variables that are needed to set a network access policy at the instance level.
      </caption>
    </table>

    A successful request returns an HTTP `204 No Content` response, which indicates that your {{site.data.keyword.hscrypto}} instance
    now enforces a network access policy. API requests to the service are restricted to the policy you set.

    This policy applies to {{site.data.keyword.hscrypto}} instances only. The network access policy does not apply to specific keys.

3. Optional: Verify that the network access policy is created by browsing the policies that are available for your {{site.data.keyword.hscrypto}} instance.

    ```sh
    $ curl -X GET \
        "https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=allowedNetwork" \
        -H "accept: application/vnd.ibm.kms.policy+json" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>"
    ```
    {: codeblock}

## Updating the network access policy for your {{site.data.keyword.hscrypto}} instance with the CLI
{: #update-network-access-policy-cli}

You can also update the network access policy for your {{site.data.keyword.hscrypto}} instance using the CLI. For more information, see [the CLI reference](/docs/key-protect?topic=key-protect-cli-plugin-key-protect-cli-reference#kp-instance-policy-update-allowed){: external}.

## Disabling the network access policy for your {{site.data.keyword.hscrypto}} instance with the key management API
{: #disable-network-access-policy-api}

As a security administrator, disable a network access policy for a {{site.data.keyword.hscrypto}} instance by making a `PUT` call to the following endpoint. See these API references to [set](/apidocs/hs-crypto#putinstancepolicy){: external} and [list](/apidocs/hs-crypto#getinstancepolicy){: external} instance policies.

```
https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=allowedNetwork
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To change a network access policy, you must be assigned a _Manager_ access policy for your {{site.data.keyword.hscrypto}} instance. To learn how IAM (identity and access management) roles map to {{site.data.keyword.hscrypto}} service actions, check out [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Disable a network access policy for your {{site.data.keyword.hscrypto}} instance by running the following cURL command.

    ```sh
    $ curl -X PUT \
        "https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=allowedNetwork" \
        -H "accept: application/vnd.ibm.kms.policy+json" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>" \
        -H "content-type: application/vnd.ibm.kms.policy+json" \
        -d '{
                "metadata": {
                    "collectionType": "application/vnd.ibm.kms.policy+json",
                    "collectionTotal": 1
                },
                "resources": [
                    {
                        "policy_type": "allowedNetwork",
                        "policy_data": {
                            "enabled": false,
                            "attributes": {
                                "allowed_network": "private-only"
                            }
                        }
                    }
                ]
            }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

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
            <strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>eu-de</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides.
          </p>
          <p>
            For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.
          </p>
        </td>
      </tr>

      <tr>
        <td><varname>port</varname></td>
        <td><strong>Required.</strong> The port number of the API endpoint.</td>
      </tr>

      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request.
          </p>
          <p>
            For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>instance_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance.
          </p>
          <p>
            For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>enabled</varname>
        </td>
        <td>
          <strong>Required.</strong> Set to <code>false</code> to remove the network access policy, that is, the policy is not enforced and your service instance is back to the default state where both the public and private network access are allowed.
        </td>
      </tr>

      <caption>
        Table 2. Describes the variables that are needed to disable a network access policy at the instance level.
      </caption>
    </table>

    A successful request returns an HTTP `204 No Content` response, which indicates that the network access policy of your {{site.data.keyword.hscrypto}} instance is updated.

3. Optional: Verify that the network access policy is disabled by browsing the policies that are available for your
   {{site.data.keyword.hscrypto}} instance.

    ```sh
    $ curl -X GET \
        "https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=allowedNetwork" \
        -H "accept: application/vnd.ibm.kms.policy+json" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>"
    ```
    {: codeblock}
