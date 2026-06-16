---

copyright:
  years: 2021, 2026
lastupdated: "2026-06-16"

keywords: monitoring, monitor metrics

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Managing metrics
{: #manage-monitoring-metrics}

After you set up your Hyper Protect Crypto Services instance, you can manage Monitoring metrics by using the service API.
{: shortdesc}

## Managing metrics settings
{: #manage-metrics-policy}

Metrics for Hyper Protect Crypto Services instances are an extra policy, with which, you can receive the operational metrics for your Hyper Protect Crypto Services instance. When you enable this policy, Monitoring can be used to monitor any operations that are performed on the resources in your Hyper Protect Crypto Services instance.

Before you enable operational metrics for your Hyper Protect Crypto Services instance, keep in mind the following considerations:

- When you enable metrics for your Hyper Protect Crypto Services instance, metrics are only reported after the time that the policy is enabled.

    Once your metrics policy is enabled, you will see operational metrics for all API requests that occur in your instance after the policy is activated. You will not be able to view any metrics prior to the time that the policy is enabled.

- You need to provision a Monitoring instance first in order to see the metrics.

    You need to [provision a Monitoring instance](/docs/monitoring?topic=monitoring-provision){: external} that is located in the same region as the Hyper Protect Crypto Services instance that you want to receive operational metrics for. After you provision the Monitoring instance, you need to [enable platform metrics](/docs/hs-crypto?topic=hs-crypto-operational-metrics#configure-monitoring).

### Enabling metrics for your Hyper Protect Crypto Services instance with the UI
{: #enable-metrics-instance-policy-ui}
{: ui}

After you create a Hyper Protect Crypto Services instance, provision a Monitoring instance, and enable platform metrics, complete the following steps to enable a metrics policy:

1. [Log in to the UI](https://cloud.ibm.com/){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your IBM Cloud resource list, select your provisioned instance of Hyper Protect Crypto Services.
4. In the UI of the selected service instance, select the **Instance policies** tab in the side menu.
5. In the **Metrics** section, check **Send metrics to IBM Cloud Monitoring** and click **Save policy**.

### Enabling metrics for your Hyper Protect Crypto Services instance with the API
{: #enable-metrics-instance-policy-api}
{: api}

As an instance manager, enable a metrics policy for a Hyper Protect Crypto Services instance by making a `PUT` call to the following endpoint.

 

```
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=metrics
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To enable metrics policies, you must be assigned a _Manager_ IAM role for your Hyper Protect Crypto Services instance. To learn how IAM roles map to Hyper Protect Crypto Services service actions, check out [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Enable a metrics policy for your Hyper Protect Crypto Services instance by running the following `curl` command.

    ```sh
    curl -X  PUT \
     "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=metrics" \
     -H "accept: application/vnd.ibm.kms.policy+json" \
     -H "authorization: Bearer <IAM_token>" \
     -H "bluemix-instance: <instance_ID>" \
     -H "content-type: application/vnd.ibm.kms.policy+json" \
     -d '{
             "metadata": {
                 "collectionType": "application/vnd.ibm.kms.policy+json",
                 "collectionTotal": 1
             },
             "resources": [
                 {
                     "policy_type": "metrics",
                     "policy_data": {
                         "enabled": false
                     }
                 }
             ]
         }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south`, that represents the geographic area where your Hyper Protect Crypto Services instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `IAM_token` | **Required.** Your IBM Cloud access token. Include the full contents of the `IAM` token, including the Bearer value, in the `curl` request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your Hyper Protect Crypto Services instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    {: caption="Describes the variables needed to enable a metrics policy" caption-side="bottom"}

    A successful request returns an HTTP `204 No Content` response, which indicates that your Hyper Protect Crypto Services instance is now enabled for reporting operational metrics.

    This new policy only reports on operations that occur after the policy is enabled.
    {: note}

3. Optional: Verify that the metrics policy is created by browsing the policies that are available for your Hyper Protect Crypto Services instance.

    ```sh
    $ curl -X GET \
        "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=metrics" \
        -H "accept: application/vnd.ibm.kms.policy+json" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>"
    ```
    {: codeblock}

### Disabling metrics for your Hyper Protect Crypto Services instance with the API
{: #disable-metrics-api}
{: api}

As an instance manager, disable an existing metrics policy for a Hyper Protect Crypto Services instance by making a `PUT` call to the following endpoint.

```plaintext
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=metrics
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To enable metrics policies, you must be assigned a _Manager_ IAM role for your Hyper Protect Crypto Services instance. To learn how IAM roles map to Hyper Protect Crypto Services service actions, check out [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Disable an existing metrics policy for your Hyper Protect Crypto Services instance by running the following `curl` command.

    ```sh
    $ curl -X PUT \
        "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=metrics" \
        -H "accept: application/vnd.ibm.kms.policy+json" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>" \
        -H "content-type: application/vnd.ibm.kms.policy+json" \
        -d '{
                "metadata": {
                    "collectionType": "application/vnd.ibm.kms.policy+json",
                    "collectionTotal": 1
                },
                "resources": [
                    {
                        "policy_type": "metrics",
                        "policy_data": {
                            "enabled": false
                        }
                    }
                ]
            }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south`, that represents the geographic area where your Hyper Protect Crypto Services instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `IAM_token` | **Required.** Your IBM Cloud access token. Include the full contents of the `IAM` token, including the Bearer value, in the `curl` request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your Hyper Protect Crypto Services instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    {: caption="Describes the variables needed to disable metrics policies" caption-side="bottom"}

    A successful request returns an HTTP `204 No Content` response, which indicates that the metrics policy is disabled for your service instance.

3. Optional: Verify that the metrics policy is disabled by browsing the policies that are available for your Hyper Protect Crypto Services instance.

    ```sh
    $ curl -X GET \
        "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/instance/policies?policy=metrics" \
        -H "accept: application/vnd.ibm.kms.policy+json" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>"
    ```
    {: codeblock}

## What's next
{: #monitor-metrics-next-steps}

To find out more about configuring your Hyper Protect Crypto Services instance with Monitoring, check out [Monitoring Operational Metrics](/docs/hs-crypto?topic=hs-crypto-operational-metrics).
