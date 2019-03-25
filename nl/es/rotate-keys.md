---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: root keys, Rotate key, key rotation

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Rotación de claves
{: #rotating-keys}

Puede rotar las claves raíz bajo demanda utilizando {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

Actualmente no se admite la rotación de claves maestras.
{: important}

Cuando se rota la clave raíz, se acorta el tiempo de vida de la clave y se limita la cantidad de información que protege dicha clave.   

Para obtener información sobre como la rotación de claves le ayuda a cumplir los estándares del sector y las mejores prácticas en criptografía, consulte [Rotación de claves](/docs/services/key-protect/concepts/key-rotation.html).

La rotación solo está disponible para las claves raíz.
{: tip}

## Rotación de claves raíz con la GUI
{: #gui}

Si prefiere rotar sus claves raíz utilizando una interfaz gráfica, puede utilizar la GUI de {{site.data.keyword.hscrypto}}.

[Después de crear o importar sus claves raíz existentes en el servicio](/docs/services/hs-crypto/create-root-keys.html), complete los siguientes pasos para rotar una clave:

1. [Inicie sesión en la consola de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/){: new_window}.
2. Desde el panel de control de {{site.data.keyword.cloud_notm}} seleccione su instancia suministrada de {{site.data.keyword.hscrypto}}.
3. Utilice la tabla de **Claves** tabla para examinar las claves en el servicio.
4. Pulse el icono ⋮ para abrir una lista de opciones para la clave que desea rotar.
5. En el menú de opciones, pulse **Rotar clave** y confirme la rotación en la pantalla siguiente.

Si importó la clave raíz inicialmente, debe proporcionar nuevo material de clave con codificación base64 para rotar la clave. Para obtener más información, consulte [Importación de claves raíz con la interfaz gráfica de usuario](/docs/services/hs-crypto/import-root-keys.html#gui).
{: tip}

## Rotación de raíz claves utilizando la API
{: #api}

[Después de designar una clave raíz en el servicio](/docs/services/hs-crypto/create-root-keys.html), puede rotar la clave realizando una llamada `POST` al siguiente punto final.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate
```
{: codeblock}

1. [Recupere sus credenciales de servicio y de autenticación para trabajar con claves en el servicio.](/docs/services/hs-crypto/access-api.html)

2. Copie el ID de la clave raíz que desea rotar.

4. Ejecute el siguiente mandato cURL para sustituir la clave con nuevo material.

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -d '{
        'payload: <material_clave>'
      }'
    ```
    {: codeblock}

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
        <td>Identificador exclusivo para la clave raíz que desea rotar.</td>
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
        <td><varname>material_clave</varname></td>
        <td>
          <p>Material de clave codificado en base64 que desea almacenar y gestionar en el servicio. Este valor es necesario si inicialmente importó el material de clave cuando añadió la clave al servicio.</p>
          <p>Para rotar una clave que {{site.data.keyword.hscrypto}} generó inicialmente, omita el atributo <code>payload</code> y pase un cuerpo de entidad de solicitud vacía. Para rotar una clave importada, proporcione un material de clave que cumpla los siguientes requisitos:</p>
          <p>
            <ul>
              <li>La clave debe ser de 256, 384 o 512 bits.</li>
              <li>Los bytes de datos, por ejemplo, 32 bytes para 256 bits, se deben codificar en base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Describe las variables necesarias para rotar una clave especificada en {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Una solicitud de rotación correcta devuelve una respuesta HTTP `204 No Content`, que indica que la clave raíz se ha sustituido por material de clave nuevo.

4. Opcional: Verifique que la clave se ha rotado ejecutando la siguiente llamada para examinar las claves en su instancia de servicio de {{site.data.keyword.hscrypto}}.

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    ```
    {: codeblock}

    Revise el valor `lastRotateDate` en el cuerpo de entidad de respuesta para comprobar la fecha y hora en que se rotó la clave por última vez.
