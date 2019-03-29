---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: Activity Tracker events, List of events

subcollection: hs-crypto

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Sucesos de {{site.data.keyword.cloudaccesstrailshort}}
{: #at-events}

Utilice el servicio de {{site.data.keyword.cloudaccesstrailfull}} para realizar el seguimiento de cómo interactúan los usuarios y las aplicaciones con {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

El servicio {{site.data.keyword.cloudaccesstrailfull_notm}} registra las actividades iniciadas por el usuario que cambian el estado de un servicio en {{site.data.keyword.cloud_notm}}.

Si desea obtener más información, consulte la [documentación de {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla).

## Lista de sucesos
{: #events}

La tabla siguiente lista las acciones que generan un suceso:

<table>
    <tr>
        <th>Acción</th>
        <th>Descripción</th>
    </tr>
    <tr>
        <td>hs-crypto.secrets.create</td>
        <td>Crear una clave</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.read</td>
        <td>Recuperar una clave por ID</td>
    </tr>
   <tr>
        <td>hs-crypto.secrets.delete</td>
        <td>Suprimir una clave por ID</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.list</td>
        <td>Recuperar una lista de claves</td>
    </tr>
    <tr>
        <td>hs-crypto.secrets.head</td>
        <td>Recuperar el número de claves</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.wrap</td>
        <td>Envolver una clave</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.unwrap</td>
        <td>Desenvolver una clave</td>
    </tr>
     <tr>
        <td>hs-crypto.secrets.rotate</td>
        <td>Rotar una clave</td>
    </tr>
    <caption style="caption-side:bottom;">Tabla 1. Acciones que generan sucesos de {{site.data.keyword.cloudaccesstrailfull_notm}}</caption>
</table>

## Dónde ver los sucesos
{: #gui}

<!-- Option 2: Add the following sentence if your service sends events to the account domain. -->

Los sucesos de {{site.data.keyword.cloudaccesstrailshort}} están disponibles en el **dominio de la cuenta** de {{site.data.keyword.cloudaccesstrailshort}} disponible en la región de {{site.data.keyword.cloud_notm}} donde se han generado los sucesos.

Por ejemplo, al crear, importar, suprimir o leer una clave en {{site.data.keyword.hscrypto}}, se genera un suceso de {{site.data.keyword.cloudaccesstrailshort}}. Estos sucesos se reenvían automáticamente al servicio de {{site.data.keyword.cloudaccesstrailshort}} en la misma región donde se proporciona el servicio de {{site.data.keyword.hscrypto}}.

Para supervisar la actividad de la API, debe suministrar el servicio de {{site.data.keyword.cloudaccesstrailshort}} en un espacio que esté disponible en la misma región donde se suministra el servicio de {{site.data.keyword.hscrypto}}. A continuación, puede ver sucesos mediante la vista de la cuenta en la IU de {{site.data.keyword.cloudaccesstrailshort}} si tiene un plan Lite, y mediante Kibana si tiene un plan Premium.

## Información adicional
{: #info}

Debido a la confidencialidad de la información para una clave de cifrado, cuando se genera un suceso como resultado de una llamada de API al servicio de {{site.data.keyword.hscrypto}}, el suceso generado no incluye información detallada sobre la clave. El suceso incluye un ID de correlación que puede utilizar para identificar la clave internamente en el entorno de nube. El ID de correlación es un campo que se devuelve como parte del campo `responseHeader.content`. Puede utilizar esta información para correlacionar la clave de {{site.data.keyword.hscrypto}} con la información de la acción de la que se ha informado a través del suceso de {{site.data.keyword.cloudaccesstrailshort}}.
