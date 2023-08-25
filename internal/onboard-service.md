---

copyright:
  years: 2020, 2023
lastupdated: "2023-08-24"

keywords: enable kyok, hyper protect crypto service onboarding, internal, kyok, onboard service, crn token

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# Onboarding your service
{: #onboard-service}

You can enable Keep Your Own Key (KYOK) for your service by integrating with {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Before you begin
{: #onboard-prereqs}

Keep in mind the following list of prerequisites before you continue to step 1.
- You must have an {{site.data.keyword.cloud_notm}} account with access to both the [staging](https://test.cloud.ibm.com/) and [production](https://cloud.ibm.com/) environments.
- You must have a basic understanding of IAM concepts, such as [granting service to service access](/docs/get-coding?topic=get-coding-servicetoservice).

Need help? You can use the [`#hp-crypto-kms` Slack channel](https://app.slack.com/client/T02J3DPUE/CFFC7M3B3){: external} or [raise a support ticket](https://github.ibm.com/ZaaS/zcrypto-support-tickets/issues/new){: external}.
For specific questions about your use case, reach out to Marco Pavone (Architect) or Chris Smith (OM).
{: tip}

## Step 1. Submit a request to onboard your service
{: #submit-request}

To submit an onboarding request, create a new issue in the
[{{site.data.keyword.hscrypto}} GitHub repository](https://github.ibm.com/ZaaS/zcrypto-backlog/issues/new?template=onboard-request.md){: external}.

In the issue, provide the following details:
- The `service-name` that uniquely identifies your service.
- The {{site.data.keyword.hscrypto}} service roles that we must
assign for your service. These service roles will define the scope of access for
your service when it accesses {{site.data.keyword.hscrypto}} on
the user's behalf. Review the
[Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles)
to determine which roles match your use case. The **Reader** service role provides the necessary permissions for
performing wrap, unwrap, and list key actions.
- The environment, staging, or production, where you need to onboard your service. After you onboard in the staging environment, you must submit another request to onboard in production.

When you submit a request, the {{site.data.keyword.hscrypto}} team will update the service registrations to include access for your service. Feel free to connect with us on the `#hyper-protect-crypto` Slack channel if you need help during this process.

## Step 2. Create a CRN token
{: #retrieve-s2s-token}

To grant access between your service (the "source" service) and {{site.data.keyword.hscrypto}} (the "target" service), we recommend using a CRN token. This process requires a single extra request to IAM.

Do not propagate the user's token through the system because this not good security hygiene. Instead, use a CRN token from IAM.
{: important}

As you can see in the following table, the subsequent API calls take a CRN token.

API call | Target | Token Type
---- | ---- | ----
[List KMS instances](#discover-kms-instances) | GHoST | CRN Token
[Get KMS endpoints](#discover-kms-instances) | GHoST | CRN Token
[Register protected resources](/docs/hs-crypto?topic=hs-crypto-register-protected-resources) | {{site.data.keyword.hscrypto}} | CRN token
Wrap or unwrap DEKs | {{site.data.keyword.hscrypto}} | CRN token

See the [#iam-adopters Slack channel](https://ibm-cloudplatform.slack.com/archives/C0NLB2W3B/p1516206027000901){: external} or see [IAM service to service documentation](/docs/get-coding?topic=get-coding-servicetoservice) for official steps and guidance.

## Step 3. Discover KMS instances
{: #discover-kms-instances}

Before you use the {{site.data.keyword.hscrypto}} API to protect customer data, you need to know how to perform two important actions:
- Gather a list of all {{site.data.keyword.hscrypto}} instances that your customer has access to view, which is set by an IAM policy with Platform Viewer role.
- Discover {{site.data.keyword.hscrypto}} regional endpoints for each instance.

Listing {{site.data.keyword.hscrypto}} instances gives your customers the choice of which root keys protect your service's resource and which type of KMS provider. The instances that contain root keys might be in any MZR - even different from the resource's location. We allow this so that customers can centrally manage keys in a region that the customer desires, while data is protected and stored elsewhere. Customers choose and own the responsibility of the location of their keys.

Both list and discover actions can be achieved by using the platform Tagging API (that is, GHoST) and a **CRN token** from earlier. Your team can search for all KMS instances that are associated with a given user by specifying `sub_type` instead of service name. This is done by querying Global Search and Tagging (GhoST).

```cURL
curl -X POST
    'https://api.global-search-tagging.cloud.ibm.com/v2/resources/search?limit=50&account_id=<account_ID>'
    -H 'Authorization: Bearer <token>'
    -H 'Content-Type: application/json'
    -d '{
    "query": "(type:resource-instance AND doc.sub_type:kms)"
    }'
```
{: codeblock}

Although you can create your {{site.data.keyword.hscrypto}}
service instances by using a user token, and then use the same token to run your
query in GhoST, we recommend that you use your CRN token, which exchanges your
customer's token with one that represents your service.
{: tip}

The following JSON output shows an example service instance. From the response,
adopting teams can see which endpoint hosts a particular KMS service instance.

```json
{
    ...,
    "doc": {
    ...,
    "id": "crn:v1:bluemix:public:hs-crypto:us-south:a/80e35ac1582a2b1a7b633e6107f9295a:67be47c6-cac0-415d-b298-0e6d45d6cb51::",
    "sub_type": "kms",
    "extensions": {
      ...,
      "endpoints": {
        "public": "<public endpoint for the instance>",
        "private": "<optional - private network endpoint for the instance>"
      }
    },
    ...
    },
    ...
}
```
{: codeblock}

Adopting services must not use the public endpoint as a redundant path in the
event the private endpoint has availability issues because of customer
expectation for security in motion. If you believe this is needed, raise
it during your CISO baseline review.
{: important}

If your service receives both a public and private endpoint in the response,
favor the private endpoints over public endpoints to enable security by default.
To use the private endpoints, your service needs to be
[VRF enabled](/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud).

After the endpoints are known, you can store the _url:port_ information to be
used later, when you're ready to perform envelope encryption on your data
encryption keys.
{: tip}

Because your instances are known, you can use the
[{{site.data.keyword.hscrypto}} key management service API](https://cloud.ibm.com/apidocs/hs-cryptot#list-keys){: external} to reveal
which keys can be used to secure your DEKs. Before you can do that, a root key
needs to be created.

## Step 4. Submit a request to integrate with Hyperwarp
{: #integrate-hyperwarp}

Hyperwarp is IBM cloud's unified publishing, subscribing, and processing event pipeline. To enable event publication and subscription with Hyperwarp and integrate your service with {{site.data.keyword.hscrypto}}, you need to first [register your service with Hyperwarp](/docs/get-coding?topic=get-coding-hyperwarp#hyperwarp-registration), and then create a new issue in the
[{{site.data.keyword.hscrypto}} GitHub repository](https://github.ibm.com/ZaaS/zcrypto-backlog/issues/new?template=hyperwarp-onboard-request.md) to enable Hyperwarp integration with {{site.data.keyword.hscrypto}}.

In the issue, provide the following details:
- The `Hyperwarp subscriber ID` that you registered your service with Hyperwarp.
- The environment, staging, or production, where you need to onboard your service. After you onboard in the staging environment, you must submit another request to onboard in production.
- The `service_name` that uniquely identifies your service.
- The `regions` where you want to onboard your service with {{site.data.keyword.hscrypto}}; for example, `us-south`.

After you submit a request, the {{site.data.keyword.hscrypto}} team will enable your service's Hyperwarp integration with {{site.data.keyword.hscrypto}}. Feel free to connect with us on the `#hp-crypto-kms` Slack channel if you need help during this process.

## Next steps
{: #onboard-next-steps}

Now that you have an instance and can discover it, you can [try out the service](/docs/hs-crypto?topic=hs-crypto-get-started) and then [start key registration](/docs/hs-crypto?topic=hs-crypto-register-protected-resources).

If you want to onboard your service with other key management services, such as {{site.data.keyword.keymanagementserviceshort}}, see [Onboard your service with {{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-onboard-service).
