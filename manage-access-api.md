---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-01"

Keywords: instance ID, account ID, Access Management, IBM Cloud

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:external: target="_blank" .external}

# Managing access to keys
{: #manage-access-api}

With {{site.data.keyword.iamlong}}, you can enable granular access control for your encryption keys by creating and modifying access policies.
{: shortdesc}

## Before you begin
{: #prereqs-manage-api}

To work with the API, generate your authentication credentials, such as your [access token](/docs/services/hs-crypto?topic=hs-crypto-retrieve-access-token) and [instance ID](/docs/services/hs-crypto?topic=hs-crypto-retrieve-instance-ID). You also need the ID of the {{site.data.keyword.hscrypto}} key that you want to manage access for.

To learn about viewing key IDs, see [Viewing keys](/docs/services/hs-crypto?topic=hs-crypto-view-keys).
{: tip}

### Retrieving your account ID
{: #retrieve-account-ID}

After you've retrieved your credentials, determine the scope of access for your new access policy by retrieving the ID of the account that contains your {{site.data.keyword.hscrypto}} instance (service instance for short).

To retrieve your account ID, complete the following steps:

1. Log in to the {{site.data.keyword.cloud_notm}} CLI.
    ```sh
    ibmcloud login [--sso]
    ```
    {: codeblock}

    **Note**: The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

    The result displays the identifying information for your account.

    ```sh
    Authenticating...
    OK

    Select an account (or press enter to skip):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Enter a number> 1
    Targeted account sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    API endpoint:   https://api.us-south.cf.cloud.ibm.com (API version: 2.75.0)
    Region:         us-south
    User:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}

2. Copy the value for your account ID.

    The _b6hnh3560ehqjkf89s4ba06i367801e_ value is an example account ID.

### Retrieving the user ID
{: #retrieve-user-ID}

Retrieve the user ID of the user whose access you would like to modify.

To retrieve the user ID, complete the following steps:

1. [Ask the user to provide an IAM token](/docs/services/hs-crypto?topic=hs-crypto-retrieve-access-token).
    The IAM token structure is as follows:

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Copy the middle value and run the following command:
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    The result shows a JSON object similar to the following example:
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. Copy the value of the `id` property.

## Creating an access policy
{: #create-policy}

To enable access control for a specific key, you can send a request to {{site.data.keyword.iamshort}} by running the following command. Repeat the command for each access policy.

```cURL
curl -X POST \
  https://iam.cloud.ibm.com/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<account_ID>",
      "region": "<region>",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

**Optional:** Verify that the policy was successfully created.

```cURL
curl -X GET \
  https://iam.cloud.ibm.com/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Updating an access policy
{: #update-policy}

You can use a retrieved policy ID to modify an existing policy for a user. Send a request to {{site.data.keyword.iamshort}} by running the following command:

```cURL
curl -X PUT \
  https://iam.cloud.ibm.com/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'If-Match': <ETag_ID> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<account_ID>",
      "region": "<region>",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

Replace `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>`, and `<key_ID>` with the appropriate values.

**Optional:** Verify that the policy was successfully updated.

```cURL
curl -X GET \
  https://iam.cloud.ibm.com/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Deleting an access policy
{: #delete-policy}

You can use a retrieved policy ID to delete an existing policy for a user. Send a request to {{site.data.keyword.iamshort}} by running the following command:

```cURL
curl -X DELETE \
  https://iam.cloud.ibm.com/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Replace `<account_ID>`, `<user_ID>`, `<policy_ID>`, and  `<Admin_IAM_token>` with the appropriate values.

**Optional:** Verify that the policy was successfully deleted.

```cURL
curl -X GET \
  https://iam.cloud.ibm.com/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}
