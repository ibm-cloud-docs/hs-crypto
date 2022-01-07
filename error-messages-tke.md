---

copyright:
  years: 2021, 2022
lastupdated: "2022-01-07"

keywords: error message, error code, error, tke error, tke error message, hpcs error messages, hyper protect crypto services error message

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:external: target="_blank" .external}
{:note: .note}
{:screen: .screen}
{:pre: .pre}

# Error messages for Trusted Key Entry
{: #error-messages-tke}

This topic lists error messages that you might encounter when you use the cloud Trusted Key Entry (TKE) CLI plug-in or the TKE application.
{: shortdesc}

This is not a complete list of error messages. Some messages that are created by other systems, such as {{site.data.keyword.iamshort}} (IAM), and are then passed to {{site.data.keyword.hscrypto}} are not covered.
{: note}

## Table of contents
{: #error-messages-tke-toc}

The error messages are sorted by alphabetical order and by HTTP status code.

### Sorted by alphabetical order of error messages
{: #error-messages-tke-sorted-by-alphabetical-order}

These are the error messages sorted by the alphabetical order.

1. Change not allowed. You are not allowed to change a threshold value if the corresponding attribute control bit is reset. - [details](#error-messages-tke-no-change-threshold-err)
2. No service instances were found for the current resource group. - [details](#error-messages-tke-no-instance-err)
3. Unauthorized: Your access token is invalid, expired, or does not have the necessary permissions to access this instance. - [details](#error-messages-tke-unauthorized-err)

### Sorted by HTTP status code
{: #error-message-tke-sorted-by-http-status-code}

These are the error messages sorted by the HTTP status code.

<table>
    <tr>
    <th>Status code</th>
    <th>Error message</th>
    </tr>
    <tr>
    <td>HTTP 400 - Bad Request</td>
    <td>
    </td>
    </tr>
    <tr>
    <td>HTTP 401 - Unauthorized</td>
    <td>Unauthorized: Your access token is invalid, expired, or does not have the necessary permissions to access this instance. - <a href="#error-messages-tke-unauthorized-t-err">details</a></td>
    </tr>
    <tr>
    <td>HTTP 403 - Forbidden</td>
    <td>
    </td>
    </tr>
    <tr>
    <td>HTTP 409 - Conflict</td>
    <td>
    </td>
    </tr>
    <tr>
    <td>HTTP 410 - Gone</td>
    <td></td>
    </tr>
    <tr>
    <td>HTTP 422 - Unprocessable Entity</td>
    <td>
    </td>
    </tr>
    <tr>
    <td>HTTP 500 - Internal Server Error</td>
    <td></td>
    </tr>
</table>


## 1 - Change not allowed...
{: #error-messages-tke-no-change-threshold-err}

### Message
{: #error-messages-tke-no-change-threshold-err-message}

Change not allowed. You are not allowed to change a threshold value if the corresponding attribute control bit is reset.

### Context
{: #error-messages-tke-no-change-threshold-err-context}

This error occurs when you use the TKE plug-in or the TKE application to set the signature thresholds. The TKE through version 0.0.11 restricts the ability to set the signature threshold and revocation signature threshold to a value other than one. The restriction can be removed by zeroizing the crypto units.

- If you use the TKE CLI plug-in, run the following command to zeroize the crypto units:

  ```
  ibmcloud tke cryptounit-zeroize
  ```
    {: pre}

- If you use the TKE application, select the **Imprint mode** tab and click **Zeroize crypto unit**.

After the zeroization, you need to set the threshold values by using the latest version of the TKE plug-in or the Trusted Key Entry application. To fully recover the state of a crypto unit, you also need to reload the master key registers and the administrators. Depending on your loading method, see [Loading master keys with the TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#load-master-keys) or [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities#load-master-key-management-utilities) for instructions.

## 2 - No service instances were found...
{: #error-messages-tke-no-instance-err}

### Message
{: #error-messages-tke-no-instance-err-message}

No service instances were found for the current resource group.

### Context
{: #error-messages-tke-no-instance-err-context}

This error occurs you use `ibmcloud tke cryptounits` to list crypto units.

It might be caused by one of the following reasons:

- You haven't logged in to the correct region or resource group where your service instance resides.
- If you have multiple accounts, you are not using the correct account with which your service instance is created. Or, your account doesn't have the permission to view the service instance.

Try the following solutions to solve the problem:

- Make sure that you are logged in to the correct region and resource group with the following command:

    ```
    ibmcloud target -r <region> -g <resource_group>
    ```
    {: pre}

- Make sure that your account is assigned the _Manager_ [service access role](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles) to list the crypto units. The account with which you create the service instance is granted as the _Administrator_ role by default and can assign various roles that correspond to the specific {{site.data.keyword.hscrypto}} permissions. For more information about roles and permissions, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).

## 3 - Unauthorized: Your access token is invalid...
{: #error-messages-tke-unauthorized-err}

### Message
{: #error-messages-tke-unauthorized-err-message}

Unauthorized. Your access token is invalid, expired, or does not have the necessary permissions to access this instance.

### HTTP status code
{: #error-messages-tke-unauthorized-err-http}

401 - Unauthorized

The HTTP `401 Unauthorized` client error status response code indicates that the
request has not been applied because it lacks valid authentication credentials
for the target resource.

### Context
{: #error-messages-tke-unauthorized-err-context}

This error occurs when you use the cloud TKE CLI plug-in or the TKE application to send requests to the {{site.data.keyword.hscrypto}} instance with an expired authentication token. An authentication token is created when you log in to the {{site.data.keyword.cloud_notm}}, but it expires after 1 hour. After 1 hour, you must log in again to continue to send requests to the {{site.data.keyword.cloud_notm}}.

- If you use the TKE CLI plug-in, log in to the {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command.
- If you use the TKE application, select the **Crypto units** tab and click **Refresh Panel**.
