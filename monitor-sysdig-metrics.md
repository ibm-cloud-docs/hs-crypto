---

copyright:
  years: 2021
lastupdated: "2021-03-12"

keywords: measure interactions, metrics, sysdig, operational metrics

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.mon_short}} operational metrics
{: #operational-metrics}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.mon_full_notm}} service to measure how users and
applications interact with {{site.data.keyword.hscrypto}}.
{: shortdesc}

{{site.data.keyword.mon_full_notm}} records data on the operations that occur inside of {{site.data.keyword.cloud_notm}}. This service allows you to gain operational visibility into the performance and health of your applications, services, and platforms. You can use its advanced features to monitor and troubleshoot, define alerts based on API response codes, and design custom dashboards.

For more information about the {{site.data.keyword.mon_short}} service, see the [getting started tutorial for {{site.data.keyword.mon_full_notm}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-getting-started-monitor){: external}.

## What metrics are available for {{site.data.keyword.hscrypto}}?
{: #hpcs-metrics-available}

You can use {{site.data.keyword.mon_short}} to track the type of API requests being made to your {{site.data.keyword.hscrypto}} instance as well as the latency of the requests.

The following contains examples of metrics that can be measured in your {{site.data.keyword.mon_short}} dashboard:

- Total requests being made to your {{site.data.keyword.hscrypto}} instance
- Successful and failed API requests categorized by API type
- API request latency over time
- Total API requests categorized by response code

**(PKCS 11 and GREP11 API also availble?)**

## Before you begin
{: #operational-metrics-considerations}

Enabling {{site.data.keyword.hscrypto}} service metrics will add new metrics to your {{site.data.keyword.mon_short}} instance. For
information on {{site.data.keyword.mon_short}} pricing, see [Pricing](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-pricing_plans){: external}.
{: important}

Before you provision an instance of {{site.data.keyword.mon_short}}, consider the following guidance:

- You need to enable the [metrics policy](/docs/hs-crypto?topic=hs-crypto-manage-sysdig-metrics) for your {{site.data.keyword.hscrypto}} instance in order to retrieve operational metrics.
- Other {{site.data.keyword.cloud_notm}} users with `administrator` or `editor` permissions can manage the {{site.data.keyword.mon_short}} service in the {{site.data.keyword.cloud_notm}}. These users must also have platform permissions to create resources within the resource group where they plan to provision the instance.

## Connecting {{site.data.keyword.mon_short}} with {{site.data.keyword.hscrypto}}
{: #connect-sysdig-hpcs}

Your dashboard show metrics for all {{site.data.keyword.hscrypto}} instances that are in the same region as the {{site.data.keyword.mon_short}} instance with an enabled metrics policy.
{: note}

### Configure a {{site.data.keyword.mon_short}} instance for metrics
{: #configure-sysdig}

To enable platform metrics in a region, complete the following steps:

1. [Provision an instance of {{site.data.keyword.mon_short}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-provision){: external} in the region of the {{site.data.keyword.hscrypto}} instance that contains an [enabled metrics policy](/docs/hs-crypto?topic=hs-crypto-manage-sysdig-metrics).
2. Go to the [monitoring dashboard](/observe/monitoring){: external}.
3. Click **Configure platform metrics**.
4. Select the region where the {{site.data.keyword.hscrypto}} instance is created.
5. Select the {{site.data.keyword.hscrypto}} instance in which you would like to receive metrics.
6. Click **Configure**.
7. Your {{site.data.keyword.hscrypto}} instance is now set for platform metrics.

## {{site.data.keyword.hscrypto}} Metrics Details
{: #hpcs-metrics}

You can use the metrics in your Sysdig dashboard to measure the types of requests being made to your service instance as well as the latency of the requests.

### API Hits
{: #api-hits}

The type and amount of API requests being made to your {{site.data.keyword.hscrypto}} instance. For example, you can track how many API requests that have been made by an authorized user by setting an [alert](#set-monitor-alerts). The alert triggers when your sysdig instance notices a frequent amount of `401` status codes being returned from your {{site.data.keyword.hscrypto}} instance.

<table>
  <tr>
    <th>Metadata</th>
    <th>Description</th>
  </tr>

  <tr>
    <td>
      Metric Name
    </td>
    <td>
      <code>ibm_kms_api_request_gauge</code>
    </td>
  </tr>

  <tr>
    <td>
      Metric Type
    </td>
    <td>
      Gauge
    </td>
  </tr>

  <tr>
    <td>
      Value Type
    </td>
    <td>
      none
    </td>
  </tr>

  <tr>
    <td>
      Segment By
    </td>
    <td>
      [Attributes for Segmentation](#attributes-for-segmentation)
    </td>
  </tr>

  <caption style="caption-side:bottom;">
    Table 1. Describes the API Hits metrics.
  </caption>
</table>

## Latency
{: #latency}

The amount of time it takes {{site.data.keyword.hscrypto}} to receive an API request and respond to it.

The latency is calculated by getting the average of all requests of the same type that occur within 60 seconds.
{: note}

<table>
  <tr>
    <th>Metadata</th>
    <th>Description</th>
  </tr>

  <tr>
    <td>
      Metric Name
    </td>
    <td>
      <code>ibm_kms_api_latency_gauge</code>
    </td>
  </tr>

  <tr>
    <td>
      Metric Type
    </td>
    <td>
      Gauge
    </td>
  </tr>

  <tr>
    <td>
      Value Type
    </td>
    <td>
      Milliseconds
    </td>
  </tr>

  <tr>
    <td>
      Segment By
    </td>
    <td>
      [Attributes for Segmentation](#attributes-for-segmentation)
    </td>
  </tr>

  <caption style="caption-side:bottom;">
    Table 2. Describes the Latency metrics.
  </caption>
</table>

## Attributes for Segmentation
{: #attributes-for-segmentation}

You can filter your metrics by using the following attributes.

<table>
  <tr>
    <th>Attribute Name</th>
    <th>Description</th>
  </tr>

  <tr>
    <td>
      <code>ibm_resource_type</code>
    </td>
    <td>
      Supported resource type is <code>instance</code>.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibm_kms_response_code</code>
    </td>
    <td>
      Response code for the {{site.data.keyword.hscrypto}}
      service API request.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibm_scope</code>
    </td>
    <td>
      The account, organization, or space GUID associated with the metric.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibm_ctype</code>
    </td>
    <td>
      public, dedicated, or local.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibm_location</code>
    </td>
    <td>
      Location of the {{site.data.keyword.hscrypto}} service
      instance.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibm_service_name</code>
    </td>
    <td>
      kms.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibm_resource</code>
    </td>
    <td>
      {{site.data.keyword.hscrypto}} service instance ID.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibm_kms_api</code>
    </td>
    <td>
      {{site.data.keyword.hscrypto}} service API name.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibm_resource_group_name</code>
    </td>
    <td>
      Resource group name associated with the
      {{site.data.keyword.hscrypto}} service instance.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibm_service_instance_name</code>
    </td>
    <td>
      {{site.data.keyword.hscrypto}} service instance name.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibm_service_instance</code>
    </td>
    <td>
      {{site.data.keyword.hscrypto}} service instance ID.
    </td>
  </tr>

  <caption style="caption-side:bottom;">
    Table 3. Describes the attributes use for segmenting metrics.
  </caption>
</table>

## Metrics Filter Attributes
{: #metrics-filter-attributes}

You can scope down your metrics by using the following scope filters. These filters are more granular than the segmentation filters.

<table>
  <tr>
    <th>Attribute Name</th>
    <th>Description</th>
  </tr>

  <tr>
    <td>
      <code>ibmResourceGroupName</code>
    </td>
    <td>
      The name of the resource group associated with the
      {{site.data.keyword.hscrypto}} service instance.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibmScope</code>
    </td>
    <td>
      The account, organization, or space GUID associated with the metric.
    </td>
  </tr>

  <tr>
    <td>
      <code>ibmServiceInstanceName</code>
    </td>
    <td>
      <p>
        The service instance associated with the metric.
      </p>
    </td>
  </tr>

  <tr>
    <td>
      <code>ibmKmsApi</code>
    </td>
    <td>
      The {{site.data.keyword.hscrypto}} API call associated
      with the metric.
    </td>
  </tr>

  <caption style="caption-side:bottom;">
    Table 3. Describes the scope filters for
    {{site.data.keyword.hscrypto}} metrics.
  </caption>
</table>

Due to {{site.data.keyword.mon_short}} limitations, you will only be able to see the values in the dropdown filters for up to six hours at a time. You can manually type in value into scope variables to use scope filters for given time periods.
{: note}

## Default Dashboards
{: #default-dashboards}

You need to configure platform metrics and enable a [metrics policy](/docs/hs-crypto?topic=hs-crypto-manage-sysdig-metrics)
on your service instance in order to view your {{site.data.keyword.hscrypto}} operational metrics dashboard.

### How to find the {{site.data.keyword.mon_short}} dashboard for your {{site.data.keyword.hscrypto}} service instance using {{site.data.keyword.hscrypto}} console
{: #monitor-dashboard-console}

After configuring your {{site.data.keyword.mon_short}} instance to receive platform metrics, complete the following steps:

1. [Provision your {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-provision#provision-gui).
2. Click **Actions** and select **Monitoring**.

### How to find the {{site.data.keyword.mon_short}} dashboard for your {{site.data.keyword.hscrypto}} service instance using observability page
{: #monitor-dashboard-observability}

After configuring your {{site.data.keyword.mon_short}} instance to receive platform metrics, complete the following steps:

1. Go to the [monitoring dashboard](/observe/monitoring){: external} and find your sysdig instance that is configured to receive platform metrics.
2. In the **View Dashboard** column, click **View {{site.data.keyword.mon_short}}**.
3. Once you are in the {{site.data.keyword.mon_short}} platform, click **Dashboards** on the side menu.
4. Select **IBM** under the **Dashboard Templates** section.
5. Select **{{site.data.keyword.hscrypto}} - Overview** to view the dashboard for your {{site.data.keyword.hscrypto}} instance.

You are able to see any metrics in your {{site.data.keyword.mon_short}} instance until you enable a metrics policy for your {{site.data.keyword.hscrypto}} instance and make API requests to your {{site.data.keyword.hscrypto}} instance.
{: note}

## Setting Alerts
{: #set-monitor-alerts}

You can set alerts on your {{site.data.keyword.mon_short}} dashboard to notify you of certain metrics. To setup alerts, complete the following steps:

1. Click **Alerts** on the side menu.
2. Click **Add Alert** and select **Metric** as the alert type.
3. Select the aggregation and the metric that you would like to be performed on.
4. Select the scope if applicable.
5. Set the metric and time requirements for the alert to trigger.
6. Configure and set up the notification channel and notification interval.
8. Click **CREATE**.

For more information on configuring metric alerts, see [Metric Alerts](https://docs.sysdig.com/en/metric-alerts.html){: external}.
