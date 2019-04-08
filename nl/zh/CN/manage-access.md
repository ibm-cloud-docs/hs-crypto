---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

Keywords: user access, Cloud IAM roles, encryption keys

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 管理用户访问权
{: #manage-access}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} 支持由 {{site.data.keyword.iamlong}} 管理的集中访问控制系统来帮助您管理加密密钥的用户和访问权。
{: shortdesc}

比较好的做法是在邀请新用户加入您的帐户或服务时，授予访问许可权。例如，考虑以下准则：

- **通过分配 Cloud IAM 角色，启用对帐户中资源的用户访问权。**
    为需要访问您帐户中加密密钥的用户创建新策略，而不是共享您的管理凭证。如果您是帐户的管理者，那么会自动分配有_管理者_策略，具有对该帐户下所有资源的访问权。
- **在所需最小作用域下授予角色和许可权。**
    例如，如果用户仅需要访问指定空间内密钥的高级视图，请向该用户授予该空间的_读取者_角色。
- **定期审计谁可管理访问控制和删除密钥资源。**
    请记住，向用户授予_管理者_角色意味着该用户除了可以销毁资源外，还可以修改其他用户的服务策略。

## 角色和许可权
{: #roles}

使用 {{site.data.keyword.iamshort}} (IAM) 可以管理和定义帐户中用户和资源的访问权。

为了简化访问，{{site.data.keyword.hscrypto}} 与 Cloud IAM 角色保持一致，以便每个用户都能根据为该用户分配的角色来查看该服务的不同方面。如果您是服务的安全管理员，那么可以分配对应于您要授予团队成员的特定 {{site.data.keyword.hscrypto}} 许可权的 Cloud IAM 角色。

下表显示身份和访问角色如何映射到 {{site.data.keyword.hscrypto}} 许可权：
<table>
  <tr>
    <th>服务访问角色</th>
    <th>描述</th>
    <th>操作</th>
  </tr>
  <tr>
    <td><p>读取者</p></td>
    <td><p>读取者可以浏览密钥的高级视图并执行打包和解包操作。读取者无法访问或修改密钥资料。</p></td>
    <td>
      <p>
        <ul>
          <li>查看密钥</li>
          <li>打包密钥</li>
          <li>解包密钥</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>写入者</p></td>
    <td><p>写入者可以创建密钥、修改密钥以及访问密钥资料。</p></td>
    <td>
      <p>
        <ul>
          <li>创建密钥</li>
          <li>查看密钥</li>
          <li>打包密钥</li>
          <li>解包密钥</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>管理者</p></td>
    <td><p>管理者可以执行读取者和写入者可执行的所有操作，包括能够删除密钥、邀请新用户以及为其他用户分配访问策略。</p></td>
    <td>
      <p>
        <ul>
          <li>读取者或写入者可以执行的所有操作</li>
          <li>删除密钥</li>
          <li>分配访问策略</li>
        </ul>
      </p>
    </td>
  </tr>
  <caption style="caption-side:bottom;">表 1. 描述身份和访问角色如何映射到 {{site.data.keyword.hscrypto}} 许可权</caption>
</table>

<!-- **Note**: Cloud IAM user roles provide access at the service or service instance level. [Cloud Foundry roles](/docs/iam/cfaccess.html) are separate and define access at the organization or the space level. -->

要了解有关 {{site.data.keyword.iamshort}} 的更多信息，请查看[用户角色和许可权](/docs/iam/users_roles.html#userroles)。


### 后续工作
{: #manage-access-next}

帐户所有者和管理员可以邀请用户并设置对应于用户可以执行的 {{site.data.keyword.hscrypto}} 操作的服务策略。

- 有关在 {{site.data.keyword.cloud_notm}} UI 中分配用户角色的更多信息，请参阅[管理 IAM 访问权](/docs/iam/mngiam.html)。
- 要了解有关授予高级许可权以访问特定加密密钥的信息，请参阅[管理对密钥的访问权](/docs/services/hs-crypto/manage-access-api.html)。
