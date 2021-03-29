---

copyright:
  years: 2020, 2021
lastupdated: "2021-01-07"

keywords: troubleshoot, problems, known issues, can't list crypto units

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

# Why can't I list crypto units?
{: #troubleshoot-list-crypto-units}
{: troubleshoot}

You get an error message when you list crypto units using command `ibmcloud tke cryptounits`.
{:shortdesc}

You might receive an error message similar to the following one:
{: tsSymptoms}

```
ibmcloud tke cryptounits
API endpoint:     https://cloud.ibm.com
Region:           XX-XX
User:             john.doe@abc.com
Account:          myaccount (GUID)
Resource group:   Default

No service instances were found for the current resource group.
```
{: screen}

It might be caused by one of the following reasons:
{: tsCauses}

- You haven't logged in to the correct region or resource group where your service instance resides.
- If you have multiple accounts, you are not using the correct account with which your service instance is created. Or, your account doesn't have the permission to view the service instance.

Try the following solutions:
{: tsResolve}

- Make sure that you are logged in to the correct region and resource group with the following command:

    ```
    ibmcloud target -r <region> -g <resource_group>
    ```
    {: pre}

- Make sure that your account is assigned the _Manager_ [service access role](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles) to list the crypto units. The account with which you create the service instance is granted as the _Administrator_ role by default and can assign various roles that correspond to the specific {{site.data.keyword.hscrypto}} permissions. For more information about roles and permissions, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).
