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

# Fornecendo o serviço
{: #provision}

É possível criar uma instância de {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} usando o console do {{site.data.keyword.cloud_notm}} ou a CLI do {{site.data.keyword.cloud_notm}}.
{: shortdesc}

## Provisionando por meio do console do {{site.data.keyword.cloud_notm}}
{: #provision-gui}

Para provisionar uma instância do {{site.data.keyword.hscrypto}} por meio do console do {{site.data.keyword.cloud_notm}}, conclua as etapas a seguir:

1. [Efetue login na conta do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/){: new_window}.
2. Clique em **Catálogo** para visualizar a lista de serviços que estão disponíveis no {{site.data.keyword.cloud_notm}}.
3. Na área de janela de navegação Todas as categorias, clique na categoria **Segurança e identidade**.
4. Na lista de serviços, clique no azulejo **{{site.data.keyword.hscrypto}}**.
5. **Opcional**: no campo **Tags**, inclua tags para organizar os seus recursos. Se as suas tags estiverem relacionadas ao faturamento, considere escrever tags como pares de chave:valor para ajudar a agrupar tags relacionadas, como `costctr:124`. Para obter mais informações sobre tags, consulte [Trabalhando com tags](/docs/resources?topic=resources-tag#tag).
6. Sob **Número de unidades de criptografia**, selecione o número de unidades de criptografia que atenda às suas necessidades de desempenho.

  Uma instância de serviço suporta até seis unidades de criptografia. Em um ambiente de produção, é recomendável selecionar pelo menos duas unidades de criptografia para ativar a alta disponibilidade. Se você selecionar três ou mais unidades de criptografia, essas unidades de criptografia serão distribuídas entre três zonas de disponibilidade suportadas na região selecionada. {: important}
7. Clique em **Criar** para provisionar uma instância do {{site.data.keyword.hscrypto}} na conta, na região e no grupo de recursos em que você efetuou login.

![Fornecendo o serviço](image/provisioning.gif "Fornecendo o serviço")
{: gif}

*Figura 1. Fornecendo o serviço*

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

### O que vem a seguir
{: #provision-next}

Descubra mais sobre como gerenciar programaticamente as suas chaves, [verifique o doc de referência da API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
