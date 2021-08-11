---

copyright:
  years: 2018, 2021
lastupdated: "2021-08-11"

keywords: how to import encryption key, upload encryption key tutorial, Bring Your Own Key, BYOK, secure import, Getting started with transporting encryption key

subcollection: hs-crypto

content-type: tutorial
services: hs-crypto
account-plan: paid
completion-time: 30m

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
{:step: data-tutorial-type='step'}


# Tutorial: Creating and importing encryption keys
{: #tutorial-import-keys}
{: toc-content-type="tutorial"}
{: toc-completion-time="30m"}

Learn how to create, encrypt, and bring your encryption keys to the cloud by using {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Objectives
{: #tutorial-import-objectives}

This tutorial walks you through creating and securely importing encryption keys into the {{site.data.keyword.hscrypto}} service. It's intended for users who are new to the key management function of {{site.data.keyword.hscrypto}}, but who might have some familiarity with key management systems. The following steps need to take about 20 minutes to complete.

- Setting up the key management API
- Preparing your {{site.data.keyword.hscrypto}} service instance to begin importing keys
- Creating and encrypting keys using the OpenSSL cryptography toolkit
- Importing an encrypted key to your {{site.data.keyword.hscrypto}} service instance

This tutorial won't incur any charges to your {{site.data.keyword.cloud_notm}} account.

## Before you begin
{: #tutorial-import-prereqs}

To get started, you need the {{site.data.keyword.cloud_notm}} CLI so that you can interact with services that you provision on {{site.data.keyword.cloud_notm}}. You also need the `openssl` and `jq` packages installed locally on your workstation.

1. Create an [{{site.data.keyword.cloud_notm}} account](https://{DomainName}){: external}.
2. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started) for your operating system.
3. Download and install the [{{site.data.keyword.keymanagementservicelong_notm}} CLI plug-in](/docs/key-protect?topic=key-protect-set-up-cli) v0.6.3 or later, and [configure it to use in {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-set-up-cli). Make sure to update the `KP_PRIVATE_ADDR` variable to the current instance key management endpoint URL.

    To check your {{site.data.keyword.keymanagementservicelong_notm}} CLI plug-in version:

    ```
    ibmcloud plugin show key-protect
    ```
    {: pre}

    To update your {{site.data.keyword.keymanagementservicelong_notm}} CLI plug-in to the latest version:

    ```
    ibmcloud plugin update key-protect -r 'IBM Cloud'
    ```
    {: pre}

4. Download and install the [OpenSSL cryptography library](https://www.openssl.org/source/){: external}.

    You can use `openssl` commands to generate encryption keys on your local workstation if you're trying out {{site.data.keyword.hscrypto}} for the first time. This tutorial requires OpenSSL version `1.0.2r` or above.

    If you're using a Mac, you can quickly get up and running with OpenSSL by using [Homebrew](https://brew.sh/){: external}. Run `brew install openssl` if you're installing the package for the first time, or run `brew upgrade openssl` to upgrade your existing package to the latest version.
    {: tip}

5. Download and install [jq](https://stedolan.github.io/jq/){: external}.

    `jq` helps you slice up JSON data. You'll use `jq` in this tutorial to grab and use specific data that's returned when you call the {{site.data.keyword.hscrypto}} key management API.

6. [Create a {{site.data.keyword.hscrypto}} service instance](/docs/hs-crypto?topic=hs-crypto-provision).
7. [Initialize the {{site.data.keyword.hscrypto}} service instance](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).
8. [Set up the {{site.data.keyword.hscrypto}} key management API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

## Task flow
{: #tutorial-flow}

The following high-level steps give you an overview on how to create and import encryption keys:

1. [Create an import token](#tutorial-import-create-token).
2. [Retrieve the import token](#tutorial-import-retrieve-token).
3. [Create an encryption key](#tutorial-import-create-key).
4. [Encrypt the nonce](#tutorial-import-encrypt-nonce).
5. [Encrypt the key](#tutorial-import-encrypt-key).
6. [Import the key](#tutorial-import-encrypted-key).
7. [Clean up](#tutorial-import-encrypted-key).

For detailed instructions, complete the following steps:

## Create an import token
{: #tutorial-import-create-token}
{: step}

With your service credentials, you can start interacting with the key management API to create and bring your encryption keys to the service.

In the following step, you'll create a [import token](/docs/hs-crypto?topic=hs-crypto-importing-keys#using-import-tokens) for your {{site.data.keyword.hscrypto}} service instance. By creating an import token based on a policy that you specify, you enable extra security for your encryption key while it's in flight to the service.

1. From the command line, change into a new `hs-crypto-test` directory.

    ```sh
    mkdir hs-crypto-test && cd hs-crypto-test
    ```
    {: pre}

    You'll use this directory to store the files that you'll create in later steps.

2. You can create an import token for your {{site.data.keyword.hscrypto}} service instance by either using the [key management API](https://{DomainName}/apidocs/hs-crypto) or using the [CLI](/docs/hs-crypto?topic=hs-crypto-set-up-cli), and then save the response to a JSON file.

    - **Use the API**:

      ```sh
      curl -X POST $HPCS_API_URL/api/v2/import_token \
          -H "Accept: application/vnd.ibm.collection+json" \
          -H "Authorization: $ACCESS_TOKEN" \
          -H "Content-Type: application/json" \
          -H "Bluemix-Instance: $INSTANCE_ID" \
          -d '{
              "expiration": 1200,
              "maxAllowedRetrievals": 1
            }' > createImportTokenResponse.json
      ```
      {: pre}

      In the request body, you can specify a policy on the import token that limits the use based on time and usage count. In this example, you set the expiration time for the import token to 1200 seconds (20 minutes), and you also allow only one retrieval of that token within the expiration time.
      {: tip}

    - **Use the {{site.data.keyword.keymanagementservicelong_notm}} CLI**:

      ```
      ibmcloud kp import-token create --instance-id $INSTANCE_ID --max-retrievals=1 --expiration=1200 > createImportTokenResponse.json
      ```
      {: pre}

3. View details for the import token.

    ```sh
    jq '.' createImportTokenResponse.json
    ```
    {: pre}

    The output displays the metadata that is associated with your import token, such as the creation date and policy details. The following snippet shows example output.

    ```json
    {
      "creationDate": "2020-06-08T16:58:29Z",
      "expirationDate": "2020-06-08T17:18:29Z",
      "maxAllowedRetrievals": 1,
      "remainingRetrievals": 1
    }
    ```
    {: screen}

## Retrieve the import token
{: #tutorial-import-retrieve-token}
{: step}

In the previous step, you created an import token and you viewed the metadata that is associated with the token.

In this step, you'll retrieve the public encryption key and nonce value that are associated with the import token. You'll need the public key to encrypt data in a later step, and the nonce to verify your secure import request to the {{site.data.keyword.hscrypto}} service.

To retrieve the import token contents:

1. Retrieve the import token that you generated the previous step, and then save the response to a JSON file.

    - **Use the API**:

      ```sh
      curl -X GET $HPCS_API_URL/api/v2/import_token \
          -H "Accept: application/vnd.ibm.collection+json" \
          -H "Authorization: $ACCESS_TOKEN" \
          -H "Bluemix-Instance: $INSTANCE_ID" > getImportTokenResponse.json
      ```
      {: pre}

    - **Use the {{site.data.keyword.keymanagementservicelong_notm}} CLI**:

      ```
      ibmcloud kp import-token show > getImportTokenResponse.json
      ```
      {: pre}

2. Optional: Inspect the contents of the import token.

    ```sh
    jq '.' getImportTokenResponse.json
    ```
    {: pre}

    The output displays detailed information about the import token. The following snippet shows example output with truncated values.

    ```json
    {
      "creationDate": "2020-06-08T16:58:29Z",
      "expirationDate": "2020-06-08T17:18:29Z",
      "maxAllowedRetrievals": 1,
      "remainingRetrievals": 0,
      "payload": "MIICIjANBgkqhkiG...",
      "nonce": "8zJE9pKVdXVe/nLb"
    }
    ```
    {: screen}

    The `payload` value represents the public key that is associated with the import token. This value is base64 encoded. For extra security, {{site.data.keyword.hscrypto}} provides a `nonce` value that is used to verify the originality of a request to the service. You'll need to encrypt and provide this value when you import your encryption key.

3. Decode and save the public key to a file called `PublicKey.pem`.

    ```sh
    jq -r '.payload' getImportTokenResponse.json | openssl enc -base64 -A -d -out PublicKey.pem
    ```
    {: pre}

    ```sh
    NONCE="$(jq -r '.nonce' getImportTokenResponse.json)"
    ```
    {: pre}

    The public key is now downloaded to your workstation in PEM format. Continue to the next step.

## Create an encryption key
{: #tutorial-import-create-key}
{: step}

With {{site.data.keyword.hscrypto}}, you can enable the security benefits of Keep Your Own Key (KYOK) by creating and uploading your own keys for use on {{site.data.keyword.cloud_notm}}.

In the following step, you'll create a 256-bit AES symmetric key on your local workstation.

This tutorial uses the OpenSSL cryptography toolkit to generate a pseudo-random key, but you might want to [explore different options](/docs/hs-crypto?topic=hs-crypto-importing-keys#plan-ahead) for generating stronger keys based on your security needs. For example, you might want to use your organization's internal key management system, backed by an on-premises hardware security module (HSM), to create and export keys.
{: note}

If you want to create a 256-bit encryption key, from the command line, run the following `openssl` command:

```sh
openssl rand 32 > PlainTextKey.bin
```
{: pre}

You can skip this step if you use your own key in this tutorial.
{: tip}

Success! Your encryption key is now saved in a file called `PlainTextKey.bin`. Continue to the next step.

## Encrypt the nonce
{: #tutorial-import-encrypt-nonce}
{: step}

For extra security, {{site.data.keyword.hscrypto}} requires nonce verification when you import a key to the service.

In cryptography, a nonce serves as a session token that checks the originality of a request to protect against malicious attacks and unauthorized calls. By using the same nonce that was distributed by {{site.data.keyword.hscrypto}}, you help to ensure that your request to upload a key is valid. The nonce value must be encrypted by using the same key that you want to import into the service.

To encrypt the nonce value:

1. If you generate the key by following [step 3](#tutorial-import-create-key), to encode the key and set the encoded value as an environment variable, perform the following command:

    ```sh
    KEY_MATERIAL=$(openssl enc -base64 -A -in PlainTextKey.bin)
    ```
    {: pre}

    You can skip this step if you use your own key in this tutorial.
    {: tip}

2. Gather the nonce value that you retrieved in [step 2](#tutorial-import-retrieve-token).

    ```sh
    NONCE=$(jq -r '.nonce' getImportTokenResponse.json)
    ```
    {: pre}

3. If you are going to use the API to perform the subsequent steps, do the following:

    You don't need to perform this step if you are going to use the {{site.data.keyword.keymanagementservicelong_notm}} CLI.
    {: tip}

    1. [Download the sample `kms-encrypt-nonce` binary](https://github.com/IBM-Cloud/kms-samples/releases/tag/v1.1){: external} that is compatible with your operating system. Extract the file, and then move the binary to the `hs-crypto-test` directory.

      The binary contains a script that you can use to run AES-CBC encryption on the nonce value by using the key that you generated in [step 2](#tutorial-import-retrieve-token). To learn more about the script, [check out the source file on GitHub](https://github.com/IBM-Cloud/kms-samples/blob/master/secure-import/encrypt.go){: external}.
      {: note}

    2. If you are using Linux&reg;, mark the file as executable by running the following  `chmod` command. You can skip this step if you are using Windows.

      ```sh
      chmod +x ./kms-encrypt-nonce
      ```
      {: pre}

4. Run the script to encrypt the nonce value with the encryption key that you generated in [step 2](#tutorial-import-retrieve-token). Then, save the response to a file called `EncryptedValues.json`.

    - **Use the API**:

      ```sh
      ./kms-encrypt-nonce -key $KEY_MATERIAL -nonce $NONCE -alg "CBC" > EncryptedValues.json
      ```
      {: pre}

    - **Use the {{site.data.keyword.keymanagementservicelong_notm}} CLI**:

      ```
      ibmcloud kp import-token nonce-encrypt --key "$KEY_MATERIAL" --nonce "$NONCE" --cbc | awk 'END{print "{\"encryptedNonce\": \""$1"\", \"iv\": \""$2"\"}";}' > EncryptedValues.json
      ```
      {: pre}

5. Optional: Inspect the contents of the JSON file.

    ```sh
    jq '.' EncryptedValues.json
    ```
    {: pre}

    The output displays the values that you'll need to provide for the next step. The following snippet shows example output with truncated values.

    ```json
    {
      "encryptedNonce": "DVy/Dbk37X8gSVwRA5U6vrHdWQy8T2ej+riIVw==",
      "iv": "puQrzDX7gU1TcTTx"
    }
    ```
    {: screen}

    The `encryptedNonce` value represents the original nonce that is wrapped (or encrypted) by the encryption key that you generated using OpenSSL. The `iv` value is the initialization vector (IV) that is created by the AES-CBC algorithm, and it's required later so that {{site.data.keyword.hscrypto}}can successfully decrypt the nonce.

## Encrypt the key
{: #tutorial-import-encrypt-key}
{: step}

Next, use the public key that was distributed by {{site.data.keyword.hscrypto}} in [step 2](#tutorial-import-retrieve-token) to encrypt the symmetric key that you generated using OpenSSL.

* Encrypt the generated key with the API, and assign the key to the environment variable:

    ```sh
    openssl pkeyutl \
      -encrypt \
      -pubin \
      -keyform PEM \
      -inkey PublicKey.pem \
      -pkeyopt rsa_padding_mode:oaep \
      -pkeyopt rsa_oaep_md:sha1 \
      -in PlainTextKey.bin \
      -out EncryptedKey.bin
    ```
    {: pre}

    ```
    ENCRYPTED_KEY=$(openssl enc -base64 -A -in EncryptedKey.bin)
    ```
    {: pre}

    If you run into a parameter settings error when you run the `openssl` command on Mac OSX, you might need to ensure that OpenSSL is properly configured for your environment. If you installed OpenSSL by using Homebrew, run `brew update` and then `brew install openssl` to get the latest version. Then, run `export PATH="/usr/local/opt/openssl/bin:$PATH"' >> ~/.bash_profile` to symlink the package. From the command line, run `which openssl && openssl version` to verify that the latest version of OpenSSL is available under the `/usr/local/` location. If you continue to encounter errors, be sure to use only the parameters that are listed in this example.
    {: tip}

* Encrypt the generated key with the {{site.data.keyword.keymanagementservicelong_notm}} CLI:

    ```
    ENCRYPTED_KEY=$(ibmcloud kp import-token key-encrypt --key $KEY_MATERIAL --pubkey "$(jq -r '.payload' getImportTokenResponse.json)" --hash SHA1  | awk 'END{print $1}')
    ```
    {: pre}

    Success! You're all set to upload your encrypted key into {{site.data.keyword.hscrypto}}. Continue to the next step.

## Import the key
{: #tutorial-import-encrypted-key}
{: step}

You can now import the encrypted key using the key management API.

To import the key:

1. Gather the encrypted nonce and the initialization vector (IV) values.

    ```sh
    ENCRYPTED_NONCE=$(jq -r '.encryptedNonce' EncryptedValues.json)
    ```
    {: pre}

    ```sh
    IV=$(jq -r '.iv' EncryptedValues.json)
    ```
    {: pre}

2. Store the encrypted key in your {{site.data.keyword.hscrypto}} service instance.

    - **Use the API**:

      ```sh
      curl -X POST  $HPCS_API_URL/api/v2/keys \
          -H "Accept: application/vnd.ibm.collection+json" \
          -H "Authorization: $ACCESS_TOKEN" \
          -H "Content-Type: application/json" \
          -H "Bluemix-Instance: $INSTANCE_ID" \
          -d '{
            "metadata": {
              "collectionType": "application/vnd.ibm.kms.key+json",
              "collectionTotal": 1
            },
            "resources": [
            {
              "name": "encrypted-root-key",
              "type": "application/vnd.ibm.kms.key+json",
              "payload": "'"$ENCRYPTED_KEY"'",
              "extractable": false,
              "encryptionAlgorithm": "RSAES_OAEP_SHA_1",
              "encryptedNonce": "'"$ENCRYPTED_NONCE"'",
              "iv": "'"$IV"'"
            }
          ]
        }' > createRootKeyResponse.json
      ```
      {: pre}

      In the request body, you provide the encryption key that you prepared in the previous step. You also supply the encrypted nonce and the IV values that are required to verify the request. Finally, the `extractable` value set to `false` designates your new key as a root key in the service that you can use for envelope encryption.

      If the API request fails with an import token expired error, [return to step 1](#tutorial-import-create-token) to create a new import token. Remember that import tokens and their associated public keys expire based on the policy that you specify at creation time.
      {: tip}

    - **Use the {{site.data.keyword.keymanagementservicelong_notm}} CLI**:

      ```
      ibmcloud kp key create new-imported-key --key-material "${ENCRYPTED_KEY}" --encrypted-nonce "${ENCRYPTED_NONCE}" --iv "${IV}" --sha1 > createRootKeyResponse.json
      ```
      {: pre}

      Behind the scenes, {{site.data.keyword.hscrypto}} receives your encrypted packet over a TLS 1.2 connection. Within a hardware security module, the system uses the private key to decrypt the symmetric key. Finally, the system uses the symmetric key and the IV to decrypt the nonce and verify the request. Your key is now stored in a tamper-resistant, FIPS 140-2 Level 4 validated hardware security module.

3. View details for the encryption key.

    ```
    jq '.' createRootKeyResponse.json
    ```
    {: pre}

    The following snippet shows an example output.

    ```json
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
      },
      "resources": [
        {
          "id": "644cba65-e240-471f-8b84-14115447d2ae",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "encrypted-root-key",
          "state": 1,
          "crn": "crn:v1:bluemix:public:hs-crypto:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:346d9f67-4bb2-481e-a3e1-3c2c646aa886:key:644cba65-e240-471f-8b84-14115447d2ae",
          "extractable": false,
          "imported": true
        }
      ]
    }
    ```
    {: screen}

    The `id` value is a unique identifier that is assigned to your key and is used for subsequent calls to the key management API. The `state` value set to 1 indicates that your encryption key is now in the [_Active_ key state](/docs/hs-crypto?topic=hs-crypto-key-states). The `crn` value provides the full scoped path to the key that specifies where the resource resides within {{site.data.keyword.cloud_notm}}. Finally, the `extractable` and `imported` values describe this resource as a root key that you imported to the service.

4. Optional: Navigate to the {{site.data.keyword.hscrypto}} dashboard to view and manage your encryption key.

    You can browse the general characteristics of your keys from the application details page. Choose from a list of options for managing your key, such as [rotating the key](/docs/hs-crypto?topic=hs-crypto-rotate-keys#rotate-root-key-gui) or [deleting the key](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-keys-gui).

## Clean up
{: #tutorial-import-clean-up}
{: step}

1. Gather the identifier for the encryption key that you imported in the previous step.

    ```sh
    ROOT_KEY_ID=$(jq -r '.resources[].id' createRootKeyResponse.json)
    ```
    {: pre}

2. Remove the encryption key from your {{site.data.keyword.hscrypto}} service instance.

    - **Use the API**:

      ```sh
      curl -X DELETE $HPCS_API_URL/api/v2/keys/$ROOT_KEY_ID \
        -H "Accept: application/vnd.ibm.collection+json" \
        -H "Authorization: $ACCESS_TOKEN" \
        -H "Bluemix-Instance: $INSTANCE_ID" | jq .
      ```
      {: pre}

    - **Use the {{site.data.keyword.keymanagementservicelong_notm}} CLI**:

      ```
      ibmcloud kp key delete {ROOT_KEY_ID}
      ```
      {: pre}

3. Remove all the local files associated with this tutorial.

    ```sh
    rm kms-encrypt-nonce *.json *.bin *.pem
    ```
    {: pre}

4. Delete the test directory that you created for this tutorial.

    ```sh
    cd .. && rm -r hs-crypto-test
    ```
    {: pre}

5. Optional: Remove your {{site.data.keyword.hscrypto}} service instance.

    ```sh
    ibmcloud resource service-instance-delete import-keys-demo
    ```
    {: pre}

    If you created more test keys in your service instance, be sure to [remove all encryption keys from your service instance](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-keys) before you deprovision the instance.
    {: tip}

## Next steps
{: #tutorial-import-next-steps}

In this tutorial, you learned how to set up the {{site.data.keyword.hscrypto}} key management API, create an encryption key, and securely import an encrypted key into your {{site.data.keyword.hscrypto}} service instance.

- Learn more about [using your root key to protect data at rest](/docs/hs-crypto?topic=hs-crypto-envelope-encryption#envelope-encryption).
- Deploy your root key across [supported cloud services](/docs/hs-crypto?topic=hs-crypto-integrate-services#integrate-services).
- Learn more about the [key management API](https://{DomainName}/apidocs/hs-crypto).
