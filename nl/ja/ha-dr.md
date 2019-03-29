---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: disaster recovery, High availability, HA, DR

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 高可用性と災害復旧
{: #ha-dr}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} は、高度に使用可能な地域サービスで、アプリケーションを保護して作動させるための自動機能を備えています。
{: shortdesc}

このページでは、可用性と災害復旧に関する {{site.data.keyword.hscrypto}} の戦略について説明します。

## 場所、テナント、可用性
{: #availability}

{{site.data.keyword.hscrypto}} はマルチテナントの地域サービスです。

{{site.data.keyword.hscrypto}} リソースは、サポートされているいずれかの [{{site.data.keyword.cloud_notm}} 地域](/docs/services/hs-crypto/regions.html)に作成できます。これらの地域は、{{site.data.keyword.hscrypto}} の要求が扱われて処理される地理上のエリアを表します。{{site.data.keyword.cloud_notm}} の各地域には、その地域のローカル・アクセス権限、待ち時間、セキュリティーに関する要件を満たす[複数のアベイラビリティー・ゾーン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/) が用意されています。

{{site.data.keyword.cloud_notm}} を使用した保存データの暗号化戦略を計画する際、最寄りの地域で {{site.data.keyword.hscrypto}} をプロビジョニングすれば、{{site.data.keyword.hscrypto}} API と対話作業をするときに接続の速度と信頼性が向上する可能性が高くなります。{{site.data.keyword.hscrypto}} リソースに依存するユーザー、アプリ、またはサービスが地理的に集中している場合は、特定の地域を選択します。その地域から遠いユーザーとサービスは待ち時間が長くなる可能性があります。

暗号鍵は、それを作成した地域に封じ込まれています。{{site.data.keyword.hscrypto}} によって暗号鍵が他の地域にコピーされたりエクスポートされたりすることはありません。
{: note}

## 災害復旧
{: #disaster-recovery}

{{site.data.keyword.hscrypto}} の地域災害復旧では、目標復旧時間 (RTO) が 1 時間になっています。このサービスは、災害時の計画と復旧に関して {{site.data.keyword.cloud_notm}} の要件に従います。詳しくは、[災害復旧](/docs/overview/zero_downtime.html#disaster-recovery)を参照してください。
