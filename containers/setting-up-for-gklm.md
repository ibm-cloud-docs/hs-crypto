# Setting up keys for GKLM

{{site.data.keyword.uko_full}} ({{site.data.keyword.uko_short}}) provides centralized key management. You can use {{site.data.keyword.uko_short}} to store the master key in ICSF. This master key protects all the keys and certificates that are stored in the IBM® Security Guardium® Key Lifecycle Manager database. 

You can configure {{site.data.keyword.uko_short}} for the new and existing installations of IBM Security Guardium Key Lifecycle Manager.

**Important:** You cannot configure IBM Security Guardium Key Lifecycle Manager servers from different deployments or setups with the same {{site.data.keyword.uko_short}} server. Such a configuration might cause unrecoverable data loss. You can do so in a replication setup.

## Deployment Scenario

In the deployment scenario presented below, there are:
- Two GKLM instances
- Two {{site.data.keyword.uko_short}} instances running the key management APIs; primary and DR
- Four {{site.data.keyword.uko_short}} instances running the crypto connect APIs; primary and failover for each GKLM instance
- Four {{site.data.keyword.uko_short}} Agents for distributing keys for each of the crypto connect API instances

![{{site.data.keyword.uko_short}} Deployment Scenario with GKLM](../images/gklm-crypto-connect.png "{{site.data.keyword.uko_short}} and GKLM with DR and Failover"){: caption="{{site.data.keyword.uko_short}} and GKLM" caption-side="bottom"} 

## Create key template for GKLM

You need to set up a key template for use with GKLM on {{site.data.keyword.uko_short}}. 

Perform the following steps to create a template:
1. Select **Vaults** &gt; **Key templates** from the menu bar. 
1. On the Key template page, click the **Create** button on the right.
1. Specify the following settings on the template creation panels. Use the **Previous** and **Next** buttons to navigate between the panels and click **Save** at the end to confirm your changes.

| Panel name | Setting | Description | 
|-----|-----| -----|
| Vault | Vault | Choose the DEFAULT vault. 
| Target Keystores | Keystore type | Select KMG Agent. |
| Target Keystores | Keystore group | Select a connection to a KMG keystore. For GKLM, at least one connection to a KMG Agent installed and running on a z/OS LPAR is required. Refer to [Connecting to keystores](uko-connect-external-keystores.md) for details. |
| Key template properties | Key template name | Enter the template name. The templates names can consist of up to 30 uppercase alphabetic characters, numerals, and hyphens. For example, you can call your template `TEAMEKMF`. |
| Key template properties | Naming scheme | Enter the pattern of the key names. All keys that are generated with this template have a name that follows this pattern. For GKLM, the fixed value `GKLM.MKEY.<ALIAS>` is required. |
| Key template properties | Key type | For GKLM you must select `CIPHER` as key type. |
| Key template properties | Algorithm | Select AES |
| Key template properties | Length | Select 256 |
| Key template properties | State | Set the Key state to `Active`. |
| Key template properties | Advanced properties | Specify `{"keystores": [{"cca_key_words": ["ANY-MODE"]}]}` |
| Summary | | Review your settings and click **Save** |
{: caption="Settings of a key template for GKLM" caption-side="top"} 

## {{site.data.keyword.uko_short}} settings in GKLM env config file

Follow the [GKLM documentation](https://www.ibm.com/docs/en/sgklm/4.2.1?topic=ekmfwuisgklm-configuring-security-guardium-key-lifecycle-manager-use-ekmf-web) for configuring IBM Security Guardium Key Lifecycle Manager to use {{site.data.keyword.uko_short}}.


## Access roles

The RACF user ID that the GKLM mTLS client certificate maps to must be authorized to the `${SAF_PROFILE_PREFIX}` application (class `APPL`) and the following access roles in the `EJBROLE` class: 

* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:generate`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:read`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:write`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:delete`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:distribute`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:non_existing:generate`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:pre_activation:activate`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:pre_activation:update`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:pre_activation:mark_compromised`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:active:deactivate`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:active:install`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:active:uninstall`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:active:mark_compromised`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:deactivated:destroy`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:deactivated:mark_compromised`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:destroyed:remove`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:destroyed_compromised:remove`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keys:destroyed:mark_compromised`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.templates:read`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.templates:write`
* `${SAF_PROFILE_PREFIX}.ekmf-rest-api.keystores:read`
* `${SAF_PROFILE_PREFIX}.crypto-connect.operations:data:encrypt`
* `${SAF_PROFILE_PREFIX}.crypto-connect.operations:data:decrypt`

For {{site.data.keyword.uko_short}} versions pre 3.1.0.2, the `${SAF_PROFILE_PREFIX}`=EKMFWEB. From v3.1.0.2, the `${SAF_PROFILE_PREFIX}` can be configured in the server.env. The default, however, is still EKMFWEB. 

You can find a sample script in the `${UKO_GKLM_CLIENT_GROUP}` group in the [{{site.data.keyword.uko_short}} z/OSMF installation workflows]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO/workflows/ukoserver/extensions/defineGklmAccess.rexx). For more details on the access roles, see [Application access and roles](install-security-roles.md).

## mTLS for GKLM
{{site.data.keyword.uko_short}} must be enabled for mTLS.

Clients that wish to connect with only mTLS need to include header `ekmf-mtls: true` with each request. 
E.g.

    curl 
    --cert client.cer \ 
    --key client.key \ 
    --request GET 'https://ekmfweb.example.com/api/v2/keys' \
    --header 'Accept: application/json' \
    --header 'ekmf-mtls: true'
