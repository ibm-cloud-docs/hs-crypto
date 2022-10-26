---

copyright:
  years: 2021, 2022
lastupdated: "2022-10-26"

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

For {{site.data.keyword.hscrypto}} instance initialization, you can use a third-party signing service to create, store, and manage the administrator signature keys that are used by Terraform or the Trusted Key Entry (TKE) CLI plug-in. With signature keys provided by the signing service, you no longer use the signature key files on the local workstation when you run Terraform and TKE CLI plug-in commands.
{: shortdesc}

## Signing service prerequisites
{: #signing-service-requirements}

Before you can use a signing service to manage signature keys, make sure that you complete the [prerequisite steps](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite) for the instance initialization.

To enable a signing service for Terraform or the TKE CLI plug-in, the signing service must be implemented as an HTTP server that implements the following two requests. All signature keys that are accessed by using the signing service must be P521 EC keys.

- GET `/keys/:name`

    This request retrieves the public key of a signature key. The public key is needed when you add a crypto unit administrator. The `:name` parameter identifies the signature key that is to be accessed. The signing service determines how `:name` values are associated with signature keys. The `:name` parameter corresponds to a `key` parameter in a Terraform resource block.

    The `:name` parameter is appended to the URL that accesses the signing service. It can contain only unreserved characters as defined by section 2.3 of [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986). The authentication token for the signature key is passed to a `GET /keys` request in the HTTP `Authorization` request header.

    This request returns the base64 encoded public key. The following is an example of the response body:

    ```json
    {
      "publickey": "<base64 encoded string of public key (ASN.1 DER encoded struct containing integer X and integer Y)>"
    }
    ```
    {: codeblock}

- POST `/sign/:name`

    This requests the signing service to sign the input data by using the signature key identified by the `:name` parameter. The `:name` parameter is appended to the URL that accesses the signing service. It can contain only unreserved characters as defined by section 2.3 of [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986). The authentication token for the signature key is passed to a `POST /sign` request in the HTTP `Authorization` request header.

    The request body contains the input data to be signed. Requests created by TKE CLI plug-in and Terraform commands also include a parameter that identifies SHA-512 as the hash algorithm to be used when generating the signature. The following is an example of the request body:

    ```json
    {
      "hash_algorithm":"sha2-512",
      "input":"<base64 encoded string of data to be signed>"
    }
    ```

    This request returns the signature that is generated over the input data using the specified signature key. The following is an example of the response body:

    ```json
    {
      "signature": "<base64 encoded string of binary data (ASN.1 DER encoded struct of integers R and S)>"
    }
    ```
    {: codeblock}

## Configuring the TKE CLI plug-in to use the signing service
{: #configure-tke-cli-for-signing-service}

Instead of using signature key files that are stored on your workstation for signing commands, configure the TKE CLI plug-in to use signature keys that are provided by your signing service by completing the following steps:

1. Set the `TKE_SIGNSERV_URL` environment variable on your workstation to the URL and port number where your signing service is running.

    After you set the `TKE_SIGNSERV_URL` environment variable, it indicates that you are using a third-party signing service for signature keys. In this case, the TKE `sigkey` commands don't perform any actions. These commands include `ibmcloud tke sigkeys`, `ibmcloud tke sigkey-add`, `ibmcloud tke sigkey-rm`, and `ibmcloud tke sigkey-sel`.
    {: note}

2. Create a file named `SIGNSERVKEYS` in the subdirectory that is identified by the `CLOUDTKEFILES` environment variable.

    This file is expected to be a JSON string representing an array that lists valid signature keys for signing commands. Each array entry must contain a `key` field and can optionally include a `token` field. The `key` field identifies a particular signature key. The `token` field authorizes use of the key. The signing service determines how the key identification and authentication token are defined. If you don't specify the `token` field in the `SIGNSERVKEYS` file, you will be prompted to enter the token value when you run TKE CLI plug-in commands, which is more secure than directly providing it in the file.

    The following lists some examples of the `SIGNSERVKEYS` file:

    - Example 1:

      ```json
      [{"key":"first-key","token":"token-for-first-key"}]
      ```

      This example specifies a single valid signature key and its authentication token. Because the token is specified, you will not be prompted to enter it when the signature key is used.

    - Example 2:

      ```json
      [{"key":"first-key"},{"key":"second-key"}]
      ```

      This example specifies two valid signature keys that can be used. Because the token is not specified, you will be prompted for the token when you use either key.

    - Example 3:

      ```json
      [{"key":"first-key"},{"key":"second-key","token":"token-for-second-key"},{"key":"third-key"}]
      ```

      This example specifies three valid signature keys that can be used. The token is specified for the second key but not for the first and third key. If you use the first or the third key, you will be prompted for the corresponding token.

    Make sure that the `SIGNSERVKEYS` file contains enough signature keys for installed administrators to meet signature threshold requirements. Otherwise, you are not able to use the signing service to perform TKE actions.
    {: note}

3. Add crypto unit administrators by using the `ibmcloud tke cryptounit-admin-add` command.

    After you set the `TKE_SIGNSERV_URL` environment variable, this command prompts you to enter a signature key identifier and its corresponding access token, as defined by the signing service, to add an administrator.

## What's next
{: #signing-service-whats-next}

- For the information about the subsequent steps to complete the service instance initialization by using the TKE CLI plug-in, see [Initializing service instances by using workstation files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).
- For how to configure Terraform to use a signing service, see [Setting up Terraform for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs).
