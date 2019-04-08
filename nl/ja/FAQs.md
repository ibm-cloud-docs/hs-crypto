---

copyright:
  years: 2018, 2019
lastupdated: "2019-33-22"

Keywords: frequently asked questions, critical security parameters, cryptographic module, Security Level

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# FAQ
{: #faqs}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} の使用に役立つ FAQ を以下に記載します。

## HSM 認証
{: #HSM-certifications}

### IBM Crypto Card (HSM) が FIPS 140-2 レベル 4 に適合すると検証されていることをどのように確認できますか?
{: #FIPS-L4}

FIPS 140-2 レベル 4 はきわめて高度な保護レベルであり、市場に広く出回っているものではありません。 IBM は最高レベルの認証済み HSM を提供するトップ企業であり、新しい世代のすべてのカードでこの検証を維持することにかなりの投資をしてきました。 高水準の保証を行うための要件は、政府が規定した要件から収集されています。 認証を検証するためには、認証が公表されている NIST ホーム・ページを参照してください。

### FIPS 140-2 のレベル 2、レベル 3、レベル 4 の間にはどのような違いがありますか?
{: #FIPS-levels}

* FIPS 140-2 レベル 2: 改ざんの証拠が残るシールを使うことや、取り外し可能なカバーやドアにはこじ開け防止ロックを付けることが要件となります。 改ざんの証拠が残るコーティングやシールが暗号モジュールに付いているので、モジュール内にある平文の暗号鍵やクリティカル・セキュリティー・パラメーター (CSP) に物理的にアクセスするためにはコーティングまたはシールを破損することが必要になります。 セキュリティー・レベル 2 では、少なくとも役割ベースの認証が必要となります。つまり、オペレーターが特定の役割を担ってそれに対応した一連のサービスを実行する許可を、暗号モジュールで認証します。

* FIPS 140-2 レベル 3: セキュリティー・レベル 3 で必要となる物理的セキュリティー・メカニズムは、暗号モジュールへの物理アクセス、使用、または変更の試行を、高い確率で検出して対応することを意図しています。 セキュリティー・レベル 3 では、ID ベースの認証メカニズムが必要になります。これは、セキュリティー・レベル 2 で規定された役割ベースの認証メカニズムによるセキュリティーを強化するものです。

* FIPS 140-2 レベル 4: このセキュリティー・レベルでは、すべての不正な物理アクセスの試行を検出して対応するという目的で、物理的セキュリティー・メカニズムにより暗号モジュールの周りに完全な保護エンベロープが提供されます。 暗号モジュールの格納装置にどの方向から侵入しようとしても非常に高い確率で検出されて、すべての平文 CSP (クリティカル・セキュリティー・パラメーター) が即時にゼロ化されます。 セキュリティー・レベル 4 の暗号モジュールは、物理的に保護されていない環境で運用する場合に役立ちます。 セキュリティー・レベル 4 はまた、環境条件や変動により電圧や温度がモジュールの通常運用の範囲外になっても、暗号モジュールからセキュリティー情報が漏えいしないように保護します。 攻撃者は、通常運用の範囲外に意図的に逸脱させることにより、暗号モジュールの保護を妨害することがあります。

## 鍵管理
{: #key-management}

### {{site.data.keyword.hscrypto}} は {{site.data.keyword.keymanagementserviceshort}} サービスと組み合わせて使用できますか?

 {{site.data.keyword.hscrypto}} は、完全互換の {{site.data.keyword.keymanagementserviceshort}} API が同梱された管理対象の暗号サービスで、Key Protect と同一のユーザー・エクスペリエンスを提供します。 主な相違点は、{{site.data.keyword.hscrypto}} が FIPS 140-2 レベル 4 認証の HSM に依存していることです。 また、お客様が管理する HSM マスター鍵 (KYOK) で完全に制御できます。 このサービスはインスタンスごとの専用サービスですが、{{site.data.keyword.keymanagementserviceshort}} はマルチテナントのセットアップになります。 {{site.data.keyword.hscrypto}} はまた、署名/検証、鍵生成、暗号ハッシュ、暗号化/復号、ラップ/アンラップなど、暗号操作のための HSM 機能も提供します。

### 鍵の名前はどのくらいの長さにできますか。
{: #key_names}

最大 50 文字の長さの鍵の名前を使用できます。

### 鍵の名前の一部として言語文字を使用できますか。
{: #key_chars}

鍵の名前の一部として言語文字 (例えば、漢字) を使用することはできません。

### 鍵を削除するとどうなりますか。
{: #key_destruction}

鍵を削除すると、その内容と関連データが完全に廃棄されます。 その鍵で暗号化されたデータにはアクセスできなくなります。

鍵を削除する前に、その鍵と関連付けられたデータにはもうアクセスする必要がないことを確認してください。

<!-- ## Pricing
{: #pricing}

### Where can I find the detailed pricing information?
{: #pricing_info}

You can refer to the **Pricing** tab on the [{{site.data.keyword.hscrypto}} home page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/hyper-protect-crypto){: new_window} for details.

### Is there a pricing example I can refer to?
{: #pricing_example}

Here is one. If you have a requirement of 5000 keys to be crypto-processed, for high availability, you need to set up two crypto units. The amount is $3140 ($1570 per crypto unit) per month. The first 1,000,000 API calls are free of charge. However, if you perform 2,000,000 API calls per month, you will be charged additional $1 ($0.01 per 10,000 API calls over 1,000,000 API calls). In total, there will be a monthly charge of $3141 ($3140 for the crypto units and $1 for the additional API calls) for your service instance.

The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Crypto unit 1 | $1570 |
| Crypto unit 2 | $1570 |
| First 1,000,000 API calls | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) | $1 ($0.01 x 100) |
| End of month charge | $3141  |

*Table 1. Charge of two crypto units with a monthly API calls of 2,000,000* -->
