---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: IBM Cloud CLI plug-in, ibmcloud commands, IBM Cloud command-line interface

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Configuration de l'interface de ligne de commande
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} fonctionne en intégration avec le plug-in de l'interface de ligne de commande de {{site.data.keyword.keymanagementservicelong_notm}}. Vous pouvez donc utiliser ce dernier pour créer, importer et gérer vos clés racine et clés standard de chiffrement.

- Pour plus d'informations sur l'utilisation de l'interface de ligne de commande, voir la documentation de référence de l'interface de ligne de commande de [{{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/cli-reference.html).
- Pour savoir comment accéder à l'interface de ligne de commande, consultez [Configuration de l'interface de ligne de commande {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/set-up-cli.html).

Avant de pouvoir utiliser le plug-in de l'interface de ligne de commande {{site.data.keyword.keymanagementserviceshort}} sur une instance {{site.data.keyword.hscrypto}}, vous devez exécuter la commande suivante :

```
export KP_PRIVATE_ADDR=<URL>
```
{: pre}

Dans cette commande, *URL* représente le point d'extrémité affiché dans la page **Manage** de l'interface utilisateur. Vous pouvez aussi obtenir l'URL de ce point d'extrémité via l'API. Par exemple :

```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
```
{: pre}

Pour les détails, [consultez la documentation de référence de l'API {{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
