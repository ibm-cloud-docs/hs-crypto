---

copyright:
  years:  2023
lastupdated: "2023-08-10"

keywords: restricting access to Hyper Protect Crypto Services, restricting access to HPCS, HPCS cbr, UKO cbr

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}

This document outlines the process for using context-based restrictions to protect your {{site.data.keyword.hscrypto}} resources. Use this document to prepare your resources for context-based restrictions. {{site.data.keyword.hscrypto}} doesn't offer scoping rules to the control plane in this current phase of implementation.{: .important}

# Protecting {{site.data.keyword.hscrypto}} resources with context-based restrictions
{: #cbr}

Context-based restrictions give account owners and administrators the ability to define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the context of access requests. Access to {{site.data.keyword.hscrypto}} resources can be controlled with context-based restrictions and Identity and Access Management (IAM) policies.
{: shortdesc}

These restrictions work with traditional IAM policies, which are based on identity, to provide an extra layer of protection. Unlike IAM policies, context-based restrictions don't assign access. Context-based restrictions check that an access request comes from an allowed context that you configure. Since both IAM access and context-based restrictions enforce access, context-based restrictions offer protection even in the face of compromised or mismanaged credentials. For more information, see [What are context-based restrictions](/docs/account?topic=account-context-restrictions-whatis).

A user must have the Administrator role on the {{site.data.keyword.hscrypto}} instances to create, update, or delete rules. A user must also have either the Editor or Administrator role on the context-based restrictions service to create, update, or delete network zones. A user with the Viewer role on the context-based restrictions service can add network zones to a rule.
{: note}

Any {{site.data.keyword.cloudaccesstraillong_notm}} or audit log events generated come from the context-based restrictions service, not {{site.data.keyword.hscrypto}}. {{site.data.keyword.hscrypto}} supports audit events only for customer interactions with context-based restrictions-protected platform endpoint calls. {{site.data.keyword.hscrypto}} does not support audit events when you enable context-based restrictions rules on the control plane API for your instances. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor).

To start protecting your {{site.data.keyword.hscrypto}} resources with context-based restrictions, see the tutorial for [Leveraging context-based restrictions to secure your resources](/docs/account?topic=account-context-restrictions-tutorial).

## How {{site.data.keyword.hscrypto}} integrates with context-based restrictions
{: #cbr-overview}

You can create context-based restrictions for the {{site.data.keyword.hscrypto}} instances and specific resources.

### Protecting {{site.data.keyword.hscrypto}} resources
{: #cbr-overview-protect-services}

You can create context-based restrictions rules to protect specific **instances**.

Instance
:   Protects a specific instance. If you include an instance in your context-based restrictions rule, resources in the network zones that you associate with the rule can interact only with resources in that instance. If you use the CLI, you can specify the `--service-instance` option to protect instances in a specific resource group. If you use the UI, you can specify the *Service instance* in the resource attributes.

## Creating network zones
{: #network-zone}

A network zone represents an allowlist of IP addresses where an access request is created. It defines a set of one or more network locations that are specified by the following attributes:

* IP addresses, which include individual addresses, ranges, or subnets.
* VPCs

### Creating network zones in the UI
{: #network-zone-ui}
{: ui}

1. Go to **Manage** > **Context-based restrictions** in the {{site.data.keyword.cloud}} console.
1. Select **Network zones**.
1. Click **Create**.
1. Name your network zone and provide a description.
1. Enter your *Allowed IP addresses.* You can enter a single IP address, a range of IP addresses, or a single CIDR.

   The **Denied IP addresses** field is optional and should include only exceptions that are contained within the IP ranges you provide in the allowed IP addresses field.
   {: note}

1. Choose your *Allowed VPCs*, selecting as many as you like. 

1. **Reference a service**: You can select {{site.data.keyword.hscrypto}} as a source service for context-based restrictions, but not as a target service. For example, you can provision a {{site.data.keyword.hscrypto}} deployment using BYOK from {{site.data.keyword.keymanagementservicefull}}. In this example, {{site.data.keyword.hscrypto}} is the source formation and {{site.data.keyword.keymanagementservicefull}} is the target formation. Then, you would create a network zone with a {{site.data.keyword.hscrypto}} service reference and create a rule associated with the network zone that targets {{site.data.keyword.keymanagementservicefull}}. To add a {{site.data.keyword.hscrypto}} service reference, for *Service Type*, IAM services is autoselected. In the *Service* dropdown, select a specific {{site.data.keyword.hscrypto}} service. If the zone you create is associated with a rule targeting {{site.data.keyword.hscrypto}}, then a service reference is not allowed.

### Creating network zones in the CLI
{: #network-zone-cli}
{: cli}

To create network zones in the CLI, [install the context-based restrictions CLI plug-in](/docs/cli?topic=cli-cbr-plugin). Use the `cbr-zone-create` command to add resources to network zones. For more information, see the [context-based restrictions CLI reference](/docs/account?topic=account-cbr-plugin#cbr-zones-cli).

Create a zone by using a command like:

```sh
ibmcloud cbr zone-create --addresses=1.1.1.1,5.5.5.5 --name=<NAME>
```
{: .pre}

Update a zone by using a command like:
```sh
ibmcloud cbr zone-update <ZONE-ID> --addresses=1.2.3.4 --name=<NAME>
```
{: .pre}

Updating requires the `ZONE-ID`, not the zone name. Use the following command to list your zones and retrieve the relevant `ZONE-ID`:
```sh
ibmcloud cbr zones
```
{: .pre}

The `zone-update` command is an overwrite. Include all of the fields that are required as if you are creating the rule from scratch. If you omit any required fields, the rule overwrites those missing fields as empty, and the rule might fail because some of those fields are required, regardless of whether they are changing the rule. {: .important}

Delete a zone by using a command like:
```sh
ibmcloud cbr zone-delete <ZONE-ID>
```
{: .pre}

## Creating rules
{: #rules}

Rules restrict access to specific cloud resources based on resource attributes and contexts.

{{site.data.keyword.hscrypto}} does not support IPv6 addresses. If an IPv6 address is included, it will be ignored.

### Creating rules in the UI
{: #rules-ui}
{: ui}

1. Go to **Manage** > **Context-based restrictions** in the {{site.data.keyword.cloud}} console.
1. Select **Rules**.
1. Click **Create**.
1. Select **Hyper Protect Crypto Services**.
1. Click **Next**.
1. Scope the rule to **Specific resources**. For more information, see [Protecting {{site.data.keyword.hscrypto}} resources](/docs/hs-crypto?topic=hs-crypto-cbr#cbr-overview-protect-services).
1. Click **Continue**.
1. Define the allowed endpoint types.
   - Keep the toggle set to **No** to allow all endpoint types.
   - Set the toggle to **Yes** to allow only specific endpoint types, then choose from the list.
1. Select a network zone or zones that you have already created, or create a new network zone by clicking **Create**.
   
   Contexts define from where your resources can be accessed, effectively linking your network zone to your rule.
   {: tip}

1. Click **Add** to add your configuration to the summary.
1. Click **Next**.
1. Name your rule.
1. Select how you want to enforce the rule. 
   
   *Report-only* is not available for {{site.data.keyword.hscrypto}}.
   {: important}

### Creating rules in the CLI
{: #rules-cli}
{: cli}

To create rules in the CLI, [install the context-based restrictions CLI plug-in](/docs/account?topic=account-cbr-plugin).

To create a rule in the CLI, you need the appropriate {{site.data.keyword.hscrypto}} `service_name`:
* `Hyper Protect Crypto Services`

Create a rule by using a command like:

```sh
ibmcloud cbr rule-create --enforcement-mode enabled --context-attributes "networkZoneId=<ZONE-ID>" --resource-group-id <RESOURCE_GROUP_ID> --service-name <SERVICE-NAME> --service-instance <SERVICE-INSTANCE> --description <DESCRIPTION>
```
{: .pre}

{{site.data.keyword.hscrypto}} does not currently support **Control plane** as an option.
{: .note}

*Report-only* is not available for {{site.data.keyword.hscrypto}}.
{: .important}

Update a rule by using a command like:

```sh
ibmcloud cbr rule-update <RULE-ID> --enforcement-mode disabled --context-attributes="networkZoneId=<ZONE-ID>" --resource-group-id  <RESOURCE_GROUP_ID> --service-name <SERVICE_NAME>  --description <DESCRIPTION>
```
{: .pre}

The `rule-update` command is an overwrite. Include all of the fields that are required as if you are creating the rule from scratch. If you omit any required fields, the rule overwrites those missing fields as empty, and the rule might fail because some of those fields are required, regardless of whether they are changing the rule. 
{: .important}

Updating requires the `RULE-ID`, not the rule name. Use the following command to list your rules and retrieve the relevant `RULE-ID`:
```sh
ibmcloud cbr rules
```
{: .pre}

Delete a rule by using a command like:
```sh
ibmcloud cbr rule-delete <RULE-ID>
```
{: .pre}

Use `ibmcloud cbr <command> — help` for a full list of options and parameters. For example, `ibmcloud cbr rule-create — help` outputs parameters for rule creation.
{: .tip}

### Creating rules in Terraform
{: #rules-tf}
{: terraform}

To create rules using Terraform, see [IBM Cloud Provider](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs){: external} in the [Terraform Registry](https://registry.terraform.io/){: external}.

To create a rule, you need the appropriate {{site.data.keyword.hscrypto}} `service_name`:
* `Hyper Protect Crypto Services`

The `ibm_cbr_rule` provides a resource for `cbr_rule` and allows a `cbr_rule` to be created, updated, and deleted.

Create a rule by using a command like:
```sh
resource "ibm_cbr_rule" "cbr_rule" {
  contexts {
        attributes {
            name = "networkZoneId"
            value = "559052eb8f43302824e7ae490c0281eb"
        }
        attributes {
               name = "endpointType"
               value = "private"
    }
  }
  description = "this is an example of a rule with one context one zone"
  enforcement_mode = "enabled"
  resources {
        attributes {
            name = "accountId"
            value = "12ab34cd56ef78ab90cd12ef34ab56cd"
        }
        attributes {
              name = "serviceName"
              value = "network-policy-enabled"
        }
        tags {
              name     = "tag_name"
              value    = "tag_value"
        }
  }
}
```
{: pre}

You can import the `ibm_cbr_rule` resource by using `id`, the globally unique ID of the rule.
```sh
terraform import ibm_cbr_rule.cbr_rule 
```
{: pre}

### Verifying your rule
{: #rules-ui-verify}

To verify that your rule is applied, go to the {{site.data.keyword.cloud}} Dashboard and select the relevant instance from your *Resource List*. Within **Recent Tasks**, you see your rule's status.

The task of creating or modifying a rule goes into your instance's task queue. Depending on workload, it might take some time for your rule enforcement to complete.{: .note}
