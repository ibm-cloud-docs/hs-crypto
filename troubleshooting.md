---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

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

# Troubleshooting
{: #troubleshooting}

General problems with using {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} might include providing the correct headers or credentials when you interact with the API. In many cases, you can recover from these problems by following a few easy steps.
{: shortdesc}

## Error occurred when deleting an initialized {{site.data.keyword.hscrypto}} instance

You might receive an error similar to the following when you delete an initialized {{site.data.keyword.hscrypto}} instance:

```
FAILED
Error response from server. Status code: 400; description: 400 DELETE https://zCryptoBroker.mybluemix.net/v2/service_instances/ failed with error status 409. Conflict.
```
{: codeblock}
{: tsSymptoms}

You have not cleared (zeroized) the initialized {{site.data.keyword.hscrypto}} instance before you delete the instance.
{: tsCauses}

Run the following command before you delete the instance:

```
ibmcloud tke domain-zeroize
```
{: codeblock}
{: tsResolve}

## Unauthorized token after running commands related to the Trusted Key Entry plug-in

You might receive messages similar to the following after you run a `tke` CLI commands:

```
ibmcloud tke domains
FAILED
Error querying crypto instances.
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

## Got `error CKR_IBM_WK_NOT_INITIALIZED` when using {{site.data.keyword.keymanagementserviceshort}} CLI or API

When you use {{site.data.keyword.keymanagementserviceshort}} CLI or API, you might got an error message similar to the following:

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

When you ran the `ibmcloud tke domain-compare` command, you did not get a `Valid` confirmation on the CURRENT MASTER KEY REGISTER.
{: tsCauses}

Make sure the HSM master key has been properly set.
{: tsResolve}

## Unable to create or delete keys
{: #unable-to-create-keys}

When you access the {{site.data.keyword.keymanagementserviceshort}} user interface, you do not see the options to add or delete keys.

From the {{site.data.keyword.cloud_notm}} dashboard, you select your instance of the {{site.data.keyword.keymanagementserviceshort}} service.
{: tsSymptoms}

You can see a list of keys, but you do not see options to add or delete keys.

You do not have the correct authorization to perform {{site.data.keyword.keymanagementserviceshort}} actions.
{: tsCauses}

Verify with your administrator that you are assigned the correct role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/services/key-protect/manage-access.html#roles).
{: tsResolve}

## Getting help and support
{: #getting-help}

If you have problems or questions when you are using {{site.data.keyword.hscrypto}}, you can check {{site.data.keyword.cloud_notm}}, or get help by searching for information or by asking questions through a forum. You can also open a support ticket.
{: shortdesc}

You can check whether {{site.data.keyword.cloud_notm}} is available by going to the [status page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/status?tags=platform,runtimes,services).

You can review the forums to see whether other users ran into the same problem. When you are using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.

- If you have technical questions about {{site.data.keyword.hscrypto}}, post your question on [Stack Overflow ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://stackoverflow.com/){: new_window} and tag your question with  "ibm-cloud" and "hyperprotect-crypto".
- For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/index.html){: new_window} forum. Include the "ibm-cloud" and "hyperprotect-crypto" tags.

See [Getting help ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/support/index.html#getting-help){: new_window} for more details about using the forums.

For more information about opening an {{site.data.keyword.IBM_notm}} support ticket, or about support levels and ticket severities, see [Contacting support ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/support/index.html#contacting-support){: new_window}.
