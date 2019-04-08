---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-21"

Keywords: release note, new

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# O que há de novo
{: #what-new}

Fique atualizado com os novos recursos que estão disponíveis para o {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Março de 2019
{: #March-2019}

### O {{site.data.keyword.hscrypto}} está disponível para uso geral
{: #ga-201903}
Novo desde: 29/03/2019

Para obter mais informações sobre a oferta {{site.data.keyword.hscrypto}}, consulte a [página inicial do {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/hyper-protect-crypto){:new_window}.

Desde 31 de março de 2019, o fornecimento de novas instâncias do Hyper Protect Crypto Services Beta não será mais possível. As instâncias existentes terão suporte até o Término da data de suporte do beta (30 de abril de 2019).

Consulte [Migrando chaves de uma instância de serviço beta](/docs/services/hs-crypto/transition-keys.html) para obter informações sobre a migração de chaves para uma instância de serviço de produção.

### Alta disponibilidade e recuperação de desastre
{: #ha-dr-new}
Novo desde: 29/03/2019

O {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, que agora suporta três zonas de disponibilidade em uma região selecionada, é um serviço altamente disponível com recursos automáticos que ajudam a manter os seus aplicativos seguros e operacionais.

É possível criar recursos do {{site.data.keyword.hscrypto}} nas [regiões suportadas do {{site.data.keyword.cloud_notm}}](/docs/services/hs-crypto/regions.html), que representam a área geográfica na qual suas solicitações do {{site.data.keyword.hscrypto}} são manipuladas e processadas. Cada região do {{site.data.keyword.cloud_notm}} contém [múltiplas zonas de disponibilidade ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/) para atender aos requisitos de acesso local, baixa latência e segurança da região.

Para obter mais informações, consulte [Alta disponibilidade e recuperação de desastre](/docs/services/hs-crypto/ha-dr.html).

### Escalabilidade
{: #scalability-new}
Novo desde: 29/03/2019

A instância de serviço pode ser dimensionada para um máximo de seis unidades de criptografia para atender ao seu requisito de desempenho. Cada unidade de criptografia pode processar criptograficamente 5000 chaves. Em um ambiente de produção, é recomendável selecionar pelo menos duas unidades de criptografia para ativar a alta disponibilidade. Selecionando três ou mais unidades de criptografia, essas unidades criptográficas são distribuídas entre três zonas de disponibilidade na região selecionada.

Leia [Provisionando o serviço](/docs/services/hs-crypto/provision.html) para obter mais informações.

## Fevereiro de 2019
{: #Feb-2019}

### {{site.data.keyword.hscrypto}}  Beta está disponível
{: #beta-201902}
Novo a partir de: 2019-02-05

{{site.data.keyword.hscrypto}}  A versão Beta é liberada. Agora é possível acessar o serviço {{site.data.keyword.hscrypto}} por meio de **Catálogo** > **Segurança e identidade** diretamente.

A partir de 5 de fevereiro de 2019, o fornecimento de novas instâncias do Hyper Protect Crypto Services Experimental não será mais possível. As instâncias existentes terão suporte até o Fim da data de suporte experimental (5 de março de 2019).

## Dezembro de 2018
{: #Dec-2018}

### Incluído: suporte para gerenciamento do HSM com KYOK
{: #hsm-kyok}
Novo a partir de: 2018-12-19

O {{site.data.keyword.hscrypto}} agora suporta a função Keep Your Own Keys (KYOK) para que você tenha mais controle e autoridade sobre seus dados com chaves de criptografia que podem ser mantidas, controladas e gerenciadas. É possível inicializar e gerenciar a sua instância de serviço com a interface da linha de comandos (CLI) do {{site.data.keyword.cloud}}.

Para obter mais informações, consulte [Inicializando instâncias de serviço para proteger o armazenamento de chave](/docs/services/hs-crypto/initialize_hsm.html).

### Incluído: Integração da API do  {{site.data.keyword.keymanagementserviceshort}}
{: #kp-api}
Novo a partir de: 2018-12-19

A API do {{site.data.keyword.keymanagementserviceshort}} está agora integrada ao Hyper Protect Crypto Services para gerar e proteger suas chaves. É possível chamar a API do {{site.data.keyword.keymanagementserviceshort}} diretamente por meio do {{site.data.keyword.hscrypto}}.

Para obter mais informações, consulte [Acessando a API](/docs/services/hs-crypto/access-api.html) e [API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](image/external_link.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto){:new_window}.

### Descontinuado: a função de acessar o  {{site.data.keyword.hscrypto}}  por meio do ACSP
{: #deprecated-acsp}
Novo a partir de: 2018-12-19

No estágio atual, o acesso ao {{site.data.keyword.hscrypto}} por meio de um cliente Advanced Cryptography Service Provider (ACSP) está sendo descontinuado. Se você estiver usando uma instância de serviço anterior, ainda será possível usar o ACSP para explorar o {{site.data.keyword.hscrypto}}.
