---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: disaster recovery, High availability, HA, DR

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Alta disponibilidade e recuperação de desastre
{: #ha-dr}

O {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} é um serviço regional altamente disponível com recursos automáticos que ajudam a manter seus aplicativos seguros e operacionais.
{: shortdesc}

Use esta página para saber mais sobre as estratégias de disponibilidade e recuperação de desastre do {{site.data.keyword.hscrypto}}.

## Locais, arrendamento e disponibilidade
{: #availability}

O {{site.data.keyword.hscrypto}}  é um serviço regional de diversos locatários.

É possível criar recursos do {{site.data.keyword.hscrypto}} em uma das [regiões suportadas do {{site.data.keyword.cloud_notm}}](/docs/services/hs-crypto/regions.html), que representam a área geográfica na qual suas solicitações do {{site.data.keyword.hscrypto}} são manipuladas e processadas. Cada região do {{site.data.keyword.cloud_notm}} contém [múltiplas zonas de disponibilidade ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/) para atender aos requisitos de acesso local, baixa latência e segurança da região.

Ao planejar sua estratégia de criptografia em repouso com o {{site.data.keyword.cloud_notm}}, lembre-se de que o fornecimento do {{site.data.keyword.hscrypto}} em uma região mais próxima a você mais provavelmente resultará em conexões mais rápidas e mais confiáveis ao interagir com as APIs do {{site.data.keyword.hscrypto}}. Escolha uma região específica se os usuários, os apps ou os serviços que dependem de um recurso do {{site.data.keyword.hscrypto}} estiverem geograficamente concentrados. Lembre-se de que os usuários e os serviços muito distantes da região podem ter latência mais alta.

Suas chaves de criptografia estão limitadas à região em que foram criadas. O {{site.data.keyword.hscrypto}} não copia ou exporta chaves de criptografia para outras regiões.
{: note}

## Recuperação de desastre
{: #disaster-recovery}

O {{site.data.keyword.hscrypto}} tem recuperação de desastre regional em vigor com um Objetivo de Tempo de Recuperação (RTO) de uma hora. O serviço segue os requisitos do {{site.data.keyword.cloud_notm}} para planejamento e recuperação de eventos de desastre. Para obter mais informações, consulte  [ Recuperação de Desastre ](/docs/overview/zero_downtime.html#disaster-recovery).
