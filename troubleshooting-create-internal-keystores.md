---

copyright:
  years: 2022
lastupdated: "2022-02-28"

keywords: troubleshoot, problems, known issues, can't create internal keystores

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

# Why can't I create internal keystores?
{: #troubleshoot-create-internal-keystores}
{: troubleshoot}

When you try to add additional internal KMS keystores, an error occurs.
{: shortdesc}

You receive the following error message when you try to add additional internal KMS keystores:
{: tsSymptoms}

- From UI:
    ```
    Adding keystore failed. The service was not able to add keystore `<keystore_ID>`.
    ```
    {: screen}

- From API:
    ```
    The operation on the keystore has failed. 
    ```
    {: screen}

For a single service instance, you can create a maximum of 50 internal KMS keystores. You have reached the limits.
{: tsCauses}

Empty and delete an existing keystore, so that you can create a new one.
{: tsResolve}

