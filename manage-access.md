---

copyright:
  years: 2018, 2019
lastupdated: "2020-03-30"

keywords: user access, IBM Cloud IAM roles, encryption keys, user permissions, manage access

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

![{{site.data.keyword.hscrypto}} roles](/image/roles.svg "{{site.data.keyword.hscrypto}} roles and responsibilities"){: caption="Figure 2. {{site.data.keyword.hscrypto}} roles and responsibilities" caption-side="bottom"}

### Platform access roles
{: #platform-mgmt-roles}

With {{site.data.keyword.iamshort}} (IAM), you, as an account owner or a service administrator, can manage and define access for service users and resources in your {{site.data.keyword.cloud_notm}} account.

To simplify access, {{site.data.keyword.hscrypto}} aligns with IAM roles so that each user has a different view of the service, according to the role the user is assigned. If you are a service administrator, you can assign Cloud IAM roles that correspond to the specific {{site.data.keyword.hscrypto}} permissions you want to grant to members of your team.

This section discusses {{site.data.keyword.cloud_notm}} IAM in the context of {{site.data.keyword.hscrypto}}. For complete IAM documentation, see [Managing access in {{site.data.keyword.cloud_notm}}](/docs/iam?topic=iam-cloudaccess).
{: note}

Use {{site.data.keyword.cloud_notm}} platform access roles to grant permissions at the account level, such as the ability to create or delete instances in your {{site.data.keyword.cloud_notm}} account.

| Action | Viewer | Editor | Operator | Admininistrator |
|-----|-----|-----|-----|----|
| View {{site.data.keyword.hscrypto}} instances | ![Check mark icon](../../icons/checkmark-icon.svg) | ![Check mark icon](../../icons/checkmark-icon.svg) | ![Check mark icon](../../icons/checkmark-icon.svg) | ![Check mark icon](../../icons/checkmark-icon.svg) |
| Create {{site.data.keyword.hscrypto}} instances |  | ![Check mark icon](../../icons/checkmark-icon.svg) | | ![Check mark icon](../../icons/checkmark-icon.svg) |
| Delete {{site.data.keyword.hscrypto}} instances | | ![Check mark icon](../../icons/checkmark-icon.svg) |  | ![Check mark icon](../../icons/checkmark-icon.svg) |
| Invite new users and manage access policies | | | | ![Check mark icon](../../icons/checkmark-icon.svg) |
{: caption="Table 2. Lists platform management roles as they apply to {{site.data.keyword.hscrypto}}" caption-side="top"}

If you're an account owner, you are automatically assigned _Administrator_ platform access to your {{site.data.keyword.hscrypto}} service instances so you can further assign roles and customize access policies for others.
{: note}

### Service access roles
{: #service-access-roles}

As a service administrator, use the service access roles to grant permissions of service users at the service level, such as the ability to view, create, or delete {{site.data.keyword.hscrypto}} keys.

- As a **Reader**, you can browse a high-level view of keys and perform wrap and unwrap actions. Readers cannot access or modify key material.
- As a **Writer**, you can create keys, modify keys, rotate keys, and access key.
- As a **Manager**, you can perform all actions that a Reader, ReaderPlus and Writer can perform, including the ability to delete keys and set dual authorization and rotation policies for keys.

The following table shows how identity and access roles map to {{site.data.keyword.hscrypto}} permissions:
<table>
  <tr>
    <th>Service access role</th>
    <th>Description</th>
    <th>Actions</th>
  </tr>
  <tr>
    <td><p>Reader</p></td>
    <td><p>A reader can browse a high-level view of keys and perform wrap and unwrap actions. Readers can't access or modify key material.</p></td>
    <td>
      <p>
        <ul>
          <li>View keys.</li>
          <li>Wrap keys.</li>
          <li>Unwrap keys.</li>
          <li>Rewrap keys.</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Writer</p></td>
    <td><p>A writer can create keys, modify keys, rotate keys, and access key material.</p></td>
    <td>
      <p>
        <ul>
          <li>Create keys.</li>
          <li>View keys.</li>
          <li>Rotate keys.</li>
          <li>Wrap keys.</li>
          <li>Unwrap keys.</li>
          <li>Rewrap keys.</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Manager</p></td>
    <td><p>A manager can perform all actions that a reader and writer can perform, including the ability to delete keys, invite new users, and assign access policies for other users.</p></td>
    <td>
      <p>
        <ul>
          <li>All actions that a reader or a writer can perform.</li>
          <li>Delete keys.</li>
        </ul>
      </p>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Table 1. Describes how identity and access roles map to {{site.data.keyword.hscrypto}} permissions</caption>
</table>

To learn more about {{site.data.keyword.iamshort}}, check out [User roles and permissions](/docs/iam?topic=iam-userroles#userroles).

## What's next
{: #manage-access-next}

Account owners and admins can invite users and set service policies that correspond to the {{site.data.keyword.hscrypto}} actions the users can perform.

For more information about assigning user roles in the {{site.data.keyword.cloud_notm}} UI, see [Managing IAM access](/docs/iam?topic=iam-iammanidaccser).
