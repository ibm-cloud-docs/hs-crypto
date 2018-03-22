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

# Exploiting PKCS#11

The provided API that is available via the ACSP client lib is [PKCS#11 ![External link icon](image/external_link.svg "External link icon")](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){:new_window}.

Applications that support PKCS#11, like openssl, can be used directly with the installed ACSP dynamic library.

End-users can use tools around pkcs11 (like ```pkcs11-tool```) to do key management, crypto operations and managing the keystore.

The following sections explains some PKCS11 terminology.

# Slots, Tokens, PINs
When creating an instance of **Hyper Protect Crypto Services** the keystore that
is provided can be further separated into logical spaces, called "slots" in
PKCS11 terminology. For the available Lite Plan there are 10 slots you can make
use of, e.g. in order to separate different applications or departments, etc.

A "token" is a logical representation of a crypto device, belonging to one slot.
In PKCS11, a token must be present in the slot, i.e. the slot must
be initialized before usage. When the service instance is created, the slots are
already initialized.

For access to any private key the user must use a user PIN, which is unique per
slot.
To get the service exploited quickly for testing purposes, in Experimental stage, there is a default
user PIN setup already: `98765432`


## Changing User PIN and SO PIN
It is highly recommended to change the default user PIN for each used slot.
Also, the admin of the service should change the SO (Security Officer) PIN
likewise, which is also unique per slot.
For the following steps the "pkcs11-tool" is recommended, which is available in
the opensc package in most popular linux distros.

### Changing the User PIN
Enter the command

```
pkcs11-tool --module /usr/lib/libacsp-pkcs11.so --slot <slot-id> --change-pin —login
```
{: codeblock}

and follow the instructions in the command line.

*Example output:*
```
2018.03.19 17:55:43.620 (72) ACSP70000I Log-level was set to INFO
2018.03.19 17:55:43.622 (72) ACSP50600I ACSP PKCS#11 client v1.5.2.1 successfully initialized
2018.03.19 17:55:43.622 (72) ACSP50601I Using acsp-common library version 1.0.9
2018.03.19 17:55:43.622 (72) ACSP50602I Using pkcs#11-wrapper library version 1.0.2
2018.03.19 17:55:43.622 (72) ACSP50519I Connecting to <...> using connection(0)
Logging in to "<...>".
Please enter User PIN:
Please enter the current PIN:
Please enter the new PIN:
Please enter the new PIN again:
PIN successfully changed
2018.03.19 17:56:04.249 (72) ACSP50610I Finalizing ACSP PKCS#11 client
2018.03.19 17:56:04.579 (72) ACSP50523I Closing connection(0)
2018.03.19 17:56:04.580 (72) ACSP50512I Connection manager thread ending
```
{: codeblock}


### Changing the SO PIN
Enter the command
```
pkcs11-tool --module /usr/lib/libacsp-pkcs11.so --slot <slot-id> --change-pin --login --login-type so
```
{: codeblock}

and follow the instructions in the command line.

*Example output:*
```
2018.03.19 18:17:04.444 (99) ACSP70000I Log-level was set to INFO
2018.03.19 18:17:04.445 (99) ACSP50600I ACSP PKCS#11 client v1.5.2.1 successfully initialized
2018.03.19 18:17:04.445 (99) ACSP50601I Using acsp-common library version 1.0.9
2018.03.19 18:17:04.445 (99) ACSP50602I Using pkcs#11-wrapper library version 1.0.2
2018.03.19 18:17:04.445 (99) ACSP50519I Connecting to <...> using connection(0)
Logging in to "<...>".
Please enter SO PIN:
Please enter the current PIN:
Please enter the new PIN:
Please enter the new PIN again:
PIN successfully changed
2018.03.19 18:17:25.917 (99) ACSP50610I Finalizing ACSP PKCS#11 client
2018.03.19 18:17:26.013 (99) ACSP50523I Closing connection(0)
2018.03.19 18:17:26.014 (99) ACSP50512I Connection manager thread ending
```
{: codeblock}
