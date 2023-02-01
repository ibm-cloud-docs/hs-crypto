---

copyright:
  years: 2021, 2023
lastupdated: "2023-02-01"

keywords: release note, new, changelog, what's new, service updates, service bulletin

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}

# {{site.data.keyword.hscrypto}} key management service API change log
{: #kms-api-change-log}

In this change log you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.hscrypto}} key management service API. The change log lists changes that have been made, ordered by the date they were released. Changes to existing API versions are designed to be compatible with existing client applications.

## API versioning
{: #kms-api-versioning}

The latest released version is `22.11`.

## February 2023
{: #kms-api-Feb-2023}

The following functions are added:

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

