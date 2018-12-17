---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-02"

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

# Troubleshooting
{: #troubleshooting}

General problems with using {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} might include providing the correct headers or credentials when you interact with the API. In many cases, you can recover from these problems by following a few easy steps.
{: shortdesc}

## Unable to delete my Cloud Foundry service instance
{: #unable-to-delete-service}

When you try to delete your {{site.data.keyword.hscrypto}} service instance, the service fails to delete as expected.

From the {{site.data.keyword.cloud_notm}} dashboard, you navigate to **Cloud Foundry Services**, and you select your instance of {{site.data.keyword.hscrypto}}. You click the ⋮ icon to open a list of options for the service offering, and you click **Delete Service**.
{: tsSymptoms}

The service fails to delete, and you see the following error:
```
403 Forbidden: This action cannot be completed because you have existing secrets in your Key Protect service. You first need to delete the secrets before you can remove the service.
```
{: screen}

On 15 December 2017, {{site.data.keyword.keymanagementserviceshort}} moved from using Cloud Foundry orgs, spaces, and roles to using IAM and resource groups. You can now provision the {{site.data.keyword.keymanagementserviceshort}} service within a resource group, without needing to specify a Cloud Foundry organization and space.
{: tsCauses}

These changes affected how deprovisioning works for older instances of the service. If you created your instance of {{site.data.keyword.keymanagementserviceshort}} before 28 September 2017, service deletion might not work as expected.

To delete an older {{site.data.keyword.keymanagementserviceshort}} service instance, you must first delete your existing keys by using the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} service.
{: tsResolve}

To delete your keys and your service instance:

1. Log in to {{site.data.keyword.cloud_notm}} with the {{site.data.keyword.cloud_notm}} CLI.

    ```sh
    ibmcloud login
    ```
    {: codeblock}

    **Note:** If the login fails, run the `bx login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the {{site.data.keyword.cloud_notm}} region, org, and space that contains your {{site.data.keyword.keymanagementserviceshort}} service instance.

    Note the names of your org and space in the CLI output. You can also run `ibmcloud cf target` to target your Cloud Foundry org and space.

    ```sh
    ibmcloud cf target -o <organization_name> -s <space_name>
    ```
    {: codeblock}

3. Retrieve your {{site.data.keyword.cloud_notm}} org and space GUIDs.

    ```sh
    ibmcloud iam org <organization_name> --guid
    ibmcloud iam space <space_name> --guid
    ```
    {: codeblock}
    Replace `<organization_name>` and `<space_name>` with the unique aliases that you assigned to your organization and space.

4. Retrieve your access token.

    ```sh
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

5. List the keys that are stored in your service instance by running the following cURL command.

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

    Replace `<access_token>`, `<organization_GUID>`, and `<space_GUID>` with the values that you retrieved in steps 3 - 4.

6. Copy the ID value for each key that is stored in your service instance.

7. Run the following cURL command to permanently delete a key and its contents.

    ```cURL
    curl -X DELETE \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

    Replace `<access_token>`, `<organization_GUID>`, `<space_GUID>`, and `<key_ID>` with the values that you retrieved in steps 3 - 5. Repeat the command for each key.    

8. Verify that your keys were deleted by running the following cURL command.

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

    Replace `<access_token>`, `<organization_GUID>`, and `<space_GUID>` with the values that you retrieved in steps 3 - 4.

9. Delete your {{site.data.keyword.keymanagementserviceshort}} service instance.

    ```sh
    ibmcloud cf delete-service "<service_instance_name>"
    ```
    {: codeblock}

10. Optional: Verify that your {{site.data.keyword.keymanagementserviceshort}} service instance was deleted by navigating to your {{site.data.keyword.cloud_notm}} dashboard.

    You can also list your available Cloud Foundry services in the targeted space by running the following command.

    ```sh
    ibmcloud cf service list
    ```
    {: codeblock}


## Unable to access the user interface
{: #unable-to-access-ui}

When you access the {{site.data.keyword.keymanagementserviceshort}} user interface, the UI does not load as expected.

From the {{site.data.keyword.cloud_notm}} dashboard, you select your instance of the {{site.data.keyword.keymanagementserviceshort}} service.
{: tsSymptoms}

You see the following error:
```
404 Not Found: Requested route ('ibm-key-protect-ui.ng.bluemix.net') does not exist.
```
{: screen}

On 15 December 2017, we added new features, such as [envelope encryption](/docs/services/key-protect/concepts/envelope-encryption.html), to the {{site.data.keyword.keymanagementserviceshort}} service. You can now provision the {{site.data.keyword.keymanagementserviceshort}} service within a resource group, without needing to specify a Cloud Foundry organization and space.
{: tsCauses}

These changes affected the user interface for older instances of the service. If you created your instance of {{site.data.keyword.keymanagementserviceshort}} before 28 September 2017, the user interface might not work as expected.

We're working to fix this issue on our end. As a temporary solution, you can continue to manage your keys by using the {{site.data.keyword.keymanagementserviceshort}} API.
{: tsResolve}

You can use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} service.

**Example request**

```cURL
curl -X GET \
https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
-H 'accept: application/vnd.ibm.collection+json' \
-H 'authorization: Bearer <access_token>' \
-H 'bluemix-org: <organization_GUID>' \
-H 'bluemix-space: <space_GUID>' \
```
{: codeblock}

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

If you have problems or questions when you are using {{site.data.keyword.keymanagementserviceshort}}, you can check {{site.data.keyword.cloud_notm}}, or get help by searching for information or by asking questions through a forum. You can also open a support ticket.
{: shortdesc}

You can check whether {{site.data.keyword.cloud_notm}} is available by going to the [status page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/status?tags=platform,runtimes,services).

You can review the forums to see whether other users ran into the same problem. When you are using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.

- If you have technical questions about {{site.data.keyword.keymanagementserviceshort}}, post your question on [Stack Overflow ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://stackoverflow.com/search?q=key-protect+ibm-cloud){: new_window} and tag your question with "ibm-cloud" and "key-protect".
- For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/key-protect/?smartspace=bluemix){: new_window} forum. Include the "ibm-cloud"
and "key-protect" tags.

See [Getting help ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/support/index.html#getting-help){: new_window} for more details about using the forums.

For more information about opening an {{site.data.keyword.IBM_notm}} support ticket, or about support levels and ticket severities, see [Contacting support ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/support/index.html#contacting-support){: new_window}.
