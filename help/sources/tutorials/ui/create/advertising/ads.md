---
keywords: Experience Platform；主页；热门主题；Google广告；Google广告源连接器；google广告连接器
title: 在UI中创建Google广告源连接
description: 了解如何使用Google UI创建Adobe Experience Platform Ads源连接。
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# 在UI中创建Google Ads源连接

>[!NOTE]
>
>Google Ads源处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

本教程提供了使用Google用户界面创建Adobe Experience Platform Ads源连接器的步骤。

## 快速入门

本教程需要对Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的Google Ads连接，则可以跳过本文档的其余部分，继续阅读上的教程 [配置数据流](../../dataflow/advertising.md)

### 收集所需的凭据

要访问您的Google Ads帐户平台，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 客户ID | 客户ID是与您要通过Google Ads API管理的Google Ads客户帐户对应的帐号。 此ID遵循的模板是 `123-456-7890`. |
| 开发人员令牌 | 开发人员令牌允许您访问Google Ads API。 您可以使用相同的开发人员令牌对所有Google广告帐户发出请求。 通过检索开发人员令牌 [登录您的manager帐户](https://ads.google.com/home/tools/manager-accounts/) 然后导航到API中心页面。 |
| 刷新令牌 | 刷新令牌是 [!DNL OAuth2] 身份验证。 此令牌允许您在访问令牌过期后重新生成该令牌。 |
| 客户端ID | 客户端ID与客户端密钥一起使用，作为 [!DNL OAuth2] 身份验证。 客户端ID和客户端密钥通过将您的应用程序标识到Google，使您的应用程序能够代表您的帐户运行。 |
| 客户端密钥 | 客户端密钥与作为 [!DNL OAuth2] 身份验证。 客户端ID和客户端密钥通过将您的应用程序标识到Google，使您的应用程序能够代表您的帐户运行。 |

阅读API概述文档，以了解 [有关Google Ads快速入门的更多信息](https://developers.google.com/google-ads/api/docs/first-call/overview).

## 连接您的Google Ads帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 **[!UICONTROL 广告]** 类别，选择 **[!UICONTROL Google Ads]**，然后选择 **[!UICONTROL 添加数据]**.

![Experience PlatformUI源目录中Google Ads源的图像](../../../../images/tutorials/create/ads/catalog.png).

的 **[!UICONTROL 连接到Google Ads]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择要连接的Google Ads帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![可用于创建Google Ads数据流的现有帐户列表的图像，其中](../../../../images/tutorials/create/ads/existing.png).

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述和您的Google广告凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![Experience PlatformUI上新帐户连接屏幕的图像](../../../../images/tutorials/create/ads/connect.png).

## 后续步骤

通过阅读本教程，您已建立与Google Ads帐户的连接。 您现在可以继续下一个教程和 [配置数据流以将广告数据引入平台](../../dataflow/advertising.md).
