---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: root keys, master keys, standard keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# Introduction aux clés
{: #introduce-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} prend en charge différents types de clés, à savoir les clés racine, les clés standard et les clés maître.
{:shortdesc}

## Clés racine
{: #introduce-root-keys}

Les *clés racine* sont des clés d'encapsulage de clés symétriques que vous pouvez gérer dans leur intégralité dans {{site.data.keyword.hscrypto}}. Vous pouvez utiliser une clé racine pour protéger d'autres clés cryptographiques avec un mécanisme de chiffrement avancé. Pour en savoir plus, voir <a href="/docs/services/key-protect/concepts/envelope-encryption.html">Chiffrement d'enveloppe</a>.

Pour gérer les clés racine, suivez les étapes décrites dans [Gérez vos clés](/docs/services/hs-crypto/index.html#manage-keys).

## Clés standard
{: #introduce-standard-keys}

Les *clés standard* sont des clés symétriques utilisées pour la cryptographie. Vous pouvez utiliser une clé standard pour chiffrer et déchiffrer directement des données.

Pour gérer les clés standard, suivez les étapes décrites dans [Gérez vos clés](/docs/services/hs-crypto/index.html#manage-keys).

## Clés maître
{: #introduce-master-keys}

Les *clés maître* sont utilisées pour chiffrer l'instance de service pour le stockage de clés. Avec la clé maître, vous détenez la racine de confiance qui chiffre la chaîne complète de clés comprenant les clés racine et les clés standard.

En raison de la sécurisation de bout en bout jusqu'à l'instance de service, seuls les administrateurs de l'instance de service peuvent définir et gérer la clé maître. Notez qu'IBM ne sauvegarde ni ne gère la clé maître et n'a aucun moyen de la copier ou de la restaurer sur une autre machine ou dans un autre centre de données.

Une instance de service ne peut avoir qu'une seule clé maître. Si vous supprimez la clé maître de l'instance de service, vous pouvez efficacement détruire par crypto-broyage toutes les données qui ont été chiffrées avec les clés gérées dans le service.

Vous pouvez gérer les clés maître en suivant la procédure [Initialisation des instances de service](/docs/services/hs-crypto/initialize_hsm.html) pour protéger le stockage de clés.

La rotation d'une clé maître n'est pas prise en charge dans la version actuelle.
{:important}
