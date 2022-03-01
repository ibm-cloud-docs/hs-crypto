---

copyright:
  years: 2021, 2022
lastupdated: "2022-03-01"

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

The latest released version is `2.93`.

## June 2021
{: #kms-api-june-2021}

The following methods are added:

- Update the key ring of a key. After you create a key, you can transfer the key to a different key ring by sending a `PATCH /api/v2/keys/{id}` request and specifying the new key ring ID.
- Purge key to permanently delete a key. After you purge a key, you are no longer able to access the key and its associated resources. This action is performed in a `DELETE /api/v2/keys/{id}/purge` request.

## April 2021
{: #kms-api-april-2021}

The method of restoring keys is updated. Now all root keys and standard keys can be restored within 30 days of the deletion and no key material is required.

