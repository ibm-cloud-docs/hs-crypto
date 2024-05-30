---

copyright:
  years: 2018, 2024
lastupdated: "2024-05-30"

keywords: access token, api key, iam token, generate access token, generate iam token, get access token, iam token api, token cli

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Retrieving an access token
{: #retrieve-access-token}

Get started with the {{site.data.keyword.hscrypto}} key management service API by authenticating your requests to the service with an {{site.data.keyword.iamlong}} (IAM) access token.
{: shortdesc}

An access token is a temporary credential that expires after 1 hour. After the acquired token expires, you must generate a new token to continue calling {{site.data.keyword.cloud_notm}} or service APIs. To maintain access to the service, regenerate the access token for your API key regularly.
{: important}

## Retrieving an access token with the CLI
{: #retrieve-token-cli}
{: cli}

You can use the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started) to quickly generate your personal Cloud IAM access token.

1. Log in to {{site.data.keyword.cloud_notm}} with the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).

    ```sh
    ibmcloud login
    ```
    {: pre}

    If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.
    {: note}

2. Select the region and resource group where you would like to create a {{site.data.keyword.hscrypto}} service instance. You can use the following command to set your target region and resource group.

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
{: api}

You can also retrieve your access token programmatically by using an [API key](/docs/account?topic=account-manapikey), and then exchanging your API key for an {{site.data.keyword.cloud_notm}} IAM token. Depending on whether you create the access token for a user or an application, use your [{{site.data.keyword.cloud_notm}} user API key](/docs/account?topic=account-userapikey) or a [service ID API key](/docs/account?topic=account-serviceidapikeys) accordingly.

1. Log in to {{site.data.keyword.cloud_notm}} with the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).

    ```sh
    ibmcloud login
    ```
    {: pre}

    If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.
    {: note}

2. Select the region and resource group that contain your provisioned {{site.data.keyword.hscrypto}} instance with the following command:

    ```sh
    ibmcloud target -r <region_name> -g <resource_group_name>
    ```
    {: pre}

3. Create an API key.

    - If you want to retrieve an access token for a user, create a user API key with the following command:

        ```sh
        ibmcloud iam api-key-create <API_key_name>
            [-d, --description <description>]
            [--file <API_key_file_name>]
        ```
        {: pre}

        Specify the API key a unique name with the `<API_key_name>` parameter. Make sure to save your API key for later use by either using the `<API_key_file_name>` parameter or copying the API key value from the command response.

    - If you want to retrieve an access token for an application, create a service ID API key by completing the following steps:

        1. Create a [service ID](/docs/account?topic=account-serviceids#create_serviceid) for your application with the following command:

            ```sh
            ibmcloud iam service-id-create <service_ID_name>
                [-d, --description <description>]
            ```
            {: pre}

            Specify the service ID a unique name with the `<service_ID_name>` parameter.

        2. Create a service ID API key with the following command:

            ```sh
            ibmcloud iam service-api-key-create <API_key_name> <service_ID_name>
                [-d, --description <description>]
                [--file <API_key_file_name>]
            ```
            {: pre}

            Specify the API key a unique name with the `<API_key_name>` parameter and replace `<service_ID_name>` with the unique alias that you assigned to your service ID in the previous step. Make sure to save your API key for later use by either using the `<API_key_file_name>` parameter or copying the API key value from the command response.

4. [Assign the user or the service ID the appropriate access](/docs/account?topic=account-assign-access-resources) to your {{site.data.keyword.hscrypto}} instance based on your access policy.

    To learn how the IAM access roles map to specific {{site.data.keyword.hscrypto}} service actions, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles).
    {: tip}

5. Call the [IAM Identity Services API](/apidocs/iam-identity-token-api#gettoken-apikey) to retrieve your access token.

    ```cURL
    curl -X POST \
      "https://iam.cloud.ibm.com/identity/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=<API_key>" > token.json
    ```
    {: codeblock}

    In the request, replace `<API_key>` with the user API key or the service ID API key that you created in the previous step. The following truncated example shows the contents of the `token.json` file:

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

    Use the full `access_token` value, prefixed by the **Bearer** token type, to programmatically manage keys for your service using the {{site.data.keyword.hscrypto}} key management service API. To see an example {{site.data.keyword.hscrypto}} key management service API request, check out [Forming your key management service API request](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api#form-kms-api-request).
