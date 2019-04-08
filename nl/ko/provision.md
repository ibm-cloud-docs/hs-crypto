---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-21"

Keywords: provision, instance of Hyper Protect Crypto Services

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:gif: data-image-type='gif'}

# 서비스 프로비저닝
{: #provision}

{{site.data.keyword.cloud_notm}} 콘솔 또는 {{site.data.keyword.cloud_notm}} CLI를 사용하여 {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}의 인스턴스를 작성할 수 있습니다.
{: shortdesc}

## {{site.data.keyword.cloud_notm}} 콘솔에서 프로비저닝
{: #provision-gui}

{{site.data.keyword.cloud_notm}} 콘솔에서 {{site.data.keyword.hscrypto}}의 인스턴스를 프로비저닝하려면 다음 단계를 완료하십시오.

1. [{{site.data.keyword.cloud_notm}} 계정 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/){: new_window}에 로그인하십시오.
2. **카탈로그**를 클릭하여 {{site.data.keyword.cloud_notm}}에서 사용 가능한 서비스의 목록을 보십시오.
3. 모든 카테고리 탐색 분할창에서 **보안 및 ID** 카테고리를 클릭하십시오.
4. 서비스 목록에서 **{{site.data.keyword.hscrypto}}** 타일을 클릭하십시오.
5. **선택사항**: **태그** 필드에서 태그를 추가하여 리소스를 구성하십시오. 태그가 청구 관련인 경우 `costctr:124`와 같은 관련 태그를 그룹화하는 데 도움이 되도록 키:값 쌍으로 태그를 작성하는 것을 고려하십시오. 태그에 대한 자세한 정보는 [태그 작업](/docs/resources?topic=resources-tag#tag)을 참조하십시오.
6. **암호화 단위 수**에서 성능 요구사항을 충족하는 암호화 단위 수를 선택하십시오.

  서비스 인스턴스는 최대 6개의 암호화 단위를 지원합니다. 프로덕션 환경에서는 고가용성을 사용하기 위해 두 개 이상의 암호화 단위를 선택하는 것이 좋습니다. 3개 이상의 암호화 단위를 선택하면 이 암호화 단위가 선택한 지역의 지원되는 3개의 가용성 구역에 분배됩니다.
  {: important}
7. **작성**을 클릭하여 로그인한 계정, 지역 및 로그인된 리소스 그룹에서 {{site.data.keyword.hscrypto}}의 인스턴스를 프로비저닝하십시오.

![서비스 프로비저닝](image/provisioning.gif "서비스 프로비저닝")
{: gif}

*그림 1. 서비스 프로비저닝*

<!-- ## Provisioning from the {{site.data.keyword.cloud_notm}} CLI
{: #provision-cli}

To provision an instance of {{site.data.keyword.hscrypto}} using the {{site.data.keyword.cloud_notm}} CLI, complete the following steps:

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview){: new_window} with the following command:

    ```sh
    curl -sl https://ibm.biz/idt-installer | bash
    ```
    {: pre}

    **Notes:** For more information about the {{site.data.keyword.cloud_notm}} CLI, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview){: new_window}.

2. Log in to {{site.data.keyword.cloud_notm}} through the {{site.data.keyword.cloud_notm}} CLI with the following command:

    ```sh
    ibmcloud login
    ```
    {: pre}

    **Notes:** If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode. -->

<!-- ### Creating a service instance within your account
{: #provision-acct-lvl}

To simplify access to your encryption keys with [{{site.data.keyword.iamlong}} roles](/docs/iam/users_roles.html#iamusermanrol), you can create one or more instances of the {{site.data.keyword.hscrypto}} service within an account, without needing to specify an org and space.

1. Log in to {{site.data.keyword.cloud_notm}} through the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview){: new_window}.

    ```sh
    ibmcloud login
    ```
    {: pre}
    **Notes:** If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the account, region, and resource group where you would like to create a {{site.data.keyword.hscrypto}} service instance.

    You can use the following command to set your target region and resource group.

    ```sh
    ibmcloud target -r <region_name> -g <resource_group_name>
    ```
    {: pre}

3. Provision an instance of {{site.data.keyword.hscrypto}} within that account and resource group.

    ```sh
    ibmcloud resource service-instance-create <instance_name> kms tiered-pricing
    ```
    {: pre}

    Replace `<instance_name>` with a unique alias for your service instance.

4. Optional: Verify that the service instance was created successfully.

    ```sh
    ibmcloud resource service-instances
    ```
    {: pre}

### Creating a service instance within an org and space
{: #provision-space-lvl}

To manage access to your encryption keys with [Cloud Foundry roles](/docs/iam/cfaccess.html), you can create an instance of the {{site.data.keyword.hscrypto}} service within a specified organization and space.  

1. Log in to {{site.data.keyword.cloud_notm}} through the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview){: new_window}.

    ```sh
    ibmcloud login
    ```
    {: pre}
    **Note:** If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the account, region, organization, and space where you would like to create a {{site.data.keyword.hscrypto}} service instance.

    You can use the following command to set your target region, org, and space.

    ```sh
    ibmcloud target -r <region> -o <organization_name> -s <space_name>
    ```
    {: pre}

3. Provision an instance of {{site.data.keyword.hscrypto}} within that account, region, organization, and space.

    ```sh
    ibmcloud service create kms tiered-pricing <instance_name>
    ```
    {: pre}

    Replace `<instance_name>` with a unique alias for your service instance.

4. Optional: Verify that the service instance was created successfully.

    ```sh
    ibmcloud service list
    ```
    {: pre}
-->

### 다음에 수행할 작업
{: #provision-next}

프로그래밍 방식으로 키를 관리하는 방법에 대해 자세히 알아보려면 [{{site.data.keyword.hscrypto}} API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")를 확인하십시오](https://{DomainName}/apidocs/hs-crypto){: new_window}.
