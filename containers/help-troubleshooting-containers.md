# Troubleshooting

The topics about troubleshooting {{site.data.keyword.uko_short}} problems provide a variety of information that can help you when you have problems associated with the {{site.data.keyword.uko_short_wp}} product. IBM® Support personnel might ask you to refer to troubleshooting information when they help you with a specific problem.

_Troubleshooting_ is a systematic approach to solving a problem. The goal of troubleshooting is to determine why something does not work as expected and how to resolve the problem.

The first step in the troubleshooting process is to describe the problem completely. Problem descriptions help you and the IBM technical-support representative know where to start to find the cause of the problem. This step includes asking yourself basic questions:

- What are the symptoms of the problem?
- Where does the problem occur?
- When does the problem occur?
- Under which conditions does the problem occur?
- Can the problem be reproduced?

## Enable Tracing
To enable tracing in EKMF Web, update `server.env` to specify 
 
`TRACE_SPEC=com.ibm.ccc.*=ALL:com.ibm.crypto.*=all:com.ibm.websphere.security.*=all:*=info:com.ibm.ws.security.*=ALL:com.ibm.ws.webcontainer.*=all:com.ibm.wsspi.webcontainer.*=all:HTTPChannel=all:GenericBNF=all:zos.native.03=all`
 
Trace output will be written to `trace.log` in the same directory as the `messages.log` and `http_access.log` files. 

## Troubleshooting information needed by IBM when reporting errors
The following files should be provided to IBM when reporting issues with EKMF Web:
 - jvm.options, 
 - server.env
 - $WLP_OUTPUT_DIR/ekmfweb/logs/messages.log
 - $WLP_OUTPUT_DIR/ekmfweb/logs/trace.log
 - $WLP_OUTPUT_DIR/ekmfweb/logs/http_access.log

Where `$WLP_OUTPUT_DIR` is defined in `server.env`.

The following additional information is also needed help in troubleshooting
 - Description of what was done when encountering the issue, including the time it happened
 - Screenshots of the issue (when possible)

## Why does the {{site.data.keyword.uko_short}} application not start as expected? 

After I installed and configured the {{site.data.keyword.uko_short}} Liberty server and issued the start command, the server does not start. 

**What’s happening**

You have followed [the documentation](install-liberty-server.md) but the server does not start. 

**Why it’s happening**

There are multiple reasons that could cause the Liberty not starting. You will need to investigate further.  

**How to fix it**

Look in the `messages.log` file which is located in the directory you specified in the `WLP_OUTPUT_DIR` parameter in `server.env` for indications on what is missing or possibly incorrectly configured. 

In some cases your web browser log might also have more information. It is sometimes required to clear the browser cache and cookies, when moving from one release to the next.

In some cases the following directories are blocking for the Liberty server recovery function. If so simply delete them as they are auto-created on startup:
* `$WLP_USER_DIR/servers/ekmfweb/logs`
* `$WLP_USER_DIR/servers/ekmfweb/tranlog`
* `$WLP_USER_DIR/servers/ekmfweb/workarea`

## Why is my connection to the {{site.data.keyword.uko_short}} Agent failing due to KMGPARM &WEBCLIENT not defined?

I'm trying to [connect {{site.data.keyword.uko_short}} to a KMG keystore](setting-up-for-pe-keys.md) but the connection fails. 

**What’s happening**

The `messages.log` shows an error stating 

```
KMGPARM &WEBCLIENT not defined in {{site.data.keyword.ekmf_short}} Agent task or user not authorized.
```

**Why it’s happening**

The error is happening because of a missing RACF authorization. The [{{site.data.keyword.uko_short}} Agent security definition](install-security-agent.md) describes the need for defining the &WEBCLIENT parameter when using {{site.data.keyword.uko_short}}. The parameter has to define which user ID {{site.data.keyword.uko_short}} will use as Agent client id (and granted correct RACF access) to connect to the {{site.data.keyword.uko_short}} Agent. If it's undefined a default user is assumed, which most likely doesn't have the correct access and the resulting error is:

```
E Error during connection setup. KMGPARM & WEBCLIENT not defined in {{site.data.keyword.ekmf_short}} Agent task or user not authorized.
```

**How to fix it**

The solution is to define the parameter as described in the [{{site.data.keyword.uko_short}} Agent security definition](install-security-agent.md), restart the {{site.data.keyword.uko_short}} Agent and restart the {{site.data.keyword.uko_short}} Liberty Server.


## Why is my connection to the {{site.data.keyword.uko_short}} Agent failing due to Host User is NOT permitted to invoke host task ?

I'm trying to [connect {{site.data.keyword.uko_short}} to a KMG keystore](setting-up-for-pe-keys.md) but the connection fails. 

**What’s happening**

The `messages.log` states

```
37,4,0, DKMS Host User is NOT (RACF) permitted to invoke host task (KMGPTRAN)
(Corresponding to the selected IP address/IP port).
```

**Why it’s happening**

This is because the user ID defined to run the Liberty Server is not granted `READ` access to the RACF profile `KMG.EKMF.KMGPRACF.<task-user>` in class FACILITY where `<task-user>` is the user ID running the {{site.data.keyword.uko_short}} Agent task. Grant this access and restart the Liberty Server to solve the issue.

```
E CWWKS2907E: SAF Service IRRSIA00_CREATE did not succeed because user <user-id> has insufficient authority to access APPL-ID EKMFWEB. SAF return code 0x00000008. RACF return code 0x00000008. RACF reason code 0x00000020.
E CWIML4537E: The login operation could not be completed. The specified principal name <user-id> is not found in the back-end repository. 
```

In this case, the `<user-id>` that was trying to log on does not have access to the `EKMFWEB` profile in the `APPL`class. 

Note that for {{site.data.keyword.uko_short}} versions from 3.1.0.2, the APPL-ID can be specified in the server.env `SAF_PROFILE_PREFIX` parameter. The default, however, is still EKMFWEB. 

**How to fix it**

Grant access for the `<user-id>` to the `EKMFWEB` profile in the `APPL`class (or the value specified for the `SAF_PROFILE_PREFIX` parameter) as described in the [security definitions for {{site.data.keyword.uko_short}} Liberty Server](install-security-wlp.md)

## Why does my browser log show timezone issues?

An error that can be shown in browser log is related to having different timezones on the workstation and the z/OS. 

**What’s happening**

No error shows on the screen, but observing the browser log, will show the following warning:

```
authorizedCallback Validation, iat rejected id_token was issued too far away from current time
authorizedCallback, token(s) validation failed, resetting
```

**Why it’s happening**

This happens in case the machine where the web browser runs has a different time compared to the z/OS system where the {{site.data.keyword.uko_short}} application is installed. 

**How to fix it**

Adjust machine to automatically use the correct timezone and ensure time is correctly set, then try to log on again.

## Why do I get a JCCA UnsatisfiedLinkError when I try to generate the Web Identity Key?

When attempting to generate the Web Identity Key, an error occurs.

**What’s happening**

The messages.log shows the following error:

```
JCCA Exception msg : jcca16_64 (Not found in java.library.path)
JCCA Exception String : java.lang.UnsatisfiedLinkError: jcca16_64 (Not found in java.library.path)
```

**Why it’s happening**

This is either because the proper ICSF FMID has not been linked to libjcca16\_64.so or because the libjcca16\_64.so file was not in the expected directory. 

**How to fix it**

Verify that the link command was indeed executed in the correct directory as described in the [{{site.data.keyword.uko_short}} Liberty setup](install-liberty-server.md) and that both the FMID file and the libjcca16\_64.so file were in this same directory. 


## Why do I have performance issues in {{site.data.keyword.uko_short}}?

{{site.data.keyword.uko_short}} is running slower than expected. 

**What’s happening**

There can be multiple reasons leading to a slowdown in performance. 

**Why it’s happening**

You can attempt a few things to find out what is happening. 

**How to fix it** 

Try the following:

* In case you have unpacked the .war files, pack them again with ZIP to have a compressed .war file
* move the compressed .war files to a `READ ONLY` mounted ZFS (on `$WLP_USER_DIR/servers/ekmfweb/apps`)
* add the following options to the `jvm.options` file:
   * `-Xcompressedrefs`
   * `-Xquickstart`
   * `-Xjit:noResumableTrapHandler`

## Why is the Db2 Native Library Not Found

**What’s happening**

EKMF Web cannot find the Db2 native library or mismatched jar/native library version

**Why it’s happening**

A misconfiguration of EKMF Web or Db2 means that EKMF Web isn’t looking for the library files in the correct location. 

**How to fix it**

Validate that the DB2_PRODUCT_PATH parameter in server.env points to the correct Db2 Product path. 
EKMF Web expects to find db2jcc4.jar at $DB2_PRODUCT_PATH/jdbc/classes and libdb2jcct2zos4_64.so at $DB2_PRODUCT_PATH/jdbc/lib.

Use a USS console to list the native libraries and run the command below

```
ls -l $DB2_PRODUCT_PATH/jdbc/lib
```

Where `$DB2_PRODUCT_PATH` is defined in server.env. The output should like the listing below

```
erwxrwxrwx   1 BPXROOT  83     8 Jun 13  2017 libdb2jcct2zos.so -> DSNAQJL2
erwxrwxrwx   1 BPXROOT  83     8 Jun 13  2017 libdb2jcct2zos4.so -> DSNAJ3L2
erwxrwxrwx   1 BPXROOT  83     8 Jun 13  2017 libdb2jcct2zos4_64.so -> DSNAJ6L2
erwxrwxrwx   1 BPXROOT  83     8 Jun 13  2017 libdb2jcct2zos_64.so -> DSNAQ6L2
```

Each `libdb2jcc...` file points to a module. These modules are loaded from the z/OS Db2 installation specified by the `STEPLIB` in the EKMF Web startup JCL. Verify that the STEPLIB is correct and that the referenced modules are present in the `STEPLIB`. 

## Why are there SQL Errors in messages.log

**What’s happening**

SQL errors can happen if the structure of the database isn’t as expected. 

**Why it’s happening**

You may have missed updates to the database as part of an upgrade of EKMF Web

**How to fix it**

Make sure you’ve run all the DDLs provided by EKMF Web. 

## Why does EKMF Web fail to save the AES Cipher keys KEK Label
When attempting to save the administration settings, an error occurs.

**What’s happening**

When saving key labels on the Administration page, EKMF Web responds with an error:
“Error saving resource AES CIPHER keys KEK label: Error during wrapping AES key with RSA KEK.”
Further, the messages.log contains errors

```
[11/23/22 14:20:30:075 GMT] 00000033 m.ccc.ekmf.web.domain.settings.EkmfWebAesCipherKeyKekSetting E Error setting KEK label to EKMF.CIPHER.KEK.
com.ibm.ccc.ekmf.web.domain.keys.services.crypto.CryptoServiceException: Error during wrapping AES key with RSA kek
Caused by: java.security.spec.InvalidKeySpecException: java.security.NoSuchProviderException: JCE cannot authenticate the provider IbmCcaCryptoProvider
Caused by: java.security.NoSuchProviderException: JCE cannot authenticate the provider IbmCcaCryptoProvider
Caused by: java.util.jar.JarException: file:/SYSC1/var/ekmfweb/ekmfweb/workarea/org.eclipse.osgi/84/data/cache/com.ibm.ws.app.manager_104/.cache/WEB-INF/lib/ccc-crypto-api-4.0.0-beta.2.jar is not signed by a trusted signer.
 
[11/23/22 14:20:30:147 GMT] 00000033 ccc.ekmf.web.domain.settings.services.DefaultSettingsService E Error with setting ekmf.web.kek.aes.label:EKMF.CIPHER.KEK.
java.util.prefs.BackingStoreException: Error during wrapping AES key with RSA kek
```

EKMF Web has attempted to use functionality from a signed JCE provider. The JVM fails to authenticate the provider and prevents EKMF Web from performing the key wrapping with an AES key. 
As a result, EKMF Web tries alternate wrappings but ultimately fails. 

**Why it’s happening**

The JCE provider is signed by a key with a certificate that is unknown to the JVM. 

**How to fix it**

Update java to the minimum required version, specified by the [program requirements](install-requirements.md), to get a JVM that has the new certificate. 

## Why does EKMF Web Return the User to the Welcome Screen After login


**What’s happening**

After successful login, EKMF web does not proceed to the keys/key template pages but returns the user back to the pre-login welcome screen. 
This may be because the authentication token (JWT) that was created at login, is only valid in the future. 

**Why it’s happening**

The time of the affected client system is ahead of the time set on the EKMF Web server. This causes the authentication token to be valid in the future. Relative to the EKMF Web server, the authentication token is outside its validity period and is therefore rejected. 

**How to fix it**

Adjust the time on the affected client system to be in-sync with the time of the EKMF Web server. 
Synchronizing both systems to the same external (NTP) time is recommended.

# Why Does the User See Acccess Denied
EKMF Web displays a message, in the upper-right corner of the page, saying Access Denied. 


**What’s happening**

EKMF Web checked the user’s access and determined that the user did not have sufficient permissions to perform the requested action. 

**Why it’s happening**

The user is lacking READ permission to one or more EJBROLE resource profiles. 

**How to fix it**

Determine the missing EJBROLE resource profile(s) and use RACF to grant the user READ access to the relevant resource profile(s).

# Why do I fail to see the changes to my key in Azure Key Vault?
{: #troubleshoot-azure-delay}
{: troubleshoot}
{: support}

After you use {{site.data.keyword.uko_full_notm}} to change the state or installation status of a key in Azure Key Vault, you fail to see the changes in the Azure UI.
{: shortdesc}

The activated key in Azure Key Vault is not updated after you change the key state or activation status in {{site.data.keyword.uko_full_notm}}.
{: tsSymptoms}

When you make changes to a managed key in {{site.data.keyword.uko_full_notm}}, it can take up to 2 minutes to reflect the changes in the Azure UI.
{: tsCauses}

Wait for 2 minutes and refresh the Azure UI to see the changes.
{: tsResolve}

# Why can't I create internal keystores?
{: #troubleshoot-create-internal-keystores}
{: troubleshoot}

When you try to add more internal KMS keystores, an error occurs.
{: shortdesc}

You receive the following error message when you try to add more internal KMS keystores:
{: tsSymptoms}

- From UI:

    > Adding keystore failed. The service was not able to add keystore `<keystore_ID>`.

- From API:

    > The operation on the keystore has failed. 
    
For a single service instance, you can create a maximum of 50 internal KMS keystores. You have reached the limits.
{: tsCauses}

Empty and delete an existing keystore so that you can create a new one.
{: tsResolve}

# Why can't I create vaults?
{: #troubleshoot-create-vault}
{: troubleshoot}
{: support}

You are not able to create a vault through either the {{site.data.keyword.hscrypto}} user interface or the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

You might receive an error message similar to one of the following messages when you create a vault:
{: tsSymptoms}

>  The service was not able to create vault "vault-name" or the vault "vault-name" is not created.

It might be caused by one of the following reasons:
{: tsCauses}

* You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions.

* The master key rotation is in progress. 

Try the following solutions: 
{: tsResolve}

* Verify with your administrator that you're assigned the _Vault Administrator_ role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-uko-manage-access#uko-service-access-roles).
* Try to create the vault again after the master key rotation is complete. For more information, see [Master key rotation](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro).

# Why can't I delete vaults?
{: #troubleshoot-delete-vault}
{: troubleshoot}

You are not able to delete vaults by using either UI or API.
{: shortdesc}

You try to delete a vault, but it fails with the following message:
{: tsSymptoms}

> The service was not able to delete vault `<vault_name>` because it still contains some keys or keystores.

If you want to delete a vault, you need to delete all managed keys, and delete or disconnect from all keystores that are managed in the vault first. The Delete function is available for empty vaults only. 
{: tsCauses}

Verify with your administrator that you're assigned [the correct role](/docs/hs-crypto?topic=hs-crypto-manage-access#roles) in the applicable resource group or service instance. And then, delete all managed keys, and delete or disconnect from all keystores that are managed in the vault, and try again.
{: tsResolve}

# Why can't I destroy managed keys?
{: #troubleshoot-destroy-managed-keys}
{: troubleshoot}

You deactivate a managed key first. However, when you try to change the key state to Destroyed, an error occurs.
{: shortdesc}

You receive the following error message when you click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Destroyed** from the UI:
{: tsSymptoms}

```
The service was not able to destroy key `<key_ID>`. The requested key has been deactivated within the last 4 hours.
```
{: screen}

The managed key was deactivated less than 4 hours ago. A managed key can be destroyed only after it is deactivated for more than 4 hours.
{: tsCauses}

Wait until it reaches 4 hours, and then try destroying the managed key again by following the same procedure.
{: tsResolve}

# Why can't I distribute keys to Azure Key Vault?
{: #troubleshoot-import-azure-key}
{: troubleshoot}
{: support}

After I create an Azure Key Vault key using {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}, I can't distribute the key to an external keystore of type Azure Key Vault.
{: shortdesc}

After you create a key in {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} and distribute it to a keystore of Azure Key Vault, you cannot find the key that is listed in the connected Key Vault instance in the Azure cloud or use it for encryption.
{: tsSymptoms}

You might have accidentally deleted a key named `EKMF-BYOK-KEK-FOR-IMPORT` in the Azure Key Vault instance that you connect to. You can distribute keys to your Azure Key Vault only if a key named `EKMF-BYOK-KEK-FOR-IMPORT` exists in the Azure Key Vault instance. By default, this key is automatically created when you successfully connect to your Azure Key Vault instance. 
{: tsCauses}

Create a key from the Azure Key Vault UI based on the following key settings. And then, activate and distribute keys that you create from the {{site.data.keyword.hscrypto}} UI to keystores again. For detailed instructions, see [Editing key details with the UI](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
{: tsResolve}


| Parameter | Value |
| --------- | ----- |
| Options   | Generate Key Encryption Key for Importing HSM-protected Keys |
| Name      | `EKMF-BYOK-KEK-FOR-IMPORT` |
| Key type  | RSA-HSM |
| Enabled   | Yes     |
{: caption="Key settings" caption-side="bottom"}



## Why do I get a message that my key has been modified while I was editing?

You performed an action on a key that failed, for example trying to sync it in the keystores. After that you tried to change the key state to `deactivated`, but it fails. 

**What’s happening**

During deactivation, you get a message saying "Deactivating key failed. Key 'name_of_the_key' cannot be deactivated because it has been modified while you were editing. Try loading the keys again by using the refresh button." But there is no refresh button. 

**Why it’s happening**

The key has not been refreshed in the UI. Even though the sync action failed, it changed the key's ETag. 

**How to fix it**

This bug will be addressed in a future release. Until then the workaround is to close the key details window and open it again. This should fetch the latest ETag of the key and allow to disable it. 

## Why do I get a warning, that my OpenAPI third-party APIs are not visible?

You get a warning message during startup in the server messages.log

**What’s happening**

```
CWWKO1613W: The OpenAPI specification third-party APIs are not visible by the OpenAPIWebProvider{contextRoot}.
```

**Why it’s happening**

{{site.data.keyword.uko_short}} uses the [WebSphere Liberty health check](https://www.ibm.com/docs/en/was-liberty/nd?topic=features-microprofile-health-31) as endpoints for the [health ckeck](system-status.md). This means that the health check is not available in the OpenAPI explorer.		

**How to fix it**

This warning can be ignored. If you want to remove it from messages.log and route them to `trace.log` instead, you can specify the following parameter in your `server.env`:

```
LOGGING_HIDE_MESSAGE=SRVE9967W,CWWKO1613W,CWWKS4001I
```

Note that you are overriding the default value (`LOGGING_HIDE_MESSAGE=SRVE9967W`), therefore it is important to add `SRVE9967W`. 

## Why do I get a warning, that my application has not started within a certain amount of seconds?

You get a warning message during startup in the server messages.log

**What’s happening**

```
CWWKZ0022W: Application ekmf-rest-api has not started in 30.002 seconds.
```

**Why it’s happening**

There is a default time out of 30 seconds in liberty for all applications. If the application takes longer to load, a warning is issued. 

**How to fix it**

Check, whether the application has started at a later point in time. Look for a message similar to `CWWKZ0001I: Application ekmf-rest-api started in 35.933 seconds.` If you find a message, that the application has started, you can ignore the warning. 

## Why am I getting warned, that isNullAllowed is reset to false?

You get a warning message during startup in the server messages.log

**What’s happening**

```
CWWJP9991W: [eclipselink.metadata] isNullAllowed is reset to false in org.eclipse.persistence.mappings.AggregateObjectMapping[basicProperties] because the aggregate has a (possibly nested) target foreign key mapping
```

**Why it’s happening**

This is an error message of the JPA (Java persistence provider) 

**How to fix it**

The warning does not affect the operation of the product. An issue has been created to address the warning. 


## Why do I get an error about a missing properties file?

You get a warning message during startup in the server messages.log

**What’s happening**

Even though the `EkmfWeb.properties` is specifying a correct path, you get the following error message 

```
CWWKF0017E: Product install path $(product_install_path) specified in product properties file EkmfWeb.properties could not be found.
```

**Why it’s happening**

This is caused by a packaging error: the “features” sub directory is missing under `$(product_install_path)/lib`. 

**How to fix it**

The message disappears after creating directory. A future product fix will address this issue.

## Why do I get a warning about illegal reflective access?

You get a warning message during startup in the server messages.log

**What’s happening**

You see one or more messages similar to the following: 

```
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by com.ibm.io.async.AbstractAsyncChannel$StartPrivilegedThread (file:/TRESA1/usr/lpp/liberty_zos/22.0.0.9/lib/com.ibm.ws.chnnelfw_1.0.68.jar) to field java.nio.Buffer.address
WARNING: Please consider reporting this to the maintainers of com.ibm.io.async.AbstractAsyncChannel$StartPrivilegedThread
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
```

**Why it’s happening**

You are using an older level of WebSphere Liberty. 

**How to fix it**

The warning does not affect product operation. To address the issue, upgrade to WebSphere Liberty version 23.0.0.7 or later, where the usage of illegal reflective access operations has been fixed and the warning message disappears. 

## Why do I get an error that access to CSNDPKT is denied?

You get an error message during startup in the server messages.log

**What’s happening**

```
Access Denied (8/90) for CCA Verb CSNDPKT called with rule array [CKM-RAKW].
```

**Why it’s happening**

During server startup, a test is run whether RSA key wrap (CCA Verb CSNDPKT ) can be executed which requires access to the [CSFSERV Resource CSFPKT](install-security-wlp.md#install-security-liberty-icsf) and the [ACP's '03B6'X and '03B7'X being enabled](install-security-wlp.md#install-security-liberty-acps). By default, they will be disabled. 

**How to fix it**

Enable the ACP's '03B6'X and '03B7'X. If this is not possible, you can still use the product with the following limitation: You can only create software based keys for Azure and Google, not hardware protected keys.


## Why do I get a message, that there is no valid TSO userid?

During the startup of the agent, you get an informational message. 

**What’s happening**

In the agent log, you see the following messages:

```
IKJ56644I NO VALID TSO USERID, DEFAULT USER ATTRIBUTES USED      
READY                                                           
KMGPTRAN  
```

**Why it’s happening**

This is a standard MVS message for a user without a TSO segment.

**How to fix it**

This message is informational and can be ignored. 


## Why do I get a warning that no ports were configured?

You get an warning message during startup in the server messages.log

**What’s happening**

```
CWWKT0015W: No ports were configured for endpoint httpEndpointWithMutualAuth. The endpoint has been disabled.
```

**Why it’s happening**

The server.xml file still contains an unused `httpEndpoint` element. 

**How to fix it**

The warning can be ignored and will be addressed in a future patch. 

## Why am I getting CWWKS4001I messages in my logs?

Your server's `messages.log` shows `CWWKS4001I` informational messages and you wonder whether you need to react to them.  

**What’s happening**

You will see a message similar to the following in `messages.log`: 

```
com.ibm.ws.security.token.internal.TokenManagerImpl
I CWWKS4001I: The security token cannot be validated. This can be for the following reasons
1. The security token was generated on another server using different keys.
2. The token configuration or the security keys of the token service which created the token has been changed.
3. The token service which created the token is no longer available.
```

**Why it’s happening**

This usually happens when a session of a logged on user expires. You can verify this by waiting until your session expires and confirm it correlates with the message being written. 

**How to fix it**

You can ignore these messages. If you want to remove it from messages.log and route them to `trace.log` instead, you can specify the following parameter in your `server.env`:

```
LOGGING_HIDE_MESSAGE=SRVE9967W,CWWKO1613W,CWWKS4001I
```

Note that you are overriding the default value (`LOGGING_HIDE_MESSAGE=SRVE9967W`), therefore it is important to add `SRVE9967W`. 

## Why do I get SRVE0321E and Error 500: javax.servlet.ServletException?

You try to start {{site.data.keyword.uko_short}} V3 but the logon panel is not showing. 

**What’s happening**

Your browser shows

```
Error 500: javax.servlet.ServletException: Filter [SecurityHeadersFilter]: com.ibm.ccc.web.filters.SecurityHeadersFilter was found, but is corrupt:
```

In the messages.log you find 

```
com.ibm.ws.webcontainer.filter
E SRVE0321E: The [SecurityHeadersFilter] filter did not load during start up.
javax.servlet.ServletException: Filter [SecurityHeadersFilter]: com.ibm.ccc.web.filters.SecurityHeadersFilter was found, but is corrupt:
```

**Why it’s happening**

You are trying to run {{site.data.keyword.uko_short}} V3 with Java V8. 

**How to fix it**

Check the [system prerequisites](install-requirements.md) and update to the required version of Java. 

## Why am I told that my certificate is invalid or not found?

You have correctly defined all required certificates and specified them in the server.env, but you are still getting errors. 

**What’s happening**

Your `messages.log` file has an error similar to the following: 

```
An FFDC Incident has been created: "java.lang.ClassNotFoundException: com.ibm.crypto.provider.safkeyring.Handler com.ibm.ws.runtime.util.URLStreamHandlerAdapter parseURL" at ffdc_24.01.09_18.37.05.0.log
E CWPKI0024E: The UKOCERT certificate alias specified by the attribute serverKeyAlias is either not found in KeyStore safkeyring:///UkoKeyRing or it is invalid.
```

**Why it’s happening**

From Java 11 the location of the keystore has been changed from `safkeyring` to `safkeyringjce`. WebSphere Liberty has been updated to automatically addresss this change. 

**How to fix it**

Check the [system prerequisites](install-requirements.md) and update to the required version of WebSphere Liberty. 

## Why do I get an SQL error for SYSTOOLS.JSON2BSON?

Even though you granted access to all tables and views, you still see SQL errors in the server `messages.log`.

**What’s happening**

The log shows messages similar to the following: 

```
DB2 engine SQL error, SQLCODE = -471, SQLSTATE = 55023, error tokens = SYSTOOLS.JSON2BSON;
00E7900C ERRORCODE=-471, SQLSTATE=55023
Error Code: -471
Call: INSERT INTO T_TEMPLATES_API_V4 (uuid, API_MODEL) VALUES (?, SYSTOOLS.JSON2BSON(?))
```

**Why it’s happening**

`SYSTOOLS.JSON2BSON` is indicating that one of the prerequisites, either the [Db2 Accessories Suite](https://www.ibm.com/support/pages/ibm-db2-accessories-suite-zos420) or the [Db2 Utilities Suite](https://www.ibm.com/docs/en/db2-for-zos/13?topic=packaging-db2-utilities-suite-zos) are not available. 

**How to fix it**

Check the [system prerequisites](install-requirements.md) and ensure all required software is available. 



