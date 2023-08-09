---

copyright:
  years: 2022, 2023
lastupdated: "2023-08-09"

keywords: release note, new, changelog, what's new, service updates, service bulletin

subcollection: hs-crypto

---


{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API change log
{: #uko-api-change-log}

In this change log you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API. The change log lists changes that have been made, ordered by the date they were released. Changes to existing API versions are designed to be compatible with existing client applications.

## API versioning
{: #uko-api-versioning}


The latest released version is `4.9.5`. The {{site.data.keyword.uko_full_notm}} API version is aligned with the IBM Enterprise Key Management Foundation - Web Edition (EKMF Web) API version.  




## December 2022
{: #uko-api-december-2022}

The following methods are added:

- Rotate a managed key
- List managed key versions

## October 2022
{: #uko-api-october-2022}

The following methods are added or updated:

- (Added) Sync a managed key in keystores
- (Updated) Create an internal keystore or a keystore connection - Add Google Cloud KMS keystore support
- (Updated) Create a key template - Add Google Cloud KMS key template support

## July 2022
{: #uko-api-july-2022}

The following methods are added:

- List associated resources for a manged key
- List associated resources for a keystore

## June 2022
{: #uko-api-june-2022}

A software development kit (SDK) for Golang is provided along with API method examples.

## March 2022
{: #uko-api-march-2022}

The following methods are introduced:

- List managed keys
- Create a managed key
- Delete a managed key
- Retrieve a managed key
- Update a managed key
- Retrieve distribution status for all keystores
- Update a managed key to match the key template
- Activate a managed key
- Deactivate a managed key
- Destroy a managed key
- List key templates
- Create a key template
- Delete a template
- Retrieve a key template
- Update a key template
- List all keystores
- Create an internal keystore or a keystore connection
- Delete an internal keystore or a connection to an external keystore
- Retrieve a keystore
- Update an internal keystore or a keystore connection
- Retrieve keystore status
- List managed keys on the keystore
- List all vaults
- Create a vault
- Delete an existing vault
- Retrieve a vault
- Update a vault

