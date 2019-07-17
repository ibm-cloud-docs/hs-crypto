---

copyright:
years: 2018, 2019
lastupdated: "2019-07-01"

Keywords: root keys, standard keys, migration, transition, beta

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:external: target="_blank" .external}

# Migrating keys from a Beta service instance
{: #migrate-keys}

If you were using a Beta service instance, and want to migrate the root keys and standard keys you managed to a {{site.data.keyword.hscrypto}} production service instance, here is the procedure you need to follow.
{: shortdesc}

IBM Cloud administrators cannot migrate the master keys because the master keys are not extractable from the crypto unit. You need to initialize the production service instance with your master key.
{:important}  

## Before you begin
{: #migrate-prerequisites}

1. [Create a service instance](/docs/services/hs-crypto?topic=hs-crypto-provision) with the Hyper Protect Crypto Services Plan.

2. [Initialize the service instance](/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm) with Trusted Key Entry plugin.

## Migrating keys
{: #migrate-keys-steps}  

Complete the following steps to migrate root keys and standard keys to the production environment.

1. [Import root keys](/docs/services/hs-crypto?topic=hs-crypto-import-root-keys) through either GUI or API.

  You can migrate the imported root keys from the Beta service instance to the production service instance.
  {:tip}

2. Unwrap the data encryption keys (DEKs) from the Beta service instance and wrap the DEKs in the production service instance:

  1. [Unwrap the data encryption keys (DEKs)](/docs/services/hs-crypto?topic=hs-crypto-unwrap-keys) from the Beta service instance with the [invoke-an-action-on-a-key API](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: external}.

  2. [Wrap the DEKs](/docs/services/hs-crypto?topic=hs-crypto-wrap-keys) in the production service instance with the [invoke-an-action-on-a-key API](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: external}.

3. Recreate standard keys by following these steps:

  1. [Retrieve standard Keys](/docs/services/hs-crypto?topic=hs-crypto-view-keys#retrieve-key-api) with the [retrieve-key-by-id API](https://{DomainName}/apidocs/hs-crypto#retrieve-a-key-by-id){: external}. This returns the payload used to create the key in the Beta instance.

  2. [Create standard keys](/docs/services/hs-crypto?topic=hs-crypto-create-standard-keys) in the new service instance with the information retrieved in the previous step through GUI or the [create-a-new-key API](https://{DomainName}/apidocs/hs-crypto#create-a-new-key){: external}.

## What's next
{: #migration-next}

To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
