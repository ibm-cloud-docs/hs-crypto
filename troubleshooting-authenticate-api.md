---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: troubleshoot, problems, known issues, can't authenticate through the key management API

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

# Why am I not authorized to make key management API request?
{: #troubleshoot-unable-to-authenticate-api}
{: troubleshoot}

When you call the {{site.data.keyword.hscrypto}} key management API, the system returns a `401 Unauthorized` error, and you're unable to make the API request.
{:shortdesc}

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
