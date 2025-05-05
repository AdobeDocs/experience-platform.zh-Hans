---
title: 使用UI将Google广告连接到Experience Platform
description: 了解如何在UI中将您的Google Ads帐户连接到Adobe Experience Platform。
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 009866abc39b06c22b7bea758ce9fdfba8c72b00
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---

# 使用UI将[!DNL Google Ads]连接到Experience Platform

>[!WARNING]
>
>[!DNL Google Ads]源当前在用户界面中不可用。 您可以使用API[&#128279;](../../../api/create/advertising/ads.md)继续将[!DNL Google Ads]数据摄取到Experience Platform 。

>[!NOTE]
>
>[!DNL Google Ads]源为测试版。 有关使用测试版标记源的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

阅读本指南，了解如何使用Experience Platform UI中的源工作区将您的[!DNL Google Ads]帐户连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Google Ads]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/advertising.md)的教程

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Google Ads] 源概述](../../../../connectors/advertising/ads.md)。

## 连接您的Google Ads帐户

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;*[!UICONTROL 源]*&#x200B;工作区。 您可以在&#x200B;*[!UICONTROL 类别]*&#x200B;面板中选择相应的类别。 或者，您可以使用搜索栏导航到要使用的特定源。

要使用[!DNL Google Ads]，请选择&#x200B;*[!UICONTROL Google]*&#x200B;下的&#x200B;**[!UICONTROL Advertising广告]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![Experience Platform UI中的源目录。](../../../../images/tutorials/create/ads/catalog.png)。

### 现有账户

要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后从界面上的帐户列表中选择要使用的帐户。

选择帐户后，选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行下一步。

![源工作流中现有帐户的选择页面。](../../../../images/tutorials/create/ads/existing.png)。

### 新帐户

如果您没有现有帐户，则必须通过提供与您的源对应的必需身份验证凭据来创建新帐户。

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供帐户名称以及帐户详细信息的描述（可选）。 接下来，提供相应的身份验证值，以便针对Experience Platform验证您的源：

* **客户端客户ID**：客户端客户ID是与您要使用[!DNL Google Ads] API管理的[!DNL Google Ads]客户端帐户对应的帐号。 此ID遵循`123-456-7890`模板。
* **登录客户ID**：登录客户ID是与您的[!DNL Google Ads]经理帐户对应的帐号，用于从特定的操作客户获取报表数据。 有关登录客户ID的详细信息，请阅读[[!DNL Google Ads] API文档](https://developers.google.com/search-ads/reporting/concepts/login-customer-id)。
* **开发人员令牌**：开发人员令牌允许您访问[!DNL Google Ads] API。 您可以使用相同的开发人员令牌针对所有[!DNL Google Ads]帐户发出请求。 通过[登录到您的经理帐户](https://ads.google.com/home/tools/manager-accounts/)并导航到API中心页面，检索您的开发人员令牌。
* **刷新令牌**：刷新令牌是[!DNL OAuth2]身份验证的一部分。 此令牌允许您在访问令牌过期后重新生成访问令牌。
* **客户端ID**：客户端ID与客户端密钥结合使用，作为[!DNL OAuth2]身份验证的一部分。 客户端ID和客户端密钥共同允许您的应用程序通过向[!DNL Google]标识您的应用程序来代表您的帐户运行。
* **客户端密钥**：客户端密钥与客户端ID结合使用，作为[!DNL OAuth2]身份验证的一部分。 客户端ID和客户端密钥共同允许您的应用程序通过向[!DNL Google]标识您的应用程序来代表您的帐户运行。
* **[!DNL Google Ads]API版本**： [!DNL Google Ads]支持的当前API版本。 尽管最新版本是`v18`，但Experience Platform上支持的最新版本是`v17`。

输入凭据后，选择&#x200B;**[!UICONTROL 连接到源]**，等待一段时间以处理连接。 完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流中的新帐户接口。](../../../../images/tutorials/create/ads/new.png)。

## 选择数据 {#select-data}

对于[!DNL Google Ads]，您必须提供在工作流的数据选择阶段进行摄取的属性列表。 为了检索这些属性，您必须使用[[!DNL Google Ads Query Builder]](https://developers.google.com/google-ads/api/fields/v17/overview_query_builder)。

在[!DNL Google Ads Query Builder]中，导航到要使用的资源类型，然后使用属性选择器选择您的属性、区段和量度。

![Google Ads查询生成器中的属性选择器。](../../../../images/tutorials/create/ads/attributes.png)

您选择的属性将填充[!DNL Google Ads Query Language]面板。 请确保您使用[!DNL Standard]模式，然后选择&#x200B;**[!DNL Enter or edit a query]**。

![选定的属性，分组到一个查询中。](../../../../images/tutorials/create/ads/enter-query.png)

接下来，选择&#x200B;**[!DNL Validate Query]**&#x200B;以验证您的[!DNL Google Ads]查询。

![Google Ads查询生成器验证器。](../../../../images/tutorials/create/ads/validate-query.png)

如果成功，[!DNL Google Ads Query Builder]将返回一条消息，指示您的查询有效。 接下来，从查询中仅复制&#x200B;**属性**。

![已成功验证查询。](../../../../images/tutorials/create/ads/copy-query.png)

导航回Experience Platform UI中源工作流的数据选择阶段，然后在&#x200B;*[!UICONTROL 列表属性]*&#x200B;面板中粘贴属性。

选择&#x200B;**[!UICONTROL 预览]**&#x200B;以预览数据，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![源工作流中的列表属性面板。](../../../../images/tutorials/create/ads/list-attributes.png)

## 创建数据流以摄取广告数据

通过学习本教程，您已建立与Google Ads帐户的连接。 您现在可以继续下一教程，并[配置数据流以将广告数据引入Experience Platform](../../dataflow/advertising.md)。
