---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-06"

keywords: iam, iam roles, user access, user permissions, manage access, access roles

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:external: target="_blank" .external}

# Managing user access
{: #manage-access}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} supports a centralized access control system, which is governed by {{site.data.keyword.iamlong}}, to help you manage users and access for your encryption keys.
{: shortdesc}

## Roles and permissions
{: #roles}

The following table shows the roles that {{site.data.keyword.hscrypto}} supports.

|Roles|Permissions|
|-----|----------------|
|Service administrator|Manages [platform access](#platform-mgmt-roles) and [service access](#service-access-roles), [grants access to keys](/docs/hs-crypto?topic=hs-crypto-grant-access-keys), creates and deletes service instances, and manages keys. An {{site.data.keyword.cloud_notm}} account owner is automatically assigned the service administrator permission.|
|Crypto unit administrator|Provides signature keys, and signs Trusted Key Entry (TKE) administrative commands such as for adding another crypto unit administrator. In some cases, a crypto unit administrator can also be a master key custodian.|
|Master key custodian|Provides master key parts for initializing a service instance. In some cases, a master key custodian can also be a crypto unit administrator.|
|Service user|Manages root keys and standard keys through user interface and APIs, and performs cryptographic operations through EP11 APIs over gRPC. Based on the [platform access roles](#platform-mgmt-roles) and [service access roles](#service-access-roles), service users can be further categorized with various permissions.|
{: caption="Table 1. Roles and permissions" caption-side="bottom"}

The following diagram illustrates the roles and permissions.

![{{site.data.keyword.hscrypto}} roles](/image/roles.svg "{{site.data.keyword.hscrypto}} roles and responsibilities"){: caption="Figure 1. {{site.data.keyword.hscrypto}} roles and responsibilities" caption-side="bottom"}

### Platform access roles
{: #platform-mgmt-roles}

With {{site.data.keyword.iamshort}} (IAM), you, as an account owner or a service administrator, can manage and define access for service users and resources in your {{site.data.keyword.cloud_notm}} account.

To simplify access, {{site.data.keyword.hscrypto}} aligns with IAM roles so that each user has a different view of the service, according to the role the user is assigned. If you are a service administrator, you can assign Cloud IAM roles that correspond to the specific {{site.data.keyword.hscrypto}} permissions you want to grant to members of your team.

This section discusses {{site.data.keyword.cloud_notm}} IAM roles in the context of {{site.data.keyword.hscrypto}}. For complete IAM documentation and how to assign access, see [Managing access in {{site.data.keyword.cloud_notm}}](/docs/iam?topic=iam-cloudaccess).
{: note}

Use {{site.data.keyword.cloud_notm}} platform access roles to grant permissions at the account level, such as the ability to create or delete instances in your {{site.data.keyword.cloud_notm}} account.

| Action | Viewer | Editor | Operator | Admininistrator |
|-----|-----|-----|-----|----|
| View {{site.data.keyword.hscrypto}} instances | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Create {{site.data.keyword.hscrypto}} instances |  | ![Check mark icon](../icons/checkmark-icon.svg) | | ![Check mark icon](../icons/checkmark-icon.svg) |
| Delete {{site.data.keyword.hscrypto}} instances | | ![Check mark icon](../icons/checkmark-icon.svg) |  | ![Check mark icon](../icons/checkmark-icon.svg) |
| Invite new users and manage access policies | | | | ![Check mark icon](../icons/checkmark-icon.svg) |
{: caption="Table 2. Lists platform management roles as they apply to {{site.data.keyword.hscrypto}}" caption-side="top"}

If you're an account owner, you are automatically assigned _Administrator_ platform access to your {{site.data.keyword.hscrypto}} service instances so you can further assign roles and customize access policies for others.
{: note}

### Service access roles
{: #service-access-roles}

As a service administrator, use the service access roles to grant permissions of service users at the service level, such as the ability to view, create, or delete {{site.data.keyword.hscrypto}} keys.

- As a **Reader**, you can browse a high-level view of keys and perform wrap and unwrap actions. Readers cannot access or modify key material.
- As a **ReaderPlus**, you can browse a high-level view of keys, access key material for standard keys, and perform wrap and unwrap actions. The ReaderPlus role cannot modify key material.
- As a **Writer**, you can create keys, modify keys, rotate keys, and access key.
- As a **Manager**, you can perform all actions that a Reader, ReaderPlus and Writer can perform, including the ability to delete keys and set dual authorization and rotation policies for keys.

The following table shows how service access roles map to {{site.data.keyword.hscrypto}} permissions.

| Action | Reader | ReaderPlus | Writer | Manager |
|-----|-----|-----|-----|----|
| Create a key | | | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Import a key | | | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Retrieve a key | | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Retrieve key metadata | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| List keys | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Wrap a key | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Unwrap a key | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Rewrap a key | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Rotate a key | | | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Disable a key | | | | ![Check mark icon](../icons/checkmark-icon.svg) |
| Enable a key | | | | ![Check mark icon](../icons/checkmark-icon.svg) |
| Schedule deletion for a key | | | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Cancel deletion for a key | | | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Delete a key | | | | ![Check mark icon](../icons/checkmark-icon.svg) |
| Restore a key | | | | ![Check mark icon](../icons/checkmark-icon.svg) |
{: #table-3}
{: caption="Table 3. Lists service access roles as they apply to {{site.data.keyword.hscrypto}} key resources" caption-side="top"}
{: tab-title="Keys"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}

| Action | Reader | ReaderPlus | Writer | Manager |
|-----|-----|-----|-----|----|
| Set key policies | | | | ![Check mark icon](../icons/checkmark-icon.svg) |
| List key policies | | | | ![Check mark icon](../icons/checkmark-icon.svg) |
| Set instance policies | | | | ![Check mark icon](../icons/checkmark-icon.svg) |
| List instance policies | | | | ![Check mark icon](../icons/checkmark-icon.svg) |
{: #table-3}
{: caption="Table 3. Lists service access roles as they apply to {{site.data.keyword.hscrypto}} policy resources" caption-side="top"}
{: tab-title="Policies"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}

| Action | Reader | ReaderPlus | Writer | Manager |
|-----|-----|-----|-----|----|
| Create an import token | | | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Retrieve an import token | | | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
{: #table-4}
{: caption="Table 4. Lists service access roles as they apply to import token resources" caption-side="top"}
{: tab-title="Import tokens"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}

| Action | Reader | ReaderPlus | Writer | Manager |
|-----|-----|-----|-----|----|
| Create a registration[^services-1] | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| List registrations for a key | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| List registrations for any key | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Update a registration[^services-2] | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Replace a registration[^services-3] | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
| Delete a registration[^services-4] | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
{: #table-5}
{: caption="Table 5. Lists service access roles as they apply to {{site.data.keyword.hscrypto}} registration resources" caption-side="top"}
{: tab-title="Registrations"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}

[^services-1]: This action is performed on your behalf by an [integrated service](/docs/hs-crypto?topic=hs-crypto-integrate-services) that has enabled support for key registration. [Learn more](/docs/hs-crypto?topic=hs-crypto-view-protected-resources)

[^services-2]: This action is performed on your behalf by an [integrated service](/docs/hs-crypto?topic=hs-crypto-integrate-services) that has enabled support for key registration. [Learn more](/docs/hs-crypto?topic=hs-crypto-view-protected-resources)

[^services-3]: This action is performed on your behalf by an [integrated service](/docs/hs-crypto?topic=hs-crypto-integrate-services) that has enabled support for key registration. [Learn more](/docs/hs-crypto?topic=hs-crypto-view-protected-resources)

[^services-4]: This action is performed on your behalf by an [integrated service](/docs/hs-crypto?topic=hs-crypto-integrate-services) that has enabled support for key registration. [Learn more](/docs/hs-crypto?topic=hs-crypto-view-protected-resources)

| Action | Reader | ReaderPlus | Writer | Manager |
|-----|-----|-----|-----|----|
| Perform cryptographic operations through GREP11 APIs | ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg)| ![Check mark icon](../icons/checkmark-icon.svg) | ![Check mark icon](../icons/checkmark-icon.svg) |
{: #table-6}
{: caption="Table 6. Lists service access roles as they apply to GREP11 resources" caption-side="top"}
{: tab-title="GREP11"}
{: tab-group="IAM-roles"}
{: class="comparison-tab-table"}

## Managing access to multiple instances
{: #manage-multiple-instances}

If you have multiple {{site.data.keyword.hscrypto}} instances in different accounts, you might need to leverage {{site.data.keyword.cloud_notm}} enterprises to manage accounts and user access.

1. **Create the enterprise hierarchy**

  {{site.data.keyword.cloud_notm}} enterprises enable you to centrally manage multiple accounts and resources. You can create an enterprise hierarchy as needed by nesting account groups or accounts within the enterprise account. The access management to the enterprise and its child accounts is isolated to provide greater security. To learn how to create an enterprise and add accounts to an enterprise, refer to [Getting started with an enterprise](/docs/account?topic=account-enterprise-tutorial) and [Best practices for setting up an enterprise](/docs/account?topic=account-enterprise-best-practices).

2. **Organize account resources in resource groups**

  {{site.data.keyword.hscrypto}} instances are associated with child accounts of the enterprise. Within each account, you can organize service instances in resource groups, so that you can assign different access policies to each resource group to enable independent access control. For how to create resource groups and organize resources, refer to [Best practices for organizing resources in a resource group](/docs/resources?topic=resources-bp_resourcegroups).

3. **Assign access to manage the enterprise and resources**

  Based on the {{site.data.keyword.hscrypto}} IAM [platform roles](#platform-mgmt-roles) and [service roles](#service-access-roles) listed above, you can assign users respective access to each tier of the enterprise hierarchy. You can also group users or [service IDs](/docs/iam?topic=iam-serviceids) by defining access groups to streamline the process of assigning access. For detailed information on assigning access, refer to [User management for enterprises](/docs/iam?topic=iam-enterprise-access) and [Best practices for assigning access](/docs/iam?topic=iam-account_setup).

4. **Use {{site.data.keyword.cloud_notm}} API keys**

  You can create [{{site.data.keyword.cloud_notm}} API keys](/docs/iam?topic=iam-manapikey) for users or services to track and control API usage. The user API key is associated with the user identity and inherits all access that the user is assigned. The service API key is granted the access that is associated with a specific service ID. API keys can also be used to [generate IAM tokens](/iam?topic=iam-iamtoken_from_apikey) for API calls authentication. For how to manage API keys, refer to [Managing user API keys](/docs/iam?topic=iam-userapikey) and [Managing service ID API keys](/docs/iam?topic=iam-serviceidapikeys).

The following is an example of how to use the enterprise to manage multiple instances and user access. Assume your organization has two {{site.data.keyword.hscrypto}} instances for development and production, and there are two separate teams managing and operating these instances. you can create the following enterprise hierarchy to better manage accounts, instances, and user access:

![An example of the enterprise hierarchy and user access management](/image/enterprise_hierarchy_example.svg "An example of the enterprise hierarchy and user access management"){: caption="Figure 2. An example of the enterprise hierarchy and user access management" caption-side="bottom"}

- Use separate accounts and distinct resource groups to manage instances for development purpose and production purpose.
- Assign users the minimum access to the corresponding resources. For example, assign the enterprise managers the administrator role for accounts and billing management; assign the developer team members the editor and manager roles for performing operations towards the development instance; assign other members the viewer and reader role for only viewing instance resources.

## What's next
{: #manage-access-next}

Account owners and admins can invite users and set service policies that correspond to the {{site.data.keyword.hscrypto}} actions the users can perform.

For more information about assigning user roles, see [Managing IAM access](/docs/iam?topic=iam-iammanidaccser).
