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

# Configuración de la CLI
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} se integra con el plugin de CLI
{{site.data.keyword.keymanagementservicelong_notm}}, por lo que puede utilizar el plugin de CLI
{{site.data.keyword.keymanagementservicelong_notm}} para crear, importar y gestionar claves raíz de cifrado y claves estándar.

- Para obtener más información sobre el uso de la CLI, consulte el [documento de consulta de CLI de {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/cli-reference.html).
- Para obtener información sobre cómo acceder a la CLI, consulte
[Configuración de la CLI de {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/set-up-cli.html).

Para poder utilizar el plugin de CLI {{site.data.keyword.keymanagementserviceshort}} en una instancia de
{{site.data.keyword.hscrypto}}, ejecute el mandato siguiente en primer lugar:

```
export KP_PRIVATE_ADDR=<URL>
```
{: pre}

En este mandato, el *URL* es el punto final que se muestra en la página **Gestionar** de la interfaz de usuario. O bien, puede recuperar el URL de punto final a través de la API. Por ejemplo:

```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
```
{: pre}

Para obtener detalles, [consulte el documento de referencia de la API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
