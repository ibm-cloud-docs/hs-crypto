---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: details of the DELETE request, delete encryption key, deleting keys, Variable Description region

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Supresión de claves
{: #deleting-keys}

Puede utilizar {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} para suprimir una clave de cifrado y su contenido, si es un administrador para el espacio de {{site.data.keyword.cloud_notm}} o la instancia de servicio de {{site.data.keyword.hscrypto}}.
{: shortdesc}

**Importante:** cuando suprime una clave, se destruye permanentemente su contenido y datos asociados. La acción no se puede revertir. No se recomienda la destrucción de recursos para los entornos de producción, pero podría ser útil para entornos temporales como la realización de pruebas o QA.

## Supresión de claves con la GUI
{: #gui}

Si prefiere suprimir sus claves de cifrado utilizando una interfaz gráfica, puede utilizar la GUI de {{site.data.keyword.hscrypto}}.

[Después de crear o importar sus claves existentes en el servicio](/docs/services/hs-crypto/create-root-keys.html), complete los siguientes pasos para suprimir una clave:

1. [Inicie sesión en la consola de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/){: new_window}.
2. Desde el panel de control de {{site.data.keyword.cloud_notm}} seleccione su instancia suministrada de {{site.data.keyword.hscrypto}}.
3. Utilice la tabla de **Claves** tabla para examinar las claves en el servicio.
4. Pulse el icono ⋮ para abrir una lista de opciones para la clave que desea suprimir.
5. En el menú de opciones, pulse **Suprimir clave** y confirme la supresión clave en la pantalla siguiente.

Después de suprimir una clave, la clave pasa al estado _Destruida_. Las claves con este estado no son recuperables. Los metadatos asociados con la clave como, por ejemplo, la fecha de supresión de la clave, se mantienen en la base de datos de {{site.data.keyword.hscrypto}}.

## Supresión de claves con la API
{: #api}

Para suprimir una clave y su contenido, realice una llamada `DELETE` al siguiente punto final.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```

1. [Recupere sus credenciales de servicio y de autenticación para trabajar con claves en el servicio](/docs/services/hs-crypto/access-api.html).

2. Recupere el ID de la clave que desea suprimir.

    Puede recuperar el ID para una clave específica haciendo una solicitud de `GET /v2/keys/` o visualizando sus claves en el panel de control de {{site.data.keyword.hscrypto}}.

3. Ejecute el mandato cURL siguiente para suprimir permanentemente la clave y sus contenidos.

    ```cURL
    curl -X DELETE \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
    ```
    {: codeblock}

    Para trabajar con claves dentro de un espacio y organización de Cloud Foundry en su cuenta, sustituya `Bluemix-Instance` con las cabeceras adecuadas de `Bluemix-org` y `Bluemix-space`. [Para obtener más información, consulte el documento de referencia de la API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
    {: tip}

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
        <td>El identificador exclusivo para la clave que desea suprimir.</td>
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
        <td><varname>preferencia_retorno</varname></td>
        <td><p>Una cabecera que altera el comportamiento del servidor para operaciones de <code>POST</code> y <code>DELETE</code>.</p><p>Cuando establece la variable <em>preferencia_retorno</em> en <code>return=minimal</code>, el servicio devuelve una respuesta de supresión satisfactoria. Cuando establece la variable en <code>return=representation</code>, el servicio devuelve tanto el material de la clave como los metadatos de la clave.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Describe las variables necesarias para suprimir claves mediante la API de {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Si la variable _preferencia_return_ se establece en `return=representation`, los detalles de la solicitud `DELETE` se devuelven en el cuerpo de entidad de la respuesta. El siguiente objeto JSON muestra un valor devuelto de ejemplo.
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    Para ver una descripción detallada de los parámetros disponibles, consulte el [documento de referencia de la API REST ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window} de {{site.data.keyword.hscrypto}}.
