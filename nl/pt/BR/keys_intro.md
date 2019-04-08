---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: root keys, master keys, standard keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# Introdução às chaves
{: #introduce-keys}

O {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} suporta vários tipos de chave, incluindo chaves raiz, chaves padrão e chaves mestras.
{:shortdesc}

## Chaves raiz
{: #introduce-root-keys}

*Chaves raiz* são chaves simétricas de agrupamento de chaves que você gerencia totalmente no {{site.data.keyword.hscrypto}}. É possível usar uma chave raiz para proteger outras chaves criptográficas com criptografia avançada. Para saber mais, consulte  <a href="/docs/services/key-protect/concepts/envelope-encryption.html"> Criptografia de Envelope </a>.

É possível gerenciar chaves raiz seguindo as etapas em [Gerenciar suas chaves](/docs/services/hs-crypto/index.html#manage-keys).

## Chaves padrão
{: #introduce-standard-keys}

*Chaves padrão* são chaves simétricas usadas para criptografia. É possível usar uma chave padrão para criptografar e decriptografar dados diretamente.

É possível gerenciar chaves padrão seguindo as etapas em [Gerenciar suas chaves](/docs/services/hs-crypto/index.html#manage-keys).

## Chaves mestras
{: #introduce-master-keys}

*Chaves mestras* são usadas para criptografar a instância de serviço para armazenamento de chave. Com a chave mestra, você possui a raiz de confiança que criptografa a cadeia inteira de chaves, incluindo chaves raiz e chaves padrão.

Por causa do canal seguro de ponta a ponta estabelecido para a instância de serviço, apenas os administradores da instância de serviço podem configurar e gerenciar a chave mestra. Observe que a IBM não faz backup da chave mestra nem toca nela e não tem como copiá-la ou restaurá-la para uma máquina ou um data center diferente.

Uma instância de serviço pode ter apenas uma chave mestra. Se você excluir a chave mestra da instância de serviço, será possível fragmentar por criptografia efetivamente todos os dados que foram criptografados com as chaves gerenciadas no serviço.

É possível gerenciar chaves mestras ao [Inicializar instâncias de serviço para proteger o armazenamento de chave](/docs/services/hs-crypto/initialize_hsm.html).

A chave mestra rotativa não é suportada no estágio atual.
{:important}
