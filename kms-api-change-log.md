---

copyright:
  years: 2021, 2024
lastupdated: "2024-02-01"

keywords: release note, new, changelog, what's new, service updates, service bulletin

subcollection: hs-crypto

---


{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.hscrypto}} key management service API change log
{: #kms-api-change-log}

In this change log you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.hscrypto}} key management service API. The change log lists changes that have been made, ordered by the date they were released. Changes to existing API versions are designed to be compatible with existing client applications.

## API versioning
{: #kms-api-versioning}

The latest released version is `23.11`.

## February 2024
{: #kms-api-feb-2024}

The following methods are updated:

- [Delete key ring](/apidocs/key-protect#deletekeyring){: external}: You can now force delete a key ring. If the keys in this key ring are not deleted before this action is performed, the keys will be moved to the default key ring.
- [List key versions](/apidocs/hs-crypto#getkeyversions){: external}: You can now view key versions of a key in any state, including the deleted key.


## February 2023
{: #kms-api-feb-2023}

The following methods are added:

- [List Keys with sorting](/apidocs/hs-crypto#:~:text=values%3A%20length%20≤%20256-,sort,-string){: external} to include lastRotateDate sorting.
- [List Keys with advanced filtering](/apidocs/hs-crypto#:~:text=Default%3A%20id-,filter,-string){: external} to including lastRotateDate filtering.
- [Create key with policy overrides](https://cloud.ibm.com/apidocs/hs-crypto#createkeywithpoliciesoverrides){: external} to enable users with Manager role to create keys with policies in a single call, overriding instance level policies.
- [Disable a key rotation policy](/apidocs/hs-crypto#:~:text=policy%2Bjson"%2C%0A%20%20%20%20%20%20%20%20"rotation"%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20"-,enabled,-"%3A%20<true%7Cfalse>%2C%0A%20%20%20%20%20%20%20%20%20%20"interval_month){: external} to allow an automatic key rotation policy to be paused temporarily.

## January 2022
{: #kms-api-jan-2022}

The following methods are added:

- Update the key ring of a key. After you create a key, you can transfer the key to a different key ring by sending a `PATCH /api/v2/keys/{id}` request and specifying the new key ring ID.
- Purge key to permanently delete a key. After you purge a key, you are no longer able to access the key and its associated resources. This action is performed in a `DELETE /api/v2/keys/{id}/purge` request.

## April 2021
{: #kms-api-april-2021}

The method of restoring keys is updated. Now all root keys and standard keys can be restored within 30 days of the deletion and no key material is required.

