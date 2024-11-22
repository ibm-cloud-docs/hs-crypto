# Managing your keys with the key management API
{: #managing-your-keys-with-the-key-management-api}

{{site.data.keyword.uko_short}} provides a RESTful API for key management. Every action that can be taken via the Web UI can also be invoked with the RESTful API. Additionally, to facilitate key management for volume encryption using zkey, {{site.data.keyword.uko_short}} supports export of AES `CIPHER` keys under some tightly controlled conditions.

## Interact with the API using the API explorer
{: #interact-with-the-api-using-the-api-explorer}
IBM WebSphere Liberty Server provides a built-in API explorer for documentation of the API, but also to try it out. To use the API explorer, perform the following steps: 

1. Select the **API** menu item and click on the "Read more" link. The API explorer will open in a new window. 
1. Click on the **Authorize** button in the top right corner.
1. Specify your `client_id`. This value has been specified during [configuration](install-liberty-server.md) as `EKMF_OAUTH_CLIENT_ID`.
1. Define your scope by setting check marks for every function that you want to authorize.
1. Click on the `Authorize` button.
1. Click on an operation you authorized for, which will be indicated by a closed lock symbol next to the operation name. 
1. Click on the **Try it out** button. You will now be able to specify your request parameters. 
1. Click **Execute** to send your request. The response will be shown in the Server response section of the operation. 


## Interact with the API using the command line
{: #interact-with-the-api-using-the-command-line}

### Using OAuth token
{: #using-oauth-token}

One way to use the API is to provide an OAuth bearer token, for example by using a cURL command similar to the following example, which saves the token in a variable called BearerToken (we use the `jq` command line tool to extract the token from the response, you can use whatever tool you're comfortable with).

#### Obtaining the OAuth token using passcode
```
BearerToken=$(curl \
  --request POST "https://ekmfweb.example.com/api/v2/system/login" \
  --header "Accept: application/json" \
  --header "Content-Type: application/json" \
  -d '{"userId":"samantha","passcode":"xtNvxqUqQgWnUwUc"}' | jq -r '.authorizationToken')
```

The `userID` is the one you use to log on to {{site.data.keyword.uko_short}} with. It is case sensitive. To get a `passcode`, click on **API** in the menu bar and copy the generated code. 

#### Obtaining the OAuth token using client ID and client secret
```
BearerToken="Bearer $(curl \
  --request POST 'https://ekmfweb.example.com/oidc/endpoint/EkmfOpenIdConnect/token' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode 'grant_type=password' \
  --data-urlencode 'client_id=${UKO_OAUTH_CLIENT_ID}' \
  --data-urlencode 'client_secret=${UKO_OAUTH_CLIENT_SECRET}' \
  --data-urlencode 'username=samantha' \
  --data-urlencode 'password=samanthaspassword' \
  --data-urlencode 'scope=openid profile email' | jq -r .access_token)"
```

**Note:** In the {{site.data.keyword.uko_short}} default configuration, no client secret is used. In this case, just leave `${UKO_OAUTH_CLIENT_SECRET}` empty. If you want to set up a client secret, you need to [adjust the server configuration using the configDropins folder](install-liberty-additional-customization.md) and move `open-id-provider-with-secret.xml` to the `configDropins/overrides` folder. 

You can now perform operations by presenting the bearer token as part of your request, like in the following example, which will return all your keys:

```
curl \
  --request GET "https://ekmfweb.example.com/api/v2/keys" \
  --header "Accept: application/json" \
  --header "Authorization: ${BearerToken}"
```


### Using mTLS
{: #using-mtls}
By far the most secure way to communicate with {{site.data.keyword.uko_short}} is through the use of [mTLS](install-liberty-server.md). Assuming that:
- you have correctly set up and exported keys on {{site.data.keyword.uko_short}} side (via RACF or similar tool), and 
- you have a file named `ekmf-web-client.p12`

#### If your curl supports PKCS#12
You can use the PKCS#12 file directly in the call to `curl` to e.g. get a list of keys:
```
curl \
  --cert-type P12 \
  --cert ekmf-web-client.p12:password-to-pkcs#12 \
  --request GET 'https://ekmfweb.example.com/api/v2/keys' \
  --header 'ekmf-mtls: true' \
  --header 'Accept: application/json'
```
or to create a key using an existing key template named 'EXAMPLE':
```
curl \
  --cert-type P12 \
  --cert ekmf-web-client.p12:password-to-pkcs#12 \
  --request POST 'https://ekmfweb.example.com/api/v2/keys' \
  --header 'ekmf-mtls: true' \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json' \
 -d '{ "templateName": "EXAMPLE", "labelTags": [ { "name": "APP", "value": "DEMO" }, { "name": "ENV", "value": "TEST" } ] }'
```


#### If your curl does not support PKCS#12

First, you need to export the certificate and private key from the PKCS#12 file:
```
openssl pkcs12 -in ekmf-web-client.p12 -out ekmf-web-client.key -nocerts -nodes
openssl pkcs12 -in ekmf-web-client.p12 -out ekmf-web-client.cer -clcerts -nokeys
```

Then you can refer to those files in the call to `curl` to e.g. get a list of keys:
```
curl \
  --cert ekmf-web-client.cer \
  --key ekmf-web-client.key \
  --request GET 'https://ekmfweb.example.com/api/v2/keys' \
  --header 'ekmf-mtls: true' \
  --header 'Accept: application/json'
```

or to create a key using an existing key template named 'EXAMPLE':
```
curl \
  --cert ekmf-web-client.cer \
  --key ekmf-web-client.key \
  --request POST 'https://ekmfweb.example.com/api/v2/keys' \
  --header 'ekmf-mtls: true' \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json' \
 -d '{ "templateName": "EXAMPLE", "labelTags": [ { "name": "APP", "value": "DEMO" }, { "name": "ENV", "value": "TEST" } ] }'
```



