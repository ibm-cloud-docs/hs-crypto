---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: troubleshoot, problems, known issues

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}

# Resolución de problemas
{: #troubleshooting}

Entre los problemas generales relacionados con la utilización de {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} se pueden incluir el suministro de cabeceras o credenciales correctas al interactuar con la API. En muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos.
{: shortdesc}

## Se ha producido un error al suprimir una instancia de {{site.data.keyword.hscrypto}} inicializada

Es posible que reciba un error similar al siguiente al suprimir una instancia de
{{site.data.keyword.hscrypto}} inicializada:

```
FAILED
Error response from server. Status code: 400; description: 400 DELETE https://zCryptoBroker.mybluemix.net/v2/service_instances/ failed with error status 409. Conflict.
```
{: codeblock}
{: tsSymptoms}

No ha borrado (puesto a cero) la instancia de {{site.data.keyword.hscrypto}} inicializada antes de suprimir la instancia.
{: tsCauses}

Ejecute el mandato siguiente antes de suprimir la instancia:
{: tsResolve}

```
ibmcloud tke domain-zeroize
```
{: codeblock}

## Señal no autorizada después de ejecutar mandatos relacionados con el plugin Trusted Key Entry

Es posible que reciba mensajes similares a los siguientes después de ejecutar los mandatos de CLI `tke`:

```
ibmcloud tke domains
FAILED
Error querying crypto instances.
Status code: 401
Message: Unauthorized
Your access token is invalid, expired, or does not have the necessary permissions to access this instance.`
```
{: codeblock}
{: tsSymptoms}

La señal no se renueva.
{: tsCauses}

Inicie sesión en {{site.data.keyword.cloud_notm}} de nuevo con el mandato `ibmcloud login` para renovar la señal.
{: tsResolve}

## Se ha obtenido el error `CKR_IBM_WK_NOT_INITIALIZED` al utilizar la CLI o la API

Al utilizar la CLI o la API, es posible que obtenga un mensaje de error similar al siguiente:

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

Al ejecutar el mandato `ibmcloud tke domain-compare`, no ha obtenido una confirmación
`Valid` sobre el CURRENT MASTER KEY REGISTER (registro de clave maestra actual).
{: tsCauses}

Asegúrese de que la clave maestra de HSM se haya establecido correctamente.
{: tsResolve}

## No se han podido crear ni suprimir claves
{: #unable-to-create-keys}

Al acceder a la interfaz de usuario de {{site.data.keyword.hscrypto}} no visualiza las opciones para añadir ni suprimir claves.

Desde el panel de control de {{site.data.keyword.cloud_notm}}, seleccione su instancia del servicio de {{site.data.keyword.hscrypto}}.
{: tsSymptoms}

Puede ver una lista de claves, pero no ve las opciones para agregar o suprimir claves.

No dispone de la autorización adecuada para realizar acciones de {{site.data.keyword.hscrypto}}.
{: tsCauses}

Verifique con el administrador que se le haya asignado el rol correcto en el grupo de recursos o la instancia de servicio. Para obtener más información sobre los roles, consulte [Roles y permisos](/docs/services/key-protect/manage-access.html#roles).
{: tsResolve}

## Obtención de ayuda y soporte
{: #getting-help}

Si tiene problemas o pregunta relacionadas con el uso de {{site.data.keyword.hscrypto}}, puede consultar {{site.data.keyword.cloud_notm}} u obtener ayuda buscando información o realizando preguntas mediante un foro. También puede abrir una incidencia de soporte.
{: shortdesc}

Puede comprobar si {{site.data.keyword.cloud_notm}} está disponible desde la [página de estado de ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/status?tags=platform,runtimes,services).

Puede revisar los foros para ver si otros usuarios han tenido el mismo problema. Cuando utilice foros para hacer una pregunta, etiquete su pregunta para que la vean los equipos de desarrollo de {{site.data.keyword.cloud_notm}}.

- Si tiene preguntas técnicas sobre {{site.data.keyword.hscrypto}}, publique su pregunta en [Stack Overflow ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://stackoverflow.com/){: new_window} y etiquete su pregunta con "ibm-cloud" e "hyperprotect-crypto".
- Para formular preguntas sobre el servicio y obtener instrucciones de iniciación, utilice el foro [IBM developerWorks dW Answers ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/answers/index.html){: new_window}. Incluya las etiquetas "ibm-cloud" e "hyperprotect-crypto".

Consulte [Obtención de ayuda ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/docs/support/index.html#getting-help){: new_window} para obtener más información sobre el uso de los foros.

Para obtener más información sobre cómo abrir una incidencia de soporte de {{site.data.keyword.IBM_notm}} o sobre los niveles de soporte y las gravedades de las incidencias, consulte [Cómo obtener soporte ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/docs/support/index.html#contacting-support){: new_window}.
