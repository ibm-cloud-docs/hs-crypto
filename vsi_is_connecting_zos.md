---

copyright:
  years: 2021

lastupdated: "2021-08-11"

keywords: connecting, zos, s390x

subcollection: hs-crypto


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:table: .aria-labeledby="caption"}

# Connecting to z/OS instances - DRAFT
{: #vsi_is_connecting_zos}

After you created your z/OS instance, you can connect to it by completing these steps.
{: shortdesc}

## Locating floating IP address
{: #locating-floating-ip-address}

If you haven’t associated a floating IP to your instance, follow Step 3 and Step 4
in [Creating an instance by using the CLI](/docs/vpc?topic=vpc-creating-virtual-servers-cli#create-instance-cli) to request a floating IP address to associate to your instance.
{: note}

If you need to locate your floating IP address for the instance to which you want to connect, complete the following steps. If you already know your floating IP address, skip to [Getting connected](#getting-connected).


1. You need to identify your floating IP ID before you can locate your floating IP address. Run the following command to identify your floating IP ID:

   ```
   ibmcloud is instance-network-interfaces <INSTANCE_ID> <NETWORK_INTERFACE_ID> --json
   ```
   {: pre}

   For this example, you'd see a response similar to the following output:

   ```
   "floating_ips": [
           {
               "crn:v1:mydomain:public:vpc:us-south:a/c4cxxxc10xx54xxx9e2xxx59xxx3fa0f::floating_ip:12345x67-8901-234x-5678-9xx01xx23x4x",
               "href": "https://us-south.myaccount.cloud.ibm.com/v1/floating_ips/12345x67-8901-234x-5678-9xx01xx23x4x",
               "id": "0738-12345x67-8901-234x-5678-9xx01xx23x4x",
               "name": “my-zos-instance”
           }
       ]
   ```
   {: screen}  

2. Now that you have your floating IP ID, you can locate your floating IP address by running the following command.

   ```
   ibmcloud is ip <FLOATING_IP_ID>
   ```
   {: pre}

   For this example, you'd see a response similar to the following output:

   ```
   ID               0738-12345x67-8901-234x-5678-9xx01xx23x4x
   Address          123.45.678.90
   Name             my-zos-instance
   Target           primary(1xx2x34x-.)
   Target Type      intf
   Target IP        12.345.6.78
   Created          1 week ago
   Status           available
   Zone             us-south-1
   Resource Group   -
   Tags             -
   ```
   {: screen}

Optionally, you can locate the floating IP address that is associated to the instance to which you want to connect through the {{site.data.keyword.cloud_notm}} console.
{: tip}

## Getting connected
{: #getting-connected}

You can connect to your z/OS instance with the following approaches:

* Use any 3270 terminal emulator that's available on your platform. The z/OS TSO listener port is 23. Therefore, the command line on your Linux platform is like `x3270 <floating ip> 23`, or you can use the command line application `c3270` that runs in a terminal without X, such as `3270 <floating ip> 23`. The default user name is `IBMUSER` and the password is 'welcome0'.

   By default, the security profile for VPC blocks port 23. The recommendation is to utilize the VPN for VPC to establish a private network connection to the environment and then connect to port 23. The VPN for VPC part is still in the works.
     {: note}

* Use the SSH utility and your private key.

   1. To connect to your instance, use your private key and run the following command:

      ```
      ssh -i <path to your private key file> root@<floating ip address>
      ```
      {: pre}

      You receive a response similar to the following example. When prompted to continue connecting, type `yes`.

      ```
      The authenticity of host 'xxx.xxx.xxx.xxx (xxx.xxx.xxx.xxx)' can't be established.
      ECDSA key fingerprint is SHA256:abcdef1Gh/aBCd1EFG1H8iJkLMnOP21qr1s/8a3a8aa.
      Are you sure you want to continue connecting (yes/no)? yes
      Warning: Permanently added 'xxx.xxx.xxx.xxx' (ECDSA) to the list of known hosts.
      ```
      {: screen}

      You are now accessing your server.

   2. Enter zPDT commands as normal Linux line commands to direct zPDT commands to the z/OS instance. For example, run the `oprmsg` commandas as the `runz` user if the z/OS instance is running. For more information about the zPDT commands, see [IBM zPDT Guide and Reference](https://www.redbooks.ibm.com/redbooks/pdfs/sg248205.pdf).

   3. When you are ready to end your connection, run the following command:

      ```
      # exit
      ```
      {: pre}
