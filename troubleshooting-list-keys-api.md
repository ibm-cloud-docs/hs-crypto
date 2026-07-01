---

copyright:
  years: 2020, 2026
lastupdated: "2026-07-01"

keywords: troubleshoot, problems, known issues, can't view or list keys

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Why can't I view or list keys?
{: #troubleshoot-unable-to-list-keys-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is deprecated. As of 28 March 2026, you can't create new instances, and access to free instances will be removed. Existing premium plan instances are supported until 28 March 2027. Any instances that still exist on that date will be deleted.
{: deprecated}
{: troubleshoot}

When you try to list keys by using the {{site.data.keyword.hscrypto}} key management service API, you're unable to view any keys in a service instance that you have access to.
{: shortdesc}

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
