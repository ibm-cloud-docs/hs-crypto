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

# {{site.data.keyword.cloudaccesstrailshort}}-Ereignisse
{: #at-events}

Der {{site.data.keyword.cloudaccesstrailfull}}-Service kann dazu verwendet werden, die Interaktion von Benutzern und Anwendungen mit {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} zu verfolgen.
{: shortdesc}

Der {{site.data.keyword.cloudaccesstrailfull_notm}}-Service zeichnet vom Benutzer initiierte Aktivitäten auf, die den Status eines Service in {{site.data.keyword.cloud_notm}} ändern.

Weitere Informationen finden Sie in der [{{site.data.keyword.cloudaccesstrailshort}}-Dokumentation](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla).

## Ereignisliste
{: #events}

In der folgenden Tabelle sind die Aktionen aufgeführt, die ein Ereignis generieren:

<table>
    <tr>
        <th>Aktion</th>
        <th>Beschreibung</th>
    </tr>
    <tr>
        <td>hs-crypto.secrets.create</td>
        <td>Schlüssel erstellen</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.read</td>
        <td>Schlüssel anhand der ID abrufen</td>
    </tr>
   <tr>
        <td>hs-crypto.secrets.delete</td>
        <td>Schlüssel anhand der ID löschen</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.list</td>
        <td>Liste mit Schlüsseln abrufen</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.head</td>
        <td>Anzahl der Schlüssel abrufen</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.wrap</td>
        <td>Wrapping für einen Schlüssel durchführen</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.unwrap</td>
        <td>Wrapping für einen Schlüssel aufheben</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.rotate</td>
        <td>Rotation eines Schlüssels</td>
    </tr>
    <caption style="caption-side:bottom;">Tabelle 1. Aktionen, die {{site.data.keyword.cloudaccesstrailfull_notm}}-Ereignisse generieren</caption>
</table>

## Ereignis anzeigen
{: #view-events-gui}

<!-- Option 2: Add the following sentence if your service sends events to the account domain. -->

{{site.data.keyword.cloudaccesstrailshort}}-Ereignisse stehen in der {{site.data.keyword.cloudaccesstrailshort}}-**Kontodomäne** zur Verfügung, die in der {{site.data.keyword.cloud_notm}}-Region verfügbar ist, in der die Ereignisse generiert werden.

Beispiel: Wenn Sie einen Schlüssel in {{site.data.keyword.hscrypto}} erstellen, importieren, löschen oder lesen, wird ein {{site.data.keyword.cloudaccesstrailshort}}-Ereignis generiert. Diese Ereignisse werden automatisch an den {{site.data.keyword.cloudaccesstrailshort}}-Service in derselben Region weitergeleitet, in der auch der {{site.data.keyword.hscrypto}}-Service bereitgestellt wird.

Zur Überwachung der API-Aktivität müssen Sie den {{site.data.keyword.cloudaccesstrailshort}}-Service in einem Bereich bereitstellen, der in derselben Region verfügbar ist, in der auch der {{site.data.keyword.hscrypto}}-Service bereitgestellt wird. Dann können Sie Ereignisse über die Kontoansicht in der {{site.data.keyword.cloudaccesstrailshort}}-Benutzerschnittstelle anzeigen, wenn Sie einen Lite-Plan verwenden; oder Sie können sie über Kibana anzeigen, wenn Sie einen Premium-Plan verwenden.

## Zusätzliche Informationen
{: #info}

Da es sich bei den Informationen für einen Verschlüsselungsschlüssel um sensible Daten handelt, enthält das Ereignis, das als Ergebnis eines API-Aufrufs an den {{site.data.keyword.hscrypto}}-Service generiert wird, keine Details zum Schlüssel. Das Ereignis enthält eine Korrelations-ID, die Sie verwenden können, um den Schlüssel intern in Ihrer Cloudumgebung zu identifizieren. Bei der Korrelations-ID handelt es sich um ein Feld, das als Teil des Felds `responseHeader.content` zurückgegeben wird. Sie können diese Informationen für die Korrelation des {{site.data.keyword.hscrypto}}-Schlüssels mit den Informationen der durch das {{site.data.keyword.cloudaccesstrailshort}}-Ereignis gemeldeten Aktion verwenden.
