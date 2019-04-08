---

copyright:
years: 2018, 2019
lastupdated: "2019-03-26"

Keywords: root keys, standard keys, migration, transition, beta

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Migration de clés depuis une instance de service bêta
{: #migrate-keys}

Si vous utilisiez une instance de service bêta et que vous voulez migrer les clés racine et les clés standard que vous avez gérées dans une instance de service de production {{site.data.keyword.hscrypto}}, suivez la procédure ci-après.
{: shortdesc}

Les administrateurs IBM Cloud ne peuvent pas migrer les clés maître car elles ne sont pas extractibles depuis l'unité crypto. Vous devez initialiser l'instance de service de production avec votre clé maître.
{:important}  

## Avant de commencer
{: #migrate-prerequisites}

1. [Créez une instance de service](/docs/services/hs-crypto/provision.html) avec le plan Hyper Protect Crypto Services.

2. [Initialisez l'instance de service](/docs/services/hs-crypto/initialize_hsm.html) avec le plug-in Trusted Key Entry.

## Migration des clés
{: #migrate-keys-steps}  

Procédez comme suit pour migrer les clés racine et les clés standard dans un environnement de production.

1. [Importez les clés racine](/docs/services/hs-crypto/import-root-keys.html) via l'interface utilisateur graphique ou l'API.

  Vous pouvez migrer les clés racine importées depuis l'instance de service bêta vers l'instance de service de production.
  {:tip}

2. Désencapsulez les clés DEK (Data Encryption Key) à partir de l'instance de service bêta et encapsulez-les dans l'instance de service de production :

  1. [Désencapsulez les clés DEK (Data Encryption Key)](/docs/services/hs-crypto/unwrap-keys.html) depuis l'instance de service bêta avec l'[API invoke-an-action-on-a-key ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: new_window}.

  2. [Encapsulez les clés DEK](/docs/services/hs-crypto/wrap-keys.html) dans l'instance de service de production avec l'[API invoke-an-action-on-a-key![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key{: new_window}).

3. Recréez les clés standard en procédant comme suit :

  1. [Extrayez les clés standard](/docs/services/hs-crypto?topic=hs-crypto-view-keys#retrieve-key-api) avec l'[API retrieve-key-by-id ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/hs-crypto#retrieve-a-key-by-id){: new_window}. Le contenu utilisé pour créer la clé dans l'instance bêta est retourné.

  2. [Créez les clés standard](/docs/services/hs-crypto/create-standard-keys.html) dans la nouvelle instance de service, avec les informations extraites à l'étape précédente, via l'interface utilisateur graphique ou l'[API create-a-new-key ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/hs-crypto#create-a-new-key){: new_window}.

## Etapes suivantes
{: #migration-next}

Pour plus d'informations sur la gestion de vos clés à l'aide d'un programme, [voir la documentation de référence de l'API {{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
