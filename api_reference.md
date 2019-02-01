---

copyright:
  years: 2018
lastupdated: "2018-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API Reference
{: #api-reference}

This document is the REST API specification for the {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}. This service is part of the {{site.data.keyword.cloud_notm}} Platform and is used to allow cryptographic operatons.
{: shortdesc}

> _**Disclaimer: This service API is currently available as Experimental version and is subject to change anytime. Refer to the Bluemix terms and conditions for services in Experimental.**_

## Base URL
{: #base_url}

```
https://zcryptobroker.mybluemix.net/crypto_v1/
```
{: codeblock}

The following table shows the operations that you can invoke with the {{site.data.keyword.hscrypto}} API.

<table>
    <tr>
        <th>Operation</th>
        <th>Description</th>
    </tr>
    <tr>
        <td><a href="/docs/services/hs-crypto/reference.html#retrieve_connection_info"><code>GET /instances/{id}</code></a></td>
        <td>Retrieves the connection information for your service instance</td>
    </tr>
    <tr>
        <td><a href="/docs/services/hs-crypto/reference.html#retrieve_config_credentials"><code>GET /credentials/{id}</code></a></td>
        <td>Retrieves the tarball of the ACSP Client Config and Credentials</td>
    </tr>
    <caption style="caption-side:bottom;">Table 1. Available operations for the {{site.data.keyword.hscrypto}} API</caption>
</table>


## Retrieve the connection info
{: #retrieve_connection_info}

Retrieves the connection info that has to be passed into {{site.data.keyword.hscrypto}} by specifying the ID of the Crypto service instance.

<table>
    <tr>
        <th>Parameters</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td><code>Authorization</code></td>
        <td>string</td>
        <td><b>Required.</b> Your {{site.data.keyword.cloud_notm}} (Bluemix) access token.</td>
    </tr>
    </tr>
        <td><code>id</code></td>
        <td>string</td>
        <td><b>Required.</b> The {{site.data.keyword.cloud_notm}} UUID that uniquely identifies the instance.</td>
    </tr>
    <caption style="caption-side:bottom;">Table 2. Parameters for the <code>GET /instances/{id}</code> operation.</caption>
</table>

### Example request
{: get_connection_request}

```cURL
curl -X GET \
    https://zcryptobroker.mybluemix.net/crypto_v1/instances/{id} \
    -H 'Authorization: {access_token}' \
```
{: codeblock}

### Responses
{: get_connection_response}

<table>
    <tr>
        <th>Code</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>200</td>
        <td>
            <p>The instance connection info was successfully retrieved.</p>
            <p><b>Example value</b></p>
            <p><pre class="screen">{
    "instance_id": "...",
    "kmkConnectionInfo": "...",
    "keyStoreMode": "read-write"
}</pre></p>
        </td>
    </tr>
    <tr>
        <td>401</td>
        <td>Your access token is invalid or does not have the necessary permissions to access this instance.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>The instance could not be found. Verify that the instance ID specified is valid.</td>
    </tr>
    <tr>
        <td>500</td>
        <td>
            <p>{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} is currently unavailable. Your request could not be processed. Please try again later.</p>
            <p>If the problem persists, note the input and output of this attempt and contact <a href="https://watson.service-now.com/wcp">{{site.data.keyword.cloud_notm}} support</a>.</p>
      </td>
    </tr>
    <caption style="caption-side:bottom;">Table 3. Response descriptions for the <code>GET /instances/{id}</code> operation.</caption>
</table>

## Retrieve the Client Config and Credentials
{: #retrieve_config_credentials}

Retrieves the tarball of ACSP Client Config and Credentials by specifying the ID of the Crypto service instance.

<table>
    <tr>
        <th>Parameters</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td><code>Authorization</code></td>
        <td>string</td>
        <td><b>Required.</b> Your {{site.data.keyword.cloud_notm}} (Bluemix) access token.</td>
    </tr>
    </tr>
        <td><code>id</code></td>
        <td>string</td>
        <td><b>Required.</b> The {{site.data.keyword.cloud_notm}} UUID that uniquely identifies the instance.</td>
    </tr>
    <caption style="caption-side:bottom;">Table 4. Parameters for the <code>GET /credentials/{id}</code> operation.</caption>
</table>

### Example request
{: get_credentials_request}

```cURL
curl -X GET \
    https://zcryptobroker.mybluemix.net/crypto_v1/credentials/{ID} \
    -H 'Authorization: <access_token>' \
```
{: codeblock}

Replace the variables in the example request according to the following table.

### Responses
{: get_credentials_response}

<table>
    <tr>
        <th>Code</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>200</td>
        <td>
            <p>The instance client config tarball was successfully retrieved. Default download filename is <code>acsp_client_config.tar</code>.</p>
            <p><b>Example value</b></p>
            <p><pre class="screen">TBU</pre></p>
        </td>
    </tr>
    <tr>
        <td>401</td>
        <td>Your access token is invalid or does not have the necessary permissions to access this instance.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>The instance could not be found. Verify that the instance ID specified is valid.</td>
    </tr>
    <tr>
        <td>500</td>
        <td>
            <p>{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} is currently unavailable. Your request could not be processed. Please try again later.</p>
            <p>If the problem persists, note the input and output of this attempt and contact <a href="https://watson.service-now.com/wcp">{{site.data.keyword.cloud_notm}} support</a>.</p>
      </td>
    </tr>
    <caption style="caption-side:bottom;">Table 5. Response descriptions for the <code>GET /credentials/{id}</code> operation</caption>
</table>
