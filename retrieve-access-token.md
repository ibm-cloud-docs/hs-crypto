---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-02"

keywords: access token, IAM token, generate access token, generate IAM token, get access token, get IAM token, IAM token API, IAM token CLI

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Retrieving an access token
{: #retrieve-access-token}

Get started with the {{site.data.keyword.hscrypto}} APIs by authenticating your requests to the service with an {{site.data.keyword.iamlong}} (IAM) access token.
{: shortdesc}

## Retrieving an access token with the CLI
{: #retrieve-token-cli}

You can use the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started) to quickly generate your personal Cloud IAM access token.

1. Log in to {{site.data.keyword.cloud_notm}} with the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started).

    ```sh
    ibmcloud login
    ```
    {: pre}

    If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.
    {: note}

3. Select the region and resource group where you would like to create a {{site.data.keyword.hscrypto}} service instance. You can use the following command to set your target region and resource group.

    ```sh
    ibmcloud target -r <region_name> -g <resource_group_name>
    ```
    {: pre}

3. Run the following command to retrieve your Cloud IAM access token.

    ```sh
    ibmcloud iam oauth-tokens
    ```
    {: pre}

    The following truncated example shows a retrieved IAM token.

    ```sh
    IAM token:  Bearer eyJraWQiOiIyM...
    ```
    {: screen}

## Retrieving an access token with the API
{: #retrieve-token-api}

You can also retrieve your access token programmatically by first creating a [service ID API key](/docs/iam?topic=iam-serviceidapikeys) for your application, and then exchanging your API key for an {{site.data.keyword.cloud_notm}} IAM token.

1. Log in to {{site.data.keyword.cloud_notm}} with the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started).

  ```sh
  ibmcloud login
  ```
  {: pre}

  If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.
  {: note}

2. Select the account, region, and resource group that contain your provisioned instance of {{site.data.keyword.hscrypto}}.

3. Create a [service ID](/docs/iam?topic=iam-serviceids#creating-a-service-id) for your application.

  ```sh
  ibmcloud iam service-id-create <service_ID_name>
                     [-d, --description DESCRIPTION]
  ```
  {: pre}

4. [Assign an access policy](/docs/iam?topic=iam-serviceidpolicy) for the service ID.

    You can assign access permissions for your service ID [by using the {{site.data.keyword.cloud_notm}} console](/docs/iam?topic=iam-serviceidpolicy#access_new). To learn how the _Manager_, _Writer_, and _Reader_ access roles map to specific {{site.data.keyword.keymanagementserviceshort}} service actions, see [Roles and permissions](/docs/services/hs-crypto?topic=hs-crypto-manage-access#roles).
    {: tip}

5. Create a [service ID API key](/docs/iam?topic=iam-serviceidapikeys).

  ```sh
  ibmcloud iam service-api-key-create <API_key_name><service_ID_name>
                     [-d, --description DESCRIPTION]
                     [--file FILE_NAME]
  ```
  {: pre}

  Replace `<service_ID_name>` with the unique alias that you assigned to your service ID in the previous step. Save your API key by downloading it to a secure location.

6. Call the [IAM Identity Services API](https://{DomainName}/apidocs/iam-identity-token-api) to retrieve your access token.

  ```cURL
  curl -X POST \
    "https://iam.cloud.ibm.com/identity/token" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -H "Accept: application/json" \
    -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_key>" > token.json
  ```
  {: codeblock}

    In the request, replace `<API_key>` with the API key that you created in the previous step. The following truncated example shows the contents of the `token.json` file:

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    Use the full `access_token` value, prefixed by the _Bearer_ token type, to programmatically manage keys for your service using the {{site.data.keyword.hscrypto}} API. To see an example {{site.data.keyword.hscrypto}} API request, check out [Forming your key management API request](/docs/services/hs-crypto?topic=hs-crypto-set-up-api#form-kms-api-request).

    Access tokens are valid for 1 hour, but you can regenerate them as needed. To maintain access to the service, regenerate the access token for your API key on a regular basis by calling the [IAM Identity Services API](https://{DomainName}/apidocs/iam-identity-token-api).   
    {: note }
