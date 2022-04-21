---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-21"

keywords: troubleshoot, problems, known issues, can't delete an initialized service instance

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:external: target="_blank" .external}
{:support: data-reuse='support'}
{:term: .term}
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Why can't I delete an initialized service instance?
{: #troubleshoot-delete-instance}
{: troubleshoot}
{: support}

You get an error when you delete an initialized service instance.
{: shortdesc}

You might receive an error similar to the following one:
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

After you zeroize the crypto unit, the administrator signature keys and the master key are cleared from the crypto unit, which means you are not able to access any root keys or standard keys that is protected by the master key. Any resources that are associated with the root keys, such as the [Immutable Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-immutable), cannot be accessed. 
{: important}