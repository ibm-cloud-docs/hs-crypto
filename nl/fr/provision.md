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

# Mise à disposition du service
{: #provision}

Vous pouvez créer une instance de {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} à l'aide de la console {{site.data.keyword.cloud_notm}} ou de l'interface de ligne de commande {{site.data.keyword.cloud_notm}}.
{: shortdesc}

## Mise à disposition à partir de la console {{site.data.keyword.cloud_notm}}
{: #provision-gui}

Pour mettre à disposition une instance de {{site.data.keyword.hscrypto}} à partir de la console {{site.data.keyword.cloud_notm}}, effectuez les étapes suivantes :

1. [Connectez-vous à votre compte {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/){: new_window}.
2. Cliquez sur **Catalogue** pour afficher la liste des services disponibles sur {{site.data.keyword.cloud_notm}}.
3. Dans le panneau de navigation Toutes les catégories, cliquez sur la catégorie **Sécurité et identité**.
4. Dans la liste de services, cliquez sur la vignette **{{site.data.keyword.hscrypto}}**.
5. **Facultatif** : dans la zone **Etiquettes**, ajoutez des étiquettes pour organiser vos ressources. Si vos étiquettes sont liées à la facturation, pensez à les écrire sous la forme de paires clé:valeur pour regrouper les étiquettes associées, comme `costctr:124`. Pour plus d'informations sur les étiquettes, voir [Utilisation d'étiquettes](/docs/resources?topic=resources-tag#tag).
6. Sous la rubrique relative au **nombre d'unités crypto**, sélectionnez le nombre d'unités crypto répondant à vos besoins de performance.

  Une instance de service prend en charge jusqu'à six unités crypto. Dans un environnement de production, il est conseillé de sélectionner au moins deux unités crypto pour activer la haute disponibilité. Si vous sélectionnez trois unités crypto ou plus, ces unités sont réparties dans les trois zones de disponibilité prises en charge dans la région sélectionnée.{: important}
7. Cliquez sur **Créer** pour mettre à disposition une instance d'{{site.data.keyword.hscrypto}} dans le compte, la région ou le groupe de ressources dans lequel vous êtes connecté.

![Mise à disposition du service](image/provisioning.gif "Mise à disposition du service")
{: gif}

*Figure 1. Mise à disposition du service*

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

### Etapes suivantes
{: #provision-next}

Pour plus d'informations sur la gestion de vos clés à l'aide d'un programme, [voir la documentation de référence de l'API {{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
