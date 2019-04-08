---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: REST API, RESTful API, access token, instance ID

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Acceso a la API
{: #access-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} se integra con la API REST de {{site.data.keyword.keymanagementserviceshort}}, que puede utilizarse con cualquier lenguaje de programación para almacenar, recuperar y generar claves.
{: shortdesc}

Para trabajar con la API, debe generar credenciales de servicio y autenticación.

## Recuperación de una señal de acceso
{: #retrieve-token}

La autenticación con {{site.data.keyword.hscrypto}} se puede realizar recuperando una señal de acceso desde {{site.data.keyword.iamshort}}. Con un [ID de servicio](/docs/iam/serviceid.html#serviceids), puede trabajar con la API de {{site.data.keyword.hscrypto}} en nombre de su servicio o de su aplicación dentro o fuera de {{site.data.keyword.cloud_notm}}, sin la necesidad de compartir sus credenciales de usuario personales.  

<!-- If you want to authenticate with your user credentials, you can retrieve your token by running `ibmcloud iam oauth-tokens` in the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview).
{: tip} -->

Siga estos pasos para recuperar una señal de acceso:

1. En la consola de {{site.data.keyword.cloud_notm}}, vaya a **Gestionar** &gt; **Seguridad** &gt; **Identidad y acceso** &gt; **ID de servicio**. Siga el proceso para [crear un ID de servicio](/docs/iam/serviceid.html#creating-a-service-id).
2. Utilice el menú **Acciones** para [definir una política de acceso para su nuevo ID de servicio](/docs/iam/serviceidaccess.html).

    Para obtener información sobre la gestión del acceso a sus recursos de {{site.data.keyword.hscrypto}}, consulte [Roles y permisos](/docs/services/hs-crypto/manage-access.html#roles).
3. Utilice la sección **claves de API** para [crear una clave de API para asociarla con el ID de servicio.](/docs/iam/serviceid_keys.html#serviceidapikeys). Guarde la clave de API descargándola en una ubicación segura.
4. Llame a la API de {{site.data.keyword.iamshort}} para recuperar su señal de acceso.

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/identity/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>" \
    ```
    {: codeblock}

    En esta solicitud, sustituya `<API_KEY>` con la clave de API que ha creado en el paso 3. El siguiente ejemplo esquematizado muestra la señal de salida:

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    Utilice el valor completo de `access_token`, con el tipo de señal _Bearer_ como prefijo, para gestionar claves mediante programación utilizando la API de {{site.data.keyword.hscrypto}} para su servicio.

    Las señales de acceso son válidas durante 1 hora, pero puede volver a generarlas cuando las necesite. Para mantener el acceso al servicio, renueve la señal de acceso de su clave de API de forma periódica llamando la API de {{site.data.keyword.iamshort}}.   
    {: tip }

## Recuperación del ID de instancia
{: #retrieve-instance-ID}

Puede recuperar la información de identificación para la instancia del servicio de {{site.data.keyword.hscrypto}} utilizando la [CLI de {{site.data.keyword.cloud_notm}}](/docs/cli/index.html#overview). Utilice un ID de instancia para gestionar las claves de cifrado dentro de una instancia especificada de {{site.data.keyword.hscrypto}} en su cuenta.

1. Inicie sesión en {{site.data.keyword.cloud_notm}} con la [CLI de {{site.data.keyword.cloud_notm}}](/docs/cli/index.html#overview).

    ```sh
    ibmcloud login
    ```
    {: pre}

    **Nota:** Si el inicio de sesión falla, ejecute el mandato `ibmcloud login --sso` para intentarlo de nuevo. El parámetro `--sso` es obligatorio al iniciar sesión con un ID federado. Si se utiliza esta opción, vaya al enlace mostrado en la salida de la CLI para generar un código de acceso puntual.

2. Seleccione la cuenta que contiene la instancia suministrada.

    Ejecute `ibmcloud resource service-instances` para listar todas las instancias de servicio suministradas en su cuenta.

3. Recupere el nombre de recurso de nube (CRN) que identifica de forma exclusiva su instancia de servicio de {{site.data.keyword.hscrypto}}.

    ```sh
    ibmcloud resource service-instance <instance_name> --id
    ```
    {: pre}

    Sustituya `<instance_name>` con el alias exclusivo que se asigna a la instancia de {{site.data.keyword.hscrypto}}. El siguiente ejemplo esquematizado muestra la salida de la CLI. El valor _42454b3b-5b06-407b-a4b3-34d9ef323901_ es un ID de instancia de ejemplo.

    ```
    crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:42454b3b-5b06-407b-a4b3-34d9ef323901::
    ```
    {: screen}

## Recuperación de la información de conexión
{: #retrieve-connection-info}

Para poder llamar a cualquiera de las API de {{site.data.keyword.keymanagementserviceshort}}, llame a la API **Recuperar la información de conexión** en primer lugar para recuperar la información de conexión. Para obtener más información, consulte [el documento de referencia de la API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

## Cómo crear una solicitud de API
{: #form-api-request}

Cuando se realiza una llamada de API al servicio, la solicitud de API se estructura de acuerdo a cómo se suministró su instancia de {{site.data.keyword.hscrypto}}.

Para crear su solicitud, hay que emparejar un [punto final de servicio regional](/docs/services/hs-crypto/regions.html) con las credenciales de autenticación adecuadas. Por ejemplo, si ha creado una instancia de servicio para la región `us-south`, utilice el siguiente punto final y las cabeceras de API para examinar claves en el servicio:

```cURL
curl -X GET \
    https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/key \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### Qué hacer a continuación
{: #api-next}

Para obtener más información sobre cómo gestionar las claves mediante programación, [consulte el documento de referencia de la API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

<!-- To see an example of how keys stored in {{site.data.keyword.hscrypto}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}. -->
