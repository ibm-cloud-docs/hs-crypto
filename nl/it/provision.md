---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-21"

Keywords: provision, instance of Hyper Protect Crypto Services

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:gif: data-image-type='gif'}

# Provisioning del servizio
{: #provision}

Puoi creare un'istanza di {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} utilizzando la console {{site.data.keyword.cloud_notm}} o la CLI {{site.data.keyword.cloud_notm}}.
{: shortdesc}

## Provisioning dalla console {{site.data.keyword.cloud_notm}}
{: #provision-gui}

Per eseguire il provisioning di un'istanza di {{site.data.keyword.hscrypto}} dalla console {{site.data.keyword.cloud_notm}}, completa la seguente procedura:

1. [Accedi al tuo account {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/){: new_window}.
2. Fai clic su **Catalogo** per visualizzare l'elenco dei sevizi disponibili in {{site.data.keyword.cloud_notm}}.
3. Dal riquadro di navigazione Tutte le categorie, fai clic sulla categoria **Sicurezza e identità**.
4. Dall'elenco di servizi, fai clic sul tile **{{site.data.keyword.hscrypto}}**.
5. **Facoltativo**: nel campo **Tag**, aggiungi delle tag per organizzare le tue risorse. Se le tue tag sono correlate alla fatturazione, considera di scriverle come coppie chiave:valore per raggruppare le tag correlate, come ad esempio `costctr:124`. Per ulteriori informazioni sulle tag, vedi [Gestione delle tag](/docs/resources?topic=resources-tag#tag).
6. In **Numero di unità di crittografia**, seleziona il numero di unità di crittografia che soddisfa i tuoi bisogni di prestazioni.

  Un'istanza del servizio supporta fino a sei unità di crittografia. In un ambiente di produzione, ti consigliamo di selezionare almeno due unità di crittografia per abilitare l'elevata disponibilità. Se selezioni tre o più unità di crittografia, vengono distribuite insieme a tre zone di disponibilità supportate nella regione selezionata.
  {: important}
7. Fai clic su **Crea** per eseguire il provisioning di un'istanza di {{site.data.keyword.hscrypto}} nell'account, regione e gruppo di risorse in cui hai eseguito l'accesso.

![Provisioning del servizio](image/provisioning.gif "Provisioning del servizio")
{: gif}

*Figura 1. Provisioning del servizio*

<!-- ## Provisioning from the {{site.data.keyword.cloud_notm}} CLI
{: #provision-cli}

To provision an instance of {{site.data.keyword.hscrypto}} using the {{site.data.keyword.cloud_notm}} CLI, complete the following steps:

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview){: new_window} with the following command:

    ```sh
    curl -sl https://ibm.biz/idt-installer | bash
    ```
    {: pre}

    **Notes:** For more information about the {{site.data.keyword.cloud_notm}} CLI, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview){: new_window}.

2. Log in to {{site.data.keyword.cloud_notm}} through the {{site.data.keyword.cloud_notm}} CLI with the following command:

    ```sh
    ibmcloud login
    ```
    {: pre}

    **Notes:** If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode. -->

<!-- ### Creating a service instance within your account
{: #provision-acct-lvl}

To simplify access to your encryption keys with [{{site.data.keyword.iamlong}} roles](/docs/iam/users_roles.html#iamusermanrol), you can create one or more instances of the {{site.data.keyword.hscrypto}} service within an account, without needing to specify an org and space.

1. Log in to {{site.data.keyword.cloud_notm}} through the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview){: new_window}.

    ```sh
    ibmcloud login
    ```
    {: pre}
    **Notes:** If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the account, region, and resource group where you would like to create a {{site.data.keyword.hscrypto}} service instance.

    You can use the following command to set your target region and resource group.

    ```sh
    ibmcloud target -r <region_name> -g <resource_group_name>
    ```
    {: pre}

3. Provision an instance of {{site.data.keyword.hscrypto}} within that account and resource group.

    ```sh
    ibmcloud resource service-instance-create <instance_name> kms tiered-pricing
    ```
    {: pre}

    Replace `<instance_name>` with a unique alias for your service instance.

4. Optional: Verify that the service instance was created successfully.

    ```sh
    ibmcloud resource service-instances
    ```
    {: pre}

### Creating a service instance within an org and space
{: #provision-space-lvl}

To manage access to your encryption keys with [Cloud Foundry roles](/docs/iam/cfaccess.html), you can create an instance of the {{site.data.keyword.hscrypto}} service within a specified organization and space.  

1. Log in to {{site.data.keyword.cloud_notm}} through the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview){: new_window}.

    ```sh
    ibmcloud login
    ```
    {: pre}
    **Note:** If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the account, region, organization, and space where you would like to create a {{site.data.keyword.hscrypto}} service instance.

    You can use the following command to set your target region, org, and space.

    ```sh
    ibmcloud target -r <region> -o <organization_name> -s <space_name>
    ```
    {: pre}

3. Provision an instance of {{site.data.keyword.hscrypto}} within that account, region, organization, and space.

    ```sh
    ibmcloud service create kms tiered-pricing <instance_name>
    ```
    {: pre}

    Replace `<instance_name>` with a unique alias for your service instance.

4. Optional: Verify that the service instance was created successfully.

    ```sh
    ibmcloud service list
    ```
    {: pre}
-->

### Operazioni successive
{: #provision-next}

Per ulteriori informazioni sulla gestione a livello programmatico delle tue chiavi, [consulta la documentazione di riferimento API di {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
