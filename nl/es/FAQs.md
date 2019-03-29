---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-21"

Keywords: frequently asked questions, critical security parameters, cryptographic module, Security Level

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Preguntas frecuentes
{: #faqs}

Utilice las siguientes preguntas más frecuentes (FAQ) como ayuda para {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.

## Certificaciones de HSM
{: #HSM}

### ¿Cómo puedo comprobar que se ha validado una tarjeta IBM Crypto (HSM) con el cumplimiento de FIPS 140-2 Nivel 4?

FIPS 140-2 Nivel 4 es un nivel de protección muy alto que no está ampliamente disponible en el mercado. IBM es el proveedor líder de HSM certificados para el nivel más alto y ha invertido mucho en mantener esta validación en cada nueva generación de tarjetas. El requisito para el nivel alto de garantía se ha recogido de los requisitos del Gobierno. Para la validación de la certificación, se le dirige a la página de inicio de NIST, ya que es ahí donde se ha publicado la certificación. 

### ¿Cuál es la diferencia entre FIPS 140-2 Nivel 2, 3 y 4?

* FIPS 140-2 Nivel 2: requisitos para pruebas de manipulación realizadas mediante precintos, candados resistentes en cubiertas extraíbles y puertas. Se colocan recubrimientos o precintos de seguridad en un módulo criptográfico para que se deba romper el recubrimiento o sello para obtener acceso físico a las claves criptográficas en texto sin formato y a los parámetros de seguridad críticos (CSP) dentro del módulo. El nivel de seguridad 2 requiere, como mínimo, autenticación basada en roles en la que un módulo criptográfico autentica la autorización de un operador para que asuma un rol específico y lleve a cabo el conjunto de servicios correspondiente.
 
* FIPS 140-2 Nivel 3: los mecanismos de seguridad física necesarios en el nivel de seguridad 3 están pensados para tener una alta probabilidad de detectar y responder a intentos de acceso físico, uso o modificación del módulo criptográfico. El nivel de seguridad 3 requiere mecanismos de autenticación basados en identidades, mejorando la seguridad proporcionada por los mecanismos de autenticación basada en roles especificados para el nivel de seguridad 2. 

* FIPS 140-2 Nivel 4: A este nivel de seguridad, los mecanismos de seguridad física proporcionan un envoltorio completo de protección alrededor del módulo criptográfico con la intención de detectar y responder a todos los intentos no autorizados de acceso físico. Es muy probable que se detecte la penetración del alojamiento del módulo criptográfico desde cualquier dirección, provocando que se pongan a cero de manera inmediata todos los parámetros de seguridad críticos (CSP) en texto sin formato. Los módulos criptográficos del nivel de seguridad 4 resultan útiles para la operación en entornos físicamente desprotegidos. El nivel de seguridad 4 también protege un módulo criptográfico frente a un compromiso en la seguridad provocado por las condiciones medioambientales o fluctuaciones fuera de los rangos de operación normales del módulo de voltaje y temperatura. Un atacante podría llevar el módulo criptográfico de manera intencionada más allá de sus rangos operativos normales para desbaratar sus defensas. 

## Gestión de claves

### ¿Se puede utilizar {{site.data.keyword.hscrypto}} en combinación con el servicio
{{site.data.keyword.keymanagementserviceshort}}?

 {{site.data.keyword.hscrypto}} es un servicio criptográfico gestionado que se suministra con una API de
{{site.data.keyword.keymanagementserviceshort}} completamente compatible, que tiene una experiencia de usuario idéntica a Key Protect. La diferencia principal es que {{site.data.keyword.hscrypto}} se basa en un HSM que se ha certificado con FIPS 140-2 nivel 4. Además, proporciona control completo al gestionar el cliente (KYOK) la clave maestra HSM. El servicio está dedicado por instancia, en comparación con la configuración multiarrendatario para {{site.data.keyword.keymanagementserviceshort}}. {{site.data.keyword.hscrypto}} ofrece también funciones de HSM para operaciones criptográficas como firmar/verificar, generar claves, hash criptográfico, cifrar/descifrar y envolver/desenvolver. 

### ¿Cuál es la longitud máxima de un nombre de clave?
{: #key_names}

Puede utilizar un nombre de clave con una longitud de hasta 50 caracteres.

### ¿Puedo utilizar caracteres de mi idioma como parte del nombre de clave?
{: #key_chars}

Los caracteres de idioma propios, como los del chino, no se pueden utilizar como parte del nombre de la clave.

### ¿Qué sucede cuando suprimo una clave?
{: #key_destruction}

Cuando suprime una clave, destruye el contenido y los datos asociados a ella de forma permanente. Ya no será posible acceder a los datos cifrados con la clave.

Antes de suprimir una clave, asegúrese de que ya no necesita acceder a ninguno de los datos asociados con la clave.
