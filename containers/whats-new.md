# What's New? 
{: #whats-new}

{{site.data.keyword.uko_full_notm}} v3.1 provides efficient and security-rich centralized key management for IBM z/OS® data set encryption on IBM Z® (also referred to as Pervasive Encryption) as well as the Cloud.

## Release notes for v3.1.0.4
{: #whats-new-3104}

New features and improvements:
* New ‘Getting started’ page
* Improvements to the ‘Overview’ page
* Simplified creation flows while working in the context of a vault, and even more simplified flow while creating a key off of a template.
* RSA algorithm support for KMG keystore type keys.
* Microsoft Double Key Encryption (DKE) keystore support
* Private endpoint (TLS proxy) support for Azure key vaults.
* Face-lifted and more streamlined confirmation modals
* New information tiles for Data sets, Audit log, API and Administration pages
* New - ‘System status’ tab under the Administration page
* Support for IBM WebSphere Application Server Liberty. For more information, see [WebSphere Application Server Liberty 24.0.0.7](https://www.ibm.com/support/pages/node/7159859?myns=swgother&mynp=OCSSD28V&mynp=OCSSEQTP&mynp=OCSSAW57&mync=E&cm_sp=swgother-_-OCSSD28V-OCSSEQTP-OCSSAW57-_-E).


## Release notes for v3.1.0.3
{: #whats-new-3103}

New features and improvements: 

* Improvements of the administration page.
* Adaptation of the new default Google delete period time from 1 day to 30 days. 
* The url to the Open API is changed from `/api/explorer` to `/openapi/ui`.
* Fix the issue of the Message Authentication Code (MAC) verification with non-system keys.

Upgrades:

* netty to 4.1.110.Final
* netty.refactor to 1.1.18
* bouncy-castle to 1.78.1 
* azure.identity to 1.12.2

Vulnerabilities:

* Issue 4014: Address CVE-2024-35255 vulnerability
* Issue 3993: Address CVE-2024-30172, CVE-2024-29857, and CVE-2024-30171 vulnerability
* Issue 3809: Address CVE-2024-29025 vulnerability

## Release notes for v3.1.0.2
{: #whats-new-3102}

New features and improvements:

* Introduction of the server.env parameter `SAF_PROFILE_PREFIX` which replaces the hardcoded value of `EKMFWEB` and affects the security definitions in the EJBROLE and APPL classes
* Removal of the limitation to 50 vaults
* The vault administrator role has been added to the documentation and workflows
* The missing views for the tables `T_VAULTS_API_V4`, `T_TEMPLATES_API_V4`, `T_KEYS_API_V4`, and `T_KEYSTORES_API_V4` have been created
* Compatibility with the latest version of WebSphere Liberty (24.0.0.2)


## Release notes for v3.1.0.1
{: #whats-new-3101}

New features and improvements:

* Key templates can now define key instance naming schemes in the user interface. In previous versions this was only possible using [custom properties](specifying-custom-properties.md). Note that the use of system placeholders in the main key naming scheme and the key instance naming scheme will have an impact on [whether a key can be rotated](uko-introduce-key-rotation-onprem.md). In addition, you can decide for some type of keystores, whether previous versions of the key should be deactivated upon key rotation. 
* The `environment` and `location` fields are obsolete and have been removed from Azure keystores. 
* Keys can now be [filtered](uko-search-key-list-onprem.md) by template alignment status.
* Keys can now be [filtered](uko-search-key-list-onprem.md) by whether the key in keystore is in sync with what is expected.
* Better support for native rate limitation for operations in different clouds.
* [Integration between {{site.data.keyword.uko_short}} and EKMF Workstation](uko-workstation-integration.md) allows for seamless management of Pervasive Encryption and AWS AES keys between the two products, including data integrity calculations. The [installation instructions](install-workstation.md) have been updated to include the steps required for shared use of EKMF Workstation and {{site.data.keyword.uko_short}}. 
    * [Use filters](uko-search-key-list-onprem.md) to display keys that can be edited by {{site.data.keyword.uko_short}} (Edit) or that are View only (secure room required) because they are managed by EKMF Workstation 
    * Multi-zone key distribution; a key created on the EKMF Workstation that spans multiple instances, zones and application names are now fully supported.
    * Support for specifying the key zone used by {{site.data.keyword.uko_short}} (defaults to `I`)
    * Support for specifying the key zone used by EKMF Workstation (defaults to `2`)
* [Migration](install-migration.md) to v3.1.0.1 can be done manually or using workflows.

Vulnerabilities:

* Issue 2596: Address CVE-2022-45868 vulnerability
* Issue 3125: Address CVE-2023-44487 vulnerability

Upgrades:

* netty to 4.1.100.Final
* reactor-netty-http to 1.1.12
* h2 to 2.2.220


## Release notes for v3.1.0.0
{: #whats-new-3100}

**Application switcher**

With {{site.data.keyword.uko_short}} v3.1 you can decide between the prevoius EKMF Web V2.1 application and the new {{site.data.keyword.uko_short}} v3.1 application. To switch between the applications, click on the switch icon ![Switch icon](/icons/switcher.svg "Switcher") in the top right corner. 

**z/OSMF workflows**

{{site.data.keyword.uko_short}} provides [z/OSMF workflows]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO) for installation, migration and other basic tasks.

**Data set dashboard**

Proactively manage your data set encryption deployment with an enterprise view of which data sets are encrypted and which keys are in use.

**Security-rich key generation**

Generate keys with IBM FIPS 140-2 level 4 certified CryptoExpress cards on IBM Z for hardware generated keys. 

[Learn more](https://www.ibm.com/products/pcie-cryptographic-coprocessor)

**Policy-based key generation**

Easily create your key templates to generate keys that adhere to your internal policies such as enforcing key naming conventions.

**Role-based access and dual control**

Comply with security standards with role-based access that defines functions for each role, and enforce dual control requiring 2 or more people to activate EKMF.

**External RESTful API**

Seamlessly integrate key management with your business processes.

[Set up keys for GKLM](https://www.ibm.com/docs/en/ekmf-web/2.1?topic=creation-setting-up-gklm)

**Advanced auditability and compliance**

Provide auditors with consolidated key management logs for all keys managed.

[Audit events in EKMF Web](https://www.ibm.com/docs/en/ekmf-web/2.0?topic=auditing-events)

**Key rotation**

Rotate managed keys, including master keys, on demand to comply with your policy requirements.

**Multi-tenancy**

Leverage secure repositories with fine-grained access controls known as vaults to enable multi-tenancy and self-service key management.

**Secure room operation**

Set up UKO for z/OS in combination with Enterprise Key Management Foundation Workstation (EKMF Workstation) for secure room operation.

[Learn more](https://www.ibm.com/downloads/cas/0PJMBR5N)

An EKMF Workstation and UKO for z/OS coexistence compatibility fix is planned for EKMF Workstation Q4 releases (9.5.4 and 10.2.4) expected end of December.
Requests for earlier delivery as an interim Fix Pack to existing versions will be considered on request.

**Notices**

- Key rotation for PE keys works only using the RESTful APIs. UI update will be provided in the first fixpack.
- CCA Firmware update is required to enable and support Azure and Google with the `CKM-RAKW` export keyword. This will require update to CCA 7.4.46 or 8.1.75 (and 7.5/8.2)

