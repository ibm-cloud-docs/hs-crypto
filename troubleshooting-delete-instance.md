---

copyright:
  years: 2020, 2023
lastupdated: "2023-09-27"

keywords: troubleshoot, problems, known issues, can't delete an initialized service instance

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I delete an initialized service instance?
{: #troubleshoot-delete-instance}
{: troubleshoot}
{: support}

You get an error when you delete an initialized service instance.
{: shortdesc}

You might receive an error similar to the following one:
{: tsSymptoms}


> FAILED
> Error Code: RC-ServiceBrokerErrorResponse
> Message: Service Broker returned error status code 409

The following reasons might cause the errors:
{: tsCauses}

- You haven't deleted root keys with the standard plan or managed keys with the {{site.data.keyword.uko_full_notm}} plan.
- You haven't cleared (zeroized) the initialized service instance before you delete the instance.

The following instructions can help you solve the problems:
{: tsRosolve}

- If you haven't deleted root keys with the standard plan or managed keys with the {{site.data.keyword.uko_full_notm}} plan, run the following commands: 

  - For root keys: 
    ```
    ibmcloud kp key delete KEY_ID_OR_ALIAS
            -i, --instance-id INSTANCE_ID
        [--key-ring          KEY_RING_ID]
        [-f, --force]
        [-o, --output      OUTPUT]
    ```
    {: codeblock}
  
  - For managed keys:
    ```
    ibmcloud hpcs uko managed-key-delete --id ID --uko-vault UKO-VAULT --if-match IF-MATCH
    ```
    {: codeblock}

    If you have zeroized the initialized service instance, you can only use the {{site.data.keyword.cloud_notm}} CLI or [{{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#delete-managed-key) to delete keys. 
    {: important}

- If you haven't cleared (zeroized) the initialized service instance, the procedure varies depending on the method that you use to initialize the service instance.

  -  If you've initialized your service instance through {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) command-line interface (CLI) plug-in, run the following command before you delete the instance:

      ```
      ibmcloud tke cryptounit-zeroize
      ```
      {: pre}

  -  If you've initialized your service instance through the TKE application, in the user interface of the application, select **Imprint mode** &gt; **Zeroize crypto unit**.

  After you zeroize the crypto unit, the administrator signature keys and the master key are cleared from the crypto unit, which means you are not able to access any root keys or standard keys that are protected by the master key. Any resources that are associated with the root keys, such as the [Immutable Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-immutable), cannot be accessed. 
  {: important}
