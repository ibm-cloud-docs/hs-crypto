---

copyright:
  years: 2018, 2021
lastupdated: "2021-08-10"

keywords: import encryption key, upload encryption key, bring your own key, byok, key material, secure import, import tokens

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

# Bringing your encryption keys to the cloud
{: #importing-keys}

Encryption keys contain subsets of information, such as the metadata that helps you identify the key, and the key material that is used to encrypt and decrypt data.
{: shortdesc}

When you use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to create keys, the service generates cryptographic key material on your behalf that's rooted in the hardware security modules (HSMs) of your {{site.data.keyword.hscrypto}} instance. But depending on your business requirements, you might need to generate key material from your internal solution, and then extend your on-premises key management infrastructure onto the cloud by importing keys into {{site.data.keyword.hscrypto}}.

| Benefit | Description |
| --- | --- |
| Keep Your Own Key (KYOK) | If you choose to export symmetric keys from your internal key management infrastructure, you can use {{site.data.keyword.hscrypto}} to securely bring them to the cloud. The KYOK feature ensures that you own the root trust of your key hierarchy and that no one except you have access to your encryption keys. |
| Secure import of root key material | When you export your keys to the cloud, you want assurance that the key material is protected while it's in flight. Mitigate against man-in-the-middle attacks by using an import token to securely import root key material into your {{site.data.keyword.hscrypto}} service instance. |
{: caption="Table 1. Describes the benefits of importing key material" caption-side="bottom"}

## Planning ahead for importing key material
{: #plan-ahead}

Keep the following considerations in mind when you're ready to import root key material to the service.

<dl>
    <dt>Review your options for creating key material</dt>
    <dd>Explore your options for creating 256-bit symmetric encryption keys based on your security needs. For example, you can use your internal key management system, backed by a FIPS-validated, on-premises hardware security module (HSM), to generate key material before you bring keys to the cloud. If you're building a proof of concept, you can also use a cryptography toolkit such as <a href="https://www.openssl.org/" target="_blank" class="external">OpenSSL</a> to generate key material that you can import into {{site.data.keyword.hscrypto}} for your testing needs.</dd>
    <dt>Choose an option for importing key material into {{site.data.keyword.hscrypto}}</dt>
    <dd>Choose from two options for importing root keys based on the level of security that's required for your environment or workload. By default, {{site.data.keyword.hscrypto}} encrypts your key material while it's in transit by using the Transport Layer Security (TLS) 1.2 protocol. If you're building a proof of concept or trying out the service for the first time, you can import root key material into {{site.data.keyword.hscrypto}} by using this default option. If your workload requires a security mechanism beyond TLS, you can also <a href="#using-import-tokens">use an import token</a> to encrypt and import root key material into the service.</dd>
    <dt>Plan ahead for encrypting your key material</dt>
    <dd>If you choose to encrypt your key material by using an import token, determine a method for running RSA encryption on the key material. You must use the <code>RSAES_OAEP_SHA_1</code> encryption scheme as specified by the <a href="https://tools.ietf.org/html/rfc3447" target="_blank" class="external">PKCS #1 v2.1 standard for RSA encryption</a>. Review the capabilities of your internal key management system or on-premises HSM to determine your options.</dd>
    <dt>Plan ahead for encrypting the nonce</dt>
    <dd>If you choose to encrypt your key material by using an import token, you must also determine a method for running AES-GCM encryption on the nonce that is distributed by {{site.data.keyword.hscrypto}}. The nonce serves as a session token that checks the originality of a request to protect against malicious attacks and unauthorized calls. Review the capabilities of your internal key management system or on-premises HSM to determine your options.</dd>
    <dt>Manage the lifecycle of imported key material</dt>
    <dd>After you import key material into the service, keep in mind that you are responsible for managing the complete lifecycle of your key. By using the {{site.data.keyword.hscrypto}} key management API, you can set an expiration date for the key when you decide to upload it into the service. However, if you want to <a href="/docs/hs-crypto?topic=hs-crypto-rotate-keys">rotate an imported root key</a>, you must generate and provide new key material to retire and replace the existing key. </dd>
</dl>

## Using import tokens
{: #using-import-tokens}

If you want to encrypt your key material before you import it into {{site.data.keyword.hscrypto}}, you can create an import token for your service instance by using the {{site.data.keyword.hscrypto}} key management API.

Import tokens are a resource type in {{site.data.keyword.hscrypto}} that enable the secure import of key material to your service instance. By using the contents of an import token to encrypt your key material on-premises, you protect root keys while they're in flight to {{site.data.keyword.hscrypto}} based on the policies that you specify. For example, you can set a policy on the import token that limits the use based on time and usage count.

### How it works
{: #how-import-tokens-work}

When you [create an import token](/docs/hs-crypto?topic=hs-crypto-create-import-tokens) for your service instance, {{site.data.keyword.hscrypto}} generates a 4096-bit RSA key-pair from the HSMs. When you [retrieve the import token](/docs/hs-crypto?topic=hs-crypto-create-import-tokens#retrieve-import-token-api), the service supplies the public key that you can use for encrypting and uploading a key to {{site.data.keyword.hscrypto}}.

The following list describes the import token workflow.

1. **You send a request to create an import token.**
   1. {{site.data.keyword.hscrypto}} generates an RSA key-pair from the crypto units (HSMs).
   2. The public key becomes available for retrieval based on the policy that you specified at creation time.
   3. The private key becomes non-extractable and never leaves the crypto unit.
2. **You send a request to retrieve the import token.**
   1. You receive the import token contents, including:
      - A public key for the encrypting key material that you want to import into the service.
      - A nonce value that's used to verify the key import request.
3. **You prepare the key that you want to import to the service.**
   1. You generate key material by using an on-premises key management mechanism.
   2. You encrypt the nonce value with the key material by using an AES-GCM encryption method that is compatible with your environment.
   3. You encrypt the key material with the public key by using an RSA encryption method that is compatible with your environment.
4. **You send a request to import the key.**
   1. You provide the encrypted key material, the encrypted nonce, and the initialization vector (IV) that was generated by the AES-GCM algorithm.
   2. {{site.data.keyword.hscrypto}} verifies your request, decrypts the encrypted packet, and stores the key material as a root key in your service instance.

You can create only one import token per service instance at a time. To learn more about retrieval limits for import tokens, [see the {{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto#postimporttoken){: external}.
{: note}



### API methods
{: #secure-import-api-methods}

Behind the scenes, the {{site.data.keyword.hscrypto}} key management API drives the import token creation process.

The following table lists the API methods that set up an import token for your service instance.

| Method | Description |
| --- | --- |
| `POST api/v2/import_token` | Create an import token |
| `GET api/v2/import_token` | Retrieve an import token |
{: caption="Table 2. Describes the key management API methods" caption-side="bottom"}

## What's next
{: #importing-keys-next}

- To learn how to create an import token for your service instance, see [Creating an import token](/docs/hs-crypto?topic=hs-crypto-create-import-tokens).
- To find out more about importing keys to the service, see [Importing root keys](/docs/hs-crypto?topic=hs-crypto-import-root-keys).
- To find out more about programmatically managing your keys in {{site.data.keyword.hscrypto}}, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
