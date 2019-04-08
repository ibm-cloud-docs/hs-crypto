---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: IBM Cloud CLI plug-in, ibmcloud commands, IBM Cloud command-line interface

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Acessando a CLI do {{site.data.keyword.keymanagementserviceshort}} em uma instância do {{site.data.keyword.hscrypto}}
{: #set-up-cli}

O {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} é integrado ao plug-in da CLI do {{site.data.keyword.keymanagementservicelong_notm}} para que seja possível usar o plug-in da CLI do {{site.data.keyword.keymanagementservicelong_notm}} para criar, importar e gerenciar chaves raiz de criptografia e chaves padrão.

Antes de ser possível usar o plug-in da CLI do {{site.data.keyword.keymanagementserviceshort}} em uma instância do {{site.data.keyword.hscrypto}} (instância de serviço para abreviação), é necessário configurar a variável de ambiente KP_KP_PRIVATE_ADDR em sua estação de trabalho:

* No Linux ou MacOS, execute o comando a seguir:

  ```
  export KP_PRIVATE_ADDR=<URL>
  ```
  {: pre}

  Neste comando, a *URL* é o terminal que é exibido na guia **Gerenciar** de seu painel provisionado do {{site.data.keyword.hscrypto}}. Por exemplo:

  ```
  export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com: < port> "
  ```
  {: pre}

* No Windows, em **Painel de controle**, digite `environment variable` na caixa de procura para localizar a janela Variáveis de ambiente. Crie uma variável de ambiente KP_PRIVATE_ADDR e configure o valor para o terminal que é exibido na guia **Gerenciar** de seu painel provisionado do {{site.data.keyword.hscrypto}}. Por exemplo, `https://us-south.hs-crypto.cloud.ibm.com:<port>`.

Também é possível recuperar a URL de terminal por meio da API. Para obter detalhes, [verifique o doc de referência da API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

- Para saber mais sobre como usar a CLI, verifique o [doc de referência da CLI do {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/cli-reference.html).
- Para saber mais sobre como acessar a CLI, verifique [Configurando a CLI do {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/set-up-cli.html).
