---

copyright:
  years: 2021, 2023
lastupdated: "2023-07-04"

keywords: change log for tke, updates to tke cli plugin, updates to cert manager cli plugin

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.hscrypto}} CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} command-line interface (CLI) plug-ins.
{: shortdesc}

## {{site.data.keyword.cloud_notm}} TKE CLI plug-in
{: #tke-cli-change-log}

### Version 1.2.3
{: #tke-cli-123}

Version 1.2.3 of the Trusted Key Entry (TKE) CLI was released on 30 June 2021.

Added the `ibmcloud tke failover-enable` command to enable or add failover crypto units after provisioning a {{site.data.keyword.hscrypto}} instance.

## {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} certificate manager CLI plug-in
{: #cert-manager-cli-change-log}

### Version 1.0.0
{: #cert-manager-cli-100}

Version 1.0.0 of the certificate manager CLI plug-in was released on July 2021.

This is the first release of the certificate manager CLI plug-in. You can use it to manage certificates and administrator signature keys for the second layer of authentication in GREP11 or PKCS #11 API connections.

## {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} CLI plug-in
{: #uko-cli-change-log}

### Updates on version 0.0.1
{: #uko-cli-001-update}

The following updates on the {{site.data.keyword.uko_full_notm}} CLI version 0.0.1 was released in June 2023.

- Add the command `hpcs uko associated-resources-for-managed-key` to list resources associated with a managed key
- Add the command `hpcs uko associated-resources-for-target-keystore` to list resources associated with all keys that are activated in a target keystore.
- Update the options for command `hpcs uko managed-keys` to list managed keys.
- Update response examples for all the commands.

### Version 0.0.1
{: #uko-cli-001}

Version 0.0.1 of the {{site.data.keyword.uko_full_notm}} CLI plug-in was released on 3 June 2022.

This is the first release of the {{site.data.keyword.uko_full_notm}} CLI. You can use it to manage vaults, keystores, and keys for {{site.data.keyword.hscrypto}} instances with the {{site.data.keyword.uko_full_notm}} plan.
