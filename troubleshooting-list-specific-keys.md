---

copyright:
  years: 2020, 2023
lastupdated: "2023-07-05"

keywords: troubleshoot, problems, known issues, can't view or list specific keys

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I view or list specific keys?
{: #troubleshoot-unable-to-list-specific-keys}
{: troubleshoot}

When you call the {{site.data.keyword.hscrypto}} key management service API, you're unable to list specific keys that you have access to.
{: shortdesc}

You call `GET api/v2/keys` to list the keys that are available in your service instance.
{: tsSymptoms}

You can see a list of keys, but you can't find a specific key that is stored in the instance. You verify with your administrator that you're assigned the applicable [level of access to keys](/docs/hs-crypto?topic=hs-crypto-grant-access-keys) that you're unable to view. You also verify with your administrator that the key belongs to the service instance that you're targeting.

The service instance contains a large number of keys, and the specific keys that you're looking for aren't returned by default when you call `GET api/v2/keys` to list keys.
{: tsCauses}

Check with an administrator to understand the total number of keys that are stored in the instance. By default, `GET api/v2/keys` returns the first 200 keys. If the service instance contains more than 200 keys, you need to use the [`offset` and `limit` parameters](/docs/hs-crypto?topic=hs-crypto-view-keys#retrieve-subset-keys-api) to list another subset of keys.
{: tsResolve}

For example, if you want to list keys 201 - 210 that are available in a service instance, you use `../keys?offset=200&limit=10` to skip the first 200 keys.
