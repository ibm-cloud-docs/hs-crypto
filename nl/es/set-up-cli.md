---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: IBM Cloud CLI plug-in, ibmcloud commands, IBM Cloud command-line interface

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Acceso a la CLI de {{site.data.keyword.keymanagementserviceshort}} en una instancia de {{site.data.keyword.hscrypto}}
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} se integra con el plugin de CLI de {{site.data.keyword.keymanagementservicelong_notm}}, por lo que puede utilizar el plugin de CLI de {{site.data.keyword.keymanagementservicelong_notm}} para crear, importar y gestionar claves raíz de cifrado y claves estándar.

Para poder utilizar el plugin de CLI de {{site.data.keyword.keymanagementserviceshort}} en una instancia de {{site.data.keyword.hscrypto}} (instancia de servicio para abreviar), deberá establecer la variable de entorno KP_KP_PRIVATE_ADDR en su estación de trabajo:

* En Linux o MacOS, ejecute el mandato siguiente:

  ```
  export KP_PRIVATE_ADDR=<URL>
  ```
  {: pre}

  En este mandato, el *URL* es el punto final que se muestra en el separador **Gestionar** del panel de control de {{site.data.keyword.hscrypto}} suministrado. Por ejemplo:

  ```
  export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
  ```
  {: pre}

* En Windows, en el **Panel de Control**, escriba `variable de entorno` en el recuadro de búsqueda para localizar la ventana Variables de entorno. Cree una variable de entorno KP_PRIVATE_ADDR y establezca el valor en el punto final que aparece en el separador **Gestionar** del panel de control de {{site.data.keyword.hscrypto}} suministrado. Por ejemplo, `https://us-south.hs-crypto.cloud.ibm.com:<port>`.

También puede recuperar el URL de punto final a través de la API. Para obtener detalles, [compruebe el documento de referencia de la API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

- Para obtener más información sobre el uso de la CLI, consulte el [documento de consulta de CLI de {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/cli-reference.html).
- Para obtener información sobre cómo acceder a la CLI, consulte [Configuración de la CLI de {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/set-up-cli.html).
