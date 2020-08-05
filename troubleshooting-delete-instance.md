---

copyright:
  years: 2020
lastupdated: "2020-07-17"

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

# Why can't I delete an initialized service instance?
{: #troubleshoot-delete-instance}
{: troubleshoot}
{: support}

You get an error when you delete an initialized service instance.
{:shortdesc}

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
