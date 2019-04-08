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

# Introdução à inicialização da instância de serviço
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> Este tutorial mostra a você como inicializar a instância de serviço carregando as chaves mestras para proteger o seu armazenamento de chave com o plug-in Trusted Key Entry. Após você inicializar a instância de serviço, será possível iniciar o gerenciamento de suas chaves raiz.   
{:shortdesc}

## Pré-requisito
{: #get-started-hsm-prerequisite}

Antes de iniciar, execute as etapas a seguir:

1. Provisione a instância do {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} (instância de serviço para abreviação). Para obter as etapas detalhadas, consulte  [ Fornecimento  {{site.data.keyword.hscrypto}} ](/docs/services/hs-crypto/provision.html).

2. Execute o comando a seguir para certificar-se de estar com login efetuado no terminal de API correto:

  ```
  Ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

3. Instale o plug-in Trusted Key Entry mais recente por meio da interface da linha de comandos (CLI) do {{site.data.keyword.cloud_notm}} com o comando a seguir:

  ```
  Ibmcloud plugin install tke
  ```
  {: pre}

  Para instalar o plug-in da CLI, consulte [Introdução à CLI do {{site.data.keyword.cloud_notm}}](/docs/cli/index.html).
  {: tip}

4. Configure a variável de ambiente CLOUDTKEFILES para indicar o subdiretório no qual deseja armazenar as partes da chave e as chaves de assinatura

##  Etapa 1: Criar as partes de chave mestra e os arquivos-chave de assinatura
{: #hsm-step1}

1. Crie uma parte de chave mestra aleatória ou uma parte de chave mestra com um valor conhecido.

  * Para criar uma parte de chave mestra aleatória, use o comando a seguir:

    ```
    ibmcloud tke mk-add -- random
    ```
    {: pre}

    Quando solicitado, insira uma descrição para a parte de chave e uma senha para o arquivo de parte de chave.

  * Para criar uma parte de chave mestra com um valor conhecido, use o comando a seguir:

    ```
    ibmcloud tke mk-add -- value
    ```
    {: pre}

    Quando solicitado, insira o valor da parte de chave conhecida como uma sequência hexadecimal e, em seguida, insira uma descrição e uma senha para o arquivo de parte de chave.

  Repita o comando para criar partes de chave adicionais.

2. Crie uma chave de assinatura com o comando a seguir:
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  Quando solicitado, insira um nome de administrador e uma senha para o arquivo-chave de assinatura.

## Etapa 2: Selecionar as unidades de criptografia com as quais você deseja trabalhar
{: #hsm-step2}

Todas as unidades de criptografia em uma instância de serviço devem ser configuradas da mesma forma.

1. É possível exibir as instâncias de serviço e as unidades de criptografia designadas para a sua conta do IBM Cloud usando o comando a seguir:

  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

2. Para selecionar unidades de criptografia adicionais com as quais trabalhar, use o comando:

  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  Quando solicitado, insira as unidades de criptografia adicionais com as quais trabalhar.

3. Para remover unidades de criptografia do conjunto com o qual você trabalhará, use o comando:

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  Quando solicitado, insira as unidades de criptografia que você deseja remover.

## Etapa 3: Incluir administradores de unidade de criptografia e sair do modo de impressão
{: #hsm-step3}

Antes de poder carregar as chaves mestras em uma unidade de criptografia, deve-se criar um ou mais administradores de unidade de criptografia e sair do modo de impressão.

1. Carregue um administrador de unidade de criptografia. Para criar um administrador de unidade criptográfica, use o comando:
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  Quando solicitado, insira o KEYNUM da chave de assinatura a ser usada para o administrador e a senha para o arquivo-chave de assinatura.

2. Selecione a chave de assinatura a ser usada para assinar comandos usando o comando:

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  Quando solicitado, insira o KEYNUM da chave de assinatura a ser usada para assinar comandos.

  Esse deve ser o mesmo que uma das chaves de assinatura usadas para carregar um administrador de unidade de criptografia na etapa 3.1.
  {: tip}

3. Saia do modo de impressão usando o comando a seguir:

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

Após você carregar um administrador de unidade de criptografia e sair do modo de impressão, será possível verificar o estado de suas unidades de criptografia usando o comando:
{: tip}

```
 ibmcloud tke cryptounit-compare
```
{: pre}

## Etapa 4: Carregar o registro de chave mestra
{: #hsm-step4}

Para carregar o registro de chave mestra, um ou mais administradores de unidade de criptografia devem ser definidos e a unidade de criptografia deve ter saído do modo de impressão.

1. Carregue o novo registro de chave mestra usando o comando a seguir:

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  Quando solicitado, insira o KEYNUM das partes de chave a serem carregadas, a senha para o arquivo-chave de assinatura e as senhas para cada parte de chave selecionada.

2. Confirme o novo registro de chave mestra com o comando a seguir:

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  Quando solicitado, insira a senha para o arquivo-chave de assinatura.

3. Mova a chave mestra para o registro de chave mestra atual com o comando a seguir:

  ```
  ibmcloud tke cryptounit-mk-setimm
  ```
  {: pre}

  Quando solicitado, insira a senha para o arquivo-chave de assinatura.

## O que vem a seguir
{: #hsm-next}

Agora é possível começar a usar a sua instância de serviço. Para obter detalhes sobre a implementação do procedimento em um ambiente de produção, consulte [Inicializando instâncias de serviço para proteger o armazenamento de chave](/docs/services/hs-crypto/initialize_hsm.html).
