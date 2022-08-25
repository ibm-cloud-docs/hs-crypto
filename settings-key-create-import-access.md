---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-25"

keywords: instance settings, service settings, key creation/import, key create policy, key creation/import, key policy

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Managing the key create and import access policy
{: #manage-keyCreateImportAccess}

After you set up your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}
instance, you can manage the key create and import access policy by using the
{{site.data.keyword.hscrypto}} key management service API.
{: shortdesc}

This policy applies only to key management service keys and related operations.
{: important}

## Understanding the key create and import access settings
{: #understand-keyCreateImportAccess-instance-policy}

The Key create and import access policy for
{{site.data.keyword.hscrypto}} instances manage
how keys are created and imported into your
{{site.data.keyword.hscrypto}} instance.

When you enable this policy, {{site.data.keyword.hscrypto}}
only permits the creation or importation of keys in your
{{site.data.keyword.hscrypto}} instance that follow the key
creation and importation settings that are listed on the key create and import access policy.

Setting and retrieving the key create and import access policy is supported through the
API only. To find out more about accessing
the {{site.data.keyword.hscrypto}} key management service API, check out
[Setting up the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

Before you enable the key create and import access policy for your
{{site.data.keyword.hscrypto}} instance, keep in mind the
following considerations:

- KeyCreateImportAccess policies do not affect keys that existed before policy creation.

    KeyCreateImportAccess policies affect only {{site.data.keyword.hscrypto}} requests that are sent after the policy is set. You still have access to all keys that existed in your {{site.data.keyword.hscrypto}} instance before the policy is created.

- KeyCreateImportAccess policies can affect your keys across various key actions.

    The `enforce_token` attribute affects imported keys during creation, rotation, and restoration. The `create_root_key`, `import_root_key`, `create_standard_key`, and `import_standard_key` attributes affect keys only at creation time. All other {{site.data.keyword.hscrypto}} actions, such as wrap and unwrap, are not affected and can be invoked on the key as usual.

## Enabling or updating the key create and import access policy for your service instance with the console
{: #enable-keyCreateImportAccess-policy-console}
{: ui}

As a security administrator, if you prefer to manage the key create and import access policy settings by using a graphical interface, you can use the {{site.data.keyword.cloud_notm}} console.

After you create a {{site.data.keyword.hscrypto}} instance,
complete the following steps to enable the key create and import access policy:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://{DomainName}/){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. In the UI of the selected service instance, select the **Instance policies** tab in the side menu.
5. In the **Create and import key access** section, check or clear the corresponding boxes to update the keyCreateImportAccess settings, and then click **Save policy**.

    - `Allow creation of root keys`: Check the box to allow root keys to be created in your {{site.data.keyword.hscrypto}} instance.
    - `Allow creation of standard keys`: Check the box to allow standard keys to be created in your {{site.data.keyword.hscrypto}} instance.
    - `Allow import of root keys`: Check the box to allow root keys to be imported into your {{site.data.keyword.hscrypto}} instance.
    - `Allow import of standard keys`: Check the box to allow standard keys to be imported into your {{site.data.keyword.hscrypto}} instance.
    - `Enable secure import`: Check the box to prevent authorized users from importing key material into your {{site.data.keyword.hscrypto}} instance without using an import token.

    After you check the box for `Enable secure import`, it is required that [secure import](/docs/hs-crypto?topic=hs-crypto-create-import-tokens) is enabled for all key import actions. Secure import is not available in the {{site.data.keyword.cloud_notm}} console, and you need to perform further actions through the CLI or API.
    {: note}

Any disabled key actions are not available in the **Add key** panel. After you check the box for `Secure import`, it is required that [secure import](/docs/hs-crypto?topic=hs-crypto-create-import-tokens) is enabled for all key import actions. Key import is not available in the {{site.data.keyword.cloud_notm}} console, and you need to perform further actions through the CLI or API.
{: note}

## Enabling and updating the key create and import access policy for your service instance with the API
{: #enable-keyCreateImportAccess-policy-api}
{: api}

As a security administrator, you can enable or update the key create and import access policy for
a {{site.data.keyword.hscrypto}} instance by making a `PUT`
call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=keyCreateImportAccess
```
{: codeblock}

If you are updating the key create and import access policy of your {{site.data.keyword.hscrypto}}
instance, keep in mind that if an attribute is
omitted from the request, the field is set to the default value and the
existing value for the omitted field is overwritten by the default value.
{: important}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To enable keyCreateImportAccess policies, you need _Manager_
    access to your {{site.data.keyword.hscrypto}}
    instance. To learn how IAM roles map to
    {{site.data.keyword.hscrypto}} actions, check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Enable or update the key create and import access policy for your
   {{site.data.keyword.hscrypto}} instance by running the
   following cURL command.

    ```sh
    $ curl -X PUT \
        "https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=keyCreateImportAccess" \
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
                        "policy_type": "keyCreateImportAccess",
                        "policy_data": {
                            "enabled": true,
                            "attributes": {
                                "create_root_key": <true/false>,
                                "create_standard_key": <true/false>,
                                "import_root_key": <true/false>,
                                "import_standard_key": <true/false>,
                                "enforce_token": <true/false>
                            }
                        }
                    }
                ]
            }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following
    table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south` or `eu-de`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `create_root_key` | **Required.** Set to `true` to allow root keys to be created in your {{site.data.keyword.hscrypto}} instance. Set to `false` to prevent root keys from being created in your instance. If this attribute is omitted, `true` is set as the default value. |
    | `create_standard_key` | **Required.** Set to `true` to allow standard keys to be created in your {{site.data.keyword.hscrypto}} instance. Set to `false` to prevent standard keys from being created in your instance. If this attribute is omitted, `true` is set as the default value. |
    | `import_root_key` | **Required.** Set to `true` to allow root keys to be imported into your {{site.data.keyword.hscrypto}} instance. Set to `false` to prevent root keys from being imported into your instance. If this attribute is omitted, `true` is set as the default value. |
    | `import_standard_key` | **Required.** Set to `true` to allow standard keys to be imported into your {{site.data.keyword.hscrypto}} instance. Set to `false` to prevent standard keys from being imported into your instance. If this attribute is omitted, `true` is set as the default value. |
    | `enforce_token` | **Required.** Set to `true` to prevent authorized users from importing key material into your {{site.data.keyword.hscrypto}} instance without using an import token. Set to `false` to allow authorized users to import key material into your instance without using an import token. If `enforce_token` is enabled, it is required that [secure import](/docs/hs-crypto?topic=hs-crypto-create-import-tokens) is enabled for all key import actions. Key import is not available through UI, and you need to perform further actions through the CLI or API. If this attribute is omitted, `false` is set as the default value. |
    {: caption="Table 1. Describes the variables that are needed to enable the key create and import access policy" caption-side="bottom"}

    A successful request returns an HTTP `204 No Content` response, which
    indicates that your {{site.data.keyword.hscrypto}}
    instance now has enabled.
    Your {{site.data.keyword.hscrypto}} instance can now only
    allow the creation or importation of keys from the methods that are specified in your
    request.

3. Optional: Verify that the key create and import access policy is created or updated by
   retrieving the policy details for your
   {{site.data.keyword.hscrypto}} instance.

    ```sh
    $ curl -X GET \
        "https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=keyCreateImportAccess" \
        -H "accept: application/vnd.ibm.kms.policy+json" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>"
    ```
    {: codeblock}

## Disabling the key create and import access policy for your service instance with the key management service API
{: #disable-key-create-import-policy-api}
{: api}

As a manager of a {{site.data.keyword.hscrypto}} instance, to disable the key create and import access policy with the key management service API, make a `PUT` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=keyCreateImportAccess
```
{: codeblock}

Do not provide any attributes when you make a request to disable your
key create and import access policy.
{: note}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To disable keyCreateImportAccess policies, you need a _Manager_
    access to your {{site.data.keyword.hscrypto}}
    instance. To learn how IAM roles map to
    {{site.data.keyword.hscrypto}} actions, check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Disable the existing key create and import access policy for your
   {{site.data.keyword.hscrypto}} instance by running the
   following cURL command.

    ```sh
    $ curl -X PUT \
        "https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=keyCreateImportAccess" \
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
                        "policy_type": "keyCreateImportAccess",
                        "policy_data": {
                            "enabled": false
                        }
                    }
                ]
            }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following
    table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    {: caption="Table 2. Describes the variables that are needed to disable the key create and import access policy" caption-side="bottom"}

    A successful request returns an HTTP `204 No Content` response, which
    indicates that the key create and import access policy is updated for your service
    instance.

3. Optional: Verify that the key create and import access policy is disabled by
   retrieving the policy details for your
   {{site.data.keyword.hscrypto}} instance.

    ```sh
    $ curl -X GET \
        "https://api.<region>.hs-crypto.cloud.ibm.com/api/v2/instance/policies?policy=keyCreateImportAccess" \
        -H "accept: application/vnd.ibm.kms.policy+json" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>"
    ```
    {: codeblock}
