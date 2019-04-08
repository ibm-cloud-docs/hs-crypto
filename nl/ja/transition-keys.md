---

copyright:
years: 2018, 2019
lastupdated: "2019-03-26"

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

# ベータ・サービス・インスタンスからの鍵の移行
{: #migrate-keys}

ベータ・サービス・インスタンスを使用しており、管理しているルート鍵と標準鍵を {{site.data.keyword.hscrypto}} の実働サービス・インスタンスに移行する場合は、以下の手順に従ってください。
{: shortdesc}

マスター鍵は暗号装置から抽出できないため、IBM Cloud 管理者はマスター鍵を移行できません。マスター鍵を使用して実動サービス・インスタンスを初期化する必要があります。
{:important}  

## 始めに
{: #migrate-prerequisites}

1. Hyper Protect Crypto Services プランを使用して[サービス・インスタンスを作成します](/docs/services/hs-crypto/provision.html)。

2. Trusted Key Entry プラグインを使用して[サービス・インスタンスを初期化します](/docs/services/hs-crypto/initialize_hsm.html)。

## 鍵の移行
{: #migrate-keys-steps}  

ルート鍵と標準鍵を実稼働環境に移行するには、以下の手順を実行します。

1. GUI か API のいずれかを使用して、[ルート鍵をインポートします](/docs/services/hs-crypto/import-root-keys.html)。

  インポートしたルート鍵をベータ・サービス・インスタンスから実動サービス・インスタンスに移行できます。
  {:tip}

2. ベータ・サービス・インスタンスからデータ暗号化鍵 (DEK) をアンラップし、実動サービス・インスタンスに DEK をラップします。

  1. [invoke-an-action-on-a-key API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: new_window}を使用して、ベータ・サービス・インスタンスから[データ暗号化鍵 (DEK) をアンラップします](/docs/services/hs-crypto/unwrap-keys.html)。

  2. [invoke-an-action-on-a-key API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key{: new_window})を使用して、実動サービス・インスタンスに[DEK をラップします](/docs/services/hs-crypto/wrap-keys.html)。

3. 次の手順に従って標準鍵を再作成します。

  1. [retrieve-key-by-id API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/hs-crypto#retrieve-a-key-by-id){: new_window}を使用して、[標準鍵を取得します](/docs/services/hs-crypto?topic=hs-crypto-view-keys#retrieve-key-api)。これにより、ベータ・インスタンスで鍵を作成するために使用されるペイロードが返されます。

  2. GUI または [create-a-new-key API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/hs-crypto#create-a-new-key){: new_window}によって前のステップで取得した情報を使用して、新規サービス・インスタンスに[標準鍵を作成します](/docs/services/hs-crypto/create-standard-keys.html)。

## 次に行うこと
{: #migration-next}

プログラムでの鍵の管理について詳しくは、[{{site.data.keyword.hscrypto}} API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/hs-crypto){: new_window} を確認してください。
