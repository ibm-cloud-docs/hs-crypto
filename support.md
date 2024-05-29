---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-29"

keywords: troubleshoot, problems, known issues, support,help

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Getting help and support for {{site.data.keyword.hscrypto}}
{: #getting-help}
{: troubleshoot}

If you experience an issue or have questions when using {{site.data.keyword.hscrypto}}, you can use the following resources before you open a support case.
{: shortdesc}

* Review the error message that is displayed on the UI. Normally, it also appends a help link to help you learn more and resolve the issue.
* Review the [FAQs](/docs/hs-crypto?topic=hs-crypto-faq-basics) in the product documentation.
* Review the [troubleshooting documentation](/docs/hs-crypto?topic=hs-crypto-sitemap#sitemap_troubleshooting_key_management_service) to troubleshoot and resolve common issues.
* Check the status of the {{site.data.keyword.Bluemix_notm}} platform and resources by going to the [Status page](https://cloud.ibm.com/status){: external}.

If you still can't resolve the problem, you can open a support case. For more information, see [Creating support cases](/docs/get-support?topic=get-support-open-case). And, if you're looking to provide feedback, see [Submitting feedback](/docs/overview?topic=overview-feedback).

## Providing support case details
{: #support-case-details}

If you need to open a support case for your issue, make sure that you include the following information for the IBM Support team to faster and better investigation:

- Your instance ID. 

    You can find the ID on your instance dashboard through **Overview** &gt; **Instance** &gt; **Instance ID**. Or, you can [retrieve the ID with the API](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID&interface=api){: external}.

- Standadn plan: Your instance KMS endpoint. 

    You can find the endpoint URL on your instance dashboard through **Overview** &gt; **Instance** &gt; **KMS public endpoint URL**. Or, you can [retrieve the API endpoint URL with the API](/apidocs/hs-crypto#getinstance){: external}.

- {{site.data.keyword.uko_full_notm}} plan: Your instance {{site.data.keyword.uko_full_notm}} endpoint.

    You can find the endpoint URL on your instance dashboard through **Overview** &gt; **Instance** &gt; **{{site.data.keyword.uko_full_notm}} endpoint URL**. 
  
- BYOHSM: Your instance HSM connector ID. 

    You can find the connector ID on your instance dashboard through **Overview** &gt; **Instance** &gt; **HSM connector ID**.
    
    The Bring Your Own HSM (BYOHSM) function is available only in the Standard Plan service instances in the VPC-based regions. For the VPC region list, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions#available-regions).
