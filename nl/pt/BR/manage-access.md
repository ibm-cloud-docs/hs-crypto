---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

Keywords: user access, Cloud IAM roles, encryption keys

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gerenciando o acesso de usuário
{: #manage-access}

O {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} suporta um sistema de controle de acesso centralizado, governado pelo {{site.data.keyword.iamlong}}, para ajudar a gerenciar usuários e o acesso às suas chaves de criptografia.
{: shortdesc}

Uma boa prática é conceder permissões de acesso à medida que você convida novos usuários à sua conta ou serviço. Por exemplo, considere as diretrizes a seguir:

- **Ative o acesso de usuário aos recursos em sua conta designando funções do Cloud IAM.**
    Em vez de compartilhar suas credenciais de administrador, crie novas políticas para os usuários que precisam de acesso às chaves de criptografia em sua conta. Se você for o administrador para sua conta, você será automaticamente designado a uma política de _Gerenciador_
com acesso a todos os recursos sob a conta.
- **Conceda funções e permissões no menor escopo necessário.**
    Por exemplo, se um usuário precisar acessar apenas uma visualização de alto nível de chaves dentro de um espaço especificado, conceda a função _Leitor_ ao usuário para esse espaço.
- **Audite regularmente quem pode gerenciar o controle de acesso e exclua recursos de chave.**
    Lembre-se de que ao conceder uma função de _Gerenciador_ a um usuário ele poderá modificar políticas de serviço para outros usuários, além de destruir recursos.

## Funções e permissões
{: #roles}

Com o {{site.data.keyword.iamshort}} (IAM), é possível gerenciar e definir o acesso para usuários e recursos em sua conta.

Para simplificar o acesso, o {{site.data.keyword.hscrypto}} se alinha com as funções do Cloud IAM para
que cada usuário tenha uma visualização diferente do serviço, de acordo com a função designada ao usuário. Se você for um
administrador de segurança para o seu serviço, poderá designar funções do Cloud IAM que correspondam às permissões específicas do
{{site.data.keyword.hscrypto}} que desejar conceder a membros da sua equipe.

A tabela a seguir mostra como as funções de identidade e acesso são mapeadas para as permissões do {{site.data.keyword.hscrypto}}:
<table>
  <tr>
    <th>Função de acesso de serviço</th>
    <th>Descrição</th>
    <th>Ações</th>
  </tr>
  <tr>
    <td><p>Leitor</p></td>
    <td><p>Um leitor pode procurar uma visualização de alto nível de chaves e executar ações de agrupamento e de desagrupamento. Leitores não podem acessar ou modificar o material de chave.</p></td>
    <td>
      <p>
        <ul>
          <li>Visualizar chaves</li>
          <li>Quebrar chaves</li>
          <li>Desagrupar chaves</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Gravador</p></td>
    <td><p>Um escritor pode criar chaves, modificar chaves e acessar o material de chave.</p></td>
    <td>
      <p>
        <ul>
          <li>Criar chaves</li>
          <li>Visualizar chaves</li>
          <li>Quebrar chaves</li>
          <li>Desagrupar chaves</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Gerente</p></td>
    <td><p>Um gerenciador pode executar todas as ações que um leitor e um gravador podem executar, incluindo a capacidade de excluir
chaves, convidar novos usuários e designar políticas de acesso para outros usuários.</p></td>
    <td>
      <p>
        <ul>
          <li>Todas as ações que um leitor ou um gravador pode executar</li>
          <li>Excluir chaves</li>
          <li>Designe políticas de acesso</li>
        </ul>
      </p>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Tabela 1. Descreve como as funções de identidade e acesso são mapeadas para permissões do {{site.data.keyword.hscrypto}}</caption>
</table>

<!-- **Note**: Cloud IAM user roles provide access at the service or service instance level. [Cloud Foundry roles](/docs/iam/cfaccess.html) are separate and define access at the organization or the space level. -->

Para saber mais sobre o {{site.data.keyword.iamshort}}, confira [Funções e permissões do usuário](/docs/iam/users_roles.html#userroles).

### O que vem a seguir
{: #manage-access-next}

Os proprietários e administradores de conta podem convidar usuários e configurar políticas de serviço que correspondem às ações do {{site.data.keyword.hscrypto}} que os usuários podem executar.

- Para obter mais informações sobre como designar funções de usuário na IU do {{site.data.keyword.cloud_notm}}, consulte [Gerenciando o acesso ao IAM](/docs/iam/mngiam.html).
- Para aprender sobre como conceder permissões avançadas para acessar chaves de criptografia específicas, veja [Gerenciando o acesso a chaves](/docs/services/hs-crypto/manage-access-api.html).
