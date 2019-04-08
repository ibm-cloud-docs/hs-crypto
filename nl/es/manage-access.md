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

# Gestión de acceso de usuario
{: #manage-access}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} da soporte a un sistema de control de acceso centralizado, gobernado por {{site.data.keyword.iamlong}}, para ayudarle a gestionar usuarios y acceder a sus claves de cifrado.
{: shortdesc}

Una buena práctica es otorgar los permisos de acceso a medida que invita a nuevos usuarios a su cuenta o servicio. Por ejemplo, tenga en cuenta las directrices siguientes:

- **Habilitar el acceso de usuario a los recursos de la cuenta asignando roles de Cloud IAM.**
    En lugar de compartir las credenciales admin, crear nuevas políticas para los usuarios que necesitan acceso a las claves de cifrado en su cuenta. Si usted es el administrador de la cuenta, se le asigna automáticamente una política de _Gestor_ con acceso a todos los recursos de la cuenta.
- **Conceder roles y permisos en el ámbito más pequeño necesario.**
    Por ejemplo, si un usuario necesita acceder solo a una vista de alto nivel de claves dentro de un espacio especificado, otorgue el rol _Lector_ al usuario para ese espacio.
- **Auditar de forma regular a quien puede gestionar el control de acceso y suprimir los recursos de clave.**
    Recuerde que otorgando un rol de _Gestor_ a un usuario significa que el usuario puede modificar políticas de servicio para otros usuarios, además de destruir recursos.

## Roles y permisos
{: #roles}

Con {{site.data.keyword.iamshort}} (IAM), podrá gestionar y definir el acceso para usuarios y recursos en su cuenta.

Para simplificar el acceso, {{site.data.keyword.hscrypto}} se alinea con los roles Cloud IAM para que cada usuario tenga una vista distinta del servicio, según el rol que se haya asignado al usuario. Si es un administrador de seguridad de su servicio, puede asignar roles de Cloud IAM que correspondan a los permisos de {{site.data.keyword.hscrypto}} específicos que desea otorgar a los miembros de su equipo.

La siguiente tabla muestra cómo los roles identidad y acceso se correlacionan con los permisos de {{site.data.keyword.hscrypto}}:
<table>
  <tr>
    <th>Rol de acceso al servicio</th>
    <th>Descripción</th>
    <th>Acciones</th>
  </tr>
  <tr>
    <td><p>Lector</p></td>
    <td><p>Un lector puede examinar una vista de alto nivel de claves y realizar acciones envolver y desenvolver. Los lectores no pueden acceder ni modificar el material de las claves.</p></td>
    <td>
      <p>
        <ul>
          <li>Ver claves</li>
          <li>Envolver claves</li>
          <li>Desenvolver claves</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Escritor</p></td>
    <td><p>Un escritor puede crear claves, modificar claves y acceder al material de las claves.</p></td>
    <td>
      <p>
        <ul>
          <li>Crear claves</li>
          <li>Ver claves</li>
          <li>Envolver claves</li>
          <li>Desenvolver claves</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Gestor</p></td>
    <td><p>Un gestor puede realizar todas las acciones que un lector y un escritor pueden realizar, incluida la capacidad de suprimir claves, invitar a nuevos usuarios y asignar políticas de acceso para otros usuarios.</p></td>
    <td>
      <p>
        <ul>
          <li>Todas las acciones que un lector o un escritor puedes realizar</li>
          <li>Suprimir claves</li>
          <li>Asignar políticas de acceso</li>
        </ul>
      </p>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Tabla 1. Describe cómo los roles de acceso e identidad se correlacionan con los permisos de {{site.data.keyword.hscrypto}}</caption>
</table>

<!-- **Note**: Cloud IAM user roles provide access at the service or service instance level. [Cloud Foundry roles](/docs/iam/cfaccess.html) are separate and define access at the organization or the space level. -->

Para obtener más información sobre {{site.data.keyword.iamshort}}, consulte [Roles de usuario y permisos](/docs/iam/users_roles.html#userroles).

### Qué hacer a continuación
{: #manage-access-next}

Los propietarios y administradores de cuentas pueden invitar a usuarios y establecer políticas de servicio que corresponden a los usuarios pueden realizar acciones de {{site.data.keyword.hscrypto}}.

- Para obtener más información sobre la asignación de roles de usuario en la interfaz de usuario de
{{site.data.keyword.cloud_notm}}, consulte [Gestión del acceso de IAM](/docs/iam/mngiam.html).
- Para obtener información sobre la concesión de permisos avanzados para acceder a claves de cifrado específicas, consulte [Gestión de claves de acceso](/docs/services/hs-crypto/manage-access-api.html).
