---

copyright:
  years: 2022
lastupdated: "2022-02-09"

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

# {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API change log
{: #uko-api-change-log}

In this change log you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API. The change log lists changes that have been made, ordered by the date they were released. Changes to existing API versions are designed to be compatible with existing client applications.

## API versioning
{: #uko-api-versioning}

The latest released version is `22.1.32`. The {{site.data.keyword.uko_full_notm}} API version is aligned with the IBM Enterprise Key Management Foundation - Web Edition (EKMF Web) API version.  

## February 2022
{: #uko-api-feb-2022}

The following methods are introduced:

- Get a list of local keystores
- Create a local keystore
- Delete a local keystore
- Find a keystore by ID
- Update properties of a local keystore
- Get local keystore status
- Get a list of keys
- Create a new key
- Delete a key by ID
- Find a key by ID
- Update a single key
- Find a key instance by ID
- Return distribution status for all keystores for a single key instance
- Modify keystore status of a key instance in all keystores where the key instance is to be installed on
- Return distribution status for a specific keystore for a single key instance
- Modify keystore status of a key instance in a single keystore
- Return a list of tags of a key
- Delete the tag of a key
- Return a single tag for provided tag name
- Modify the tag of a key
- Create a template
- Delete a template
- Find a template by ID
- Update properties of a template
- Get the gross set of keystores a template distributes keys to
- Find a latest template version by ID
- Get a list of keystores
- Create a keystore
- Delete a keystore
- Find a keystore by name
- Update properties of a keystore
- Get keystore status
- Get a list of vaults in the system
- Create a vault
- Get managed keys from a keystore
- Get keystore tags for keystore types
- Get a list of templates
- Get detailed information of a build
