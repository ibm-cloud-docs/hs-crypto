---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: disaster recovery, High availability, HA, DR

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Haute disponibilité et récupération après sinistre
{: #ha-dr}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} est un service régional haute disponibilité avec des fonctionnalités automatiques qui aident à préserver la sécurité et la continuité de fonctionnement de vos applications.
{: shortdesc}

Utilisez cette page pour en apprendre plus sur les stratégies de disponibilité et de récupération après sinistre de {{site.data.keyword.hscrypto}}.

## Lieux, location et disponibilité
{: #availability}

{{site.data.keyword.hscrypto}} est un service régional multi-locataire.

Vous pouvez créer des ressources {{site.data.keyword.hscrypto}} dans l'une des [régions {{site.data.keyword.cloud_notm}}](/docs/services/hs-crypto/regions.html) prises en charge, c'est-à-dire les secteurs géographiques où vos demandes {{site.data.keyword.hscrypto}} sont prises en charge et traitées. Chaque région {{site.data.keyword.cloud_notm}} contient [plusieurs zones de disponibilité ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/) afin de répondre à ses exigences d'accès local, de faible temps de latence et de sécurité.

Au moment de planifier votre stratégie de chiffrement des données au repos avec {{site.data.keyword.cloud_notm}}, gardez à l'esprit qu'en approvisionnant {{site.data.keyword.hscrypto}} dans une région aussi proche que possible de chez vous, vous aurez plus de chances d'obtenir des connexions rapides et fiables pour interagir avec les API de {{site.data.keyword.hscrypto}}. Choisissez une région spécifique si les utilisateurs, les applications ou les services dépendant d'une ressource {{site.data.keyword.hscrypto}} sont tous concentrés autour d'un même secteur. N'oubliez pas que les utilisateurs et les services trop éloignés de la région choisie auront peut-être à subir des temps de latence pénalisants.

Vos clés de chiffrement sont confinées dans la région où vous les créez. {{site.data.keyword.hscrypto}} ne les copie pas ni ne les exporte vers d'autres régions.
{: note}

## Récupération après sinistre
{: #disaster-recovery}

{{site.data.keyword.hscrypto}} met en oeuvre un service régional de récupération après sinistre avec un objectif de temps de reprise (RTO) d'une heure. Le service obéit aux règles d'{{site.data.keyword.cloud_notm}} en ce qui concerne la planification face aux risques d'événements catastrophiques et la récupération de tels événements. Pour plus d'informations, consultez [Récupération après sinistre](/docs/overview/zero_downtime.html#disaster-recovery).
