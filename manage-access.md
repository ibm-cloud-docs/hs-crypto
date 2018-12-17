---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-02"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Managing user access to keys
{: #manage-access}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} supports a centralized access control system, governed by {{site.data.keyword.iamlong}}, to help you manage users and access for your encryption keys.
{: shortdesc}

A good practice is to grant access permissions as you invite new users to your account or service. For example, consider the following guidelines:

- **Enable user access to the resources in your account by assigning Cloud IAM roles.**
    Rather than sharing your admin credentials, create new policies for users who need access to the encryption keys in your account. If you are the admin for your account, you are automatically assigned a _Manager_ policy with access to all resources under the account.
- **Grant roles and permissions at the smallest scope needed.**
    For example, if a user needs to access only a high-level view of keys within a specified space, grant the _Reader_ role to the user for that space.
- **Regularly audit who can manage access control and delete key resources.**
    Remember that granting a _Manager_ role to a user means that the user can modify service policies for other users, in addition to destroying resources.

## Roles and permissions
{: #roles}

With {{site.data.keyword.iamshort}} (IAM), you can manage and define access for users and resources in your account.

To simplify access, {{site.data.keyword.hscrypto}} aligns with Cloud IAM roles so that each user has a different view of the service, according to the role the user is assigned. If you are a security admin for your service, you can assign Cloud IAM roles that correspond to the specific {{site.data.keyword.hscrypto}} permissions you want to grant to members of your team.

The following table shows how identity and access roles map to {{site.data.keyword.hscrypto}} permissions:
<table>
  <tr>
    <th>Service access role</th>
    <th>Description</th>
    <th>Actions</th>
  </tr>
  <tr>
    <td><p>Reader</p></td>
    <td><p>A reader can browse a high-level view of keys and perform wrap and unwrap actions. Readers cannot access or modify key material.</p></td>
    <td>
      <p>
        <ul>
          <li>View keys</li>
          <li>Wrap keys</li>
          <li>Unwrap keys</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Writer</p></td>
    <td><p>A writer can create keys, modify keys, and access key material.</p></td>
    <td>
      <p>
        <ul>
          <li>Create keys</li>
          <li>View keys</li>
          <li>Wrap keys</li>
          <li>Unwrap keys</li>
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
          <li>All actions that a reader or a writer can perform</li>
          <li>Delete keys</li>
          <li>Assign access policies</li>
        </ul>
      </p>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Table 1. Describes how identity and access roles map to {{site.data.keyword.hscrypto}} permissions</caption>
</table>

**Note**: Cloud IAM user roles provide access at the service or service instance level. [Cloud Foundry roles ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/iam/cfaccess.html){: new_window} are separate and define access at the organization or the space level.

To learn more about {{site.data.keyword.iamshort}}, check out [User roles and permissions ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/iam/users_roles.html#userroles){: new_window}.

### What's next

Account owners and admins can invite users and set service policies that correspond to the {{site.data.keyword.hscrypto}} actions the users can perform.

- For more information about assigning user roles in the {{site.data.keyword.cloud_notm}} UI, see [Managing IAM access ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/iam/mngiam.html){: new_window}.
- To learn about granting advanced permissions to access specific encryption keys, see [Managing access to keys](/docs/services/hs-crypto/manage-access-api.html).
