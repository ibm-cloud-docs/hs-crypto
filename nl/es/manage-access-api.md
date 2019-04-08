---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

Keywords: instance ID, account ID, Access Management

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gestión de acceso a las claves
{: #manage-access-api}

Con {{site.data.keyword.iamlong}}, puede habilitar el control de acceso granular para sus claves de cifrado y crear y modificar las políticas de acceso.
{: shortdesc}

Esta página le guía a través de casos de ejemplo para gestionar el acceso a las claves de cifrado con la [API de gestión de accesos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://iampap.ng.bluemix.net/v1/docs/#/Policies/post_v1_policies){: new_window}.

## Antes de empezar
{: #prereqs-manage-api}

Para trabajar con la API, genere las credenciales de autenticación, como la [señal de acceso](/docs/services/hs-crypto/access-api.html#retrieve-token) y el [ID de instancia](/docs/services/hs-crypto/access-api.html#retrieve-instance-ID). También necesita el ID de la clave de {{site.data.keyword.hscrypto}} para la que desea gestionar el acceso.

Para obtener más información sobre la visualización de ID de clave, consulte [Visualización de claves](/docs/services/hs-crypto/view-keys.html).
{: tip}

### Recuperación del ID de cuenta
{: #retrieve-account-ID}

Después de haber recuperado las credenciales, determine el ámbito de acceso de su nueva política de acceso recuperando el ID de la cuenta que contiene la instancia de {{site.data.keyword.hscrypto}} (instancia de servicio para abreviar).

Para recuperar el ID de cuenta, siga estos pasos:

1. Inicie la sesión en la CLI de {{site.data.keyword.cloud_notm}}.
    ```sh
    ibmcloud login [--sso]
    ```
    {: codeblock}

    **Nota**: el parámetro `--sso` es obligatorio al iniciar sesión con un ID federado. Si se utiliza esta opción, vaya al enlace mostrado en la salida de la CLI para generar un código de acceso puntual.

    El resultado muestra la información de identificación para su cuenta.

    ```sh
    Authenticating...
    OK

    Seleccione una cuenta (o pulse Intro para omitir):

    1. cuenta-ejemplo (b6hnh3560ehqjkf89s4ba06i367801e)
    Especifique un número> 1
    Cuenta de destino cuenta-ejemplo (b6hnh3560ehqjkf89s4ba06i367801e)

    Punto final de la API:   https://api.ng.bluemix.net (versión API: 2.75.0)
    Región:                  us-south
    Usuario:                 admin
    Cuenta:                  cuenta-ejemplo (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}

2. Copie el valor de su ID de cuenta.

    El valor _b6hnh3560ehqjkf89s4ba06i367801e_ es un ID de cuenta de ejemplo.

### Recuperación del ID de usuario
{: #retrieve-user-ID}

Recupere el ID de usuario del usuario cuyo acceso desea modificar.

Para recuperar el ID de usuario, siga estos pasos:

1. [Solicite al usuario proporcionar una señal de IAM](/docs/services/hs-crypto/access-api.html#retrieve-token).
    La estructura de la señal IAM es la siguiente:

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Copie el valor medio y ejecute el mandato siguiente:
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    El resultado muestra un objeto JSON similar al del ejemplo siguiente:
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. Copie el valor de la propiedad de `id`.

## Creación de una política de acceso
{: #create-policy}

Para habilitar el control de acceso para una clave específica, puede enviar una solicitud a {{site.data.keyword.iamshort}} ejecutando el mandato siguiente. Repita el mandato para cada política de acceso.

```cURL
curl -X POST \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<ID_cuenta>/users/<ID_usuario>/policies \
  -H 'Authorization: Bearer <señal_IAM_admin>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<ID_cuenta>",
      "region": "<región>",
      "serviceInstance": "<ID_instancia>",
      "resourceType": "key",
      "resource": "<ID_clave>"
    }
  ]
}'
```
{: codeblock}

<!-- If you need to manage access to keys within a specified Cloud Foundry org and space, replace `serviceInstance` with `organizationId` and `spaceId`. To learn more, see the [Access Management API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.
{: tip}

Replace `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>`, and `<key_ID>` with the appropriate values. -->

**Opcional:** Verifique que la política se ha creado satisfactoriamente.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Actualización de una política de acceso
{: #update-policy}

Puede utilizar un ID de política recuperado para modificar una política existente para un usuario. Envíe una solicitud a {{site.data.keyword.iamshort}} ejecutando el mandato siguiente:

```cURL
curl -X PUT \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<ID_cuenta>/users/<ID_usuario>/policies/<ID_política> \
  -H 'Authorization: Bearer <señal_IAM_admin>' \
  -H 'If-Match': <ID_ETag> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<ID_cuenta>",
      "region": "<región>",
      "serviceInstance": "<ID_instancia>",
      "resourceType": "key",
      "resource": "<ID_clave>"
    }
  ]
}'
```
{: codeblock}

Sustituya `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` y `<key_ID>` por los valores adecuados.

**Opcional:** verifique que la política se ha actualizado correctamente.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Supresión de una política de acceso
{: #delete-policy}

Puede utilizar un ID de política recuperado para suprimir una política existente para un usuario. Envíe una solicitud a {{site.data.keyword.iamshort}} ejecutando el mandato siguiente:

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Sustituya `<account_ID>`, `<user_ID>`, `<policy_ID>` y `<Admin_IAM_token>` por los valores adecuados.

**Opcional:** Verifique la política se ha suprimido satisfactoriamente.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}
