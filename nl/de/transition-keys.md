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

# Schlüssel aus einer Betaserviceinstanz migrieren
{: #migrate-keys}

Wenn Sie eine Betaserviceinstanz verwendet haben und die verwalteten Rootschlüssel und Standardschlüssel in eine {{site.data.keyword.hscrypto}}-Produktionsserviceinstanz migrieren möchten, müssen Sie anhand der folgenden Prozedur vorgehen.
{: shortdesc}

IBM Cloud-Administratoren können die Masterschlüssel nicht migrieren, da die Masterschlüssel nicht aus der Verschlüsselungseinheit extrahiert werden können. Sie müssen die Produktionsserviceinstanz mit Ihrem Masterschlüssel initialisieren.
{:important}  

## Vorbereitungen
{: #migrate-prerequisites}

1. [Erstellen Sie eine Serviceinstanz](/docs/services/hs-crypto/provision.html) mit dem Hyper Protect Crypto Services-Plan. 

2. [Initialisieren Sie die Serviceinstanz](/docs/services/hs-crypto/initialize_hsm.html) mit dem Plug-in "Trusted Key Entry". 

## Schlüssel migrieren
{: #migrate-keys-steps}  

Führen Sie die folgenden Schritte aus, um Rootschlüssel und Standardschlüssel in die Produktionsumgebung zu migrieren. 

1. [Importieren Sie die Rootschlüssel](/docs/services/hs-crypto/import-root-keys.html) entweder über die GUI oder die API. 

  Sie können die importierten Rootschlüssel aus der Betaserviceinstanz in die Produktionsserviceinstanz migrieren.
  {:tip}

2. Heben Sie das Wrapping der Datenverschlüsselungsschlüssel (Data Encryption Keys, DEKs) in der Betaserviceinstanz auf und führen Sie das Wrapping der DEKs in der Produktionsserviceinstanz durch: 

  1. [Heben Sie das Wrapping der Datenverschlüsselungsschlüssel (DEKs)](/docs/services/hs-crypto/unwrap-keys.html) in der Betaserviceinstanz mit der [API invoke-an-action-on-a-key ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: new_window} auf. 

  2. [Führen Sie das Wrapping der DEKs](/docs/services/hs-crypto/wrap-keys.html) in der Produktionsserviceinstanz mit der [API invoke-an-action-on-a-key ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key{: new_window}) aus. 

3. Führen Sie die folgenden Schritte aus, um die Standardschlüssel erneut zu erstellen: 

  1. [Rufen Sie die Standardschlüssel](/docs/services/hs-crypto?topic=hs-crypto-view-keys#retrieve-key-api) mit der [API retrieve-key-by-id ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto#retrieve-a-key-by-id){: new_window} ab. Dadurch werden die Nutzdaten zurückgegeben, die zum Erstellen des Schlüssels in der Betainstanz verwendet werden. 

  2. [Erstellen Sie die Standardschlüssel](/docs/services/hs-crypto/create-standard-keys.html) in der neuen Serviceinstanz mit den Informationen, die im vorherigen Schritt über die GUI oder die [API create-a-new-key ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto#create-a-new-key){: new_window} abgerufen wurden. 

## Weitere Schritte
{: #migration-next}

Weitere Informationen zur programmgesteuerten Verwaltung von Schlüsseln [finden Sie in der {{site.data.keyword.hscrypto}}-API-Referenzdokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
