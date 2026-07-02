---

copyright:
  years: 2020, 2026
lastupdated: "2026-07-01"

keywords: troubleshoot, problems, known issues, can't authenticate through the key management service API

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Why am I not authorized to make key management service API request?
{: #troubleshoot-unable-to-authenticate-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is deprecated. As of 28 March 2026, you can't create new instances, and access to free instances will be removed. Existing premium plan instances are supported until 28 March 2027. Any instances that still exist on that date will be deleted.
{: deprecated}
{: troubleshoot}

When you call the {{site.data.keyword.hscrypto}} key management service API, the system returns a `401 Unauthorized` error, and you're unable to make the API request.
{: shortdesc}

You call any {{site.data.keyword.hscrypto}} key management service API method. You see an error response similar to the following JSON object:
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
