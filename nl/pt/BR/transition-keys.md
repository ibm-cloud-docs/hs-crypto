---

copyright:
years: 2018, 2019
lastupdated: "2019-03-26"

Keywords: root keys, standard keys, migration, transition, beta

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Migrando chaves de uma instância de serviço beta
{: #migrate-keys}

Se você estava usando uma instância de serviço beta e deseja migrar as chaves raiz e as chaves padrão que você gerenciou para uma instância de serviço de produção do {{site.data.keyword.hscrypto}}, aqui está o procedimento que você precisará seguir.
{: shortdesc}

Os administradores do IBM Cloud não podem migrar as chaves mestras porque as chaves mestras não são extraíveis da unidade de criptografia. É necessário inicializar a instância de serviço de produção com a sua chave mestra.
{:important}  

## Antes de iniciar
{: #migrate-prerequisites}

1. [Crie uma instância de serviço](/docs/services/hs-crypto/provision.html) com o Hyper Protect Crypto Services Plan.

2. [Inicialize a instância de serviço](/docs/services/hs-crypto/initialize_hsm.html) com o plug-in Trusted Key Entry.

## Migrando chaves
{: #migrate-keys-steps}  

Conclua as etapas a seguir para migrar chaves raiz e chaves padrão para o ambiente de produção.

1. [Importe chaves raiz](/docs/services/hs-crypto/import-root-keys.html) por meio da GUI ou da API.

  É possível migrar as chaves raiz importadas da instância de serviço beta para a instância de serviço de produção.
  {:tip}

2. Desagrupe as chaves de criptografia de dados (DEKs) da instância de serviço beta e agrupe as DEKs na instância de serviço de produção:

  1. [Desagrupe as chaves de criptografia de dados (DEKs)](/docs/services/hs-crypto/unwrap-keys.html) da instância de serviço beta com a API [invoke-an-action-on-a-key ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: new_window}.

  2. [Agrupe as DEKs](/docs/services/hs-crypto/wrap-keys.html) na instância de serviço de produção com a API [invoke-an-action-on-a-key ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key{: new_window}).

3. Recrie chaves padrão seguindo estas etapas:

  1. [Recupere chaves padrão](/docs/services/hs-crypto?topic=hs-crypto-view-keys#retrieve-key-api) com a API [retrieve-key-by-id ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto#retrieve-a-key-by-id){: new_window}. Isso retorna a carga útil usada para criar a chave na instância Beta.

  2. [Crie chaves padrão](/docs/services/hs-crypto/create-standard-keys.html) na nova instância de serviço com as informações recuperadas na etapa anterior por meio da GUI ou da API [create-a-new-key ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto#create-a-new-key){: new_window}.

## O que vem a seguir
{: #migration-next}

Para descobrir mais sobre como gerenciar programaticamente as suas chaves, [verifique o doc de referência da API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
