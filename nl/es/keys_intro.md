---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: root keys, master keys, standard keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# Introducción a las claves
{: #introduce-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} admite varios tipos de claves, incluyendo claves raíz, claves estándar y claves maestras.
{:shortdesc}

## Claves raíz

Las *claves raíz* son claves que se utilizan para envolver otras claves y que gestiona en su totalidad con {{site.data.keyword.hscrypto}}. Una clave raíz sirve para proteger otras claves criptográficas con cifrado avanzado. Para obtener más información, consulte <a href="/docs/services/key-protect/concepts/envelope-encryption.html">Cifrado de sobre</a>.

Puede gestionar claves raíz siguiendo los pasos de [Gestionar las claves](/docs/services/hs-crypto/index.html#manage-keys).

## Claves estándar

Las *claves estándar* son claves simétricas que se utilizan para la criptografía. Puede utilizar una clave estándar para cifrar y descifrar datos directamente.

Puede gestionar claves estándar siguiendo los pasos de [Gestionar las claves](/docs/services/hs-crypto/index.html#manage-keys).

## Claves maestras

Las *claves maestras* se utilizan para cifrar la instancia criptográfica (HSM) que procesa de manera criptográfica y gestiona las claves raíz y las claves estándar. Con la clave maestra, es propietario de la raíz de confianza que cifra toda la cadena de claves, incluyendo las claves raíz y las claves estándar.

Debido al canal seguro de extremo a extremo con la instancia criptográfica (HSM), únicamente los administradores de la instancia de {{site.data.keyword.hscrypto}} pueden establecer y gestionar la clave maestra. Tenga en cuenta que IBM no realiza copias de seguridad ni toca la clave maestra, y no tiene ninguna manera de copiarla ni restaurarla en una máquina o centro de datos diferente.

Una instancia criptográfica (HSM) solo puede tener una clave maestra. Si suprime la clave maestra de la instancia de
{{site.data.keyword.hscrypto}}, puede destruir criptográficamente de forma efectiva todos los datos que se han cifrado con las claves gestionadas en el servicio.

Puede gestionar claves maestras con la [Inicialización de instancias criptográficas para proteger el almacén de claves](/docs/services/hs-crypto/initialize_hsm.html).

No se admite la rotación de clave maestra en la etapa actual.
{:important}
