---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-09"

keywords: troubleshoot, problems, known issues, can't delete service, can't use hyper protect crypto services, can't create key, can't delete key

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:external: target="_blank" .external}
{:support: data-reuse='support'}
{:term: .term}

# Troubleshooting
{: #troubleshooting}

General problems with using {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} might include providing the correct headers or credentials when you interact with the API. In many cases, you can recover from these problems by following a few easy steps.
{: shortdesc}

When using `ibmcloud` CLI, to get the detailed error message, set `IBMCLOUD_TRACE=true`.
{: tip}

## Blocked PIN on EP11 smart card
{: #troubleshoot-block-smart-card}
{: troubleshoot}
{: support}

You try to use an EP11 smart card for an operation that requires personal identification number (PIN) entry and get an error similar to the following error:
{: tsSymptoms}

![Blocked PIN on EP11 smart card](/image/blocked_PIN.gif "Blocked PIN on EP11 smart card"){: caption="Figure 1. Blocked PIN on EP11 smart card" caption-side="bottom"}

If an incorrect PIN is entered on an EP11 smart card 3 times, the smart card becomes blocked and can't be used for operations that require PIN entry.
{: tsCauses}

Take the following steps to unblock the EP11 smart card:
{: tsResolve}
1. Start the Smart Card Utility Program.
2. Select **EP11 Smart Card** &gt; **Unblock EP11 smart card** from the pull-down menu.
3. When prompted, insert the certificate authority smart card for the smart card zone of the EP11 smart card in smart card reader 1 and click **OK**.
4. When prompted, enter the first certificate authority PIN on the smart card reader PIN pad.
5. When prompted, enter the second certificate authority PIN on the smart card reader PIN pad.
5. When prompted, insert the EP11 smart card to be unblocked in smart card reader 2 and click **OK**.

<!-- ## Failed to activate the new master key during the master key rotation process
{: #troubleshoot-master-key-rotation}
{: troubleshoot}
{: support}

You are not able to activate the new master key after you run the `cryptounit-mk-rotate` command.
{: tsSymptoms}

You accidentally exit the TKE CLI window when the root keys are being rewrapped by the new master key after you run the `cryptounit-mk-rotate` command.
{: tsCauses}

Run the `cryptounit-mk-rotate` command again to resume the root key rewrap operations. When prompted, enter the password for the current signature key file to activate the new master key.
{: tsResolve} -->

## Got a `CKR_IBM_WK_NOT_INITIALIZED` error when you use CLI or API
{: #troubleshoot-error-CLI-API}
{: troubleshoot}
{: support}

When you use CLI or API, you might got an error message similar to the following message:
{: tsSymptoms}

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}

When you ran the `ibmcloud tke cryptounit-compare` command, you didn't get a `Valid` confirmation on the CURRENT MASTER KEY REGISTER.
{: tsCauses}

Make sure the HSM [master key](#x2908413){: term} has been properly set.
{: tsResolve}

## No smart card readers found when you start application
{: #troubleshoot-no-smart-card}
{: troubleshoot}
{: support}

You might get an error similar to the following one when you start the Smart Card Utility Program or the Trusted Key Entry application. The error can occur even when two Identiv SPR332 V2 smart card readers are attached to USB ports on your workstation.
{: tsSymptoms}

![No smart card readers found when you start the application](/image/no_smart_card_readers.gif "Blocked PIN on EP11 smart card"){: caption="Figure 2. No smart card readers found when you start the application" caption-side="bottom"}

The Identiv SPR332 smart card readers are not attached to your workstation, or the device driver for the smart card reader is not correctly installed on your workstation.
{: tsCauses}

Attach two Identiv SPR332 smart card readers to the USB ports of your workstation. If you've attached two Identiv SPR332 smart card readers to your workstation and still get this error, [install the device driver](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#install-smart-card-reader-driver).
{: tsResolve}

<!--[Installing smart card reader driver on Windows 10](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#reader-driver-windows) or [Installing smart card reader driver on Linux](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#reader-driver-linux) to install the device driver.-->

## Unable to authenticate through the key management API
{: #unable-to-authenticate-api}
{: troubleshoot}

When you call the {{site.data.keyword.hscrypto}} key management API, the system returns a `401 Unauthorized` error, and you're unable to make the API request.

You call any {{site.data.keyword.hscrypto}} key management API method. You see an error response similar to the following JSON object:
{: tsSymptoms}

```
{
  "metadata":
  {
    "collectionType":"application/vnd.ibm.kms.error+json",
    "collectionTotal":1
  },
  "resources":[
    {
      "errorMsg":"Unauthorized: The user does not have access to the specified resource"
    }
  ]
}
```
{: screen}

You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions in the specified service instance.
{: tsCauses}

Verify with an administrator that you are assigned the correct platform and service access roles in the applicable service instance. For more information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles).
{: tsResolve}

## Unable to create or import keys
{: #unable-to-create-keys}
{: troubleshoot}
{: support}

When you access the {{site.data.keyword.hscrypto}} user interface, you do not see the options to add keys or import keys.
{: tsSymptoms}

From the {{site.data.keyword.cloud_notm}} dashboard, you select your instance of the {{site.data.keyword.hscrypto}} service. You can see a list of keys, but you do not see options to add keys or import keys.

You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions.
{: tsCauses}

Verify with your administrator that you're assigned the correct role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles).
{: tsResolve}

## Unable to change signature thresholds
{: #troubleshoot-unable-to-change-signature-thresholds}
{: troubleshoot}

You receive an error similar to the following when you try to change the signature threshold or revocation signature threshold. The error can be reported by either the TKE plug-in or the Trusted Key Entry application.
{: tsSymptoms}

```
FAILED
Error reported by EP11 crypto module.
Return code: 209
Reason code: 71
Error message: Change not allowed.  You are not allowed to change a threshold value if the corresponding attribute control bit is reset.
```
{: screen}

The TKE plug-in through version 0.0.11 restricts the ability to set the signature threshold and revocation signature threshold to a value other than one. The restriction can be removed by zeroizing the crypto unit.
{: tsCauses}

To set the signature threshold or revocation signature threshold to a value greater than one, [zeroize the crypto unit](/docs/hs-crypto?topic=hs-crypto-delete-instance#zeroize-crypto-unit-step). This removes the restriction. Then reinstall the administrators that you want to use and set the threshold values by using either the latest version of the TKE plug-in or the Trusted Key Entry application.
{: tsResolve}

Zeroizing a crypto unit clears the master key registers. To fully recover the state of a crypto unit after zeroizing it, you need to reload the master key registers and the administrators. Depending on your loading method, see [Loading master keys with the TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#load-master-keys) or [Loading master keys with the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities#load-master-key-management-utilities) for instructions.

## Unable to delete keys
{: #unable-to-delete-keys}
{: troubleshoot}

When you use the {{site.data.keyword.hscrypto}} user interface or REST API, you're unable to delete a key.

From the {{site.data.keyword.cloud_notm}} dashboard, you select your instance of the {{site.data.keyword.hscrypto}} service.
{: tsSymptoms}

You're assigned a _Manager_ access policy for the service instance. You try to delete a key, but the action fails with the following error message.

```
Conflict: Key could not be deleted. Status: 409, Correlation ID: 160cc463-71d1-4b30-a5f2-d3f7e9f2b75e
```
{: screen}

This key is actively protecting one or more cloud resources, such as a Cloud Object Storage bucket.
{: tsCauses}

For your protection, {{site.data.keyword.hscrypto}} prevents the deletion of a key that's actively encrypting data in the cloud.
{: tsResolve}

To delete the key, first delete the resources that are associated with the key, and then delete the key.

## Unable to delete an initialized service instance
{: #troubleshoot-delete-instance}
{: troubleshoot}
{: support}

You might receive an error similar to the following one when you delete an initialized service instance:
{: tsSymptoms}

```
FAILED
Error Code: RC-ServiceBrokerErrorResponse
Message: Service Broker returned error status code 409
```
{: screen}

You haven't cleared (zeroized) the initialized service instance before you delete the instance.
{: tsCauses}

The procedure varies depending on the method that you use to initialize the service instance.
{: tsResolve}

-  If you've initialized your service instance through {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) command-line interface (CLI) plug-in, run the following command before you delete the instance:

    ```
    ibmcloud tke cryptounit-zeroize
    ```
    {: pre}

-  If you've initialized your service instance through the TKE application, in the user interface of the application, select **Imprint mode** &gt; **Zeroize crypto unit**.

## Unable to list crypto units
{: #troubleshoot-list-crypto-units}
{: troubleshoot}

You might receive an error message similar to the following one when you list crypto units using command `ibmcloud tke cryptounits`:
{: tsSymptoms}

```
ibmcloud tke cryptounits
API endpoint:     https://cloud.ibm.com
Region:           XX-XX
User:             john.doe@abc.com
Account:          myaccount (GUID)
Resource group:   Default

No service instances were found for the current resource group.
```
{: screen}

It might be caused by one of the following reasons:
{: tsCauses}

- You haven't logged in to the correct region or resource group where your service instance resides.
- If you have multiple accounts, you are not using the correct account with which your service instance is created. Or, your account doesn't have the permission to view the service instance.

Try the following solutions:
{: tsResolve}

- Make sure that you are logged in to the correct region and resource group with the following command:

    ```
    ibmcloud target -r <region> -g <resource_group>
    ```
    {: pre}

- Make sure that your account is assigned at least a _Viewer_ [platform access role](/docs/hs-crypto?topic=hs-crypto-manage-access#platform-mgmt-roles) to view the service instance information. The account with which you create the service instance is granted as the _Administrator_ role by default and can assign various roles that correspond to the specific {{site.data.keyword.hscrypto}} permissions. For more information about roles and permissions, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).

## Unable to rotate root keys
{: #unable-to-rotate-root-keys}
{: troubleshoot}
{: support}

When you access the {{site.data.keyword.hscrypto}} user interface, you do not see the options to rotate root keys.
{: tsSymptoms}

From the {{site.data.keyword.cloud_notm}} dashboard, you see a list of keys in the **Keys** table. However, by selecting the key that you want to rotate and clicking the overflow icon, you don't see the **Rotate key** option on the list.

You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions.
{: tsCauses}

Verify with your administrator that you're assigned the correct role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles).
{: tsResolve}

## Unable to view or list keys
{: #unable-to-list-keys-api}
{: troubleshoot}

When you try to list keys by using the {{site.data.keyword.hscrypto}} key management API, you're unable to view any keys in a service instance that you have access to.

You call `GET api/v2/keys` to list the keys that are available in your service instance. The system returns a response similar to the following JSON object:
{: tsSymptoms}

```
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 0
    }
}
```
{: screen}

You do not have the correct authorization to view the requested range of keys.
{: tsCauses}

Contact an administrator to check your permissions. If the service instance contains keys that you're unable to view, verify that you're assigned the applicable [level of access to keys](/docs/hs-crypto?topic=hs-crypto-grant-access-keys) in the service instance.
{: tsResolve}

## Unable to view or list specific keys
{: #unable-to-list-specific-keys}
{: troubleshoot}

When you call the {{site.data.keyword.hscrypto}} key management API, you're unable to list specific keys that you have access to.

You call `GET api/v2/keys` to list the keys that are available in your service instance.
{: tsSymptoms}

You can see a list of keys, but you can't find a specific key that's stored in the instance. You verify with your administrator that you're assigned the applicable [level of access to keys](/docs/hs-crypto?topic=hs-crypto-grant-access-keys) that you're unable to view. You also verify with your administrator that the key belongs to the service instance that you're targeting.

The service instance contains a large number of keys, and the specific keys that you're looking for aren't returned by default when you call `GET api/v2/keys` to list keys.
{: tsCauses}

Check with an administrator to understand the total number of keys that are stored in the instance. By default, `GET api/v2/keys` returns the first 200 keys. If the service instance contains more than 200 keys, you need to use the [`offset` and `limit` parameters](/docs/hs-crypto?topic=hs-crypto-view-keys#retrieve-subset-keys-api) to list another subset of keys.
{: tsResolve}

For example, if you want to list keys 201 - 210 that are available in a service instance, you use `../keys?offset=200&limit=10` to skip the first 200 keys.

## Unauthorized when you run TKE CLI plug-in commands
{: #troubleshoot-unauthorized-token}
{: troubleshoot}
{: support}

You might receive messages similar to the following one after you run a `tke` CLI command:
{: tsSymptoms}

```
ibmcloud tke cryptounits
FAILED
Error querying service instances.
Status code: 401
Message: Unauthorized
Your access token is invalid, expired, or does not have the necessary permissions to access this instance.`
```
{: codeblock}

To run TKE CLI plug-in commands that send requests to the {{site.data.keyword.cloud_notm}}, you must have a valid authentication token. An authentication token is created when you log in to the {{site.data.keyword.cloud_notm}}, but it expires after 1 hour.  After 1 hour, you must log in again to continue to send requests to the {{site.data.keyword.cloud_notm}}.
{: tsCauses}

Log in to {{site.data.keyword.cloud_notm}} again with the `ibmcloud login` command to refresh the token.
{: tsResolve}

## Unauthorized when you start the Trusted Key Entry application
{: #troubleshoot-unauthorized-token-tke-application}
{: troubleshoot}
{: support}

You receive an error similar to the following one when you start the Trusted Key Entry application.
{: tsSymptoms}

![Unauthorized when you run TKE CLI plug-in commands](/image/tke_401.gif "Unauthorized when you run TKE CLI plug-in commands"){: caption="Figure 3. Unauthorized when you start the Trusted Key Entry application" caption-side="bottom"}

A valid authentication token is needed for the TKE application to send requests to {{site.data.keyword.cloud_notm}}. You must log in to {{site.data.keyword.cloud_notm}} with the {{site.data.keyword.cloud_notm}} CLI to create a valid authentication token before you can run the TKE application. These might be the causes of this error:
{: tsCauses}

- You've not logged in to {{site.data.keyword.cloud_notm}} to create an authentication token.
- Your authentication token has expired after 1 hour.

From the command line, log in to the {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command. Click **Refresh Panel** on the **Crypto units** tab to retry the query of your service instance.
{: tsResolve}

## Getting help and support
{: #getting-help}
{: troubleshoot}
{: support}

If you've problems or questions when you're using {{site.data.keyword.hscrypto}}, you can check {{site.data.keyword.cloud_notm}}, or get help by searching for information or by asking questions through a forum. You can also open a support ticket.

You can check whether {{site.data.keyword.cloud_notm}} is available by going to the [status page](https://cloud.ibm.com/status?tags=platform,runtimes,services).

You can review the forums to see whether other users ran into the same problem. When you're using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.

If you have questions about {{site.data.keyword.hscrypto}}, post your question on [Stack Overflow](https://stackoverflow.com/questions/tagged/hyper-protect-crypto){: external} and tag your question with  "ibm-cloud" and "hyper-protect-crypto".

See [Getting help](/docs/get-support?topic=get-support-getting-customer-support){: external} for more details about using the forums.

For more information about opening an {{site.data.keyword.IBM_notm}} support ticket, or about support levels and ticket severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support){: external}.
