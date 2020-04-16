---

copyright:
  years: 2018, 2020
lastupdated: "2020-04-07"

keywords: troubleshoot, problems, known issues, can't delete service, can't use Hyper Protect Crypto Services, can't create key, can't delete key

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

## Error occurred when you delete an initialized service instance
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

## Got `error CKR_IBM_WK_NOT_INITIALIZED` when you use CLI or API
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


## Unable to create or delete keys
{: #unable-to-create-keys}
{: troubleshoot}
{: support}

When you access the {{site.data.keyword.hscrypto}} user interface, you do not see the options to add or delete keys.
{: tsSymptoms}

From the {{site.data.keyword.cloud_notm}} dashboard, you select your instance of the {{site.data.keyword.hscrypto}} service. You can see a list of keys, but you do not see options to add or delete keys.

You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions.
{: tsCauses}

Verify with your administrator that you're assigned the correct role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles).
{: tsResolve}

## 401 error (unauthorized) when you run TKE CLI plug-in commands
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

## 401 error (unauthorized) when you start the Trusted Key Entry application
{: #troubleshoot-unauthorized-token-tke-application}
{: troubleshoot}
{: support}

You receive an error similar to the following one when you start the Trusted Key Entry application.
{: tsSymptoms}

![Unauthorized when you run TKE CLI plug-in commands](/image/tke_401.gif "Unauthorized when you run TKE CLI plug-in commands"){: caption="Figure 3. Unauthorized when you start the Trusted Key Entry application" caption-side="bottom"}

A valid authentication token is needed for the TKE application to send requests to {{site.data.keyword.cloud_notm}}. You must log in to {{site.data.keyword.cloud_notm}} with the {{site.data.keyword.cloud_notm}} CLI to create a valid authentication token before you can run the TKE application. These might be the causes of this error:
{: tsCauses}

- you've not logged in to {{site.data.keyword.cloud_notm}} to create an authentication token.
- Your authentication token has expired after 1 hour.

<!--Open a command prompt window (on the Windows&reg; operating system) or terminal window (on the Linux&reg; operating system), -->

Open a Linux terminal window and log in to the {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command. Click **Refresh Panel** on the **Crypto units** tab to retry the query of your service instance.
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
