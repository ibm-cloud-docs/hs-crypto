---

copyright:
years: 2018, 2019
lastupdated: "2019-03-26"

Keywords: root keys, standard keys, migration, transition, beta

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Migración de claves de una instancia de servicio beta
{: #migrate-keys}

Si ha estado utilizando una instancia de servicio beta y desea migrar las claves raíz y las claves estándar que ha gestionado a una instancia de servicio de producción de {{site.data.keyword.hscrypto}}, este es el procedimiento que debe seguir.
{: shortdesc}

Los administradores de IBM Cloud no pueden migrar las claves maestras porque las claves maestras no se pueden extraer de la unidad criptográfica. Debe inicializar la instancia de servicio de producción con la clave maestra.
{:important}  

## Antes de empezar
{: #migrate-prerequisites}

1. [Cree una instancia de servicio](/docs/services/hs-crypto/provision.html) con el plan Hyper Protect Crypto Services.

2. [Inicialice la instancia de servicio](/docs/services/hs-crypto/initialize_hsm.html) con el plugin Trusted Key Entry.

## Migración de claves
{: #migrate-keys-steps}  

Realice los pasos siguientes para migrar claves raíz y claves estándar al entorno de producción.

1. [Importe claves raíz](/docs/services/hs-crypto/import-root-keys.html) a través de la GUI o de la API.

  Puede migrar las claves raíz importadas desde la instancia de servicio beta a la instancia de servicio de producción.
  {:tip}

2. Desenvuelva las claves de cifrado de datos (DEK) de la instancia de servicio beta y envuelva las DEK en la instancia de servicio de producción:

  1. [Desenvuelva las claves de cifrado de datos (DEK)](/docs/services/hs-crypto/unwrap-keys.html) de la instancia de servicio beta con la [API invoke-an-action-on-a-key ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: new_window}.

  2. [Envuelva las DEK](/docs/services/hs-crypto/wrap-keys.html) en la instancia de servicio de producción con la
[API invoke-an-action-on-a-key
![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key{: new_window}).

3. Vuelva a crear las claves estándar siguiendo estos pasos:

  1. [Recupere las claves estándar](/docs/services/hs-crypto?topic=hs-crypto-view-keys#retrieve-key-api) con la
[API retrieve-key-by-id ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/hs-crypto#retrieve-a-key-by-id){: new_window}. Esto devuelve la carga útil utilizada para crear la clave en la instancia beta.

  2. [Cree claves estándar](/docs/services/hs-crypto/create-standard-keys.html) en la nueva instancia de servicio con la información recuperada en el paso anterior a través de la GUI o de la [API create-a-new-key
![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/hs-crypto#create-a-new-key){: new_window}.

## Qué hacer a continuación
{: #migration-next}

Para obtener más información sobre cómo gestionar las claves mediante programación, [consulte el documento de referencia de la API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
