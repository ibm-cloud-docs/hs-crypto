---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-20"

keywords: crypto erasure, erase data, enable KYOK, onboard to hyper protect crypto services, hpcs onboarding, internal, key registration, KYOK

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Planning for crypto erasure
{: #key-erasure}

Erasing data across the cloud is coordinated by {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} and requires adopting services to take the appropriate actions.
{: shortdesc}

KYOK crypto erasure is an effort to bridge the gap and ensure that when a customer deletes the key, it raises service events that invalidates the data encryption keys (DEKs) without deleting the data source itself. 

Benefits of crypto erasure:

- Data becomes unusable up to four hours after deleting keys.
- Evidence is captured showing all DEKs are erased per adopting service.

## Impacts to your service
{: #crypto-erasure-impact}

When a root key is destroyed, your service must stop the use of the DEK when notified.

Your service needs to not attempt to destroy the data, even if the key is destroyed. It is the customer's responsibility to also destroy their data. This is important for accidental key deletion or the ability to restore keys, where having the encrypted data available would be necessary.
{: important}

## Before you begin
{: #crypto-erasure-prereqs}

Before invalidating a data encryption key (DEK), register your cloud resource with {{site.data.keyword.hscrypto}} and
[onboard to Hyperwarp](/docs/get-coding?topic=get-coding-hyperwarp){: external}
as a subscriber to {{site.data.keyword.hscrypto}}.

After the BSS team approves your Hyperwarp request, open a new [Hyperwarp Integration Onboarding Request Issue](https://github.ibm.com/kms/customer-issues/blob/master/.github/ISSUE_TEMPLATE/hyperwarp-integration-onboard-request.md){: external}
with {{site.data.keyword.hscrypto}}.
{: note}

## Deleting cryptographically protected keys
{: #crypto-erasure-key}

### Step 1. Delete a root key
{: #crypto-erasure-delete-root-key}

You can find the ID for a key in your {{site.data.keyword.hscrypto}} instance by [retrieving a list of your keys](/docs/hs-crypto?topic=hs-crypto-view-keys), or by accessing the UI.

Once you locate the key ID, delete the key by making a call to `DELETE /v2/keys`.

### Step 2. Check for a Hyperwarp deletion event
{: #crypto-erasure-receive-hyperwarp-event}

When {{site.data.keyword.hscrypto}} receives a delete key request from your cloud service, the content and data with the key is deleted and the key is moved into the Destroyed state. A Hyperwarp notification is sent to all cloud services that have registrations associated with the key.

Your service will only receive Hyperwarp events if the root key has registrations that are associated with it.
{: note}

### Step 3. Check the state of the deleted key and flush associated data encryption keys (DEKs)
{: #crypto-erasure-check-key-state}

You can check the state of the deleted key by [viewing details about the key](/docs/hs-crypto?topic=hs-crypto-view-key-details#view-key-details-api) and if the key is in the destroyed state, flush the DEKs.

It is mandatory that all DEKs are flushed after deleting a root key.
{: important}

Use the [adopters guide](https://github.ibm.com/kms/Adopter_services/blob/master/src/github.ibm.com/skms/key-protect/event_processor.go){: external} for more information on processing the Hyperwarp event.
{: note}

### Step 4. Notify {{site.data.keyword.hscrypto}} that the associated DEKs have been flushed
{: #crypto-erasure-notify-hs-crypto}

After checking the key state and taking necessary steps, your service can acknowledge the deletion of the root key and key state through the [event API](/apidocs/hs-crypto#eventacknowledge){: external}.

Services have a timeframe of four hours to confirm with {{site.data.keyword.hscrypto}} that all appropriate actions have been taken.
{: important}

Run the following cURL command to acknowledge the Hyperwarp deletion event:

```cURL
curl -X POST \
  https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/event_ack \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'content-type: application/json' \
  -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.event_acknowledge+json",
      "collectionTotal": 1
    },
    "resources": [
      {
        "eventId": "<event_ID>",
        "adopterKeyState": "<key_state>",
        "timestamp": "<time_stamp>",
        "keyStateData": {
          "rewrappedKeyVersion": "<key_version>"
        }
      }
    ]
  }'
```
{: codeblock}

Replace the variables in the example request according to the following table.

| Variable | Description |
| --- | --- |
| `region` | **Required.** The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
| `port` | **Required.** The port number of the API endpoint. |
| `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the `Bearer` value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
| `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
| `event_ID` | **Required.** The identifier for the Hyperwarp event that you want to acknowledge. |
| `key_state` | **Required.** The adopter's reported state of the key at the time of processing the Hyperwarp event. |
| `time_stamp` | **Required.** The date that the Hyperwarp event was processed by the adopter service. The date format follows RFC 3339. |
| `key_version` | **Required if the adopter state is "DEK_ENABLED".** The ID of the key version that was used to rewrap the wrapped data encryption key (wDEK). |
{: caption="Table 1. Describes the variables needed to acknowledge a Hyperwarp event with the API" caption-side="bottom"}

## Monitor logs for an end-to-end key deletion event in activity tracker
{: #crypto-erasure-monitor-logs}

For audit purposes, you can monitor the activity trail of a deleted root key through Activity Tracker. The following is an example of a successful root key deletion event.

**[Need to add an image displaying the activity tracker fields for a successful end to end key deletion event]**

## Next steps
{: #crypto-erasure-next-steps}

Your service is crypto erasure ready! 

- Validate that your service is [KYOK ready](/docs/hs-crypto?topic=hs-crypto-kyok-cheatsheet#kyok-required-actions).
