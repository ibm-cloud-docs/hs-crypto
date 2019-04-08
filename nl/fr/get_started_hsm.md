---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-15"

Keywords: key storage, service instance, HSM, hardware security module

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}  
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# Initiation à l'initialisation d'une instance de service
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> Ce tutoriel explique comment initialiser l'instance de service en chargeant les clés maître pour protéger votre stockage de clés avec le plug-in Trusted Key Entry. Une fois l'instance de service initialisée, vous pouvez commencer à gérer vos clés racine.   
{:shortdesc}

## Prérequis
{: #get-started-hsm-prerequisite}

Avant de commencer, effectuez les étapes suivantes :

1. Mettez à disposition l'instance {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} (ou instance de service, en abrégé). Pour les étapes détaillées, voir [Mise à disposition de {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/provision.html).

2. Exécutez la commande suivante pour vous assurer que vous êtes connecté au noeud final d'API correct :

  ```
  ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

3. Installez la dernière version du plug-in Trusted Key Entry via l'interface de ligne de commande d'{{site.data.keyword.cloud_notm}}, avec la commande suivante :

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  Pour installer le plug-in de l'interface de ligne de commande, voir [Initiation à l'interface de ligne de commande d'{{site.data.keyword.cloud_notm}}](/docs/cli/index.html).
  {: tip}

4. Faites pointer la variable d'environnement CLOUDTKEFILES sur le sous-répertoire où vous voulez stocker les parties de clés et les clés de signature.

##  Etape 1 : Créez les fichiers des parties de clé maître et des clés de signature.
{: #hsm-step1}

1. Créez une partie de clé maître aléatoire ou une partie de clé maître avec une valeur connue.

  * Pour créer une partie de clé maître aléatoire, utilisez la commande suivante :

    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    Lorsque vous y êtes invité, entrez une description pour la partie de clé et un mot de passe pour son fichier.

  * Pour créer une partie de clé maître avec une valeur connue, utilisez la commande suivante :

    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    Lorsque vous y êtes invité, entrez la valeur connue de la partie de clé sous forme de chaîne hexadécimale, puis entrez une description et un mot de passe pour son fichier.

  Répétez l'une ou l'autre de ces commandes pour créer des parties de clé supplémentaires.

2. Créez une clé de signature avec la commande suivante :
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  Lorsque vous y êtes invité, entrez un nom d'administrateur et un mot de passe pour l'accès au fichier de clé de signature.

## Etape 2 : Sélectionnez les unités crypto avec lesquelles vous voulez travailler
{: #hsm-step2}

Toutes les unités crypto d'une instance de service doivent être configurées de la même façon.

1. Vous pouvez afficher les instances de service et les unités crypto affectées à votre compte IBM Cloud en utilisant la commande suivante :

  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

2. Pour sélectionner des unités crypto supplémentaires à utiliser, servez-vous de la commande :

  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  Lorsque vous y êtes invité, entrez les unités crypto supplémentaires que vous voulez utiliser.

3. Pour retirer des unités crypto de l'ensemble que vous allez utiliser, utilisez la commande :

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  Lorsque vous y êtes invité, entrez les unités crypto que vous voulez retirer.

## Etape 3 : Ajoutez des administrateurs d'unités crypto et quittez le mode imprint
{: #hsm-step3}

Avant de pouvoir charger les clés maître dans une unité crypto, vous devez créer un ou plusieurs administrateurs d'unités crypto et quitter le mode imprint.

1. Chargez un administrateur d'unité crypto. Pour créer un administrateur d'unité crypto, utilisez la commande :
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  Lorsque vous y êtes invité, entrez le KEYNUM de la clé de signature à utiliser pour l'administrateur et le mot de passe pour l'accès au fichier de clé de signature.

2. Sélectionnez la clé de signature à utiliser pour signer les commandes, en utilisant la commande :

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  Lorsque vous y êtes invité, entrez le KEYNUM de la clé de signature à utiliser pour signer les commandes.

  La clé utilisée ici doit être la même que l'une des clés de signature utilisées pour charger un administrateur d'unité crypto à l'étape 3.1.
  {: tip}

3. Quittez le mode imprint en utilisant la commande suivante :

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

Une fois que vous avez chargé un administrateur d'unité crypto et quitté le mode imprint, vous pouvez vérifier l'état de vos unités crypto en utilisant la commande :
{: tip}

```
 ibmcloud tke cryptounit-compare
```
{: pre}

## Etape 4 : Chargez le registre de clé maître
{: #hsm-step4}

Pour charger le registre de clé maître, un ou plusieurs administrateurs d'unités crypto doivent être définis et l'unité crypto doit avoir quitté le mode imprint.

1. Chargez le nouveau registre de clé maître en utilisant la commande suivante :

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  Lorsque vous y êtes invité, entrez le KEYNUM des parties de clé à charger, le mot de passe pour l'accès au fichier de clé de signature et le mot de passe de chaque partie de clé sélectionnée.

2. Validez le nouveau registre de clé maître en utilisant la commande suivante :

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  Lorsque vous y êtes invité, entrez le mot de passe pour l'accès au fichier de clé de signature.

3. Transférez la clé maître dans le registre de clé maître en vigueur, avec la commande suivante :

  ```
  ibmcloud tke cryptounit-mk-setimm
  ```
  {: pre}

  Lorsque vous y êtes invité, entrez le mot de passe pour l'accès au fichier de clé de signature.

## Etapes suivantes
{: #hsm-next}

Vous pouvez maintenant commencer à utiliser votre instance de service. Pour plus de détails sur l'implémentation de la procédure dans un environnement de production, voir la rubrique [Initialisation des instances de service](/docs/services/hs-crypto/initialize_hsm.html) pour protéger le stockage de clés.
