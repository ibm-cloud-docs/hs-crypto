---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-15"

Keywords: key storage, service instance, HSM, hardware security module

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}  
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# Guía de inicio de la inicialización de instancias de servicio
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> En esta guía de aprendizaje se muestra cómo inicializar la instancia de servicio cargando las claves maestras para proteger el almacén de claves con el plugin Trusted Key Entry. Después de inicializar la instancia de servicio, puede empezar a gestionar las claves raíz.   
{:shortdesc}

## Requisito previo
{: #get-started-hsm-prerequisite}

Antes de empezar, realice los siguientes pasos:

1. Suministre la instancia de {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} (instancia de servicio para abreviar). Para ver los pasos detallados, consulte [Suministro de {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/provision.html).

2. Ejecute el mandato siguiente para asegurarse de que ha iniciado sesión en el punto final de API correcto:

  ```
  ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

3. Instale el plugin Trusted Key Entry más reciente a través de la interfaz de línea de mandatos (CLI) de {{site.data.keyword.cloud_notm}} con el mandato siguiente:

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  Para instalar el plugin de CLI, consulte [Iniciación a la CLI de {{site.data.keyword.cloud_notm}}](/docs/cli/index.html).
  {: tip}

4. Establezca la variable de entorno CLOUDTKEFILES para indicar el subdirectorio donde desea almacenar los componentes de clave y las claves de firma

##  Paso 1: Crear los componentes de clave maestra y los archivos de claves de firma
{: #hsm-step1}

1. Cree un componente de clave maestra aleatorio o un componente de clave maestra con un valor conocido.

  * Para crear un componente de clave maestra aleatorio, utilice el mandato siguiente:

    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    Cuando se le solicite, especifique una descripción para el componente de clave y una contraseña para el archivo de componente de clave.

  * Para crear un componente de clave maestra con un valor conocido, utilice el mandato siguiente:

    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    Cuando se le solicite, especifique el valor de componente de clave conocido como una serie hexadecimal y, a continuación, especifique una descripción y una contraseña para el archivo de componente de clave.

  Repita cualquier de los mandatos para crear componentes de clave adicionales.

2. Cree una clave de firma con el mandato siguiente:
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  Cuando se le solicite, especifique un nombre del administrador y una contraseña para el archivo de claves de firma.

## Paso 2: Seleccionar las unidades criptográficas con las que desee trabajar
{: #hsm-step2}

Todas las unidades criptográficas de una instancia de servicio debe estar configuradas de la misma manera.

1. Puede mostrar las instancias de servicio y las unidades criptográficas asignadas a su cuenta de usuario de IBM Cloud utilizando el mandato siguiente:

  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

2. Para seleccionar unidades criptográficas adicionales con las que trabajar, utilice el mandato siguiente:

  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  Cuando se le solicite, especifique las unidades criptográficas adicionales con las que desee trabajar.

3. Para eliminar unidades criptográficas del conjunto con el que se va a trabajar, utilice el mandato siguiente:

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  Cuando se le solicite, especifique las unidades criptográficas que desee eliminar.

## Paso 3: Añadir administradores de unidad criptográfica y salir de la modalidad de impresión
{: #hsm-step3}

Para poder cargar las claves maestras en una unidad criptográfica, primero debe crear uno o más administradores de unidad criptográfica y salir de la modalidad de impresión.

1. Cargue un administrador de unidad criptográfica. Para crear un administrador de unidad criptográfica, utilice el mandato siguiente:
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  Cuando se le solicite, especifique el KEYNUM de la clave de firma que debe utilizar el administrador y la contraseña para el archivo de claves de firma.

2. Seleccione la clave de firma a utilizar para firmar mandatos utilizando el mandato siguiente:

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  Cuando se le solicite, especifique el KEYNUM de la clave de firma a utilizar para firmar los mandatos.

  Esta debe ser la misma que una de las claves de firma utilizadas para cargar un administrador de unidad criptográfica en el paso 3.1.
  {: tip}

3. Salga de la modalidad de impresión utilizando el mandato siguiente:

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

Después de cargar un administrador de unidad criptográfica y salir de la modalidad de impresión, puede comprobar el estado de las unidades criptográficas utilizando el mandato siguiente:
{: tip}

```
 ibmcloud tke cryptounit-compare
```
{: pre}

## Paso 4: Cargar el registro de clave maestra
{: #hsm-step4}

Para cargar el registro de clave maestra, debe definirse uno o más administradores de unidad criptográfica y la unidad criptográfica debe haber salido de la modalidad de impresión.

1. Cargue el nuevo registro de clave maestra utilizando el mandato siguiente:

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  Cuando se le solicite, especifique el KEYNUM de los componentes de clave que se van a cargar, la contraseña para el archivo de claves de firma y las contraseñas de cada componente de clave seleccionado.

2. Confirme el nuevo registro de clave maestra con el mandato siguiente:

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  Cuando se le solicite, especifique la contraseña para el archivo de claves de firma.

3. Mueva la clave maestra al registro de clave maestra actual con el mandato siguiente:

  ```
  ibmcloud tke cryptounit-mk-setimm
  ```
  {: pre}

  Cuando se le solicite, especifique la contraseña para el archivo de claves de firma.

## Qué hacer a continuación
{: #hsm-next}

Ahora puede empezar a utilizar la instancia de servicio. Para obtener detalles sobre cómo implementar el procedimiento en un entorno de producción, consulte [Inicialización de instancias de servicio para proteger el almacén de claves](/docs/services/hs-crypto/initialize_hsm.html).
