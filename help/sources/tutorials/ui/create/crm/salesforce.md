---
title: 使用Salesforce用户界面连接您的Experience Platform帐户
description: 了解如何使用用户界面连接您的Salesforce帐户并将CRM数据引入Experience Platform。
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 11e9e1a25a45f4011f15b1e28753a98d4158012c
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 3%

---

# 使用UI将您的[!DNL Salesforce]帐户连接到Experience Platform

阅读本指南，了解如何使用Experience Platform用户界面连接您的[!DNL Salesforce]帐户并将您的CRM数据导入Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有经过身份验证的[!DNL Salesforce]帐户，则可以跳过本文档的其余部分，并转到有关[为CRM数据配置数据流](../../dataflow/crm.md)的教程。

### 收集所需的凭据 {#gather-required-credentials}

[!DNL Salesforce]源支持通过OAuth2客户端凭据进行身份验证。

| 凭据 | 描述 |
| --- | --- |
| 环境 URL | [!DNL Salesforce]源实例的URL。 环境URL的格式为`https://[domain].my.salesforce.com`。 |
| 客户端 ID | 在OAuth2身份验证中，客户端ID与客户端密钥结合使用。 客户端ID和客户端密钥共同使您的应用程序能够代表您的帐户运行，方法是向[!DNL Salesforce]标识您的应用程序。 |
| 客户端密码 | 客户端密钥与客户端ID结合使用，作为OAuth2身份验证的一部分。 客户端ID和客户端密钥共同使您的应用程序能够代表您的帐户运行，方法是向[!DNL Salesforce]标识您的应用程序。 |
| API 版本 | 您正在使用的[!DNL Salesforce]实例的REST API版本。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本`52`，则必须以`52.0`的形式输入值。 如果此字段留空，则Experience Platform将自动使用最新可用版本。 |
| 包含已删除的对象 | 一个布尔值，用于确定是否包括软删除的记录。 如果设置为true，软删除的记录可以包含在您的[!DNL Salesforce]查询中，并从您的帐户摄取到Experience Platform中。如果未指定配置，此值默认为`false`。 |

有关为[!DNL Salesforce]使用OAuth的更多信息，请阅读有关OAuth授权流程](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)的[[!DNL Salesforce] 指南。

## 连接您的[!DNL Salesforce]帐户

在Experience Platform UI中，从左侧菜单导航到&#x200B;**[!UICONTROL Sources]**&#x200B;以打开[!UICONTROL Sources]工作区。 使用左侧的目录浏览类别，或使用搜索栏快速查找要连接的源。

在&#x200B;*[!UICONTROL CRM]*&#x200B;类别下选择&#x200B;**[!DNL Salesforce]**，然后选择&#x200B;**[!UICONTROL Add data]**。

>[!TIP]
>
>在源目录中，如果未连接任何帐户，您将看到&#x200B;**[!UICONTROL Set up]**；如果帐户已经过身份验证，您将看到&#x200B;**[!UICONTROL Add data]**。

![已选择Salesforce源卡的Experience Platform UI上的源目录。](../../../../images/tutorials/create/salesforce/catalog.png)

此时会显示&#x200B;**[!UICONTROL Connect to Salesforce]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 使用现有帐户

要使用现有帐户，请选择&#x200B;**[!UICONTROL Existing account]**，然后从显示的列表中选择要使用的帐户。 完成后，选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![您的组织中已存在的经过身份验证的Salesforce帐户的列表。](../../../../images/tutorials/create/salesforce/existing.png)

### 创建新帐户

要创建新帐户，请选择&#x200B;**[!UICONTROL New account]**&#x200B;并为您的新[!DNL Salesforce]帐户提供名称和描述。

对于OAuth 2客户端凭据，选择&#x200B;**[!UICONTROL OAuth2 Client Credential]**，然后提供以下凭据的值：

* 环境 URL
* 客户端 ID
* 客户端密码
* API 版本
* 包括删除对象

完成后，选择&#x200B;**[!UICONTROL Connect to source]**。


![通过提供适当的身份验证凭据来创建新的Salesforce帐户的界面。](../../../../images/tutorials/create/salesforce/new.png)

### 跳过样本数据预览 {#skip-preview-of-sample-data}

在数据选择步骤中，摄取大型表或数据文件时可能会遇到超时。 您可以跳过数据预览以规避超时，并且仍可以查看架构，尽管没有示例数据。 要跳过数据预览，请启用&#x200B;**[!UICONTROL Skip previewing sample data]**&#x200B;切换开关。

工作流的其余部分将保持不变。 唯一需要注意的是，跳过数据预览可能会阻止在映射步骤中自动验证已计算和必填字段，您随后必须在映射期间手动验证这些字段。

## 后续步骤

通过学习本教程，您已建立与[!DNL Salesforce]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入 [!DNL Experience Platform]](../../dataflow/crm.md)。
