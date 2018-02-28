---

copyright:
  years: 2018
lastupdated: "2018-02-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}

> _**Disclaimer: The {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is still in experimental phase. Therefore, this service might change anytime, including the service name, configuration steps, etc.**_

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} for short) helps you encrypt your data at the safety and security level of System z cryptography in a convenient and cost competitive manner. 
{:shortdesc}

{{site.data.keyword.hscrypto}} brings the security and integrity of System z to the cloud. The same state-of-the-art cryptographic technology that banks and financial services rely on is now offered to cloud users via {{site.data.keyword.cloud_notm}}. Behind the cloud, {{site.data.keyword.hscrypto}} offers network addressable hardware security modules (HSMs) to provide safe and secure cryptography via PKCS#11 application programming interfaces. {{site.data.keyword.hscrypto}} is also accessible by several popular programming languages like Java, JavaScript, Swift, and so on.

You can access {{site.data.keyword.hscrypto}} via and Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to complete the cryptography.

This tutorial shows you how to provision and configure {{site.data.keyword.hscrypto}}.


## Provisioning the service

You can create an instance of {{site.data.keyword.hscrypto}} from the {{site.dat a.keyword.cloud_notm}} console.

Complete the following steps to provision {{site.data.keyword.hscrypto}}:
1. Log in to your [{{site.data.keyword.cloud_notm}} account ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/).
2. Visit [{{site.data.keyword.cloud_notm}} Experimental Services ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/catalog/labs/) to see the list of services in experimental phase.
3. From the **All Categories** navigation pane on the left, click the **Security** category under **Platform**.
4. From the list of services, click the **HyperSecure Crypto Services** tile.
5. Select the **zCrypto Free Plan**, and click **Create** to provision an instance of {{site.data.keyword.IBM_notm}} CloudCrypto in the account, region, and resource group where you log in.


## Installing ACSP client

Install the ACSP client in your local environment. 
1. Download the [`acsp-pkcs11-client_1.5-3.5_amd64.deb`](http://nginx.bluemixsecurity.com/acsp-pkcs11-client_1.5-3.5_amd64.deb){:new_window} file.  If the downloading doesn't start automatically, right click the link and save it.
2. Run the `acsp-pkcs11-client_1.5-3.5_amd64.deb` file to install the ACSP client.

The installation also includes the ACSP client library.  For more information, see [ACSP client library](client_lib.html).


## Configuring ACSP client

> _**Disclaimer: At the current stage, the CloudCrypto service provides only self-signed certificates.**_
  
You need to configure credentials in your ACSP client to make it operational. 
## Getting credentials
After you provision the {{site.data.keyword.cloud_notm}} HyperSecure Crypto Services instance, download the configuration credentials of ACSP client. 

1. In your {{site.data.keyword.hscrypto}} service instance, select **Manage** from the navigation on the left.
2. On the Manage screen, click the **Download Config** button to download the `acsp_client_credentials.uue` file.
3. Copy the `acsp_client_credentials.uue` file to the `/opt/ibm/acsp-pkcs11-client/config` directory in your local environment.
4. In the `/opt/ibm/acsp-pkcs11-client/config` directory, decode the file with the following command:
       `base64 -D -i acsp_client_credentials.uue -o acsp_client_credentials.tgz`
5. Extract the client credentials file with the following command:
       `tar zxf acsp_client_credentials.tgz`
6. Rename the client configuration file with the following command:
       `mv acsp.properties.client acsp.properties`
7. Change group id of these files with the following command:
       `chown root.pkcs11 *`


Now your ACSP client is operational and your {{site.data.keyword.hscrypto}} is ready to use!
