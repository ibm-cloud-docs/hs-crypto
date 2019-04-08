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

# Evénements {{site.data.keyword.cloudaccesstrailshort}}
{: #at-events}

Utilisez le service {{site.data.keyword.cloudaccesstrailfull}} pour savoir comment les utilisateurs et les applications interagissent avec {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

Le service {{site.data.keyword.cloudaccesstrailfull_notm}} enregistre les activités initiées par l'utilisateur qui changent l'état d'un service dans {{site.data.keyword.cloud_notm}}.

Pour plus d'informations, voir la [documentation {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla).

## Liste des événements
{: #events}

Le tableau suivant répertorie les actions qui génèrent un événement :

<table>
    <tr>
        <th>Action</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>hs-crypto.secrets.create</td>
        <td>Créer une clé</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.read</td>
        <td>Extraire une clé par ID</td>
    </tr>
   <tr>
        <td>hs-crypto.secrets.delete</td>
        <td>Supprimer une clé par ID</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.list</td>
        <td>Extraire une liste de clés</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.head</td>
        <td>Extraire le nombre de clés</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.wrap</td>
        <td>Encapsuler une clé</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.unwrap</td>
        <td>Désencapsuler une clé</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.rotate</td>
        <td>Rotation d'une clé</td>
    </tr>
    <caption style="caption-side:bottom;">Tableau 1. Actions qui génèrent des événements {{site.data.keyword.cloudaccesstrailfull_notm}}</caption>
</table>

## Où consulter les événements
{: #view-events-gui}

<!-- Option 2: Add the following sentence if your service sends events to the account domain. -->

Les événements {{site.data.keyword.cloudaccesstrailshort}} sont disponibles dans le **domaine de compte** d'{{site.data.keyword.cloudaccesstrailshort}} qui est disponible dans la région {{site.data.keyword.cloud_notm}} dans laquelle les événements sont générés.

Par exemple, lorsque vous créez, importez, supprimez ou lisez une clé dans {{site.data.keyword.hscrypto}}, un événement {{site.data.keyword.cloudaccesstrailshort}} est généré. Ces événements sont transmis automatiquement au service {{site.data.keyword.cloudaccesstrailshort}} dans la région dans laquelle le service {{site.data.keyword.hscrypto}} a été mis à disposition.

Pour surveiller l'activité des API, vous devez mettre à disposition le service {{site.data.keyword.cloudaccesstrailshort}} dans un espace qui est disponible dans la région dans laquelle le service {{site.data.keyword.hscrypto}} a été mis à disposition. Ensuite, vous pouvez afficher les événements via la vue de compte dans l'interface utilisateur d'{{site.data.keyword.cloudaccesstrailshort}} si vous utilisez un plan Lite, et via Kibana si vous utilisez un plan Premium.

## Informations supplémentaires
{: #info}

En raison de la sensibilité des informations pour une clé de chiffrement, lorsqu'un événement est généré suite à un appel API du service {{site.data.keyword.hscrypto}}, il n'inclut pas d'informations détaillées sur la clé. Il inclut un ID de corrélation que vous pouvez utiliser pour identifier la clé en interne dans votre environnement cloud. L'ID de corrélation est une zone renvoyée dans la zone `responseHeader.content`. Vous pouvez utiliser cette information pour corréler la clé {{site.data.keyword.hscrypto}} avec les informations de l'action rapportées via l'événement {{site.data.keyword.cloudaccesstrailshort}}.
