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

*Chaves raiz* são chaves simétricas de agrupamento de chaves que você gerencia totalmente no {{site.data.keyword.hscrypto}}. É possível usar uma chave raiz para proteger outras chaves criptográficas com criptografia avançada. Para saber mais, consulte  <a href="/docs/services/key-protect/concepts/envelope-encryption.html"> Criptografia de Envelope </a>.

É possível gerenciar chaves raiz seguindo as etapas em [Gerenciar suas chaves](/docs/services/hs-crypto/index.html#manage-keys).

## Chaves padrão

*Chaves padrão* são chaves simétricas usadas para criptografia. É possível usar uma chave padrão para criptografar e decriptografar dados diretamente.

É possível gerenciar chaves padrão seguindo as etapas em [Gerenciar suas chaves](/docs/services/hs-crypto/index.html#manage-keys).

## Chaves mestras

*Chaves mestras* são usadas para criptografar a instância de criptografia (HSM) que processa por criptografa e gerencia chaves raiz e chaves padrão. Com a chave mestra, você possui a raiz de confiança que criptografa a cadeia inteira de chaves, incluindo chaves raiz e chaves padrão.

Por causa do canal seguro de ponta a ponta estabelecido para a instância de criptografia (HSM), apenas os administradores da instância do {{site.data.keyword.hscrypto}} podem configurar e gerenciar a chave mestra. Observe que a IBM não faz backup da chave mestra nem toca nela e não tem como copiá-la ou restaurá-la para uma máquina ou um data center diferente.

Uma instância de criptografia (HSM) pode ter somente uma chave mestra. Se você excluir a chave mestra da instância do {{site.data.keyword.hscrypto}}, será possível fragmentar por criptografia efetivamente todos os dados que foram criptografados com as chaves gerenciadas no serviço.

É possível gerenciar chaves mestras ao [Inicializar instâncias de criptografia para proteger o armazenamento de chaves](/docs/services/hs-crypto/initialize_hsm.html).

A rotação da chave mestra não é suportada no estágio atual.
{:important}
