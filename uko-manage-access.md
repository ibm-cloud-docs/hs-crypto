---

copyright:
  years: 2018, 2022
lastupdated: "2022-04-08"

keywords: iam, iam roles, user access, user permissions, manage access, access roles

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}

# Managing user access
{: #uko-manage-access}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} supports a centralized access control system, which is governed by {{site.data.keyword.iamlong}}, to help you manage users and access for your encryption keys.
{: shortdesc}

## Roles and permissions
{: #uko-roles}

The following table shows the roles that {{site.data.keyword.hscrypto}} supports.

| Roles | Permissions |
| ----- | --------------- |
| Service administrator | Manages [platform access](#uko-platform-mgmt-roles) and [service access](#uko-service-access-roles), [grants access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults), creates and deletes service instances, and manages keys. An {{site.data.keyword.cloud_notm}} account owner is automatically assigned the service administrator permission. |
| Crypto unit administrator | Provides signature keys, and signs Trusted Key Entry (TKE) administrative commands such as for adding another crypto unit administrator. In some cases, a crypto unit administrator can also be a master key custodian. |
| Master key custodian | Provides master key parts for initializing a service instance. In some cases, a master key custodian can also be a crypto unit administrator. |
| Certificate administrator | Sets up and manages administrator signature keys and client certificates to enable the second layer of TLS authentication in GREP11 or PKCS #11 API connections. The administrator needs to be assigned the Certificate Manager IAM [service access role](#uko-service-access-roles) to perform the corresponding actions. |
| Service user | Manages root keys and standard keys through user interface and the API, and performs cryptographic operations through the PKCS #11 API or the Enterprise PKCS #11 over gRPC (GREP11) API. Based on the [platform access roles](#uko-platform-mgmt-roles) and [service access roles](#uko-service-access-roles), service users can be further categorized with various permissions. |
{: caption="Table 1. Roles and permissions" caption-side="bottom"}



### IAM platform access roles
{: #uko-platform-mgmt-roles}

With {{site.data.keyword.iamshort}} (IAM), you, as an account owner or a service administrator, can manage and define access for service users and resources in your {{site.data.keyword.cloud_notm}} account.

To simplify access, {{site.data.keyword.hscrypto}} aligns with [IAM roles](/docs/account?topic=account-userroles) so that each user has a different view of the service, according to the role the user is assigned. If you are a service administrator, you can assign Cloud IAM roles that correspond to the specific {{site.data.keyword.hscrypto}} permissions you want to grant to members of your team.

The following table lists the {{site.data.keyword.cloud_notm}} IAM roles in the context of {{site.data.keyword.hscrypto}}. For complete IAM documentation and how to assign access, see [Best practices for setting up custom roles for {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-role-best-practices).
{: note}

Use {{site.data.keyword.cloud_notm}} platform access roles to grant permissions at the account level, such as the ability to create or delete instances in your {{site.data.keyword.cloud_notm}} account.

| Action | Viewer | Editor | Operator | Administrator |
|-----|-----|-----|-----|----|
| View {{site.data.keyword.hscrypto}} instances. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Create {{site.data.keyword.hscrypto}} instances. |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Delete {{site.data.keyword.hscrypto}} instances. | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Invite new users and manage access policies. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
{: caption="Table 2. Lists platform management roles as they apply to {{site.data.keyword.hscrypto}}" caption-side="bottom"}

If you're an account owner, you are automatically assigned _Administrator_ platform access to your {{site.data.keyword.hscrypto}} service instances so you can further assign roles and customize access policies for others.
{: note}

### IAM service access roles
{: #uko-service-access-roles}

As a service administrator, you can use the service access roles to grant permissions of service users at the service level, such as the ability to view, create, or delete {{site.data.keyword.hscrypto}} keys.

- As a **Reader**, you can browse a high-level view of keys. Readers cannot create, modify, or delete keys.
- As a **ReaderPlus**, you have the same permissions as a Reader, with the additional ability to retrieve a standard key's material.
- As a **Writer**, you can create, modify, rotate, and use keys. Writers cannot delete or disable keys.
- As a **Manager**, you can perform all actions that a Reader, ReaderPlus and Writer can perform, including the ability to delete keys and set policies for keys. 
- As a **VMware KMIP Manager**, you can configure KMIP for VMware with {{site.data.keyword.hscrypto}} to enable encryption with your own root keys.

- As a **Certificate Manager**, you can manage administrator signature keys and client certificates for the second layer of authentication in GREP11 or PKCS #11 API connections.
- As a **Vault Administrator**, you can manage vaults, keystores, and templates, and perform destructive lifecycle actions on managed keys in {{site.data.keyword.uko_full_notm}}. Different vaults can be used to separate teams, lines of business, or customers. You can also add paid keystores if you already exceed the limit of free keystores.
- As a **Key Custodian - Creator**, you can create and manage keys in {{site.data.keyword.uko_full_notm}}. For a complete key lifecycle, both the Key Custodian - Creator and Key Custodian - Deployer roles are needed.
- As a **Key Custodian - Deployer**, you can deploy and manage keys in {{site.data.keyword.uko_full_notm}}. For a complete key lifecycle, both the Key Custodian - Creator and Key Custodian - Deployer roles are needed.  

To implement separation of duties, assign Key Custodian - Creator and Key Custodian - Deployer roles to different people.
{: note}


The following table shows how service access roles map to {{site.data.keyword.hscrypto}} permissions. IAM roles are the default roles provided. You can also [define and create service-level custom roles](/docs/account?topic=account-custom-roles) according to the needs of your enterprise.

* Trusted Key Entry (TKE) uses either smart cards or software CLI plug-in with IAM authentication. Commands that deals with managing keys locally on the smart card or CLI are not included. Those commands do not interact with the HSM domain.


* {{site.data.keyword.uko_full_notm}} is used for multicloud key management and orchestration. Apart from setting default IAM roles, you can also [create custom {{site.data.keyword.uko_full_notm}} roles](/docs/hs-crypto?topic=hs-crypto-uko-role-best-practices) according to your needs.



* HSM APIs (the PKCS #11 API and the GREP11 API) are used for application-level encryption.

* Key Management Interoperability Protocol (KMIP) adapter is used to configure the KMIP for VMware service with {{site.data.keyword.hscrypto}} to enable vSphere encryption or vSAN encryption by using your own root keys.

* Certificate Manager Server receives and processes requests for setting up certificate administrator signature keys and client certificates to enable the second layer of authentication in GREP11 or PKCS #11 API connections.

| Action | Reader | ReaderPlus | Writer | Manager |
|--------|--------|------------|--------|---------|
| TKE view state: `ibmcloud tke cryptounit-admins`,`ibmcloud tke cryptounit-compare`,`ibmcloud tke cryptounit-thrhlds`,`ibmcloud tke cryptounit-mk`. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| TKE set context: `ibmcloud tke-cryptounit-add`, `ibmcloud tke-cryptounit-rm`. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| TKE admin add or remove: `ibmcloud tke cryptounit-admin-add`, `ibmcloud tke cryptounit-admin-rm`.| | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| TKE Set Admin Quorum Threshold: `ibmcloud tke -cryptounit-thrhld-set.`|  |  |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | 
| TKE Master Key operations (load, rotate, clear, zeroize, recover): `ibmcloud tke cryptounit-mk-*`, `ibmcloud tke auto-init`, `ibmcloud tke auto-mk-rotate`, `ibmcloud tke auto-recover`. |  |  |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
{: #table-3}
{: caption="Table 3. Lists service access roles as they apply to {{site.data.keyword.hscrypto}} TKE commands" caption-side="bottom"}
{: tab-title="Trusted Key Entry commands"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}


| Action | Reader | Key custodian - Deployer | Key custodian - Creator | Vault administrator | Manager |
|-----|-----|----|----|-----|-----|
| Activate a preactive key. | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | | |  |
| Destroy a preactive key. | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| | |
| Deactivate an active key. | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| | | |
| Install an active key. | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | | |
| Uninstall an active key.| | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| | |
| Destroy a deactivated key. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| |
| Install a deactivated key. | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| | |
| Reactivate a deactivated key. | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| | | |
| Uninstall a deactivated key. | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | | |
| Remove a destroyed key from Vault. | | | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Read managed key details. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| List managed keys. | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Write or edit managed key details. | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | | |
| Delete a managed key. | | | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Generate key materials for a key. | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| | |
| Distribute a key into assigned keystores. | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | | |
| Write key activation or expiration dates. | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | | |
| Write key tags. | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| | |
| Read target keystore details. |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| List target keystores. | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Write or edit target keystore details. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| |
| Delete an internal keystore, or disconnect from an external keystore. | | | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Read key template details. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| List key templates. | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| Write or edit key templates. | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Delete key templates. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| |
| Read vault details. |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| List vaults. | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Write or edit vault details. | | | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Delete a vault. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| |
| Start billing of UKO base price by using external keystores. | | | |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Create a paid keystore beyond the free amount. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")| |
{: #table-4}
{: caption="Table 4. Lists service access roles as they apply to {{site.data.keyword.uko_full_notm}}" caption-side="bottom"}
{: tab-title="{{site.data.keyword.uko_full_notm}}"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}


| Action | Reader | ReaderPlus | Writer | Manager | KMS Key Purge |
|-----|-----|-----|-----|----|------|
| Create a key. | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Import a key. | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Retrieve a key. | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |  ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Retrieve key metadata. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | | |
| Retrieve key total. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| List keys.| ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Wrap a key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Unwrap a key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Rewrap a key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Patch a key. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Rotate a key. | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Disable a key. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Enable a key. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Schedule deletion for a key. | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Cancel deletion for a key. | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Delete a key. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Purge a key.   |   |   |   |   |  ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Restore a key. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Set key policies. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| List key policies. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Set instance policies. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| List instance policies. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Create an import token. | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Retrieve an import token. | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Create a registration.<sup>1</sup> | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| List registrations for a key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| List registrations for any key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Update a registration.<sup>1</sup> | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Replace a registration.<sup>1</sup> | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Delete a registration.<sup>1</sup> | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Create a key ring. | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| List key rings. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Delete a key ring. | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Create a key alias.| | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
| Delete a key alias.| | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | |
{: #table-5}
{: caption="Table 5. Lists service access roles as they apply to {{site.data.keyword.hscrypto}} key resources" caption-side="bottom"}
{: tab-title="Key management service"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}

1: This action is performed on your behalf by an [integrated service](/docs/hs-crypto?topic=hs-crypto-integrate-services) that enables support for key registration. [Learn more](/docs/hs-crypto?topic=hs-crypto-view-protected-resources).

| Action | Reader | ReaderPlus | Writer | Manager |
|-----|-----|-----|-----|----|
| Get mechanism list and information |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Create or delete keystore | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| List keystores | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Generate key | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Generate key pair |  |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Store key |  |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Generate random | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| List keys | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Get or set key attribute | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Wrap key | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Rewrap key | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Unwrap key | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Update key | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Encrypt  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Decrypt | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Sign | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Verify | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Digest | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
{: #table-6}
{: caption="Table 6. Lists service access roles as they apply to HSM APIs" caption-side="bottom"}
{: tab-title="HSM APIs"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}

| Action | Reader | ReaderPlus | Writer | Manager | VMware KMIP Manager |
|-----|-----|-----|-----|----|-----|
| Activate KMIP endpoint. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Deactivate KMIP endpoint. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Get status of KMIP endpoint. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Add client certificates to KMIP endpoint for usage of mutual TLS. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| Delete client certificates from KMIP endpoint for usage of mutual TLS. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
{: #table-7}
{: caption="Table 7. Lists service access roles as they apply to KMIP adapter" caption-side="bottom"}
{: tab-title="KMIP adapter"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}

| Action | Reader | ReaderPlus | Writer | Manager | Certificate Manager |
|-----|-----|-----|-----|----|-----|
| Create the administrator signature key. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Refresh and update the administrator signature key. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Retrieve the administrator signature key of the certificate administrator. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Delete the administrator signature key of the certificate administrator. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| Create or update the client certificates. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| List all client certificates that are managed by the certificate administrator. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Retrieve client certificates. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| Delete client certificates. | | | | | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
{: #table-8}
{: caption="Table 8. Lists service access roles as they apply to Certificate Manager" caption-side="bottom"}
{: tab-title="Certificate Manager Server"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}

## Assigning access to {{site.data.keyword.hscrypto}}
{: #assign-access-iam}

You can assign access to {{site.data.keyword.hscrypto}} through the console, CLI, or API.

### Assigning access to {{site.data.keyword.hscrypto}} in the console
{: #assign-access-console}
{: ui}

There are two common ways to assign access in the console:

* Access policies per user. You can manage access policies per user from the **Manage** > **Access (IAM)** > **Users** page in the console. For information about the steps to assign IAM access, see [Managing access to resources](/docs/account?topic=account-assign-access-resources&interface=ui#access-resources-console).
* Access groups. Access groups are used to streamline access management by assigning access to a group once, then you can add or remove users as needed from the group to control their access. You manage access groups and their access from the **Manage** > **Access (IAM)** > **Access groups** page in the console. For more information, see [Assigning access to a group in the console](/docs/account?topic=account-groups&interface=ui#access_ag).


### Assigning access to {{site.data.keyword.hscrypto}} in the CLI
{: #assign-access-cli}
{: cli}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access ro resources by using the CLI](/docs/account?topic=account-assign-access-resources&interface=cli#access-resources-cli). The following example shows a command for assigning the `Writer` role for the service instance:

Use `<hs-crypto>` for the service name. Also, use quotations around role names that are more than one word like the example here.
{: tip}

```bash
ibmcloud iam user-policy-create USER@EXAMPLE.COM --service-name hs-crypto --service-instance <instance-id> --roles "Writer"
```
{: pre}

### Assigning access to {{site.data.keyword.hscrypto}} by using the API
{: #assign-access-api}
{: api}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the API](/docs/account?topic=account-assign-access-resources&interface=api) or the [Create a policy API docs](/apidocs/iam-policy-management#create-policy). Role cloud resource names (CRN) in the following table are used to assign access with the API.


| Role name | Role CRN | 
|---------------|-----------------|
| Viewer                 | `crn:v1:bluemix:public:hs-crypto::::serviceRole:Viewer`        |
| Operator               | `crn:v1:bluemix:public:hs-crypto::::serviceRole:Operator`      | 
| Editor                 | `crn:v1:bluemix:public:hs-crypto::::serviceRole:Editor`        | 
| Administrator          | `crn:v1:bluemix:public:hs-crypto::::serviceRole:Administrator` | 
| Reader         | `crn:v1:bluemix:public:hs-crypto::::serviceRole:Reader`        |
| ReaderPlus         | `crn:v1:bluemix:public:hs-crypto::::serviceRole:ReaderPlus`        |
| Writer         | `crn:v1:bluemix:public:hs-crypto::::serviceRole:Writer`        | 
| Manager        | `crn:v1:bluemix:public:hs-crypto::::serviceRole:Manager`       | 
| VMware KMIP Manager | `crn:v1:bluemix:public:hs-crypto::::serviceRole:VMwareKMIPManager` | 
| Certificate Manager         | `crn:v1:bluemix:public:hs-crypto::::serviceRole:CertificateManager`        |
| Vault Administrator         | `crn:v1:bluemix:public:hs-crypto::::serviceRole:VaultAdministrator`        |
| Key Custodian - Creator         | `crn:v1:bluemix:public:hs-crypto::::serviceRole:KeyCustodianCreator`   | 
| Key Custodian - Deployer        | `crn:v1:bluemix:public:hs-crypto::::serviceRole:KeyCustodianDeployer`  | 
{: caption="Table 9. Role ID values for API use" caption-side="bottom"}

The following example is for assigning the `Writer` role for the service instance:

Use `<hs-crypto>` for the service name, and refer to the Role ID values table to ensure that you're using the correct value for the CRN.
{: tip}

```curl 
curl -X POST 'https://iam.cloud.ibm.com/v1/policies' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json' -d '{
  "type": "access",
  "description": "Hyper Protect Crypto Services",
  "subjects": [
    {
      "attributes": [
        {
          "name": "iam_id",
          "value": "IBMid-123453user"
        }
      ]
    }'
  ],
  "roles":[
    {
      "role_id": "crn:v1:bluemix:public:hs-crypto::::serviceRole:Writer"
    }
  ],
  "resources":[
    {
      "attributes": [
        {
          "name": "accountId",
          "value": "$ACCOUNT_ID"
        },
        {
          "name": "serviceName",
          "value": "hs-crypto"
        }
      ]
    }
  ]
}
```
{: curl}
{: codeblock}

```java
SubjectAttribute subjectAttribute = new SubjectAttribute.Builder()
      .name("iam_id")
      .value("IBMid-123453user")
      .build();

PolicySubject policySubjects = new PolicySubject.Builder()
      .addAttributes(subjectAttribute)
      .build();

PolicyRole policyRoles = new PolicyRole.Builder()
      .roleId("crn:v1:bluemix:public:hs-crypto::::serviceRole:Writer")
      .build();

ResourceAttribute accountIdResourceAttribute = new ResourceAttribute.Builder()
      .name("accountId")
      .value("ACCOUNT_ID")
      .operator("stringEquals")
      .build();

ResourceAttribute serviceNameResourceAttribute = new ResourceAttribute.Builder()
      .name("serviceName")
      .value("hs-crypto")
      .operator("stringEquals")
      .build();

PolicyResource policyResources = new PolicyResource.Builder()
      .addAttributes(accountIdResourceAttribute)
      .addAttributes(serviceNameResourceAttribute)
      .build();

CreatePolicyOptions options = new CreatePolicyOptions.Builder()
      .type("access")
      .subjects(Arrays.asList(policySubjects))
      .roles(Arrays.asList(policyRoles))
      .resources(Arrays.asList(policyResources))
      .build();

Response<Policy> response = service.createPolicy(options).execute();
Policy policy = response.getResult();

System.out.println(policy);
```
{: java}
{: codeblock}
   
```javascript
const policySubjects = [
  {
    attributes: [
      {
        name: 'iam_id',
        value: 'IBMid-123453user',
      },
    ],
  },
];
const policyRoles = [
  {
    role_id: 'crn:v1:bluemix:public:hs-crypto::::serviceRole:Writer',
  },
];
const accountIdResourceAttribute = {
  name: 'accountId',
  value: 'ACCOUNT_ID',
  operator: 'stringEquals',
};
const serviceNameResourceAttribute = {
  name: 'serviceName',
  value: 'hs-crypto',
  operator: 'stringEquals',
};
const policyResources = [
  {
    attributes: [accountIdResourceAttribute, serviceNameResourceAttribute]
  },
];
const params = {
  type: 'access',
  subjects: policySubjects,
  roles: policyRoles,
  resources: policyResources,
};

iamPolicyManagementService.createPolicy(params)
  .then(res => {
    examplePolicyId = res.result.id;
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: javascript}
{: codeblock}
   
```python
policy_subjects = PolicySubject(
  attributes=[SubjectAttribute(name='iam_id', value='IBMid-123453user')])
policy_roles = PolicyRole(
  role_id='crn:v1:bluemix:public:hs-crypto::::serviceRole:Writer')
account_id_resource_attribute = ResourceAttribute(
  name='accountId', value='ACCOUNT_ID')
service_name_resource_attribute = ResourceAttribute(
  name='serviceName', value='hs-crypto')
policy_resources = PolicyResource(
  attributes=[account_id_resource_attribute,
        service_name_resource_attribute])

policy = iam_policy_management_service.create_policy(
  type='access',
  subjects=[policy_subjects],
  roles=[policy_roles],
  resources=[policy_resources]
).get_result()

print(json.dumps(policy, indent=2))
```
{: python}
{: codeblock}
   
```go
subjectAttribute := &iampolicymanagementv1.SubjectAttribute{
  Name:  core.StringPtr("iam_id"),
  Value: core.StringPtr("IBMid-123453user"),
}
policySubjects := &iampolicymanagementv1.PolicySubject{
  Attributes: []iampolicymanagementv1.SubjectAttribute{*subjectAttribute},
}
policyRoles := &iampolicymanagementv1.PolicyRole{
  RoleID: core.StringPtr("crn:v1:bluemix:public:hs-crypto::::serviceRole:Writer"),
}
accountIDResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("accountId"),
  Value:    core.StringPtr("ACCOUNT_ID"),
  Operator: core.StringPtr("stringEquals"),
}
serviceNameResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("serviceName"),
  Value:    core.StringPtr("hs-crypto"),
  Operator: core.StringPtr("stringEquals"),
}
policyResources := &iampolicymanagementv1.PolicyResource{
  Attributes: []iampolicymanagementv1.ResourceAttribute{
    *accountIDResourceAttribute, *serviceNameResourceAttribute}
}

options := iamPolicyManagementService.NewCreatePolicyOptions(
  "access",
  []iampolicymanagementv1.PolicySubject{*policySubjects},
  []iampolicymanagementv1.PolicyRole{*policyRoles},
  []iampolicymanagementv1.PolicyResource{*policyResources},
)

policy, response, err := iamPolicyManagementService.CreatePolicy(options)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(policy, "", "  ")
fmt.Println(string(b))
```
{: go}
{: codeblock}

### Assigning access to {{site.data.keyword.hscrypto}} by using Terraform
{: #assign-access-terraform}
{: terraform}

The following example is for assigning the `Writer` role for your service instance:

Use `<hs-crypto>` for the service name.
{: tip}

```terraform
resource "ibm_iam_user_policy" "policy" {
  ibm_id = "test@example.com"
  roles  = ["Writer"]

  resources {
    service = "hs-crypto"
  }
}
```
{: codeblock}

For more information, see [ibm_iam_user_policy](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_user_policy){: external}.

## Managing access to multiple instances
{: #uko-manage-multiple-instances}

If you have multiple {{site.data.keyword.hscrypto}} instances in different accounts, you might need to leverage {{site.data.keyword.cloud_notm}} enterprises to manage accounts and user access.

1. **Create the enterprise hierarchy**

    With {{site.data.keyword.cloud_notm}} enterprises, you can centrally manage multiple accounts and resources. You can create an enterprise hierarchy as needed by nesting account groups or accounts within the enterprise account. The access management to the enterprise and the child accounts is isolated to provide greater security. To learn how to create an enterprise and add accounts to an enterprise, see [Getting started with an enterprise](/docs/account?topic=account-enterprise-tutorial) and [Best practices for setting up an enterprise](/docs/account?topic=account-enterprise-best-practices).

2. **Organize account resources in resource groups**

    {{site.data.keyword.hscrypto}} instances are associated with child accounts of the enterprise. Within each account, you can organize service instances in resource groups so that you can assign different access policies to each resource group to enable independent access control. For how to create resource groups and organize resources, see [Best practices for organizing resources](/docs/account?topic=account-account_setup).

3. **Assign access to manage the enterprise and resources**

    Based on the {{site.data.keyword.hscrypto}} IAM [platform roles](#uko-platform-mgmt-roles) and [service roles](#uko-service-access-roles) that are listed, you can assign users respective access to each tier of the enterprise hierarchy. You can also group users or [service IDs](/docs/account?topic=account-serviceids) by defining access groups to streamline the process of assigning access. For more information about assigning access, see [User management for enterprises](/docs/account?topic=account-enterprise-access) and [Managing access to resources](/docs/account?topic=account-assign-access-resources).

4. **Use {{site.data.keyword.cloud_notm}} API keys**

    You can create [{{site.data.keyword.cloud_notm}} API keys](/docs/account?topic=account-manapikey) for users or services to track and control API usage. The user API key is associated with the user identity and inherits all access that the user is assigned. The service API key is granted the access that is associated with a specific service ID. API keys can also be used to [generate IAM tokens](/docs/account?topic=account-iamtoken_from_apikey) for API calls authentication. For how to manage API keys, see [Managing user API keys](/docs/account?topic=account-userapikey) and [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys).

The following example shows how to use the enterprise to manage multiple instances and user access. Assume that your organization has two {{site.data.keyword.hscrypto}} instances for development and production, and two separate teams are managing and operating these instances. you can create the following enterprise hierarchy to better manage accounts, instances, and user access:

![An example of the enterprise hierarchy and user access management](/images/enterprise_hierarchy_example.svg "An example of the enterprise hierarchy and user access management"){: caption="Figure 2. An example of the enterprise hierarchy and user access management" caption-side="bottom"}

- Use separate accounts and distinct resource groups to manage instances for development purpose and production purpose.
- Assign users the minimum access to the corresponding resources. For example, assign the enterprise managers the administrator role for accounts and billing management. Assign the developer team members the editor and manager roles for performing operations toward the development instance. Assign other members the viewer and reader role for viewing only instance resources.

## What's next
{: #uko-manage-access-next}

Account owners and admins can invite users and set service policies that correspond to the {{site.data.keyword.hscrypto}} actions the users can perform. For more information about assigning user roles, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).

