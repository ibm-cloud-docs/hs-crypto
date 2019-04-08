---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: root key, data encryption key, Hyper Protect Crypto Services

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Envolvimiento de claves
{: #wrap-keys}

Puede gestionar y proteger sus claves de cifrado con una clave raíz utilizando la API de {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, si es un usuario con los privilegios necesarios.
{: shortdesc}

Cuando envuelve una clave de cifrado de datos (DEK) con una clave raíz, {{site.data.keyword.hscrypto}} combina la robustez de varios algoritmos para proteger la privacidad y la integridad de sus datos cifrados.  

Para conocer cómo el envolvimiento de claves ayuda a controlar la seguridad de los datos en reposo en la nube, consulte [Cifrado de sobre](/docs/services/key-protect/concepts/envelope-encryption.html).

## Envolvimiento de claves utilizando la API
{: #wrap-keys-api}

Proteja una clave de cifrado de datos (DEK) específica con una clave raíz que gestionará en {{site.data.keyword.hscrypto}}.

Cuando proporcione una clave raíz para el envolvimiento, asegúrese de que la clave raíz es de 128, 192 o 256 bits para que la llamada de envolvimiento sea satisfactoria. Si crea una clave raíz en el servicio, {{site.data.keyword.hscrypto}} genera una clave de 256 bits a partir de sus HSM, soportada por el algoritmo AES-CBC.

[Después de designar una clave raíz en el servicio](/docs/services/hs-crypto/create-root-keys.html), puede envolver una DEK con cifrado avanzado realizando una llamada `POST` al siguiente punto final.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap
```
{: codeblock}

1. [Recupere sus credenciales de servicio y de autenticación para trabajar con claves en el servicio.](/docs/services/hs-crypto/access-api.html)

2. Copie el material de la clave de la DEK que desea gestionar y proteger.

    Si tiene privilegios de gestor o escritor para su instancia de servicio de {{site.data.keyword.hscrypto}}, [puede recuperar el material de una clave específica realizando una solicitud `GET /v2/keys/<key_ID>`](/docs/services/hs-crypto/view-keys.html#api).

3. Copie el ID de la clave raíz que desea utilizar para envolver.

4. Ejecute el siguiente mandato cURL para proteger la clave con una operación de envolvimiento.

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<clave_datos>",
      "aad": ["<datos_adicionales>", "<datos_adicionales>"]
    }'
    ```
    {: codeblock}
    <!--    To work with keys within a Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [For more information, see the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
        {: tip} -->

    Sustituya las variables en la solicitud de ejemplo siguiendo la siguiente tabla.

    <table>
      <tr>
        <th>Variable</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td><varname>región</varname></td>
        <td>La abreviatura de región, como <code>us-south</code> o <code>eu-gb</code>, que representa el área geográfica donde reside su instancia de servicio de {{site.data.keyword.hscrypto}}. Para obtener más información, consulte <a href="/docs/services/hs-crypto/regions.html#endpoints">Puntos finales de servicio regionales</a>.</td>
      </tr>
      <tr>
        <td><varname>ID_clave</varname></td>
        <td>Identificador exclusivo para la clave raíz que desea utilizar para envolver.</td>
      </tr>
      <tr>
        <td><varname>señal_IAM</varname></td>
        <td>Su señal de acceso de {{site.data.keyword.cloud_notm}}. Incluya el contenido completo de la señal <code>IAM</code>, incluido el valor de Bearer, en la solicitud cURL. Para obtener más información, consulte <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">Recuperación de una señal de acceso</a>.</td>
      </tr>
      <tr>
        <td><varname>ID_instancia</varname></td>
        <td>El identificador exclusivo que está asignado a su instancia de servicio de {{site.data.keyword.hscrypto}}. Para obtener más información, consulte <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">Recuperación de un ID de instancia</a>.</td>
      </tr>
      <tr>
        <td><varname>ID_correlación</varname></td>
        <td>Opcional: el identificador exclusivo que se ha utilizado para rastrear y correlacionar transacciones.</td>
      </tr>
      <tr>
        <td><varname>preferencia_retorno</varname></td>
        <td><p>Una cabecera que altera el comportamiento del servidor para operaciones de <code>POST</code> y <code>DELETE</code>.</p><p>Cuando establece la variable <em>preferencia_retorno</em> en <code>return=minimal</code>, el servicio solo devuelve los metadatos de la clave como, por ejemplo, el nombre de clave y valor de ID, en el cuerpo de entidad de la respuesta. Cuando establece la variable en <code>return=representation</code>, el servicio devuelve tanto el material de la clave como los metadatos de la clave.</p></td>
      </tr>
      <tr>
        <td><varname>clave_datos</varname></td>
        <td>Opcional: el material de la clave de la DEK que desea gestionar y proteger. El valor del <code>texto sin formato</code> debe estar codificado en base64. Para generar una nueva DEK, omita el atributo <code>plaintext</code>. El servicio genera un texto sin formato aleatorio (32 bytes) y envuelve dicho valor.</td>
      </tr>
      <tr>
        <td><varname>datos_adicionales</varname></td>
        <td>Opcional: datos de autenticación adicionales (AAD) que se utilizan para proteger aún más la clave. Cada serie puede contener hasta 255 caracteres. Si proporcionó los AAD cuando realizó al servicio la llamada de envolvimiento, debe especificar los mismos AAD durante la llamada de desenvolvimiento subsiguiente.<br></br>Importante: El servicio {{site.data.keyword.hscrypto}} no guarda datos de autenticación adicionales. Si proporciona AAD, guarde los datos en una ubicación segura para asegurarse de que pueda acceder y proporcionar los mismos AAD durante las llamadas de desenvolvimiento subsiguientes.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Describe las variables necesarias para envolver una clave especificada en {{site.data.keyword.hscrypto}}.</caption>
    </table>

    La clave envuelta, con el material de la clave codificado en base64, se devuelve en el cuerpo de entidad de la respuesta. El siguiente objeto JSON muestra un valor devuelto de ejemplo.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
