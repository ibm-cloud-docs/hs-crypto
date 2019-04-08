---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: data encryption key, original key material, unwrap call

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Desenvolvimiento de claves
{: #unwrap-keys}

Las claves de cifrado de datos (DEK) se desenvuelven para acceder a sus contenidos mediante la API de {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, si es un usuario con los privilegios necesarios. El proceso de desenvolvimiento descifra y comprueba la integridad y el contenido de las DEK, devolviendo el material original de la clave a su servicio de datos de {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Para conocer cómo el envolvimiento de claves ayuda a controlar la seguridad de los datos en reposo en la nube, consulte [Cifrado de sobre](/docs/services/key-protect/concepts/envelope-encryption.html).

## Desenvolvimiento de claves utilizando la API
{: #unwrap-key-api}

[Después de realizar al servicio una llamada de envolvimiento](/docs/services/hs-crypto/wrap-keys.html), puede desenvolver una clave de cifrado de datos (DEK) específica para acceder a su contenido realizando una llamada `POST` al siguiente punto final.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_id>?action=unwrap
```
{: codeblock}

1. [Recupere sus credenciales de servicio y de autenticación para trabajar con claves en el servicio](/docs/services/hs-crypto/access-api.html).

2. Copie el ID de la clave raíz que ha utilizado para realizar la solicitud inicial de envolvimiento.

    Puede recuperar el ID de una clave realizando una solicitud `GET /v2/keys` o visualizando sus claves en la interfaz gráfica de usuario de {{site.data.keyword.hscrypto}}.

3. Copie el valor del `texto cifrado` devuelto durante la solicitud inicial de envolvimiento.

4. Ejecute el siguiente mandato cURL para descifrar y autenticar el material de la clave.

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "ciphertext": "<clave_datos_cifrados>",
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
        <td>El identificador único de la clave raíz que ha utilizado para la solicitud inicial de envolvimiento.</td>
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
        <td><varname>datos_adicionales</varname></td>
        <td>Opcional: datos de autenticación adicionales (AAD) que se utilizan para proteger aún más la clave. Cada serie puede contener hasta 255 caracteres. Si proporcionó los AAD cuando realizó al servicio la llamada de envolvimiento, debe especificar los mismos AAD durante la llamada de desenvolvimiento.</td>
      </tr>
      <tr>
        <td><varname>claves_datos_cifrados</varname></td>
        <td>El valor <code>ciphertext</code> devuelto durante la operación de envolvimiento.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Describe las variables necesarias para desenvolver las claves de {{site.data.keyword.hscrypto}}.</caption>
    </table>

    El material original de la clave se devuelve en el cuerpo de entidad de la respuesta. El siguiente objeto JSON muestra un valor devuelto de ejemplo.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg=="
    }
    ```
    {:screen}
