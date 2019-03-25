---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-21"

Keywords: frequently asked questions, critical security parameters, cryptographic module, Security Level

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Foire aux questions
{: #faqs}

Vous pouvez utiliser la foire aux questions ci-dessous pour vous aider à utiliser {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.

## Certifications HSM
{: #HSM}

### Comment puis-je m'assurer qu'une carte cryptographique (HSM) IBM a reçu la certification de conformité à la norme FIPS 140-2 Level 4 ?

FIPS 140-2 Level 4 est un très haut niveau de protection qui n'est pas largement disponible sur le marché. IBM est le premier fournisseur de cartes HSM certifiées au plus haut niveau et a beaucoup investi pour maintenir ce niveau de validation à chaque nouvelle génération de cartes. L'exigence d'un haut niveau de sécurité découle des conditions imposées par le Gouvernement fédéral des États-Unis. Pour la validation de la certification, vous êtes dirigé vers la page d'accueil du NIST car c'est sur ce site que la certification a été publiée.

### Quelles sont les différences entre les niveaux 2, 3 et 4 de FIPS 140-2 ?

* FIPS 140-2 Level 2 : exige la présence de témoins de violation par des scellés ou plombs ainsi que de serrures ou cadenas anti-effraction sur les couvercles amovibles et les portes. Le module cryptographique est pourvu d'un revêtement, scellé ou plomb qui doit être brisé pour obtenir l'accès physique aux clés cryptographiques et aux paramètres de sécurité critiques (CSP) stockés en clair dans le module. Le niveau de sécurité 2 exige, au minimum, un système d'authentification basé sur des rôles, dans lequel un module cryptographique authentifie un opérateur et reconnaît qu'il est autorisé à assumer un rôle spécifique et à exécuter un ensemble correspondant de services.
 
* FIPS 140-2 Level 3 : les mécanismes physiques de sécurité requis au niveau 3 sont censés avoir une forte probabilité de détecter les tentatives d'accès physique, d'utilisation ou de modification du module cryptographique et d'y répondre. Le niveau de sécurité 3 exige des mécanismes d'authentification fondés sur l'identité, ce qui renforce la sécurité assurée par les mécanismes d'authentification à base de rôles spécifiés pour le niveau de sécurité 2.  

* FIPS 140-2 Level 4 : à ce niveau de sécurité, ce sont des mécanismes physiques qui interviennent pour offrir une enveloppe de protection complète autour du module cryptographique, l'objectif étant de détecter toutes les tentatives d'accès physique non autorisé et d'y répondre. La pénétration dans l'enceinte du module cryptographique, d'où qu'elle vienne, a une très forte probabilité d'être détectée, avec pour conséquence immédiate la mise à zéro de tous les paramètres de sécurité critiques (CSP) stockés en clair dans le module. Les modules cryptographiques atteignant le niveau de sécurité 4 de la norme FIPS 140-2 sont utiles dans les environnements physiquement non protégés. 
Au niveau de sécurité 4, le module cryptographique est également protégé contre toute atteinte à la sécurité profitant de conditions environnementales ou de fluctuations de la tension électrique ou de la température en dehors des plages normales de fonctionnement du module. Une excursion intentionnelle en dehors des plages normales de fonctionnement pourrait être utilisée par un attaquant pour contrecarrer les défenses du module cryptographique. 

## Gestion des clés 

### {{site.data.keyword.hscrypto}} peut-il être utilisé combiné au service {{site.data.keyword.keymanagementserviceshort}} ?

 En tant que crypto-service géré, {{site.data.keyword.hscrypto}} est fourni avec une API {{site.data.keyword.keymanagementserviceshort}} entièrement compatible et offrant à l'utilisateur une expérience identique à celle de Key Protect. La principale différence est que {{site.data.keyword.hscrypto}} dépend d'un HSM qui a reçu la certification FIPS 140-2 Level 4. Il permet aussi au client de garder le contrôle total en gérant lui-même la clé maîtresse du HSM (mécanisme KYOK). Il s'agit d'un service dédié par instance, contrairement à {{site.data.keyword.keymanagementserviceshort}} dont la configuration est multi-locataire. Enfin, {{site.data.keyword.hscrypto}} offre aussi des capacités HSM pour les opérations cryptographiques telles que la signature/vérification, la génération de clés, le hachage cryptographique, le chiffrement/déchiffrement et l'encapsulage/désencapsulage de clés. 

### Quelle est la longueur maximale d'un nom de clé ?
{: #key_names}

Vous pouvez utiliser un nom de clé comprenant jusqu'à 50 caractères.

### Peut-on utiliser des caractères alphabétiques dans le nom de clé ?
{: #key_chars}

Les caractères de langue, comme le chinois, ne peuvent pas être inclus dans le nom de clé.

### Que se passe-t-il si je supprime une clé ?
{: #key_destruction}

Lorsque vous supprimez une clé, vous détruisez définitivement son contenu et les données qui lui sont associées. Les données qui ont été chiffrées avec la clé ne seront plus accessibles.

Avant de supprimer une clé, assurez-vous que vous n'avez plus besoin d'accéder aux données qui lui sont associées.
