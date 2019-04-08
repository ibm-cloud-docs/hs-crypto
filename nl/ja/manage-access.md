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

# ユーザーのアクセス権限の管理
{: #manage-access}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} では、暗号鍵のユーザーおよびアクセス権限の管理に役立つように、{{site.data.keyword.iamlong}} によって管理される集中アクセス制御システムをサポートしています。
{: shortdesc}

新規ユーザーをアカウントまたはサービスに招待する際にアクセス許可を付与することをお勧めします。 例えば、以下のガイドラインについて考慮してください。

- **Cloud IAM 役割を割り当てることで、アカウントのリソースに対するユーザーのアクセス権限を有効にします。**
    管理者の資格情報を共有するのではなく、管理者アカウントの暗号鍵にアクセスする必要があるユーザー向けに新規ポリシーを作成します。 アカウントの管理者には、アカウント内のすべてのリソースに対してアクセス権限を持つ_管理者_ ポリシーが自動的に割り当てられます。
- **必要最小限の有効範囲で、役割および許可を付与します。**
    例えば、ユーザーが指定のスペース内の鍵の概略ビューにのみアクセスする必要がある場合、そのユーザーには、そのスペースに対する_読者_ の役割のみを付与します。
- **アクセス制御の管理および鍵リソースの削除を行うことのできるユーザーを定期的に監査します。**
    ユーザーに対して_管理者_ の役割を付与することは、そのユーザーは他のユーザーのサービス・ポリシーを変更できるだけでなく、リソースを破棄することもできることを意味します。

## 役割と許可
{: #roles}

{{site.data.keyword.iamshort}} (IAM) を使用して、アカウント内のユーザーやリソースに対するアクセス権限を管理および定義できます。

アクセスを簡素化するために、{{site.data.keyword.hscrypto}} は Cloud IAM 役割と調整し、ユーザーが割り当てられている役割に応じて、各ユーザーが異なるビューのサービスを持つようにします。 サービスのセキュリティー管理者は、チームのメンバーに付与する特定の {{site.data.keyword.hscrypto}} 許可に対応する Cloud IAM 役割を割り当てることができます。

次の表は、ID とアクセス役割が {{site.data.keyword.hscrypto}} 許可にどのようにマップされるかを示しています。
<table>
  <tr>
    <th>サービスのアクセス役割</th>
    <th>説明</th>
    <th>アクション</th>
  </tr>
  <tr>
    <td><p>読者</p></td>
    <td><p>読者は、鍵の概略ビューを表示し、ラップおよびアンラップのアクションを実行できます。 読者は、鍵の素材へのアクセスおよび変更はできません。</p></td>
    <td>
      <p>
        <ul>
          <li>鍵の表示</li>
          <li>鍵のラップ</li>
          <li>鍵のアンラップ</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>作成者</p></td>
    <td><p>作成者は、鍵の作成、鍵の変更、および鍵の素材へのアクセスを行えます。</p></td>
    <td>
      <p>
        <ul>
          <li>鍵の作成</li>
          <li>鍵の表示</li>
          <li>鍵のラップ</li>
          <li>鍵のアンラップ</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>管理者</p></td>
    <td><p>管理者は、鍵の削除、新規ユーザーの招待、および他のユーザーに対するアクセス・ポリシーの割り当てなど、読者および作成者が実行できるすべてのアクションを実行できます。</p></td>
    <td>
      <p>
        <ul>
          <li>読者または作成者が実行できるすべてのアクション</li>
          <li>鍵の削除</li>
          <li>アクセス・ポリシーの割り当て</li>
        </ul>
      </p>
    </td>
  </tr>
  <caption style="caption-side:bottom;">表 1. ID およびアクセス役割が {{site.data.keyword.hscrypto}} 許可にどのようにマップされるのかについての説明</caption>
</table>

<!-- **Note**: Cloud IAM user roles provide access at the service or service instance level. [Cloud Foundry roles](/docs/iam/cfaccess.html) are separate and define access at the organization or the space level. -->

{{site.data.keyword.iamshort}} について詳しくは、[ユーザーの役割と許可](/docs/iam/users_roles.html#userroles)を確認してください。

### 次に行うこと
{: #manage-access-next}

アカウントの所有者および管理者は、ユーザーを招待し、ユーザーが実行できる {{site.data.keyword.hscrypto}} アクションに対応するサービス・ポリシーを設定できます。

- {{site.data.keyword.cloud_notm}} UI でのユーザー役割の割り当てについて詳しくは、[IAM アクセス権限の管理](/docs/iam/mngiam.html)を参照してください。
- 特定の暗号鍵にアクセスするための高度な許可の付与については、[鍵へのアクセス権限の管理](/docs/services/hs-crypto/manage-access-api.html)を参照してください。
