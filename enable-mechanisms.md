---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-16"

keywords: enable mechanisms, BTC, bitcoin mechanism, BIP32, BIP 0032, Schnorr, enable deterministic wallets, Digital Asset Platforms

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:preview: .preview}
{:term: .term}

# Enabling crypto mechanisms
{: #enable-mechanisms}

After some crypto features and mechanisms are enabled in {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, you, as a crypto unit administrator, might need to manually enable them in your {{site.data.keyword.hscrypto}} instance before you can start using these features and mechanisms.

HSM firmware is updated in the [supported {{site.data.keyword.cloud_notm}} regions](/docs/hs-crypto?topic=hs-crypto-regions) to enable the following features. If your service instance is provisioned after the HSM firmware updates are deployed in the corresponding region, this feature is enabled by default. However, for any existing service instance, where the master key is set up before the HSM firmware update is rolled out, you need to enable the features manually as needed.

## Enabling BIP32 deterministic wallets
{: #enable-BIP32}

A Bitcoin Improvement Proposal (BIP) describes a feature for bitcoin, and the processes or environment. The BIP 0032 (BIP32) standard is used for hierarchical deterministic wallets to define how to derive private and public keys of a wallet.

To enable BIP32, follow these steps:

### Step 1: Verify the BIP32 enablement
{: #verify-BIP32-enablement}

To check whether the BIP32 feature is already enabled in your service instance, perform the following steps:

Before you perform the steps, make sure you have [provisioned a service instance](/docs/hs-crypto?topic=hs-crypto-provision) and initialized the service instance with either [the Trusted Key Entry (TKE) command-line interface (CLI) plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).
{: tip}

1. In the CLI, update the TKE CLI plug-in to the latest version with the following command:

    ```
    ibmcloud plugin update tke
    ```
    {: pre}

2. To check whether the BIP32 feature is enabled, run the following command:

    ```
    ibmcloud tke cryptounit-compare
    ```
    {: pre}

    The following output is an example of what is to be displayed. If the BIP32 feature is enabled, the `XCP_CPB_BTC` column is specified as `Set` in the `CONTROL POINTS` section:

    ```
    CONTROL POINTS
    SERVICE INSTANCE: f410ea28-691a-4708-a580-1f813e0a6d31
    CRYPTO UNIT NUM   XCP_CPB_BTC
    1                 Set
    2                 Set
    ```
    {: screen}

    If `Not Set` is displayed, perform the following steps to manually enable the BIP32 feature.

### Step 2: Enable BIP32 manually
{: #enable-bip32-manually}

To enable BIP32 for your service instance, follow these steps:

1. Check and make sure all crypto units in your service instance are selected with the following command:

    ```
    ibmcloud tke cryptounits
    ```
    {: pre}

    The following output is an example of what is to be displayed. All selected crypto units are marked `true` in the `SELECTED` column:

    ```
    SERVICE INSTANCE: 482cf2ce-a06c-4265-9819-0b4acf54f2ba
    CRYPTO UNIT NUM   SELECTED   LOCATION
    1                 true       [us-south].[AZ3-CS3].[02].[03]
    2                 true       [us-south].[AZ2-CS2].[02].[03]
    ```
    {: screen}

2. If any of the crypto units are not selected, run the following command and follow the prompts to add the crypto units to the selected list:

    ```
    ibmcloud tke cryptounit-add
    ```
    {: pre}

3. To enable the BIP32 feature, run the following command:

    ```
    ibmcloud tke cryptounit-cp-btc
    ```
    {: pre}

4. (Optional) To confirm that the BIP32 feature is enabled, run the `ibmcloud tke cryptounit-compare` command again, and make sure that `XCP_CPB_BTC` is marked as `Set` for all crypto units in the output.

## Enabling Edwards-curve Digital Signature Algorithm
{: #enable-EdDSA}

Edwards-curve Digital Signature Algorithm (EdDSA) is a modern and secure digital signature algorithm based on performance-optimized elliptic curves.

To enable EdDSA, follow these steps:

### Step 1: Verify the EdDSA enablement
{: #verify-EdDSA-enablement}

To check whether the EdDSA feature is already enabled in your service instance, perform the following steps:

Before you perform the steps, make sure you have [provisioned a service instance](/docs/hs-crypto?topic=hs-crypto-provision) and initialized the service instance with either [the Trusted Key Entry (TKE) command-line interface (CLI) plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).
{: tip}

1. In the CLI, update the TKE CLI plug-in to the latest version with the following command:

    ```
    ibmcloud plugin update tke
    ```
    {: pre}

2. To check whether the EdDSA feature is enabled, run the following command:

    ```
    ibmcloud tke cryptounit-compare
    ```
    {: pre}

    The following output is an example of what is to be displayed. If the EdDSA feature is enabled, the `XCP_CPB_ALG_EC_25519` column is specified as `Set` in the `CONTROL POINTS` section:

    ```
    CONTROL POINTS
    SERVICE INSTANCE: f410ea28-691a-4708-a580-1f813e0a6d31
    CRYPTO UNIT NUM   XCP_CPB_ALG_EC_25519
    1                 Set
    2                 Set

    ```
    {: screen}

    If `Not Set` is displayed, perform the following steps to manually enable the EdDSA feature.

### Step 2: Enable EdDSA manually
{: #enable-EdDSA-manually}

To enable EdDSA for your service instance, follow these steps:

1. Check and make sure all crypto units in your service instance are selected with the following command:

    ```
    ibmcloud tke cryptounits
    ```
    {: pre}

    The following output is an example of what is to be displayed. All selected crypto units are marked `true` in the `SELECTED` column:

    ```
    SERVICE INSTANCE: 482cf2ce-a06c-4265-9819-0b4acf54f2ba
    CRYPTO UNIT NUM   SELECTED   LOCATION
    1                 true       [us-south].[AZ3-CS3].[02].[03]
    2                 true       [us-south].[AZ2-CS2].[02].[03]
    ```
    {: screen}

2. If any of the crypto units are not selected, run the following command and follow the prompts to add the crypto units to the selected list:

    ```
    ibmcloud tke cryptounit-add
    ```
    {: pre}

3. To enable the EdDSA feature, run the following command:

    ```
    ibmcloud tke cryptounit-cp-eddsa
    ```
    {: pre}

4. (Optional) To confirm that the EdDSA feature is enabled, run the `ibmcloud tke cryptounit-compare` command again, and make sure that `XCP_CPB_ALG_EC_25519` is marked as `Set` for all crypto units in the output.

## Enabling the Schnorr algorithm
{: #enable-schnorr}

The Schnorr algorithm can be used as a signing scheme to generate digital signatures. It is proposed as an alternative algorithm to the Elliptic Curve Digital Signature Algorithm (ECDSA) for cryptographic signatures in the Bitcoin system. The Schnorr signature is known for the simplicity and efficiency.

To enable the Schnorr algorithm, follow these steps:

### Step 1: Verify the Schnorr algorithm enablement
{: #verify-schnorr-enablement}

To check whether the Schnorr algorithm is already enabled in your service instance, perform the following steps:

Before you perform the steps, make sure you have [provisioned a service instance](/docs/hs-crypto?topic=hs-crypto-provision) and initialized the service instance with either [the Trusted Key Entry (TKE) command-line interface (CLI) plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).
{: tip}

1. In the CLI, update the TKE CLI plug-in to the latest version with the following command:

    ```
    ibmcloud plugin update tke
    ```
    {: pre}

2. To check whether the Schnorr algorithm is enabled, run the following command:

    ```
    ibmcloud tke cryptounit-compare
    ```
    {: pre}

    The following output is an example of what is to be displayed. If the Schnorr algorithm is enabled, the `XCP_CPB_ECDSA_OTHER` column is specified as `Set` in the `CONTROL POINTS` section:

    ```
    CONTROL POINTS
    SERVICE INSTANCE: f410ea28-691a-4708-a580-1f813e0a6d31
    CRYPTO UNIT NUM   XCP_CPB_ECDSA_OTHER
    1                 Set
    2                 Set
    ```
    {: screen}

    If `Not Set` is displayed, perform the following steps to manually enable the Schnorr algorithm.

### Step 2: Enable the Schnorr algorithm manually
{: #enable-schnorr-manually}

To enable the Schnorr algorithm for your service instance, follow these steps:

1. Check and make sure all crypto units in your service instance are selected with the following command:

    ```
    ibmcloud tke cryptounits
    ```
    {: pre}

    The following output is an example of what is to be displayed. All selected crypto units are marked `true` in the `SELECTED` column:

    ```
    SERVICE INSTANCE: 482cf2ce-a06c-4265-9819-0b4acf54f2ba
    CRYPTO UNIT NUM   SELECTED   LOCATION
    1                 true       [us-south].[AZ3-CS3].[02].[03]
    2                 true       [us-south].[AZ2-CS2].[02].[03]
    ```
    {: screen}

2. If any of the crypto units are not selected, run the following command and follow the prompts to add the crypto units to the selected list:

    ```
    ibmcloud tke cryptounit-add
    ```
    {: pre}

3. To enable the Schnorr algorithm, run the following command:

    ```
    ibmcloud tke cryptounit-cp-sig-other
    ```
    {: pre}

4. (Optional) To confirm that the Schnorr algorithm is enabled, run the `ibmcloud tke cryptounit-compare` command again, and make sure that `XCP_CPB_ECDSA_OTHER` is marked as `Set` for all crypto units in the output.

## What's next
{: #next-enable-mechanisms}

You can now start using [the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) or [the GREP11 API](/docs/hs-crypto?topic=hs-crypto-set-up-grep11-api) to perform cryptographic operations and protect deterministic wallets.

* For more information about the TKE CLI commands, check out the [TKE CLI reference](/docs/hs-crypto?topic=hs-crypto-cli-plugin-hpcs-cli-plugin#tke-cli-plugin).
* For more information about the PKCS #11 API, check out [Introducing PKCS #11](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro) and [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).
* For more information about the GREP11 API, check out [Introducing EP11 over gRPC](/docs/hs-crypto?topic=hs-crypto-grep11_intro) and [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
* To learn more about the differences and relationships between PKCS #11 and GREP11 API, see [Introducing cloud HSM](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm).
