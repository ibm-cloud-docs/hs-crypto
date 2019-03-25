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

# Configurando a CLI
{: #set-up-cli}

O {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} é integrado ao plug-in da CLI do {{site.data.keyword.keymanagementservicelong_notm}} para que seja possível usar o plug-in da CLI do {{site.data.keyword.keymanagementservicelong_notm}} para criar, importar e gerenciar chaves raiz de criptografia e chaves padrão.

- Para saber mais sobre como usar a CLI, verifique o [doc de referência da CLI do {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/cli-reference.html).
- Para saber mais sobre como acessar a CLI, verifique [Configurando a CLI do {{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect/set-up-cli.html).

Antes de ser possível usar o plug-in da CLI do {{site.data.keyword.keymanagementserviceshort}} em uma instância do {{site.data.keyword.hscrypto}}, execute o comando a seguir primeiro:

```
export KP_PRIVATE_ADDR=<URL>
```
{: pre}

Nesse comando, a *URL* é o terminal exibido na página **Gerenciar** da interface com o usuário. Ou é possível recuperar a URL do terminal por meio da API. Por exemplo:

```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com: < port> "
```
{: pre}

Para obter detalhes, [verifique o doc de referência da API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
