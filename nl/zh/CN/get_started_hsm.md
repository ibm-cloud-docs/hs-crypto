---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-15"

Keywords: key storage, service instance, HSM, hardware security module

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}  
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# 服务实例初始化入门
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> 此教程为您演示如何通过装入主密钥来初始化服务实例，以使用 Trusted Key Entry 插件保护密钥存储器。在初始化服务实例之后，就可以开始管理根密钥了。   
{:shortdesc}

## 先决条件
{: #get-started-hsm-prerequisite}

开始之前，请先执行以下步骤：

1. 供应 {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} 实例（简称服务实例）。有关详细步骤，请参阅[供应 {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/provision.html)。

2. 运行以下命令，以确保已登录到正确的 API 端点：

  ```
  ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

3. 通过 {{site.data.keyword.cloud_notm}} 命令行界面 (CLI) 利用以下命令来安装最新的 Trusted Key Entry 插件：

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  要安装 CLI 插件，请参阅 [{{site.data.keyword.cloud_notm}} CLI 入门](/docs/cli/index.html)。
  {: tip}

4. 设置环境变量 CLOUDTKEFILES 以指示要用于存储密钥部件和签名密钥的子目录

##  第 1 步：创建主密钥和签名密钥文件
{: #hsm-step1}

1. 创建随机主密钥部件或带有已知值的主密钥部件。

  * 要创建随机主密钥部件，请使用以下命令：

    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    在系统提示时，输入对密钥部件的描述以及密钥部件文件的密码。

  * 要创建带有已知值的主密钥部件，请使用以下命令：

    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    在系统提示时，输入十六进制字符串形式的已知密钥部件值，然后输入密钥部件文件的描述和密码。

  重复上述任一命令可创建其他密钥部件。

2. 使用以下命令创建签名密钥：
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  在系统提示时，输入签名密钥文件的管理员名称和密码。

## 第 2 步：选择要使用的加密单元
{: #hsm-step2}

必须对服务实例中的所有加密单元进行相同的配置。

1. 您可以使用以下命令来显示已分配给您的 IBM Cloud 帐户的服务实例和加密单元：

  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

2. 要选择想使用的其他加密单元，请使用命令：

  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  在系统提示时，输入要使用的其他加密单元。

3. 要从您将使用的集合中除去加密单元，请使用命令：

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  在系统提示时，输入要除去的加密单元。

## 第 3 步：添加加密单元管理员，然后退出印记模式
{: #hsm-step3}

要能够将主密钥装入加密单元中，您必须先创建一个或多个加密单元管理员，然后退出印记模式。

1. 装入加密单元管理员。要创建加密单元管理员，请使用命令：
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  在系统提示时，输入签名密钥的 KEYNUM 以用于签名密钥文件的管理员和密码。

2. 使用以下命令来选择要用于对命令签名的签名密钥：

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  在系统提示时，输入签名密钥的 KEYNUM 以用于对命令签名。

  此值必须与在步骤 3.1 中用于装入加密单元管理员的某个签名密钥相同。
  {: tip}

3. 使用以下命令退出印记模式：

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

在装入加密单元管理员并退出印记模式之后，您可以使用以下命令来检查加密单元状态：
{: tip}

```
 ibmcloud tke cryptounit-compare
```
{: pre}

## 第 4 步：装入主密钥寄存器
{: #hsm-step4}

要装入主密钥寄存器，必须定义一个或多个加密单元管理员，并且该加密单元必须保持为印记模式。

1. 使用以下命令装入新的主密钥寄存器：

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  在系统提示时，输入要装入的密钥部件的 KEYNUM、签名密钥文件的密码，以及每个选定密钥部件的密码。

2. 使用以下命令提交新的主密钥寄存器：

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  在系统提示时，输入签名密钥文件的密码。

3. 使用以下命令将主密钥移动到当前主密钥寄存器：

  ```
  ibmcloud tke cryptounit-mk-setimm
  ```
  {: pre}

  在系统提示时，输入签名密钥文件的密码。

## 后续工作
{: #hsm-next}

现在您可以开始使用服务实例了。有关在生产环境中实施此过程的详细信息，请参阅[初始化服务实例以保护密钥存储器](/docs/services/hs-crypto/initialize_hsm.html)。
