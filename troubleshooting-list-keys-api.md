---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: troubleshoot, problems, known issues, can't view or list keys

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

# Why can't I view or list keys?
{: #troubleshoot-unable-to-list-keys-api}
{: troubleshoot}

When you try to list keys by using the {{site.data.keyword.hscrypto}} key management API, you're unable to view any keys in a service instance that you have access to.
{:shortdesc}

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
