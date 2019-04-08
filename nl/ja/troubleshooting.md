---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: troubleshoot, problems, known issues

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}

# トラブルシューティング
{: #troubleshooting}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} の使用に関する一般的な問題には、API との対話の際に正しいヘッダーまたは資格情報を提供することが含まれることがあります。 多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{: shortdesc}

## 初期化されたサービス・インスタンスを削除する際にエラーが発生する
{: #troubleshoot-delete-instance}

初期化されたサービス・インスタンスを削除する際に、以下のようなエラーを受け取ることがあります。

```
FAILED
Error response from server. Status code: 400; description: 400 DELETE https://zCryptoBroker.mybluemix.net/v2/service_instances/ failed with error status 409. Conflict.
```
{: codeblock}
{: tsSymptoms}

インスタンスを削除する前に、初期化されたサービス・インスタンスをクリア (ゼロ化) していませんでした。
{: tsCauses}

インスタンスを削除する前に、次のコマンドを実行してください。
{: tsResolve}

```
ibmcloud tke domain-zeroize
```
{: codeblock}

## Trusted Key Entry プラグインに関連したコマンドの実行後の無許可トークン
{: #troubleshoot-unauthorized-token}

`tke` CLI コマンドを実行した後に以下のようなメッセージを受け取ることがあります。

```
ibmcloud tke domains
FAILED
Error querying crypto instances.
Status code: 401
Message: Unauthorized
Your access token is invalid, expired, or does not have the necessary permissions to access this instance.`
```
{: codeblock}
{: tsSymptoms}

トークンが更新されていません。
{: tsCauses}

`ibmcloud login` コマンドにより {{site.data.keyword.cloud_notm}} に再びログインして、トークンを更新します。
{: tsResolve}

## CLI または API の使用時に `error CKR_IBM_WK_NOT_INITIALIZED` を受け取った
{: #troubleshoot-error-CLI-API}

CLI または API を使用する際に、以下のようなエラー・メッセージを受け取ることがあります。

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

`ibmcloud tke domain-compare` コマンドを実行したときに、CURRENT MASTER KEY REGISTER で `Valid` 確認を受け取りませんでした。
{: tsCauses}

HSM マスター鍵が適切に設定されていることを確認してください。
{: tsResolve}

## 鍵の作成または削除ができない
{: #unable-to-create-keys}

{{site.data.keyword.hscrypto}} ユーザー・インターフェースにアクセスしたときに、鍵の追加や削除のためのオプションが表示されません。

{{site.data.keyword.cloud_notm}} ダッシュボードで、{{site.data.keyword.hscrypto}} サービスのインスタンスを選択します。
{: tsSymptoms}

鍵のリストは表示されますが、鍵の追加や削除のためのオプションが表示されません。

{{site.data.keyword.hscrypto}} アクションを実行するための正しい許可を持っていません。
{: tsCauses}

該当するリソース・グループまたはサービス・インスタンスにおいて正しい役割を割り当てられているかどうか、管理者と共に検証してください。 役割について詳しくは、[役割と許可](/docs/services/key-protect/manage-access.html#roles)を参照してください。
{: tsResolve}

## ヘルプおよびサポートの利用
{: #getting-help}

{{site.data.keyword.hscrypto}} の使用中に問題や質問が生じた場合は、{{site.data.keyword.cloud_notm}} を調べてください。または、フォーラムで情報を検索したり質問したりして役に立つ情報を得ることもできます。 サポート・チケットを開くこともできます。
{: shortdesc}

[「状況」ページ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/status?tags=platform,runtimes,services) にアクセスして、{{site.data.keyword.cloud_notm}} が使用可能かどうかを確認できます。

フォーラムを参照して、他のユーザーも同じ問題を経験していないか調べることができます。 フォーラムを使用して質問するときは、{{site.data.keyword.cloud_notm}} 開発チームの目に止まるように、質問にタグを付けてください。

- {{site.data.keyword.hscrypto}} について技術的な質問がある場合は、[スタック・オーバーフロー ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://stackoverflow.com/questions/tagged/hyper-protect-crypto){: new_window} に質問を投稿し、その質問に「ibm-cloud」と「hyper-protect-crypto」のタグを付けてください。
- サービスや使用開始の手順についての質問には、[IBM developerWorks dW Answers ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/answers/topics/hyper-protect-crypto/){: new_window} フォーラムを使用してください。 「ibm-cloud」と「hyper-protect-crypto」のタグを付けてください。

フォーラムの使用について詳しくは、[ヘルプの利用 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/get-support?topic=get-support-using-avatar#using-avatar){: new_window} を参照してください。

{{site.data.keyword.IBM_notm}} サポート・チケットのオープンや、サポート・レベルおよびチケットの重大度について詳しくは、[サポートへの問い合わせ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/get-support?topic=get-support-getting-customer-support){: new_window} を参照してください。
