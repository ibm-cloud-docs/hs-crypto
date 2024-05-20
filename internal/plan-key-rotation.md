---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-20"

keywords: enable kyok, onboarding hpcs, onboarding hyper protect crypto services, key rotation, key rewrap, dek rewrap

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Planning for key rotation
{: #dek-rewrap}

Rotating root keys is coordinated by {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} and requires adopting services to take the appropriate actions so that customer's existing data encryption keys (DEKs) are protected by the latest key version.
{: shortdesc}

## Impacts to your service
{: #dek-rewrap-impacts}

When a root key is rotated, your service must rewrap all DEKs associated with the rotated key when notified. Your service needs to persist the new wrapped data encryption key (wDEK).

## Before you begin
{: #dek-rewrap-prereqs}

Before rewrapping a data encryption key (DEK), register your cloud resource with {{site.data.keyword.hscrypto}} and
[onboard to Hyperwarp](/docs/get-coding?topic=get-coding-hyperwarp){: external} as a subscriber to {{site.data.keyword.hscrypto}}.

After the BSS team approves your Hyperwarp request, open a new [Hyperwarp Integration Onboarding Request Issue](https://github.ibm.com/kms/customer-issues/blob/master/.github/ISSUE_TEMPLATE/hyperwarp-integration-onboard-request.md){: external} with {{site.data.keyword.hscrypto}}.
{: note}

## Rotating cryptographically protected keys
{: #dek-rewrap-key}

### Step 1: Rotate a root key.
{: #dek-rewrap-rotate-root-key}

You can find the ID for a key in your {{site.data.keyword.hscrypto}} instance by [retrieving a list of your keys](/docs/hs-crypto?topic=hs-crypto-view-keys), or by accessing the UI.

Once you find the key ID, rotate the key by making a call to `POST /api/v2/keys/{id}?action=rotate`.

### Step 2: Check for a Hyperwarp rotation event from {{site.data.keyword.hscrypto}} 
{: #dek-rewrap-receive-hyperwarp-event}

When {{site.data.keyword.hscrypto}} receives a rotate key request from your cloud service, a new key version is created for the key. The new key version becomes available for wrap operations. A Hyperwarp notification is sent to all cloud services that have registrations that are associated with the key.

Your service will only receive Hyperwarp events if the root key has registrations that are associated with it.
{: note}

### Step 3: Take action to rewrap data encryption keys
{: #dek-rewrap-logic}

You can check the state of the rotated key by [viewing the key's metadata](/docs/hs-crypto?topic=hs-crypto-view-key-details#view-key-details-api) and if the key is in the active state, rewrap the DEK.

Rewrap the wDEK by making a call to `POST /api/v2/keys/{id}?action=rewrap`. Store the new wrapped data encryption key (ciphertext) for future encryptions operations so that your data is protected by the latest root key.

Use the [adopters guide](https://github.ibm.com/kms/Adopter_services/blob/master/src/github.ibm.com/skms/hs-crypto/event_processor.go){: external} for more information on processing the Hyperwarp event.
{: note}

### Step 4: Notify {{site.data.keyword.hscrypto}} that DEK rewrap is completed
{: #dek-wrap-notify-hs-crypto}

Services have a timeframe of 4 hours to confirm with {{site.data.keyword.hscrypto}} that all appropriate actions have been taken after receiving a hyperwarp notification.
{: important}

Run the following cURL command to acknowledge the Hyperwarp rotation event:

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

## Monitor logs for an end-to-end key rotation event in activity tracker
{: #dek-rewrap-monitor-logs}

For audit purposes, you can monitor the activity trail of a rotated root key through Activity Tracker. The following example is a successful root key rotation event.

```json
{
  "eventTime": "2020-05-13T19:12:13.32+0000",
  "outcome": "success",
  "message": "Hyper Protect Crypto Services: ack-rotate secret ",
  "action": "kms.secrets.ack-rotate",
  "initiator": {
    "id": "iam-ServiceId-201939482-d276-4dcs-bec8-9999999",
    "name": "Hyper Protect Crypto Services",
    "typeURI": "service/security/account/serviceid",
    "credential": {
      "type": "apikey"
    }
  },
  "target": {
    "id": "crn:v1:bluemix:public:hs-crypto:us-south:a/b3e8ea4428c24cefa34454bd8acccc:dd24cdc0-2c77-40a7-8680-53ccd41d9888:key:d68bf025-e21d-4569-92c0-47bc22aadddd",
    "typeURI": "kms/secrets"
  },
  "observer": {
    "name": "ActivityTracker"
  },
  "reason": {
    "reasonCode": 200,
    "reasonType": "OK"
  },
  "severity": "warning",
  "responseData": {
    "eventAckData": {
      "eventId": "a3afd231-f9d3-4f95-afc5-fc84389fffff",
      "eventType": "rotation",
      "keyState": "DEK_ENABLED",
      "eventAckTimeStamp": "2020-05-13T14:10:12Z",
      "newKeyVersionId": "be729de1-7e3a-46df-9c43-72e38e412333",
      "newKeyVersionCreationDate": "2020-05-13T19:09:42.267695+00:00",
      "oldKeyVersionId": "d68bf025-e21d-4569-92c0-47bc22a54444",
      "oldKeyVersionCreationDate": "2020-05-13T19:09:40.839662+00:00"
    }
  },
  "dataEvent": false,
  "saveServiceCopy": true,
  "correlationId": "214333a-9331-4620-bf00-bbb1a92eeee",
  "logSourceCRN": "v1:bluemix:public:kms:us-south:a/b3e8ea4428c24cefa34454bd8acccc:dd24cdc0-2c77-40a7-8680-53ccd41d9888::"
}
```
{: codeblock}

## Next steps
{: #dek-rewrap-next-steps}

Your service now supports envelope encryption, which one of the core capabilities needed. Next, you can map your protected resource to the root key.

- Head over to implement [crypto-erasure](/docs/hs-crypto?topic=hs-crypto-key-erasure).
