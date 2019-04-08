---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-21"

Keywords: release note, new

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Novedades
{: #what-new}

Consulte información actualizada sobre las nuevas características disponibles para {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Marzo de 2019
{: #March-2019}

### {{site.data.keyword.hscrypto}} está disponible de forma general
{: #ga-201903}
Novedad desde: 29-03-2019

Para obtener más información sobre la oferta de {{site.data.keyword.hscrypto}}, consulte la página de inicio de [{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/hyper-protect-crypto){:new_window}.

A partir del 31 de marzo de 2019, ya no será posible el suministro de nuevas instancias de Hyper Protect Crypto Services Beta. Las instancias existentes seguirán teniendo soporte hasta que llegue la fecha de finalización del soporte beta (30 de abril de 2019).

Consulte [Migración de claves de una instancia de servicio beta](/docs/services/hs-crypto/transition-keys.html) para obtener información sobre la migración de claves a una instancia de servicio de producción.

### Alta disponibilidad y recuperación tras desastre
{: #ha-dr-new}
Novedad desde: 29-03-2019

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, que ahora admite tres zonas de disponibilidad en una región seleccionada, es un servicio de alta disponibilidad con funciones automáticas que le ayudan a mantener sus aplicaciones seguras y operativas.

Puede crear recursos de {{site.data.keyword.hscrypto}} en las [regiones de {{site.data.keyword.cloud_notm}}](/docs/services/hs-crypto/regions.html) admitidas, que representan la zona geográfica donde se pueden gestionar y procesar sus solicitudes de {{site.data.keyword.hscrypto}}. Cada región de {{site.data.keyword.cloud_notm}} contiene [varias zonas de disponibilidad ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/) para cumplir los requisitos de acceso, baja latencia y seguridad de la región.

Para obtener más información, consulte [Alta disponibilidad y recuperación tras desastre](/docs/services/hs-crypto/ha-dr.html).

### Escalabilidad
{: #scalability-new}
Novedad desde: 29-03-2019

La instancia de servicio se puede escalar hasta un máximo de seis unidades criptográficas para ajustarse a sus requisitos de rendimiento. Cada unidad criptográfica puede procesar de manera criptográfica 5000 claves. En un entorno de producción, se recomienda seleccionar al menos dos unidades criptográficas para habilitar la alta disponibilidad. Al seleccionar tres o más unidades criptográficas, estas unidades criptográficas se distribuyen en tres zonas de disponibilidad en la región seleccionada.

Consulte [Suministro del servicio](/docs/services/hs-crypto/provision.html) para obtener más información.

## Febrero de 2019
{: #Feb-2019}

### La Beta de {{site.data.keyword.hscrypto}} está disponible
{: #beta-201902}
Novedad desde: 05-02-2019

Se publica la versión Beta de {{site.data.keyword.hscrypto}}. Ahora puede acceder al servicio de {{site.data.keyword.hscrypto}} a través de **Catálogo** > **Seguridad e identidad** directamente.

A partir del 5 de febrero de 2019, ya no será posible el suministro de nuevas instancias de Hyper Protect Crypto Services Experimental. Las instancias existentes seguirán teniendo soporte hasta que llegue la fecha de finalización del soporte experimental (5 de marzo de 2019).

## Diciembre de 2018
{: #Dec-2018}

### Se ha añadido: soporte para la gestión de HSM con KYOK
{: #hsm-kyok}
Novedad desde: 19-12-2018

{{site.data.keyword.hscrypto}} ahora admite Keep Your Own Keys (KYOK), de manera que tiene más control y autoridad sobre los datos con claves de cifrado que puede mantener, controlar y gestionar. Puede inicializar y gestionar la instancia de servicio con la interfaz de línea de mandatos (CLI) de {{site.data.keyword.cloud}}.

Para obtener más información, consulte [Inicialización de instancias de servicio para proteger el almacén de claves](/docs/services/hs-crypto/initialize_hsm.html).

### Se ha añadido: integración de la API de {{site.data.keyword.keymanagementserviceshort}}
{: #kp-api}
Novedad desde: 19-12-2018

La API de {{site.data.keyword.keymanagementserviceshort}} ahora se integra con Hyper Protect Crypto Services para generar y proteger sus claves. Puede llamar a la API de {{site.data.keyword.keymanagementserviceshort}} directamente a través de {{site.data.keyword.hscrypto}}.

Para obtener más información, consulte [Acceso a la API](/docs/services/hs-crypto/access-api.html) y
[API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](image/external_link.svg "Icono de enlace externo")](https://{DomainName}/apidocs/hs-crypto){:new_window}.

### En desuso: función de acceso a {{site.data.keyword.hscrypto}} a través de ACSP
{: #deprecated-acsp}
Novedad desde: 19-12-2018

En la etapa actual, el acceso a {{site.data.keyword.hscrypto}} a través de un cliente de Advanced Cryptography Service Provider (ACSP) queda en desuso. Si utiliza una instancia de servicio anterior, podrá seguir utilizando ACSP para explorar {{site.data.keyword.hscrypto}}.
