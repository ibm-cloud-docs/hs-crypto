---

copyright:
  years: 2021
lastupdated: "2021-07-21"

keywords: signing service, manage signature keys, customer-writtn signing service, third-party signing service

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

# Using a signing service to manage signature keys for instance initialization
{: #signing-service-signature-key}

For {{site.data.keyword.hscrypto}} instance initialization, you can use a third-party signing service to create, store, and manage the administrator signature keys that are used by the Trusted Key Entry (TKE) CLI plug-in.
{: shortdesc}

Before you can use a signing service to manage sinature keys, make sure that you complete the [prerequisite steps](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite) for the instance intialization.

## Requirements on the signing service
{: #signing-service-requirements}

To enable a signing service for the TKE CLI plug-in, make sure that the signing service implements the following two API methods:

- GET `/keys/:name`

  This method is used to retrieve the public key of a signature key pair that is used to create a cryto unit administrator. The `:name` parameter is the unique identifier of a signature key. The signing service determines how the `:name` parameter is defined and set specifically. As the `:name` parameter is appended to the URI that is sent to the signing service, it must contain only unreserved characters as defined by section 2.3 of [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986).

  To make a successful API request, make sure that the following inputs are provided:

  - In the request path: The host URL and port number where the signing service is running.
  - In the request header: The authenticaion token for the key that you want to retrieve.

  This method returns the base64 encoded public key. The following is an example of the reponse body:

  ```
  {
    "publickey": "<base64 encoded string of public key (ASN.1 DER encoded struct containing integer X and integer Y)>"
  }
  ```
  {: codeblock}

- POST `/sign/:name`

  This method is used to sign arbitrary data by using the private key of a signature key pair. With the TKE CLI plug-in, it can be used to sign the TKE CLI administrative commands. The `:name` parameter is the unique identifier of a signature key. The signing service determines how the `:name` parameter is defined and set specifically. As the `:name` parameter is appended to the URI that is sent to the signing service, it must contain only unreserved characters as defined by section 2.3 of [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986).

  To make a successful API request, make sure that the following inputs are provided:

  - In the request path: The host URL and port number where the signing service is running.
  - In the request header: The authenticaion token for the key that you want to retrieve.
  - In the request body: The `hash_algorithm` parameter needs to be set to `sha2-512`; the `inputs` parameter needs to be set to the base64 encoded string of an assembled TKE CLI administrator command with the ASN.1 encoded struct.

  This method returns the base64 encoded signature. The following is an example of the response body:

  ```
  {
    "signature": "<base64 encoded string of binary data (ASN.1 DER encoded struct of integers R and S)>"
  }
  ```
  {: codeblock}

## Configuring the TKE CLI plug-in to use the signing service
{: #configure-tke-cli-for-signing-service}

Instead of using signature key files that are stored on your workstation for signing commands, configure the TKE CLI plug-in to use signature keys provided by your signing service by completing the following steps:

1. Set the `TKE_SIGNSERV_URL` environment variable on your workstation to the URL and port number where your signing service is running.

  After you set the `TKE_SIGNSERV_URL` environment variable, it indicates that you are using a third-party signing service for signature keys. In this case, the TKE `sigkey` commands don't perform any actions. These commands include `ibmcloud tke sigkeys`, `ibmcloud tke sigkey-add`, `ibmcloud tke sigkey-rm`, and `ibmcloud tke sigkey-sel`.
  {: note}
2. Create a file named `SIGNSERVKEYS` in the subdirectory that is identified by the `CLOUDTKEFILES` environment variable.

  This file is expected to be a JSON string representing an array that lists valid signature keys for signing commands. Each array entry must contain a `key` field and can optionally include a `token` field. The `key` field identifies a particular signature key. The `token` field authorizes use of the key. The signing service determines how the key identification and authentication token are defined. If you don't specify the `token` field in the `SIGNSERVKEYS` file, you are prompted to enter the token value when you run TKE CLI plug-in commands, which is more secure than directly providing it in the file.

  The following lists some examples of the `SIGNSERVKEYS` file:

  - [{"key":"first-key","token":"token-for-first-key"}]

    This example specifies a single valid signature key and its authentication token. Because the token is specified, you will not be prompted to enter it when the signature key is used.
  - [{"key":"first-key"},{"key":"second-key"}]

    This specifies two valid signature keys that can be used. Because the token is not specified, you will be prompted for the token when you use either key.
  - [{"key":"first-key"},{"key":"second-key","token":"token-for-second-key"},{"key":"third-key"}]

    This specifies three valid signature keys that can be used. The token is specified for the second key but not for the first and third key. If you use the first or the third key, you will be prompted for the corresponding token.

  Make sure the `SIGNSERVKEYS file` contains enough signature keys for installed administrators to meet signature threshold requirements. Otherwise, you are not able to use the signing service to perform TKE actions.
  {: note}
3. Add cryto unit administrators by using the `ibmcloud tke cryptounit-admin-add` command.

  After you set the `TKE_SIGNSERV_URL` environment variable, this command prompts you to enter a signature key identifier and its corresponding access token, as defined by the signing service, to add an administrator. The signature key identifier must be contained in the `SIGNSERVKEYS` file.

## What's next
{: #signing-service-whats-next}

- For the information about the subsequent steps to complete the service instance initialization, see [Initializing service instances using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).
- You can also use a signing service for Terraform. For more information, see [Setting up Terraform for {{site.data.keyword.hscrypto}}](docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs).
