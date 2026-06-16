---

copyright:
  years: 2021, 2026
lastupdated: "2026-06-16"

keywords: change log for tke, updates to tke cli plugin, updates to cert manager cli plugin

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Hyper Protect Crypto Services CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the IBM Cloud&reg; Hyper Protect Crypto Services command-line interface (CLI) plug-ins.
{: shortdesc}

## IBM Cloud TKE CLI plug-in
{: #tke-cli-change-log}

### Version 1.2.3
{: #tke-cli-123}

Version 1.2.3 of the Trusted Key Entry (TKE) CLI was released on 30 June 2021.

Added the `ibmcloud tke failover-enable` command to enable or add failover crypto units after provisioning a Hyper Protect Crypto Services instance.

IBM Cloud Trusted Key Entry (TKE) CLI and Management Utilities now support IBM 4770 CryptoExpress8S (CEX8S) cards.

## IBM Cloud Hyper Protect Crypto Services certificate manager CLI plug-in
{: #cert-manager-cli-change-log}

### Version 1.0.0
{: #cert-manager-cli-100}

Version 1.0.0 of the certificate manager CLI plug-in was released on July 2021.

This is the first release of the certificate manager CLI plug-in. You can use it to manage certificates and administrator signature keys for the second layer of authentication in GREP11 or PKCS #11 API connections.

## IBM Cloud Hyper Protect Crypto Services Unified Key Orchestrator CLI plug-in
{: #uko-cli-change-log}

### Updates on version 0.0.1 - April 2024
{: #uko-cli-001-update-2404}

The following updates on the Unified Key Orchestrator CLI version 0.0.1 was released in April 2024.

- Remove the parameter `--uko-vault`
- Add key algorithms `ec`, `des`, and `dilithium`
- Update all commands examples and responses
- Add headers for each command

### Updates on version 0.0.1 - June 2023
{: #uko-cli-001-update-2306}

The following updates on the Unified Key Orchestrator CLI version 0.0.1 was released in June 2023.

- Add the command `hpcs uko associated-resources-for-managed-key` to list resources associated with a managed key
- Add the command `hpcs uko associated-resources-for-target-keystore` to list resources associated with all keys that are activated in a keystore.
- Update the options for command `hpcs uko managed-keys` to list managed keys.
- Update response examples for all the commands.

### Version 0.0.1
{: #uko-cli-001}

Version 0.0.1 of the Unified Key Orchestrator CLI plug-in was released on 3 June 2022.

This is the first release of the Unified Key Orchestrator CLI. You can use it to manage vaults, keystores, and keys for Hyper Protect Crypto Services instances with the Unified Key Orchestrator plan.
