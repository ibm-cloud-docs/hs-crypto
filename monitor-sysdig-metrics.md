---

copyright:
  years: 2021, 2023
lastupdated: "2023-02-08"

keywords: measure interactions, metrics, monitoring, operational metrics

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.mon_short}} operational metrics
{: #operational-metrics}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.mon_full_notm}} service to measure how users and
applications interact with {{site.data.keyword.hscrypto}}.
{: shortdesc}

{{site.data.keyword.mon_full_notm}} records data on the operations that occur inside of {{site.data.keyword.cloud_notm}}. With this service, you can gain operational visibility into the performance and health of your applications, services, and platforms. You can use the advanced features to monitor and troubleshoot, define alerts based on API response codes, and design custom dashboards.

For more information about the {{site.data.keyword.mon_short}} service, see the [getting started tutorial for {{site.data.keyword.mon_full_notm}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-getting-started-monitor){: external}.

## What metrics are available for {{site.data.keyword.hscrypto}}?
{: #hpcs-metrics-available}

You can use {{site.data.keyword.mon_short}} to track the type of API requests that are made to your {{site.data.keyword.hscrypto}} instance as well as the latency of the requests.

The following list contains examples of metrics that can be measured in your {{site.data.keyword.mon_short}} dashboard:

- Total requests that are made to your {{site.data.keyword.hscrypto}} instance.
- Successful and failed API requests categorized by API type.
- API request latency over time.
- Total API requests categorized by response code.



## Before you begin
{: #operational-metrics-considerations}

Enabling {{site.data.keyword.hscrypto}} service metrics add new metrics to your {{site.data.keyword.mon_short}} instance. For more
information about {{site.data.keyword.mon_short}} pricing, see [Pricing](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-pricing_plans){: external}.
{: important}

Before you provision an instance of {{site.data.keyword.mon_short}}, consider the following guidance:

- You need to enable the [metrics policy](/docs/hs-crypto?topic=hs-crypto-manage-monitoring-metrics) for your {{site.data.keyword.hscrypto}} instance in order to retrieve operational metrics.
- Other {{site.data.keyword.cloud_notm}} users with `administrator` or `editor` permissions can manage the {{site.data.keyword.mon_short}} service in the {{site.data.keyword.cloud_notm}}. These users must also have platform permissions to create resources within the resource group where they plan to provision the instance.

## Connecting {{site.data.keyword.mon_short}} with {{site.data.keyword.hscrypto}}
{: #connect-monitoring-hpcs}

Your dashboard show metrics for all {{site.data.keyword.hscrypto}} instances that are in the same region as the {{site.data.keyword.mon_short}} instance with an enabled metrics policy.
{: note}

### Configure a {{site.data.keyword.mon_short}} instance for metrics
{: #configure-monitoring}

To enable platform metrics in a region, complete the following steps:

1. [Provision an instance of {{site.data.keyword.mon_short}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-provision){: external} in the region of the {{site.data.keyword.hscrypto}} instance that contains an [enabled metrics policy](/docs/hs-crypto?topic=hs-crypto-manage-monitoring-metrics).
2. Go to the [monitoring dashboard](/observe/monitoring){: external}.
3. Click **Configure platform metrics**.
4. Select the region where the {{site.data.keyword.hscrypto}} instance is created.
5. Select the {{site.data.keyword.hscrypto}} instance in which you would like to receive metrics.
6. Click **Configure**.
7. Your {{site.data.keyword.hscrypto}} instance is now set for platform metrics.

## {{site.data.keyword.hscrypto}} Metrics Details
{: #hpcs-metrics}

You can use the metrics in your Monitoring dashboard to measure the types of requests that are made to your service instance as well as the latency of the requests.

### API Hits
{: #api-hits}

The type and number of API requests that are made to your {{site.data.keyword.hscrypto}} instance. For example, you can track how many API requests that are made by an authorized user by setting an [alert](#set-monitor-alerts). The alert triggers when your Monitoring instance notices a frequent number of `401` status codes that are returned from your {{site.data.keyword.hscrypto}} instance.

| Metadata | Description |
| --- | --- |
| Metric Name | `ibm_hpcs_api_request_gauge` |
| Metric Type | Gauge |
| Value Type | none |
| Segment By | [Attributes for Segmentation](#attributes-for-segmentation) |
{: caption="Table 1. Describes the API Hits metrics."}

## Latency
{: #latency}

The number of time it takes {{site.data.keyword.hscrypto}} to receive an API request and respond to it.

The latency is calculated by getting the average of all requests of the same type that occur within 60 seconds.
{: note}

| Metadata | Description |
| --- | --- |
| Metric Name | `ibm_hpcs_api_latency_gauge` |
| Metric Type | Gauge |
| Value Type | Milliseconds |
| Segment By | [Attributes for Segmentation](#attributes-for-segmentation) |
{: caption="Table 2. Describes the Latency metrics."}

## Attributes for Segmentation
{: #attributes-for-segmentation}

You can filter your metrics by using the following attributes.

| Attribute Name | Description |
| --- | --- |
| `ibm_resource_type` | Supported resource type is `instance`. |
| `ibm_hpcs_response_code` | Response code for the {{site.data.keyword.hscrypto}} service API request. |
| `ibm_scope` | The account, organization, or space GUID associated with the metric. |
| `ibm_ctype` | Public, dedicated, or local. |
| `ibm_location` | Location of the {{site.data.keyword.hscrypto}} service instance. |
| `ibm_service_name` | kms. |
| `ibm_resource` | {{site.data.keyword.hscrypto}} service instance ID. |
| `ibm_hpcs_api` | {{site.data.keyword.hscrypto}} service API name. |
| `ibm_resource_group_name` | Resource group name associated with the {{site.data.keyword.hscrypto}} service instance. |
| `ibm_service_instance_name` | {{site.data.keyword.hscrypto}} service instance name. |
| `ibm_service_instance` | {{site.data.keyword.hscrypto}} service instance ID. |
{: caption="Table 3. Describes the attributes use for segmenting metrics."}


## Default Dashboards
{: #default-dashboards}

You need to configure platform metrics and enable a [metrics policy](/docs/hs-crypto?topic=hs-crypto-manage-monitoring-metrics)
on your service instance in order to view your {{site.data.keyword.hscrypto}} operational metrics dashboard.

### How to find the {{site.data.keyword.mon_short}} dashboard for your {{site.data.keyword.hscrypto}} service instance by using {{site.data.keyword.hscrypto}} console
{: #monitor-dashboard-console}

After you configure your {{site.data.keyword.mon_short}} instance to receive platform metrics, complete the following steps:

1. [Provision your {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-provision#provision-gui).
2. On your {{site.data.keyword.hscrypto}} instance page, click **Actions** > **Monitoring**. 
       On your first usage, you might see a welcome wizard. To advance to the dashboard selection menu, select **Next** and then **Skip** at the bottom of the **Choosing an installation method** page. Accept the prompts that follow. You can then select **{{site.data.keyword.hscrypto}}**.

   The metrics dashboards are available only after metrics have started to be recorded. This might take a few minutes to initialize.
   {: note}

You are now on the {{site.data.keyword.hscrypto}} dashboard, and can start monitoring metrics of the service instance.

### How to find the {{site.data.keyword.mon_short}} dashboard for your {{site.data.keyword.hscrypto}} service instance by using observability page
{: #monitor-dashboard-observability}

After you configure your {{site.data.keyword.mon_short}} instance to receive platform metrics, complete the following steps:

1. Go to the [monitoring dashboard](/observe/monitoring){: external} and find your Monitoring instance that is configured to receive platform metrics.
2. In the **View Dashboard** column, click **View {{site.data.keyword.mon_short}}**.
3. Once you are in the {{site.data.keyword.mon_short}} platform, click **Dashboards** on the side menu.
4. Select **IBM** under the **Dashboard Templates** section.
5. Select **{{site.data.keyword.hscrypto}} - Overview** to view the dashboard for your {{site.data.keyword.hscrypto}} instance.

You are able to see any metrics in your {{site.data.keyword.mon_short}} instance until you enable a metrics policy for your {{site.data.keyword.hscrypto}} instance and make API requests to your {{site.data.keyword.hscrypto}} instance.
{: note}

### How to scope down your metrics by using Metrics Filter Attributes
{: #metrics-filter-attributes}

You can scope down your metrics by using the following scope filters.

| Attribute Name | Description |
| --- | --- |
| `ibmResourceGroupName` | The name of the resource group associated with the {{site.data.keyword.hscrypto}} service instance. |
| `ibmScope` | The account, organization, or space GUID associated with the metric. |
| `ibmServiceInstanceName` | The service instance associated with the metric. |
| `ibmHpcsApi` | The {{site.data.keyword.hscrypto}} API calls associated with the metric. |
{: caption="Table 4. Describes the scope filters for {{site.data.keyword.hscrypto}} metrics."}

Because of {{site.data.keyword.mon_short}} limitations, you are able to see the values in the filters for up to 6 hours at a time. You can manually type in value into scope variables to use scope filters for given time periods.
{: note}

## Setting Alerts
{: #set-monitor-alerts}

You can set alerts on your {{site.data.keyword.mon_short}} dashboard to notify you of certain metrics. To set up alerts, complete the following steps:

1. Click **Alerts** on the side menu.
2. Click **Add Alert** and select **Metric** as the alert type.
3. Select the aggregation and the metric that you would like to be performed on.
4. Select the scope if applicable.
5. Set the metric and time requirements for the alert to trigger.
6. Configure and set up the notification channel and notification interval.
8. Click **CREATE**.

For more information about configuring metric alerts, see [Metric Alerts](https://docs.sysdig.com/en/metric-alerts.html){: external}.
