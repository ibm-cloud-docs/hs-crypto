---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

Keywords: release note, new

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 最新情報
{: #what-new}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} で使用可能な新規フィーチャーに関する最新情報を確認してください。
{: shortdesc}

## 2019 年 3 月
{: #March-2019}

### {{site.data.keyword.hscrypto}} は一般出荷可能
次の時点の最新情報: 2019 年 3 月 29 日

{{site.data.keyword.hscrypto}} のオファリングについて詳しくは、[{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ホーム・ページ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/cloud/hyper-protect-crypto){:new_window} を参照してください。

### 高可用性と災害復旧
次の時点の最新情報: 2019 年 3 月 29 日

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} は、高度に使用可能な地域サービスで、アプリケーションを保護して作動させるための自動機能を備えています。

{{site.data.keyword.hscrypto}} リソースは、サポートされている [{{site.data.keyword.cloud_notm}} 地域](/docs/services/hs-crypto/regions.html)に作成できます。これらの地域は、{{site.data.keyword.hscrypto}} の要求が扱われて処理される地理上のエリアを表します。{{site.data.keyword.cloud_notm}} の各地域には、その地域のローカル・アクセス権限、待ち時間、セキュリティーに関する要件を満たす[複数のアベイラビリティー・ゾーン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/) が用意されています。

詳しくは、[高可用性と災害復旧](/docs/services/hs-crypto/ha-dr.html)を参照してください。

## 2019 年 2 月
{: #Feb-2019}

### {{site.data.keyword.hscrypto}} ベータを使用可能
次の時点の最新情報: 2019 年 2 月 5 日

{{site.data.keyword.hscrypto}} ベータ版がリリースされました。{{site.data.keyword.hscrypto}} サービスに**「カタログ」**>**「セキュリティーおよび ID」**から直接アクセスできるようになりました。

2019 年 2 月 5 日以降、新しい Hyper Protect Crypto Services Experimental インスタンスのプロビジョニングができなくなります。既存のインスタンスは、試験サポートの終了日 (2019 年 3 月 5 日) までサポートされます。

## 2018 年 12 月
{: #Dec-2018}

### 追加: KYOK による HSM 管理のサポート
次の時点の最新情報: 2018 年 12 月 19 日

{{site.data.keyword.hscrypto}} は Keep Your Own Keys (KYOK: 自分の鍵の保持) をサポートするようになったので、保持、制御、管理を行える暗号鍵を使用して、データに対する制御権と権限をさらに強化することができます。{{site.data.keyword.cloud}} コマンド・ライン・インターフェース (CLI) で暗号インスタンス (HSM) を初期化して管理することができます。

詳しくは、[鍵ストレージを保護するための暗号インスタンスの初期化](/docs/services/hs-crypto/initialize_hsm.html)を参照してください。

### 追加: {{site.data.keyword.keymanagementserviceshort}} API の統合
次の時点の最新情報: 2018 年 12 月 19 日

{{site.data.keyword.keymanagementserviceshort}} API は、鍵を生成して保護するために、Hyper Protect Crypto Services と統合されるようになりました。{{site.data.keyword.keymanagementserviceshort}} API は、{{site.data.keyword.hscrypto}} から直接呼び出すことができます。

詳しくは、[API へのアクセス](/docs/services/hs-crypto/access-api.html)および [{{site.data.keyword.hscrypto}} API ![外部リンク・アイコン](image/external_link.svg "外部リンク・アイコン")](https://cloud.ibm.com/apidocs/hs-crypto){:new_window} を参照してください。

### 非推奨: ACSP によって {{site.data.keyword.hscrypto}} にアクセスする機能
次の時点の最新情報: 2018 年 12 月 19 日

現段階では、Advanced Cryptography Service Provider (ACSP) クライアントによる {{site.data.keyword.hscrypto}} へのアクセスは非推奨になっています。以前のサービス・インスタンスを使用している場合は、引き続き ACSP を使用して {{site.data.keyword.hscrypto}} を利用することができます。
