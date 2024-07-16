---
title: 在UI中创建Google Ads Source连接
description: 了解如何使用Google UI创建Adobe Experience Platform Ads源连接。
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---

# 在UI中创建Google Ads源连接

>[!WARNING]
>
>[!DNL Google Ads]源暂时不可用。 Adobe正在努力解决此源的问题。

>[!NOTE]
>
>Google广告源为测试版。 有关使用测试版标记源的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

本教程提供了使用Google用户界面创建Adobe Experience Platform Ads源连接的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已拥有有效的Google Ads连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/advertising.md)的教程

### 收集所需的凭据

要访问Google广告帐户平台，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 客户端客户 ID | 客户端客户ID是与您要使用Google Ads API管理的Google Ads客户端帐户对应的帐号。 此ID遵循`123-456-7890`模板。 |
| 登录客户Id | 登录客户ID是与您的Google广告管理器帐户对应的帐号，用于从特定的运营客户获取报表数据。 有关登录客户ID的详细信息，请阅读[Google Ads API文档](https://developers.google.com/search-ads/reporting/concepts/login-customer-id)。 |
| 开发人员令牌 | 通过开发人员令牌，您可以访问Google Ads API。 您可以使用相同的开发人员令牌针对所有Google Ads帐户发出请求。 通过[登录到您的经理帐户](https://ads.google.com/home/tools/manager-accounts/)并导航到API中心页面，检索您的开发人员令牌。 |
| 刷新令牌 | 刷新令牌是[!DNL OAuth2]身份验证的一部分。 此令牌允许您在访问令牌过期后重新生成访问令牌。 |
| 客户端 ID | 客户端ID与客户端密钥结合使用，作为[!DNL OAuth2]身份验证的一部分。 通过同时使用客户端ID和客户端密钥，您的应用程序可以在Google中标识您的应用程序，从而代表您的帐户运行。 |
| 客户端密码 | 客户端密钥与客户端ID结合使用，作为[!DNL OAuth2]身份验证的一部分。 通过同时使用客户端ID和客户端密钥，您的应用程序可以在Google中标识您的应用程序，从而代表您的帐户运行。 |

阅读[有关Google Ads入门的更多信息](https://developers.google.com/google-ads/api/docs/first-call/overview)的API概述文档。

## 连接您的Google Ads帐户

在Platform UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!UICONTROL Advertising]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Google Ads]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![Experience PlatformUI中的源目录。](../../../../images/tutorials/create/ads/catalog.png)。

此时会显示&#x200B;**[!UICONTROL 连接到Google广告]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

若要连接现有帐户，请选择您要连接的Google Ads帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![源工作流中现有帐户的选择页面。](../../../../images/tutorials/create/ads/existing.png)。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单中，提供名称、可选描述和您的Google Ads凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![源工作流中的新帐户接口。](../../../../images/tutorials/create/ads/new.png)。

## 后续步骤

通过学习本教程，您已建立与Google Ads帐户的连接。 您现在可以继续下一教程，并[配置数据流以将广告数据引入Platform](../../dataflow/advertising.md)。
