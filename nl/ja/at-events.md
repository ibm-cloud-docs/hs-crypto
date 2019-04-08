---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: Activity Tracker events, List of events

subcollection: hs-crypto

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.cloudaccesstrailshort}} イベント
{: #at-events}

{{site.data.keyword.cloudaccesstrailfull}} サービスを使用して、ユーザーとアプリケーションが {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} と対話する方法を追跡します。
{: shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} サービスは、{{site.data.keyword.cloud_notm}} のサービスの状態を変更する、ユーザーが開始したアクティビティーを記録します。

詳しくは、[{{site.data.keyword.cloudaccesstrailshort}} の資料](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla)を参照してください。

## イベントのリスト
{: #events}

以下の表に、イベントを生成するアクションをリストします。

<table>
    <tr>
        <th>アクション</th>
        <th>説明</th>
    </tr>
    <tr>
        <td>hs-crypto.secrets.create</td>
        <td>鍵を作成します</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.read</td>
        <td>ID によって鍵を取得します</td>
    </tr>
   <tr>
        <td>hs-crypto.secrets.delete</td>
        <td>ID によって鍵を削除します</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.list</td>
        <td>鍵のリストを取得します</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.head</td>
        <td>鍵の数を取得します</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.wrap</td>
        <td>鍵をラップします</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.unwrap</td>
        <td>鍵をアンラップします</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.rotate</td>
        <td>鍵をローテートします</td>
    </tr>
    <caption style="caption-side:bottom;">表 1. {{site.data.keyword.cloudaccesstrailfull_notm}} イベントを生成するアクション</caption>
</table>

## イベントの表示場所
{: #view-events-gui}

<!-- Option 2: Add the following sentence if your service sends events to the account domain. -->

{{site.data.keyword.cloudaccesstrailshort}} イベントは、イベントが生成される {{site.data.keyword.cloud_notm}} 地域で使用可能な {{site.data.keyword.cloudaccesstrailshort}} **アカウント・ドメイン**で使用できます。

例えば、{{site.data.keyword.hscrypto}} で鍵の作成、インポート、削除、または読み取りを行うと、{{site.data.keyword.cloudaccesstrailshort}} イベントが生成されます。 これらのイベントは、{{site.data.keyword.hscrypto}} サービスがプロビジョンされる地域と同じ地域の {{site.data.keyword.cloudaccesstrailshort}} サービスに自動的に転送されます。

API アクティビティーをモニターするには、{{site.data.keyword.hscrypto}} サービスがプロビジョンされる地域と同じ地域で使用可能なスペースで {{site.data.keyword.cloudaccesstrailshort}} サービスをプロビジョンする必要があります。 その後、ライト・プランを利用している場合は {{site.data.keyword.cloudaccesstrailshort}} UI のアカウント・ビューから、プレミアム・プランを利用している場合は Kibana からイベントを表示することができます。

## 追加情報
{: #info}

暗号鍵に関する情報の機密性により、{{site.data.keyword.hscrypto}} サービスに対する API 呼び出しの結果でイベントが生成されるときに、生成されるイベントには鍵に関する詳細情報は含められません。 このイベントには、クラウド環境で内部的に鍵を識別するために使用できる相関 ID が含められます。 この相関 ID は、`responseHeader.content` フィールドの一部として返されるフィールドです。 この情報を使用して、{{site.data.keyword.hscrypto}} 鍵を、{{site.data.keyword.cloudaccesstrailshort}} イベントを通じて報告されたアクションの情報と相互に関連付けることができます。
