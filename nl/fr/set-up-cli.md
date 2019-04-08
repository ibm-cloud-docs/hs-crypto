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

# Accès à l'interface de ligne de commande {{site.data.keyword.keymanagementserviceshort}} sur une instance {{site.data.keyword.hscrypto}}
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} fonctionne en intégration avec le plug-in de l'interface de ligne de commande d' {{site.data.keyword.keymanagementservicelong_notm}}. Vous pouvez donc utiliser ce dernier pour créer, importer et gérer vos clés racine et clés standard de chiffrement.

Avant de pouvoir utiliser le plug-in d'interface de ligne de commande {{site.data.keyword.keymanagementserviceshort}} sur une instance {{site.data.keyword.hscrypto}} (ou instance de service, en abrégé), vous devez configurer la variable KP_KP_PRIVATE_ADDR sur votre poste de travail :

* Sous Linux ou MacOS, exécutez la commande suivante :

  ```
  export KP_PRIVATE_ADDR=<URL>
  ```
  {: pre}

  Dans cette commande, *URL* est le point d'extrémité qui s'affiche sur l'onglet **Gérer** de votre tableau de bord {{site.data.keyword.hscrypto}} mis à disposition. Par exemple :

  ```
  export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
  ```
  {: pre}

* Sous Windows, dans **Panneau de configuration**, tapez `environment variable` dans la zone Rechercher pour localiser la fenêtre Variables d'environnement. Créez une variable d'environnement KP_PRIVATE_ADDR et définissez sa valeur sur le point d'extrémité qui s'affiche sur l'onglet **Gérer** de votre tableau de bord {{site.data.keyword.hscrypto}} mis à disposition. Exemple : `https://us-south.hs-crypto.cloud.ibm.com:<port>`.

Vous pouvez aussi extraire l'URL de point d'extrémité via l'API. Pour plus de détails, [voir la documentation de référence de l'API {{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

- Pour plus d'informations sur l'utilisation de l'interface de ligne de commande, voir la documentation de référence de l'interface de ligne de commande de [{{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/cli-reference.html).
- Pour savoir comment accéder à l'interface de ligne de commande, consultez [Configuration de l'interface de ligne de commande {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/set-up-cli.html).
