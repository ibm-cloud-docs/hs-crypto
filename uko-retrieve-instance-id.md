---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-27"

keywords: service id, service ids, instance id, get instance id, get instance guid, instance id api, instance id cli

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Retrieving your instance ID
{: #uko-retrieve-instance-ID}

You can target an individual {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance for operations by including the unique identifier, or instance ID, in API requests to the service.
{: shortdesc}

## Viewing your instance ID with the UI
{: #uko-view-instance-ID}
{: ui}

You can view the instance ID that is associated with your {{site.data.keyword.hscrypto}} service instance by navigating to your {{site.data.keyword.cloud_notm}} resource list.

1. [Log in to the UI](https://{DomainName}){: external}.
2. Go to **Menu** &gt; **Resource list**, and then click **Services** to browse a list of your cloud services.
3. Click the table row that describes your {{site.data.keyword.hscrypto}} service instance.
4. Go to **Overview** &gt; **Instance**, and copy the **Instance ID** value.

    This **Instance ID** uniquely identifies your {{site.data.keyword.hscrypto}} service instance.

## Retrieving an instance ID with the CLI
{: #uko-retrieve-instance-ID-cli}
{: cli}

You can also retrieve the instance ID for your service instance by using the {{site.data.keyword.cloud_notm}} CLI.

1. Log in to {{site.data.keyword.cloud_notm}} with the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).

    ```sh
    ibmcloud login
    ```
    {: pre}

    If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.
    {: note}

2. Select the region and resource group that contain your provisioned instance of {{site.data.keyword.hscrypto}}. You can use the following command to set your target region and resource group.

    ```sh
    ibmcloud target -r <region_name> -g <resource_group_name>
    ```
    {: pre}


3. Retrieve the Cloud Resource Name (CRN) that uniquely identifies your {{site.data.keyword.hscrypto}} service instance.

    ```sh
    ibmcloud resource service-instance <instance_name> --id
    ```
    {: pre}

    Replace `<instance_name>` with the unique alias that you assigned to your {{site.data.keyword.hscrypto}} service instance. The following truncated example shows the CLI output.

    ```
    crn:v1:public:hs-crypto:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:42454b3b-5b06-407b-a4b3-34d9ef323901:: 42454b3b-5b06-407b-a4b3-34d9ef323901
    ```
    {: screen}

    The `42454b3b-5b06-407b-a4b3-34d9ef323901` value is an example instance ID.


## Retrieving an instance ID with the API
{: #uko-retrieve-instance-ID-api}
{: api}

You might want to retrieve the instance ID programmatically to help you build and connect your application. You can call the [{{site.data.keyword.cloud_notm}} Resource Controller API](/apidocs/resource-controller){: external}, and then pipe the JSON output to `jq` to extract this value.

1. [Retrieve an {{site.data.keyword.cloud_notm}} IAM access token](/docs/hs-crypto?topic=hs-crypto-uko-retrieve-access-token).
2. Call the [Resource Controller API](/apidocs/resource-controller){: external} to retrieve your instance ID.

    ```curl
    curl -X GET \
    https://resource-controller.cloud.ibm.com/v2/resource_instances \
    -H 'Authorization: Bearer <access_token>' | jq -r '.resources[] | select(.name | contains("<instance_name>")) | .guid'
    ```
    {: codeblock}

    Replace `<instance_name>` with the unique alias that you assigned to your {{site.data.keyword.hscrypto}} service instance. The following output shows an example instance ID:

    ```
    42454b3b-5b06-407b-a4b3-34d9ef323901
    ```
    {: screen}

