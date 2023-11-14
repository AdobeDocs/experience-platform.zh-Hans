---
title: 在UI中创建Google Ads源连接
description: 了解如何使用Google UI创建Adobe Experience Platform Ads源连接。
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---

# 在UI中创建Google Ads源连接

>[!NOTE]
>
>Google广告源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

本教程提供了使用Google用户界面创建Adobe Experience Platform Ads源连接的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的Google广告连接，则可以跳过本文档的其余部分并继续阅读上的教程 [配置数据流](../../dataflow/advertising.md)

### 收集所需的凭据

要访问Google广告帐户平台，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 客户端客户ID | 客户端客户ID是与您要使用Google Ads API管理的Google Ads客户端帐户对应的帐号。 此ID遵循的模板 `123-456-7890`. |
| 登录客户Id | 登录客户ID是与您的Google广告管理器帐户对应的帐号，用于从特定的运营客户获取报表数据。 有关登录客户ID的更多信息，请阅读 [Google Ads API文档](https://developers.google.com/google-ads/api/docs/migration/login-customer-id). |
| 开发人员令牌 | 通过开发人员令牌，您可以访问Google Ads API。 您可以使用相同的开发人员令牌针对所有Google Ads帐户发出请求。 通过以下方式检索您的开发人员令牌 [登录到您的经理帐户](https://ads.google.com/home/tools/manager-accounts/) 然后导航到API中心页面。 |
| 刷新令牌 | 刷新令牌是的一部分 [!DNL OAuth2] 身份验证。 此令牌允许您在访问令牌过期后重新生成访问令牌。 |
| 客户端ID | 客户端ID与客户端密钥一起使用，作为的一部分 [!DNL OAuth2] 身份验证。 通过同时使用客户端ID和客户端密钥，您的应用程序可以在Google中标识您的应用程序，从而代表您的帐户运行。 |
| 客户端密码 | 客户端密钥与客户端ID结合使用，作为的一部分 [!DNL OAuth2] 身份验证。 通过同时使用客户端ID和客户端密钥，您的应用程序可以在Google中标识您的应用程序，从而代表您的帐户运行。 |

阅读API概述文档 [有关Google广告入门的更多信息](https://developers.google.com/google-ads/api/docs/first-call/overview).

## 连接您的Google Ads帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示了多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 **[!UICONTROL 广告]** 类别，选择 **[!UICONTROL Google Ads]**，然后选择 **[!UICONTROL 添加数据]**.

![Experience PlatformUI中的源目录。](../../../../images/tutorials/create/ads/catalog.png).

此 **[!UICONTROL 连接到Google Ads]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择要连接的Google Ads帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![源工作流中现有帐户的选择页面。](../../../../images/tutorials/create/ads/existing.png).

### 新帐户

如果您正在使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入表单中，提供名称、可选描述和您的Google Ads凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后等待一段时间以建立新连接。

![源工作流程中的新帐户界面。](../../../../images/tutorials/create/ads/new.png).

## 后续步骤

通过学习本教程，您已建立与Google Ads帐户的连接。 您现在可以继续下一教程和 [配置数据流以将广告数据引入Platform](../../dataflow/advertising.md).
