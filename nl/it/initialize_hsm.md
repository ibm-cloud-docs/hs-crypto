---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-21"

Keywords: key storage, HSM, hardware security module

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# Inizializzazione delle istanze del servizio
{: #initialize-hsm}

Prima di utilizzare l'istanza {{site.data.keyword.hscrypto}} (istanza del servizio in breve), devi caricare i registri della chiave master utilizzando il plugin Trusted Key Entry.
{:shortdesc}

Per inizializzare le istanze del servizio, devi prima caricare la chiave master con il plugin Trusted Key Entry nella tua istanza del servizio di archiviazione delle chiavi. Il plugin Trusted Key Entry ti consente di caricare i tuoi valori della chiave master.

Per un'introduzione all'inizializzazione dell'istanza del servizio e altri concetti, vedi [Introduzione all'inizializzazione dell'istanza del servizio](/docs/services/hs-crypto/service_instance_concepts.html#introduce-service).

Il seguente diagramma ti fornisce una panoramica della procedura che devi seguire per inizializzare l'istanza del servizio. Fai clic su ogni passo nel diagramma per le istruzioni dettagliate.

<img usemap="#home_map1" border="0" class="image" id="image_ztx_crb_f1b2" src="image/hsm_initialization_flow.png" width="750" alt="Fai clic su ogni passo per ottenere ulteriori dettagli sul flusso." style="width:750px;" />
<map name="home_map1" id="home_map1">
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-crypto-prerequisites" alt="Verifica l'endpoint API" title="Verifica l'endpoint API" shape="rect" coords="151, 20, 241, 78" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-crypto-prerequisites" alt="Configura la CLI" title="Configura la CLI" shape="rect" coords="276, 20, 365, 78" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-crypto-prerequisites4" alt="Installa il plugin TKE" title="Installa il plugin TKE" shape="rect" coords="401, 20, 493, 78" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-crypto-prerequisites4" alt="Configura la directory locale per i file della chiave" title="Configura la directory locale per i file della chiave" shape="rect" coords="528, 20, 619, 78" />

<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#Identify_crypto_units" alt="Visualizza le unità di crittografia assegnate" title="Visualizza le unità di crittografia assegnate" shape="rect" coords="148, 111, 241, 171" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#Identify_crypto_units1" alt="Aggiungi le unità di crittografia" title="Aggiungi le unità di crittografia" shape="rect" coords="276, 111, 366, 171" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#Identify_crypto_units2" alt="Rimuovi le unità di crittografia" title="Rimuovi le unità di crittografia" shape="rect" coords="402, 111, 493, 171" />

<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step1-create-signature-keys" alt="Crea una o più chiavi di firma" title="Crea le chiavi di firma" shape="rect" coords="149, 206, 242, 264" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step2-load-admin" alt="Gestisci gli amministratori dell'unità di crittografia" title="Gestisci gli amministratori dell'unità di crittografia" shape="rect" coords="281, 206, 366, 264" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step2-load-admin" alt="Aggiungi uno o più amministratori nell'unità di crittografia di destinazione" title="Aggiungi gli amministratori dell'unità di crittografia" shape="rect" coords="242, 296, 312, 358" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step3-exit-imprint-mode" alt="Esci dalla modalità impronta nell'unità di crittografia di destinazione" title="Esci dalla modalità impronta" shape="rect" coords="328, 301, 396, 359" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step4-create-master-key" alt="Crea una serie di parti della chiave master da utilizzare" title="Crea una serie di parti della chiave master" shape="rect" coords="401, 208, 493, 266" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step5-load-master-key" alt="Carica i registri della chiave master" title="Carica il registro della chiave master" shape="rect" coords="525, 207, 620, 264" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step5-load-master-key" alt="Carica i nuovi registri della chiave master" title="Carica il nuovo registro della chiave master" shape="rect" coords="455, 297, 525, 358" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step6-commit-master-key" alt="Esegui il commit del nuovo registro della chiave master" title="Esegui il commit del nuovo registro della chiave master" shape="rect" coords="539, 297, 610, 358" />
<area href="/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm#step7-activate-master-key" alt="Attiva la chiave master" title="Attiva il registro della chiave master" shape="rect" coords="619, 297, 689, 358" />
</map>

*Figura 1. Flusso di attività dell'inizializzazione dell'istanza del servizio*

Per completare questa attività potrebbero essere necessari 20-30 minuti.

## Prima di cominciare
{: #initialize-crypto-prerequisites}

1. Immetti il seguente comando per assicurarti di aver eseguito l'accesso all'endpoint API corretto:

  ```
  ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

2. Installa il plugin {{site.data.keyword.keymanagementservicefull}}. Per la procedura dettagliata, vedi [Configurazione della CLI](/docs/services/hs-crypto/set-up-cli.html). Quando accedi alla [CLI {{site.data.keyword.cloud_notm}}](/docs/cli/index.html#overview), ricevi una notifica quando sono disponibili degli aggiornamenti. Assicurati di mantenere aggiornato il tuo plugin {{site.data.keyword.keymanagementservicefull}} in modo da poter usare i comandi e gli indicatori disponibili per il plugin della CLI Trusted Key Entry.
{: #initialize-crypto-prerequisites2}

3. Installa il plugin Trusted Key Entry più recente con il seguente comando:
{: #initialize-crypto-prerequisites3}

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  **Importante:** se stai utilizzando l'istanza beta di {{site.data.keyword.hscrypto}}, esegui 'ibmcloud plugin install tke -v 0.0.4' per ottenere la versione beta più recente del plugin Trusted Key Entry. Non installare le versioni successive del plugin Trusted Key Entry.

4. Imposta la variabile di ambiente CLOUDTKEFILES sulla tua workstation. Specifica una directory in cui vuoi vengano creati e salvati i file della parte della chiave master e della chiave di firma. Crea la directory se ancora non esiste.
{: #initialize-crypto-prerequisites4}

  * Su Linux o MacOS, aggiungi la seguente riga al file `.bash_profile`:
     ```
     export CLOUDTKEFILES=<path>
     ```
     {: pre}
     Ad esempio, puoi specificare *path* con `/Users/tke-files`.
  * Su Windows, nel **Pannello di controllo**, immetti `environment variable` nella casella di ricerca per individuare la finestra Variabili di ambienti. Crea una variabile di ambiente CLOUDTKEFILES e impostane il valore sul percorso ai file della chiave. Ad esempio, `C:\users\tke-files`.

## Aggiunta e rimozione delle unità di crittografia assegnate a un account utente
{: #Identify_crypto_units}

Le unità di crittografia assegnate a un account utente di {{site.data.keyword.cloud_notm}} si trovano in un gruppo noto come *istanza del servizio*. Un'istanza del servizio può avere fino a sei unità di crittografia. Tutte le unità di crittografia in un'istanza del servizio dovrebbero essere configurate allo stesso modo. Se non è possibile accedere a una parte di {{site.data.keyword.cloud_notm}}, le unità di crittografia in un'istanza del servizio possono essere utilizzate in modo intercambiabile per il bilanciamento del carico o per la disponibilità.

Le unità di crittografia assegnate a un utente {{site.data.keyword.cloud_notm}} iniziano in uno stato cancellato noto come *modalità di impronta*. 

I registri della chiave master in tutte le unità di crittografia in una sola istanza del servizio devono essere impostati allo stesso modo. La stessa serie di amministratori deve essere aggiunta a tutte le unità di crittografia e tutte le unità di crittografia devono uscire dalla modalità di impronta contemporaneamente.

* Per visualizzare le istanze del servizio e le unità di crittografia assegnati a un account utente, utilizza il seguente comando:
  {: #Identify_crypto_units1}
  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

  Il seguente è un output di esempio che viene visualizzato. La colonna SELECTED nella tabella di output identifica le unità di crittografia che verranno utilizzate dai successivi comandi di gestione emessi dal plug-in Trusted Key Entry. 

  ```
  SERVICE INSTANCE: 482cf2ce-a06c-4265-9819-0b4acf54f2ba
  CRYPTO UNIT NUM   SELECTED   LOCATION
  1                 true       [us-south].[AZ3-CS3].[02].[03]
  2                 true       [us-south].[AZ2-CS2].[02].[03]

  SERVICE INSTANCE: 96fe3f8d-9792-45bc-a9fb-2594222deaf2
  CRYPTO UNIT NUM   SELECTED   LOCATION
  3                 true       [us-south].[AZ1-CS4].[00].[03]
  4                 true       [us-south].[AZ2-CS5].[03].[03]
  ```
  {: screen}

* Per aggiungere ulteriori unità di crittografia all'elenco di unità di crittografia selezionato, utilizza il seguente comando:
  {: #Identify_crypto_units2}
  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  Viene visualizzato un elenco delle unità di crittografia che sono assegnate all'account utente corrente. Quando richiesto, immetti un elenco di numeri di unità di crittografia da aggiungere all'elenco delle unità di crittografia selezionato.

* Per rimuovere le unità di crittografia dall'elenco di unità di crittografia selezionato, utilizza il seguente comando:
  {: #Identify_crypto_units3}
  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  Viene visualizzato un elenco delle unità di crittografia che sono assegnate all'account utente corrente. Quando richiesto, immetti un elenco di numeri di unità di crittografia da rimuovere dall'elenco delle unità di crittografia selezionato.

  **Suggerimento:** in generale, vengono selezionate tutte o nessuna delle unità di crittografia in un'istanza del servizio. In questo modo, i successivi comandi di gestione aggiornano in modo coerente tutte le unità di crittografia di un'istanza del servizio. Tuttavia, se le unità di crittografia di un'istanza del servizio vengono configurate in modo diverso, devi selezionare e utilizzare le unità di crittografia singolarmente per ripristinare una configurazione coerente per tutte le unità di crittografia in un'istanza del servizio.

  Puoi confrontare le impostazioni di configurazione delle unità di crittografia selezionate con il seguente comando:
  ```
  ibmcloud tke cryptounit-compare
  ```
  {: pre}

## Caricamento delle chiavi master
{: #load-master-keys}

<!-- A service instance is implemented as one or more crypto units on IBM cryptographic coprocessors. -->

Prima di poter caricare il nuovo registro della chiave master, aggiungi uno o più amministratori nelle unità di crittografia di destinazione ed esci dalla modalità di impronta.

Per caricare il nuovo registro della chiave master, completa le seguenti attività utilizzando il plug-in della CLI {{site.data.keyword.cloud_notm}}:

### Passo 1: crea una o più chiavi di firma
{: #step1-create-signature-keys}

Per caricare il nuovo registro della chiave master, un amministratore dell'unità di crittografia deve firmare il comando con una chiave di firma univoca. Il primo passo è di creare uno o più file delle chiavi di firma che contengono le chiavi di firma sulla tua workstation. <!-- The private part of the signature key file is used to create signatures. The public part is placed in a certificate that is installed in a target crypto unit to define a crypto unit administrator. -->

**Importante**: per motivi di sicurezza, il proprietario della chiave di firma può essere una persona diversa dai proprietari delle parti della chiave master. Il proprietario della chiave di firma deve essere l'unica persona a conoscere la password associata al file delle chiavi di firma.

* Per visualizzare le chiavi di firma esistenti sulla workstation, utilizza il seguente comando:
  ```
  ibmcloud tke sigkeys
  ```
  {: pre}

* Per creare e salvare una nuova chiave di firma sulla workstation, utilizza il seguente comando:
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  Quando richiesto, immetti un nome amministratore e una password per proteggere il file delle chiavi di firma. Devi ricordare la password. Se la password viene persa, non è possibile utilizzare la chiave di firma.

* Per selezionare l'amministratore per la firma di futuri comandi, utilizza il comando:
  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  Viene visualizzato un elenco di file delle chiavi di firma trovati sulla workstation. Quando richiesto, immetti il numero chiave del file delle chiavi di firma da selezionare per la firma dei successivi comandi di gestione. <!--If a signature key file is already selected for signing administrative commands, this is indicated when the list of signature key files is displayed. -->

  <!-- **Tip**: Before you run the `cryptounit-exit-impr` command to exit imprint mode, the command needs to be signed by a crypto unit administrator using the signature key. After the crypto unit exits imprint mode, all commands to the crypto unit must be signed. -->

### Passo 2: aggiungi uno o più amministratori nell'unità di crittografia di destinazione
{: #step2-load-admin}

<!-- After a crypto unit exits imprint mode, all administrative commands sent to the crypto unit must be signed by an administrator that is added to the crypto unit. -->

* Per visualizzare gli amministratori esistenti per un'unità di crittografia, utilizza il seguente comando:
  ```
  ibmcloud tke cryptounit-admins
  ```
  {: pre}

* Per aggiungere un nuovo amministratore, utilizza il seguente comando:
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  Viene visualizzato un elenco dei file delle chiavi di firma trovati sulla workstation.

  Quando richiesto, seleziona il file delle chiavi di firma associato all'amministratore dell'unità di crittografia che deve essere aggiunto. Quindi, immetti la password per il file delle chiavi di firma selezionato.

  Se necessario, puoi ripetere il comando per aggiungere ulteriori amministratori dell'unità di crittografia. Qualsiasi amministratore può eseguire in modo indipendente i comandi nell'unità di crittografia.

  Nella modalità di impronta, non è necessario firmare il comando per aggiungere un amministratore dell'unità di crittografia. Dopo aver lasciato la modalità di impronta, per aggiungere degli amministratori dell'unità di crittografia, il comando da utilizzare deve essere firmato da un amministratore dell'unità di crittografia che è stato già aggiunto nell'unità di crittografia.

### Passo 3: esci dalla modalità di impronta nell'unità di crittografia di destinazione
{: #step3-exit-imprint-mode}

Un'unità di crittografia in modalità di impronta non è considerata sicura. In modalità di impronta, non puoi eseguire la maggior parte dei comandi di gestione, come il caricamento del nuovo registro della chiave master.

Dopo aver aggiunto uno o più amministratori dell'unità di crittografia, esci dalla modalità di impronta utilizzando il comando:

  ```
  ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

  **Importante:** il comando per uscire dalla modalità di impronta deve essere firmato da uno degli amministratori dell'unità di crittografia aggiunti utilizzando la chiave di firma. Dopo che l'unità di crittografia ha lasciato la modalità di impronta, tutti i comandi per l'unità di crittografia devono essere firmati.

### Passo 4: crea una serie di parti della chiave master da utilizzare
{: #step4-create-master-key}

Ogni parte della chiave master viene salvata in un file protetto da password sulla workstation.

**Importante**: devi creare almeno due parti della chiave master. Per motivi di sicurezza, è possibile utilizzare tre parti della chiave master e ciascuna parte può essere posseduta da una persona diversa. Il proprietario della parte della chiave deve essere l'unica persona a conoscere la password associata al file delle parti della chiave.

* Per visualizzare le parti della chiave master esistenti sulla workstation, utilizza il seguente comando:
  ```
  ibmcloud tke mks
  ```
  {: pre}

* Per creare e salvare una parte della chiave master casuale sulla workstation, utilizza il comando:
  ```
  ibmcloud tke mk-add --random
  ```
  {: pre}

  Quando richiesto, immetti una descrizione per la parte della chiave e una password per proteggere il file delle parti della chiave. Devi ricordare la password. Se la password viene persa, non puoi utilizzare la parte della chiave.

* Per immettere un valore di parte della chiave noto e salvarlo in un file sulla workstation, utilizza il seguente comando:
  ```
  ibmcloud tke mk-add --value
  ```
  {: pre}

  Quando richiesto, immetti il valore di parte della chiave come stringa esadecimale per la parte della chiave a 32 byte. Quindi, immetti una descrizione per la parte della chiave e una password per proteggere il file delle parti della chiave.

### Passo 5: carica il nuovo registro della chiave master
{: #step5-load-master-key}

**Importante**: per caricare un registro della chiave master, tutti i file delle parti della chiave master e il file delle chiavi di firma devono essere presenti su una workstation comune. Se i file sono stati creati su workstation separate, assicurati che i nomi file siano diversi per evitare conflitti. I proprietari dei file delle parti della chiave master e il proprietario del file delle chiavi di firma, devono immettere le password del file quando il registro della chiave master viene caricato sulla workstation comune.

Per informazioni su come viene caricata la chiave master, vedi le illustrazioni dettagliate in [Registri della chiave master](/docs/services/hs-crypto/service_instance_concepts.html#introduce-key-registers).

Per caricare il nuovo registro della chiave master, utilizza il seguente comando:
```
ibmcloud tke cryptounit-mk-load
```
{: pre}

Viene visualizzato un elenco di parti della chiave master trovate sulla workstation.

Quando richiesto, immetti le parti della chiave da caricare nel nuovo registro della chiave master. Quindi, immetti la password per ogni file delle parti della chiave selezionato.

### Passo 6: esegui il commit del nuovo registro della chiave master
{: #step6-commit-master-key}

Il caricamento del nuovo registro della chiave master colloca il nuovo registro nello stato full uncommitted. Prima di poter utilizzare il nuovo registro della chiave master per inizializzare o ricodificare l'archiviazione chiavi, colloca il nuovo registro della chiave master nello stato committed. Per informazioni su come viene caricata la chiave master, vedi le illustrazioni dettagliate in [Registri della chiave master](/docs/services/hs-crypto/service_instance_concepts.html#introduce-key-registers).

Per eseguire il commit del nuovo registro della chiave master, utilizza il seguente comando:
```
ibmcloud tke cryptounit-mk-commit
```
{: pre}

### Passo 7: attiva la chiave master
{: #step7-activate-master-key}

Attiva la chiave master spostandola nel registro della chiave master corrente utilizzando il seguente comando:

```
ibmcloud tke cryptounit-mk-setimm
```
{: pre}

## Operazioni successive
{: #initialize-crypto-next}

Vai alla scheda **Manage** del tuo dashboard {{site.data.keyword.hscrypto}} gestito per gestire le chiavi root e standard.

Per ulteriori dettagli sulle altre opzioni dei comandi del plugin Trusted Key Entry, immetti il seguente comando nella CLI:

```
ibmcloud tke help
```
{: pre}

<!--
## Reference: Other Trusted Key Entry plug-in commands
{: #initialize-crypto-reference}

The following list describes the remaining commands implemented by the plug-in and discusses when they would be used.

* **ibmcloud tke mk-rm**

  This command removes a file that contains a master key part from the workstation.

  After you enter the command, a list of master key parts that are found on the workstation is displayed. When prompted, enter the key number of the key part that is to be removed.

  After a key part is removed from the local workstation, it can no longer be used.

* **ibmcloud tke sigkey-rm**

  This command removes a file that contains a signature key from the workstation.

  After you enter the command, a list of signature keys found on the workstation is displayed. When prompted, enter the key number of the signature key file that is to be removed.

  Be cautious of removing a signature key from the workstation. If any crypto units that are assigned to the user account exit imprint mode, and if the signature key being removed from the workstation is the only added administrator for the crypto unit, executing new administrative functions in the crypto unit is not possible after you remove the signature key. If no backup of the signature key file exists, the only way for recovery is to contact {{site.data.keyword.cloud_notm}} support to clear the crypto unit and place it in imprint mode.

* **ibmcloud tke cryptounit-admin-rm**

  This command removes an administrator from the selected crypto units.

  When this command is issued for a crypto unit in imprint mode, this command does not need to be signed. After the crypto unit exits imprint mode, this command must be signed by an existing crypto unit administrator.

  For a crypto unit not in imprint mode, the command fails if the administrator being removed is the last administrator defined for the crypto unit.


* **ibmcloud tke cryptounit-zeroize**

  This command clears the selected crypto units and places them back in imprint mode.  All crypto unit administrators are removed, and the new and current master key registers are cleared.

  When this command is issued for a crypto unit in imprint mode, this command does not need to be signed. After the crypto unit exits imprint mode, this command must be signed by an existing crypto unit administrator.

  When this command is issued to a group of crypto units, the current signature key must be recognized as a crypto unit administrator by all crypto units not in imprint mode in order for the command to be accepted.


* **ibmcloud tke cryptounit-mk**

  This command displays the status and verification pattern for the new and current master key registers for the selected crypto units.

* **ibmcloud tke cryptounit-mk-clrcur**

  This command clears the current master key register in the selected crypto units.

  This command cannot be executed in imprint mode.

  Clearing the current master key register makes any key storage protected by the current master key unusable.

* **ibmcloud tke cryptounit-mk-clrnew**

  This command clears the new master key register in the selected crypto units.

  This command cannot be executed in imprint mode.

* **ibmcloud tke cryptounit-mk-setimm**

  This command moves the value of the new master key register to the current master key register, and clears the new master key register in the selected crypto units.

  This command cannot be executed in imprint mode.

  This command does not initialize or re-encipher key storage and should be used only when key storage in the target LPARs is prepared to accept the new master key value. If in doubt, do not use this command, because it can cause keys in existing key storage to become unusable.

The following is a full list of plug-in commands. You can also find the commands by using the plug-in help function:
```
NAME:
   ibmcloud tke - A CLI plug-in to manage crypto module cryptounits in the IBM Cloud
USAGE:
   ibmcloud tke command [arguments...] [command options]

COMMANDS:
   mks                Lists master key parts stored on this workstation.
   mk-add             Creates and saves a new master key part.
   mk-rm              Removes a master key part from this workstation.
   sigkeys            Lists the signature keys stored on this workstation.
   sigkey-add         Generates and saves a new signature key.
   sigkey-rm          Removes a signature key from this workstation.
   sigkey-sel         Selects the signature key to use to sign commands.
   cryptounits            Displays the cryptounits for the current resource group.
   cryptounit-add         Adds cryptounits to the set of cryptounits to work with.
   cryptounit-rm          Removes cryptounits from the set of cryptounits to work with.
   cryptounit-admins      Lists administrators added in the selected cryptounits.
   cryptounit-admin-add   Add a cryptounit administrator to the selected cryptounits.
   cryptounit-admin-rm    Removes a cryptounit administrator from the selected cryptounits.
   cryptounit-compare     Compares configuration settings of the selected cryptounits.
   cryptounit-exit-impr   Exits imprint mode in the selected cryptounits.
   cryptounit-zeroize     Zeroizes the selected cryptounits.
   cryptounit-mk          Displays master key registers for the selected cryptounits.
   cryptounit-mk-clrcur   Clears the current master key register.
   cryptounit-mk-clrnew   Clears the new master key register.
   cryptounit-mk-commit   Commits the new master key register.
   cryptounit-mk-setimm   Does set immediate on the master key registers.
   cryptounit-mk-load     Loads the new master key register.
   help, h            Show help
   ```
-->
