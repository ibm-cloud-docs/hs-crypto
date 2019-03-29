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

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} prend en charge différents types de clés, à savoir les clés racine, les clés standard et les clés maîtresses.
{:shortdesc}

## Root Keys (Clés racine)

Les *clés racine* sont des clés d'encapsulage de clés symétriques que vous pouvez gérer dans leur intégralité dans {{site.data.keyword.hscrypto}}. Vous pouvez utiliser une clé racine pour protéger d'autres clés cryptographiques avec un mécanisme de chiffrement avancé. Pour en savoir plus, voir <a href="/docs/services/key-protect/concepts/envelope-encryption.html">Chiffrement d'enveloppe</a>.

Pour gérer les clés racine, suivez les étapes décrites dans [Gérez vos clés](/docs/services/hs-crypto/index.html#manage-keys).

## Standard keys (Clés standard)

Les *clés standard* sont des clés symétriques utilisées pour la cryptographie. Vous pouvez utiliser une clé standard pour chiffrer et déchiffrer directement des données.

Pour gérer les clés standard, suivez les étapes décrites dans [Gérez vos clés](/docs/services/hs-crypto/index.html#manage-keys).

## Clés maîtresses

Les *clés maîtresses* servent à chiffrer l'instance crypto (HSM) qui chiffre elle-même et gère les clés racine et les clés standard. Avec la clé maîtresse, vous détenez la racine de confiance qui chiffre la chaîne complète de clés comprenant les clés racine et les clés standard.

En raison de la sécurisation de bout en bout jusqu'à l'instance crypto (HSM), seuls les administrateurs de l'instance {{site.data.keyword.hscrypto}} peuvent définir et gérer la clé maîtresse. Notez qu'IBM ne sauvegarde ni ne gère la clé maîtresse et n'a aucun moyen de la copier ou de la restaurer sur une autre machine ou dans un autre centre de données.

Une instance crypto (HSM) ne peut avoir qu'une seule clé maîtresse. Supprimer la clé maîtresse de l'instance {{site.data.keyword.hscrypto}} est un moyen efficace de détruire (crypto-broyage) toutes les données qui ont été chiffrées avec les clés gérées dans le service.

Vous pouvez gérer vos clés maîtresses lors de l'[initialisation des instances crypto pour protéger le stockage des clés](/docs/services/hs-crypto/initialize_hsm.html).

La rotation des clés maîtresses n'est pas prise en charge dans la version actuelle.
{:important}
