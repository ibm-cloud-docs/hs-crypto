---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

Keywords: release note, new

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Nouveautés
{: #what-new}

Tenez-vous informé des nouvelles fonctions qui sont disponibles pour {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Mars 2019
{: #March-2019}

### {{site.data.keyword.hscrypto}} est en disponibilité générale
Nouveau depuis le 29-03-2019

Pour plus d'informations sur l'offre {{site.data.keyword.hscrypto}}, consultez la [page d'accueil d'{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/hyper-protect-crypto){:new_window}.

### Haute disponibilité et récupération après sinistre
Nouveau depuis le 29-03-2019

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} est un service régional haute disponibilité avec des fonctionnalités automatiques qui aident à préserver la sécurité et le fonctionnement de vos applications.

Vous pouvez créer des ressources {{site.data.keyword.hscrypto}} dans les [régions {{site.data.keyword.cloud_notm}}](/docs/services/hs-crypto/regions.html) prises en charge, c'est-à-dire les secteurs géographiques où vos demandes {{site.data.keyword.hscrypto}} sont prises en charge et traitées. Chaque région {{site.data.keyword.cloud_notm}} contient [plusieurs zones de disponibilité ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/) afin de répondre à ses exigences d'accès local, de faible temps de latence et de sécurité.

Pour plus d'informations, consultez [Haute disponibilité et récupération après sinistre](/docs/services/hs-crypto/ha-dr.html).

## Février 2019
{: #Feb-2019}

### {{site.data.keyword.hscrypto}} Bêta est disponible
Nouveau depuis le 05-02-2019

La version Bêta de {{site.data.keyword.hscrypto}} est publiée. Vous pouvez maintenant accéder directement au service {{site.data.keyword.hscrypto}} en sélectionnant **Catalogue** > **Sécurité et identité**.

A compter du 5 février 2019, la mise à disposition de nouvelles instances Hyper Protect Crypto Services Experimental n'est plus possible. Les instances existantes bénéficient du support jusqu'à la date prévue (5 mars 2019).

## Décembre 2018
{: #Dec-2018}

### Ajouté : support de la gestion HSM avec KYOK
Nouveau depuis le 19-12-2018

{{site.data.keyword.hscrypto}} supporte désormais le mécanisme KYOK (Keep Your Own Keys). Les clés de chiffrement que vous utilisez et gérez sont les vôtres. Vous avez ainsi plus de contrôle et de droits sur vos données. Vous pouvez initialiser et gérer votre instance crypto (HSM) avec l'interface de ligne de commande d'{{site.data.keyword.cloud}}.

Pour plus d'informations, consultez [Initialisation des instances crypto pour protéger le stockage des clés](/docs/services/hs-crypto/initialize_hsm.html).

### Ajouté : intégration de l'API {{site.data.keyword.keymanagementserviceshort}}
Nouveau depuis le 19-12-2018

L'API {{site.data.keyword.keymanagementserviceshort}} est à présent intégrée avec Hyper Protect Crypto Services pour générer et protéger vos clés. Vous pouvez appeler l'API {{site.data.keyword.keymanagementserviceshort}} directement via {{site.data.keyword.hscrypto}}.

Pour plus d'informations, consultez [Accès à l'API](/docs/services/hs-crypto/access-api.html) et [API {{site.data.keyword.hscrypto}} ![Icône de lien externe](image/external_link.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/hs-crypto){:new_window}.

### Déprécié : fonction d'accès à {{site.data.keyword.hscrypto}} via ACSP
Nouveau depuis le 19-12-2018

L'accès à {{site.data.keyword.hscrypto}} via un client ACSP (Advanced Cryptography Service Provider) est déprécié dans la version actuelle. Si vous utilisez une ancienne instance de service, vous pouvez toujours utiliser ACSP pour explorer {{site.data.keyword.hscrypto}}.
