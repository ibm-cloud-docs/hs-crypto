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

# Eventi {{site.data.keyword.cloudaccesstrailshort}}
{: #at-events}

Utilizza il servizio {{site.data.keyword.cloudaccesstrailfull}} per tenere traccia di come gli utenti e le applicazioni interagiscono con {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

Il servizio {{site.data.keyword.cloudaccesstrailfull_notm}} registra le attività avviate dall'utente che modificano lo stato di un servizio in {{site.data.keyword.cloud_notm}}.

Per ulteriori informazioni, vedi la [documentazione di {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla).

## Elenco di eventi
{: #events}

La seguente tabella elenca le azioni che generano un evento:

<table>
    <tr>
        <th>Azione</th>
        <th>Descrizione</th>
    </tr>
    <tr>
        <td>hs-crypto.secrets.create</td>
        <td>Crea una chiave</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.read</td>
        <td>Richiama una chiave per ID</td>
    </tr>
   <tr>
        <td>hs-crypto.secrets.delete</td>
        <td>Elimina una chiave per ID</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.list</td>
        <td>Richiama un elenco di chiavi</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.head</td>
        <td>Richiama il numero delle chiavi</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.wrap</td>
        <td>Impacchetta una chiave</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.unwrap</td>
        <td>Spacchetta una chiave</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.rotate</td>
        <td>Esegui una rotazione di una chiave</td>
    </tr>
    <caption style="caption-side:bottom;">Tabella 1. Azioni che generano gli eventi {{site.data.keyword.cloudaccesstrailfull_notm}}</caption>
</table>

## Dove visualizzare gli eventi
{: #gui}

<!-- Option 2: Add the following sentence if your service sends events to the account domain. -->

Gli eventi {{site.data.keyword.cloudaccesstrailshort}} sono disponibili nel **dominio dell'account** {{site.data.keyword.cloudaccesstrailshort}}disponibile nella regione {{site.data.keyword.cloud_notm}} in cui vengono generati gli eventi.

Ad esempio, quando crei, importi, elimini o leggi una chiave in {{site.data.keyword.hscrypto}}, viene generato un evento {{site.data.keyword.cloudaccesstrailshort}}. Questi eventi vengono automaticamente inoltrati al servizio {{site.data.keyword.cloudaccesstrailshort}} nella stessa regione in cui è stato eseguito il provisioning del servizio {{site.data.keyword.hscrypto}}.

Per monitorare l'attività API, devi eseguire il provisioning del servizio {{site.data.keyword.cloudaccesstrailshort}} in uno spazio nella stessa regione in cui è stato eseguito il provisioning del servizio {{site.data.keyword.hscrypto}}. Successivamente, puoi visualizzare gli eventi tramite la vista account nell'IU {{site.data.keyword.cloudaccesstrailshort}} se hai un piano lite e tramite Kibana se hai un piano premium.

## Ulteriori informazioni
{: #info}

A causa della riservatezza delle informazioni di una chiave crittografata, quando viene generato un evento come risultato di una chiamata API al servizio {{site.data.keyword.hscrypto}}, l'evento generato non include le informazioni dettagliate sulla chiave. L'evento include l'ID di correlazione che puoi utilizzare per identificare la chiave internamente nel tuo ambiente cloud. L'ID di correlazione è un campo restituito come parte del campo `responseHeader.content`. Puoi utilizzare queste informazioni per correlare la chiave {{site.data.keyword.hscrypto}} con le informazioni dell'azione riportata tramite l'evento {{site.data.keyword.cloudaccesstrailshort}}.
