---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

Keywords: user access, Cloud IAM roles, encryption keys

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gestion des accès utilisateur
{: #manage-access}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} prend en charge un système de contrôle d'accès centralisé, régi par {{site.data.keyword.iamlong}}, afin de vous aider à gérer les utilisateurs et les accès pour vos clés de chiffrement.
{: shortdesc}

Il est recommandé d'accorder des droits d'accès lorsque vous invitez de nouveaux utilisateurs à rejoindre votre compte ou votre service. Examinons, par exemple, les instructions suivantes :

- **Autorisez l'accès utilisateur aux ressources de votre compte en affectant des rôles Cloud IAM.**
    Au lieu de partager vos données d'identification administrateur, créez de nouvelles règles pour les utilisateurs qui ont besoin d'accéder aux clés de chiffrement dans votre compte. Si vous êtes administrateur de votre compte, une règle _Responsable_ vous est automatiquement affectée, qui vous donne accès à toutes les ressources du compte.
- **Accordez des rôles et des droits à la portée la plus restreinte possible.**
    Par exemple, si un utilisateur n'a besoin d'accéder qu'à une vue globale des clés dans un espace donné, accordez-lui le rôle _Lecteur_ pour cet espace.
- **Effectuez un audit régulier des utilisateurs qui peuvent gérer le contrôle d'accès et supprimer des ressources de clé.**
    N'oubliez pas que l'affectation du rôle _Responsable_ à un utilisateur lui donne le droit de modifier les règles de service d'autres utilisateurs, ainsi que de détruire des ressources.

## Rôles et droits
{: #roles}

IAM ({{site.data.keyword.iamshort}}) permet de gérer et de définir l'accès applicable aux utilisateurs et aux ressources de votre compte.

Pour simplifier l'accès, {{site.data.keyword.hscrypto}} s'aligne sur les rôles Cloud IAM afin que chaque utilisateur dispose d'une vue différente du service, selon le rôle qui lui est affecté. Si vous êtes l'administrateur de sécurité de votre service, vous pouvez affecter des rôles Cloud IAM qui correspondent aux droits {{site.data.keyword.hscrypto}} spécifiques que vous voulez accorder aux membres de votre équipe.

Le tableau suivant montre la façon dont les rôles Identity and Access sont mappés aux droits {{site.data.keyword.hscrypto}} :
<table>
  <tr>
    <th>Rôle d'accès au service</th>
    <th>Description</th>
    <th>Actions</th>
  </tr>
  <tr>
    <td><p>Lecteur</p></td>
    <td><p>Un lecteur peut parcourir une vue globale des clés et effectuer des actions d'encapsulage et de désencapsulage. Il ne peut pas accéder à la matière (octets) d'une clé ni la modifier.</p></td>
    <td>
      <p>
        <ul>
          <li>Affichage de clés</li>
          <li>Encapsulage de clés</li>
          <li>Désencapsulage de clés</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Auteur</p></td>
    <td><p>Un auteur peut créer et modifier des clés et accéder à leur matière (octets).</p></td>
    <td>
      <p>
        <ul>
          <li>Création de clés</li>
          <li>Affichage de clés</li>
          <li>Encapsulage de clés</li>
          <li>Désencapsulage de clés</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Responsable</p></td>
    <td><p>Un responsable peut effectuer toutes les actions qu'un lecteur et qu'un auteur peuvent exécuter, notamment supprimer des clés, inviter de nouveaux utilisateurs et gérer les règles d'accès des autres utilisateurs.</p></td>
    <td>
      <p>
        <ul>
          <li>Toutes les actions qu'un lecteur ou un auteur peut effectuer</li>
          <li>Suppression de clés</li>
          <li>Affectation de règles d'accès</li>
        </ul>
      </p>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Tableau 1. Description de la façon dont les rôles Identity and Access sont mappés aux droits {{site.data.keyword.hscrypto}}</caption>
</table>

<!-- **Note**: Cloud IAM user roles provide access at the service or service instance level. [Cloud Foundry roles](/docs/iam/cfaccess.html) are separate and define access at the organization or the space level. -->

Pour en savoir plus sur {{site.data.keyword.iamshort}}, voir la section [Rôles et droits utilisateur](/docs/iam/users_roles.html#userroles).

### Etapes suivantes
{: #manage-access-next}

Les propriétaires de compte et les administrateurs peuvent inviter des utilisateurs et définir des règles de service qui correspondent aux actions {{site.data.keyword.hscrypto}} que les utilisateurs peuvent exécuter.

- Pour plus d'informations sur l'attribution de rôles aux utilisateurs dans l'Interface utilisateur {{site.data.keyword.cloud_notm}}, voir [Gestion de l'accès IAM](/docs/iam/mngiam.html).
- Pour en savoir plus sur l'affectation de droits avancés pour accéder à des clés de chiffrement spécifiques, voir [Gestion de l'accès aux clés](/docs/services/hs-crypto/manage-access-api.html).
