---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: root keys, master keys, standard keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# 鍵の概要
{: #introduce-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} は、ルート鍵、標準鍵、マスター鍵など、いくつかの鍵タイプをサポートします。
{:shortdesc}

## ルート鍵

*ルート鍵* は、ユーザーが {{site.data.keyword.hscrypto}} 内で完全に管理する、対称鍵ラップ鍵です。 ルート鍵を使用して、拡張暗号化によって他の暗号鍵を保護できます。 詳しくは、<a href="/docs/services/key-protect/concepts/envelope-encryption.html">エンベロープ暗号化</a>を参照してください。

[鍵の管理](/docs/services/hs-crypto/index.html#manage-keys)の手順を実行することで、ルート鍵を管理できます。

## 標準鍵

*標準鍵* は、暗号化に使用される対称鍵です。 標準鍵を使用して、直接、データを暗号化および暗号化解除できます。

[鍵の管理](/docs/services/hs-crypto/index.html#manage-keys)の手順を実行することで、標準鍵を管理できます。

## マスター鍵

*マスター鍵*は、ルート鍵と標準鍵を暗号化処理して管理する暗号インスタンス (HSM) を暗号化するときに使用します。マスター鍵を使用することによって、お客様はルート鍵や標準鍵などの鍵のチェーン全体を暗号化する Root of Trust (信頼の基点) を所有します。

暗号インスタンス (HSM) に対してはエンドツーエンドのセキュア・チャネルが設定されているので、{{site.data.keyword.hscrypto}} インスタンスの管理者のみがそのマスター鍵を設定して管理することができます。IBM では、マスター鍵をバックアップしたり関与したりすることはなく、別のマシンやデータ・センターにコピーしたりリストアしたりする手段はないことに注意してください。

1 つの暗号インスタンス (HSM) で設定できるマスター鍵は 1 つだけです。{{site.data.keyword.hscrypto}} インスタンスのマスター鍵を削除すると、そのサービスで管理されている鍵で暗号化されたすべてのデータの暗号破棄作業を効率的に行うことができます。

[鍵ストレージを保護するために暗号インスタンスを初期化](/docs/services/hs-crypto/initialize_hsm.html)する際に、マスター鍵を管理できます。

マスター鍵のローテーションは、現段階ではサポートされていません。
{:important}
