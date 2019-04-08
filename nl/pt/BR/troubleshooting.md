---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: troubleshoot, problems, known issues

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}

# Detectando Problemas
{: #troubleshooting}

Problemas gerais com o uso do {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} podem incluir o fornecimento de cabeçalhos ou credenciais corretos quando você interage com a API. Em muitos casos, é possível recuperar-se desses problemas seguindo algumas etapas simples.
{: shortdesc}

## Ocorreu um erro ao excluir uma instância de serviço inicializada
{: #troubleshoot-delete-instance}

É possível receber um erro semelhante ao seguinte ao excluir uma instância de serviço inicializada:

```
FAILED Resposta do erro do servidor. Status code: 400; description: 400 DELETE https://zCryptoBroker.mybluemix.net/v2/service_instances/ failed with error status 409. Conflito.
```
{: codeblock}
{: tsSymptoms}

Você não limpou (zerou) a instância de serviço inicializada antes de excluir a instância.
{: tsCauses}

Execute o comando a seguir antes de excluir a instância:
{: tsResolve}

```
ibmcloud tke domain-zeroize
```
{: codeblock}

## Token não autorizado depois de executar comandos relacionados ao plug-in Trusted Key Entry
{: #troubleshoot-unauthorized-token}

É possível receber mensagens semelhantes às seguintes depois de executar comandos da CLI `tke`:

```
ibmcloud tke domains
FAILED
Error querying crypto instances.
Status code: 401
Message: Unauthorized
Your access token is invalid, expired, or does not have the necessary permissions to access this instance.`
```
{: codeblock}
{: tsSymptoms}

O token não é atualizado.
{: tsCauses}

Efetue login no {{site.data.keyword.cloud_notm}} novamente com o comando `ibmcloud login` para atualizar o token.
{: tsResolve}

## Obtido o erro `CKR_IBM_WK_NOT_INITIALIZED` ao usar a CLI ou a API
{: #troubleshoot-error-CLI-API}

Ao usar a CLI ou a API, é possível obter uma mensagem de erro semelhante à seguinte:

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

Quando você executou o comando `ibmcloud tke domain-compare`, não obteve uma confirmação `Valid` no CURRENT MASTER KEY REGISTER.
{: tsCauses}

Certifique-se de que a chave mestra do HSM tenha sido configurada corretamente.
{: tsResolve}

## Não é possível criar ou excluir chaves
{: #unable-to-create-keys}

Ao acessar a interface com o usuário do {{site.data.keyword.hscrypto}}, você não vê as opções para incluir ou excluir chaves.

No painel do {{site.data.keyword.cloud_notm}}, selecione sua instância do serviço {{site.data.keyword.hscrypto}}.
{: tsSymptoms}

É possível ver uma lista de chaves, mas opções para incluir ou excluir chaves não são exibidas.

Você não tem a autorização correta para executar ações do {{site.data.keyword.hscrypto}}.
{: tsCauses}

Verifique com o seu administrador se você está designado com a função correta no grupo de recursos aplicável ou na instância de serviço. Para obter mais informações sobre funções, veja [Funções e permissões](/docs/services/key-protect/manage-access.html#roles).
{: tsResolve}

## Obtendo ajuda e suporte
{: #getting-help}

Se você tiver problemas ou perguntas quando estiver usando o {{site.data.keyword.hscrypto}}, poderá verificar o {{site.data.keyword.cloud_notm}} ou obter ajuda procurando informações ou fazendo perguntas por meio de um fórum. Também é possível abrir um chamado de suporte.
{: shortdesc}

É possível verificar se o {{site.data.keyword.cloud_notm}} está disponível acessando a [página de status ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/status?tags=platform,runtimes,services).

Você pode revisar os fóruns para ver se outros usuários tiveram o mesmo problema. Quando estiver usando os fóruns para fazer uma pergunta, identifique sua pergunta para que ela seja vista pela equipe de desenvolvimento do {{site.data.keyword.cloud_notm}}.

- Se você tiver perguntas técnicas sobre o {{site.data.keyword.hscrypto}}, poste a sua pergunta no [Stack Overflow ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://stackoverflow.com/questions/tagged/hyper-protect-crypto){: new_window} e identifique a sua pergunta com "ibm-cloud" e "hyper-protect-crypto".
- Para perguntas sobre o serviço e instruções de introdução, use o fórum [IBM developerWorks dW Answers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/answers/topics/hyper-protect-crypto/){: new_window}. Inclua as identificações "ibm-cloud" e "hyper-protect-crypto".

Consulte [Obtendo ajuda![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/get-support?topic=get-support-using-avatar#using-avatar){: new_window} para obter mais detalhes sobre o uso dos fóruns.

Para obter mais informações sobre como abrir um chamado de suporte do {{site.data.keyword.IBM_notm}} ou sobre níveis de suporte e severidades de chamado, veja [Entrando em contato com o suporte ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/get-support?topic=get-support-getting-customer-support){: new_window}.
