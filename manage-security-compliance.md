---

copyright:
years: 2020, 2021
lastupdated: "2021-04-27"

keywords: security for Hyper Protect Crypto Services, compliance for Hyper Protect Crypto Services, security and compliance for Hyper Protect Crypto Services, rules for Hyper Protect Crypto Services,

subcollection: hs-crypto

---

{:external: target="_blank" .external}
{:note: .note}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:term: .term}

# Managing security and compliance with {{site.data.keyword.hscrypto}}
{: #manage-security-compliance}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is integrated with the
{{site.data.keyword.compliance_short}} to help you manage security and
compliance for your organization.
{: shortdesc}



With the {{site.data.keyword.compliance_short}}, you can:


* Define rules for {{site.data.keyword.hscrypto}} that can help
  to standardize resource configuration.




## Governing {{site.data.keyword.hscrypto}} resource configuration with config rules
{: #govern-crypto}

As a security or compliance focal, you can use the
{{site.data.keyword.compliance_short}} to
[define configuration rules](/docs/security-compliance?topic=security-compliance-rules){: external}
for the {{site.data.keyword.hscrypto}} instances that you
create.


This service only supports the ability to view the results of your configuration scans in the Security and Compliance Center. It is not necessary to set up a collector to use configuration rules.
{: note}

[Config rules](#x3084914){: term}
are used to monitor and optionally enforce the configuration standards that you
want to implement across your accounts. To learn more about the
available properties that you can use to create a rule for
{{site.data.keyword.hscrypto}}, review the following table.

| Resource Kind | Property Name | Operator | Value | Description |
| ------------- | ------------- | -------- | ----- | ----------- |
| `instance` | `allowed_network`| `string_equals` | public-and-private<br>private-only | Specifies the type of endpoint the {{site.data.keyword.hscrypto}} instance can be accessed from. Refer to <br>[Managing network access policies](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies) for more information. |
| `instance` | `dual_auth_delete`| `is_true`<br>`is_false` | n/a | Require/Disallow enablement of dual authorization to delete keys in the {{site.data.keyword.hscrypto}} instance. Requirement applies to subsequently created keys and will not apply to pre-existing keys. Refer to [Managing dual authorization](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) for more information. |
| `instance` | `key_create_and_import.create_root_key` | `is_true`<br>`is_false` | n/a | Allow/Disallow root keys to be created in the {{site.data.keyword.hscrypto}} instance. Refer to [Managing a key create and import access policy](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess) for more information. |
| `instance` | `key_create_and_import.import_root_key`| `is_true`<br>`is_false` | n/a | Allow/Disallow root keys to be imported into the {{site.data.keyword.hscrypto}} instance. Refer to [Managing a key create and import access policy](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess) for more information. |
| `instance` | `key_create_and_import.create_standard_key` | `is_true`<br>`is_false` | n/a | Allow/Disallow standard keys to be created in the {{site.data.keyword.hscrypto}} instance. Refer to [Managing a key create and import access policy](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess) for more information. |
| `instance` | `key_create_and_import.import_standard_key` | `is_true`<br>`is_false` | n/a | Allow/Disallow standard keys to be imported into the {{site.data.keyword.hscrypto}} instance. Refer to [Managing a key create and import access policy](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess) for more information. |
| `instance` | `key_create_and_import.enforce_token` | `is_true`<br>`is_false` | n/a | Restrict/Allow the import of key material into the {{site.data.keyword.hscrypto}} instance without using an import token. Refer to [Managing a key create and import access policy](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess) for more information. |
| `instance` | `metrics` | `is_true`<br>`is_false` | n/a | Require/Restrict {{site.data.keyword.hscrypto}} instance metrics to be forwarded to instance owner's {{site.data.keyword.monitoringfull}}. Refer to [Managing metrics](/docs/hs-crypto?topic=hs-crypto-manage-monitoring-metrics) for more information. |
| `key` | `dual_auth_delete`| `is_true`<br>`is_false` | n/a | Require/Disallow dual authorization to delete the given key in the {{site.data.keyword.hscrypto}} instance. Refer to [Setting dual authorization policies for keys](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy) for more information.|
| `key` | `rotation.enabled` | `is_true`<br>`is_false` | n/a | Require/Disallow active rotation policy on specified key(s). Refer to [Setting a rotation policy](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy) for more information. |
| `key` | `rotation.interval_month`| `num_equals`<br>`num_not_equals`<br>`num_less_than`<br>`num_less_than_equals`<br>`num_greater_than`<br>`num_greater_than_equals` | 1 ≤ Value ≤ 12 | Specifies the given key's rotation interval (in months). Automatic rotation policies can only be applied to root keys with non-imported material. Refer to [Setting a rotation policy](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy) for more information. |

{: caption="Table 1. Config rule properties and target attributes for {{site.data.keyword.hscrypto}}" caption-side="top"}

To learn more about config rule capabilities, see
[What is a config rule?](/docs/security-compliance?topic=security-compliance-what-is-rule){: external}.
