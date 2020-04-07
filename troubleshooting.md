---

copyright:
  years: 2018, 2019
lastupdated: "2019-10-18"

Keywords: troubleshoot, problems, known issues, can't delete service, can't use Hyper Protect Crypto Services, can't create key, can't delete key

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

# Troubleshooting for {{site.data.keyword.hscrypto}}
{: #troubleshooting}

General problems with using {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} might include providing the correct headers or credentials when you interact with the API. In many cases, you can recover from these problems by following a few easy steps.
{: shortdesc}

When using `ibmcloud` CLI, to get the detailed error message, set `IBMCLOUD_TRACE=true`.
{: tip}

## Error occurred when deleting an initialized service instance
{: #troubleshoot-delete-instance}
{: troubleshoot}

You might receive an error similar to the following when you delete an initialized service instance:

```
FAILED
Error Code: RC-ServiceBrokerErrorResponse
Message: Service Broker returned error status code 409
```
{: codeblock}
{: tsSymptoms}

You have not cleared (zeroized) the initialized service instance before you delete the instance.
{: tsCauses}

Run the following command before you delete the instance:
{: tsResolve}

```
ibmcloud tke cryptounit-zeroize
```
{: codeblock}

## Unauthorized token after running commands related to the Trusted Key Entry plug-in
{: #troubleshoot-unauthorized-token}
{: troubleshoot}

You might receive messages similar to the following after you run a `tke` CLI commands:

```
ibmcloud tke cryptounits
FAILED
Error querying service instances.
Status code: 401
Message: Unauthorized
Your access token is invalid, expired, or does not have the necessary permissions to access this instance.`
```
{: codeblock}
{: tsSymptoms}

The token is not refreshed.
{: tsCauses}

Log in to {{site.data.keyword.cloud_notm}} again with the `ibmcloud login` command to refresh the token.
{: tsResolve}

## Got `error CKR_IBM_WK_NOT_INITIALIZED` when using CLI or API
{: #troubleshoot-error-CLI-API}
{: troubleshoot}

When you use CLI or API, you might got an error message similar to the following:

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

When you ran the `ibmcloud tke cryptounit-compare` command, you did not get a `Valid` confirmation on the CURRENT MASTER KEY REGISTER.
{: tsCauses}

Make sure the HSM master key has been properly set.
{: tsResolve}

## Unable to create or delete keys
{: #unable-to-create-keys}
{: troubleshoot}

When you access the {{site.data.keyword.hscrypto}} user interface, you do not see the options to add or delete keys.

From the {{site.data.keyword.cloud_notm}} dashboard, you select your instance of the {{site.data.keyword.hscrypto}} service.
{: tsSymptoms}

You can see a list of keys, but you do not see options to add or delete keys.

You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions.
{: tsCauses}

Verify with your administrator that you are assigned the correct role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/services/hs-crypto?topic=hs-crypto-manage-access#roles).
{: tsResolve}

## Getting help and support
{: #getting-help}
{: troubleshoot}

If you have problems or questions when you are using {{site.data.keyword.hscrypto}}, you can check {{site.data.keyword.cloud_notm}}, or get help by searching for information or by asking questions through a forum. You can also open a support ticket.
{: shortdesc}

You can check whether {{site.data.keyword.cloud_notm}} is available by going to the [status page](https://cloud.ibm.com/status?tags=platform,runtimes,services).

You can review the forums to see whether other users ran into the same problem. When you are using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.

- If you have technical questions about {{site.data.keyword.hscrypto}}, post your question on [Stack Overflow](https://stackoverflow.com/questions/tagged/hyper-protect-crypto){: external} and tag your question with  "ibm-cloud" and "hyper-protect-crypto".
- For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/hyper-protect-crypto){: external} forum. Include the "ibm-cloud" and "hyper-protect-crypto" tags.

See [Getting help](/docs/get-support?topic=get-support-getting-customer-support){: external} for more details about using the forums.

For more information about opening an {{site.data.keyword.IBM_notm}} support ticket, or about support levels and ticket severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support){: external}.
