---

copyright:
  years: 2021, 2024
lastupdated: "2024-10-09"

keywords: security for Hyper Protect Crypto Services, compliance for Hyper Protect Crypto Services, security and compliance for Hyper Protect Crypto Services, rules for Hyper Protect Crypto Services,

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Managing security and compliance with {{site.data.keyword.hscrypto}}
{: #manage-security-compliance}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is integrated with the
{{site.data.keyword.compliance_short}} to help you manage security and
compliance for your organization.
{: shortdesc}



With the {{site.data.keyword.compliance_short}}, you can:


* Define rules for {{site.data.keyword.hscrypto}} that can help to standardize resource configuration.




## Governing {{site.data.keyword.hscrypto}} resource configuration with config rules
{: #govern-crypto}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define configuration rules for the {{site.data.keyword.hscrypto}} instances that you create.



This service only supports the ability to view the results of your configuration scans in the Security and Compliance Center. It is not necessary to set up a collector to use configuration rules.
{: note}


[Config rules](#x3084914){: term} are used to monitor and optionally enforce the configuration standards that you want to implement across your accounts. To learn more about the available properties that you can use to create a rule for {{site.data.keyword.hscrypto}}, review the following table.

| Resource Kind | Property Name | Operator | Value | Description |
| ------------- | ------------- | -------- | ----- | ----------- |
| `instance` | `allowed_network`| `string_equals` | public-and-private<br>private-only | Specifies the type of endpoint the {{site.data.keyword.hscrypto}} instance can be accessed from. Refer to <br>[Managing network access policies](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies) for more information. |
{: caption="Config rule properties and target attributes for {{site.data.keyword.hscrypto}}" caption-side="bottom"}
