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

# Introduzione all'inizializzazione dell'istanza del servizio
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> Questa esercitazione ti mostra come inizializzare l'istanza del servizio caricando le chiavi master per proteggere il tuo archivio di chiavi con il plug-in Trusted Key Entry. Dopo aver inizializzato l'istanza del servizio, puoi iniziare a gestire le tue chiavi root.   
{:shortdesc}

## Prerequisito
{: #get-started-hsm-prerequisite}

Prima di iniziare, completa i seguenti passi:

1. Esegui il provisioning dell'istanza {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} (istanza del servizio in breve). Per la procedura dettagliata, vedi [Provisioning di {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/provision.html).

2. Immetti il seguente comando per assicurarti di aver eseguito l'accesso all'endpoint API corretto:

  ```
  ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

3. Installa la versione più recente del plug-in Trusted Key Entry tramite la CLI (command-line interface) {{site.data.keyword.cloud_notm}} utilizzando il seguente comando:

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  Per installare il plug-in della CLI, vedi [Introduzione alla CLI {{site.data.keyword.cloud_notm}}](/docs/cli/index.html).
  {: tip}

4. Imposta la variabile di ambiente CLOUDTKEFILES per indicare la sottodirectory in cui vuoi memorizzare le parti della chiave e le chiavi di firma

##  Passo 1: crea le parti della chiave master e i file delle chiavi di firma
{: #hsm-step1}

1. Crea una parte della chiave master casuale o una parte della chiave master con un valore noto.

  * Per una parte della chiave master casuale, utilizza il seguente comando:

    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    Quando richiesto, immetti una descrizione per la parte della chiave e una password per il file delle parti della chiave.

  * Per creare una parte della chiave master con un valore noto, utilizza il seguente comando:

    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    Quando richiesto, immetti il valore di parte della chiave noto come stringa esadecimale, quindi immetti una descrizione e una password per il file delle parti della chiave.

  Ripeti entrambi i comandi per creare ulteriori parti della chiave.

2. Crea una chiave di firma con il seguente comando:
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  Quando richiesto, immetti un nome amministratore e una password per il file delle chiavi di firma.

## Passo 2: seleziona le unità di crittografia con cui vuoi lavorare
{: #hsm-step2}

Tutte le unità di crittografia in un'istanza del servizio devono essere configurate allo stesso modo.

1. Puoi visualizzare le istanze del servizio e le unità di crittografia assegnati al tuo account IBM Cloud utilizzando il seguente comando:

  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

2. Per selezionare ulteriori unità di crittografia con cui lavorare, utilizza il comando:

  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  Quando richiesto, immetti le unità di crittografia aggiuntive con cui lavorare.

3. Per rimuovere le unità di crittografia dalla serie con cui lavorerai, utilizza il comando:

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  Quando richiesto, immetti le unità di crittografia che vuoi rimuovere.

## Passo 3: aggiungi gli amministratori dell'unità di crittografia ed esci dalla modalità di impronta
{: #hsm-step3}

Prima di poter caricare le chiavi master in un'unità di crittografia, devi creare uno o più amministratori dell'unità di crittografia e uscire dalla modalità di impronta.

1. Carica un amministratore dell'unità di crittografia. Per creare un amministratore dell'unità di crittografia, utilizza il comando:
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  Quando richiesto, immetti il KEYNUM della chiave di firma da utilizzare per l'amministratore e la password per il file delle chiavi di firma.

2. Seleziona la chiave di firma da utilizzare per firmare i comandi utilizzando il comando:

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  Quando richiesto, immetti il KEYNUM della chiave di firma da utilizzare per firmare i comandi.

  Questo deve essere uguale a una delle chiavi di firma utilizzate per caricare un amministratore dell'unità di crittografia nel passo 3.1.
  {: tip}

3. Esci dalla modalità di impronta utilizzando il seguente comando:

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

Dopo aver caricato un amministratore dell'unità di crittografia ed essere uscito dalla modalità di impronta, puoi controllare lo stato delle tue unità di crittografia utilizzando il comando:
{: tip}

```
 ibmcloud tke cryptounit-compare
```
{: pre}

## Passo 4: carica il registro della chiave master
{: #hsm-step4}

Per caricare il registro della chiave master, è necessario definire uno o più amministratori dell'unità di crittografia e l'unità di crittografia deve aver lasciato la modalità di impronta.

1. Carica il nuovo registro della chiave master utilizzando il seguente comando:

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  Quando richiesto, immetti il KEYNUM delle parti della chiave da caricare, la password per il file delle chiavi di firma e le password per ogni parte della chiave selezionata.

2. Esegui il commit del nuovo registro della chiave master utilizzando il seguente comando:

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  Quando richiesto, immetti la password per il file delle chiavi di firma.

3. Sposta la chiave master nel registro della chiave master corrente utilizzando il seguente comando:

  ```
  ibmcloud tke cryptounit-mk-setimm
  ```
  {: pre}

  Quando richiesto, immetti la password per il file delle chiavi di firma.

## Operazioni successive
{: #hsm-next}

Ora puoi iniziare a utilizzare la tua istanza del servizio. Per i dettagli sull'implementazione della procedura in un ambiente di produzione, vedi [Inizializzazione delle istanze del servizio per proteggere l'archiviazione chiavi](/docs/services/hs-crypto/initialize_hsm.html).
