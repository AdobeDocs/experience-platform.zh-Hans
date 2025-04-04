---
keywords: Experience Platform；主页；热门主题；Hubspot；Hubspot
solution: Experience Platform
title: 在UI中创建HubSpot Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建HubSpot源连接。
exl-id: 452b7290-b9e8-4728-8b58-0e0c76bd9449
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# 在用户界面中创建[!DNL HubSpot]源连接

Adobe Experience Platform中的Source连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用[!DNL Experience Platform]用户界面创建[!DNL HubSpot]源连接器的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经有[!DNL HubSpot]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/marketing-automation.md)的教程。

### 收集所需的凭据

要在[!DNL Experience Platform]上访问您的[!DNL HubSpot]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientId` | 与您的[!DNL HubSpot]应用程序关联的客户端ID。 |
| `clientSecret` | 与您的[!DNL HubSpot]应用程序关联的客户端密钥。 |
| `accessToken` | 最初验证您的OAuth集成时获得的访问令牌。 |
| `refreshToken` | 最初对您的OAuth集成进行身份验证时获得的刷新令牌。 |

有关入门的详细信息，请参阅此[[!DNL HubSpot] 文档](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

## 连接您的[!DNL HubSpot]帐户

收集所需的凭据后，您可以按照以下步骤将您的[!DNL HubSpot]帐户关联到[!DNL Experience Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!UICONTROL 营销自动化]**&#x200B;类别下，选择&#x200B;**[!UICONTROL HubSpot]**。 如果这是您第一次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的[!DNL HubSpot]连接器。

![目录](../../../../images/tutorials/create/hubspot/catalog.png)

将显示&#x200B;**[!UICONTROL 连接到HubSpot]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL HubSpot]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后留出一些时间来建立新连接。

![连接](../../../../images/tutorials/create/hubspot/connect.png)

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL HubSpot]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/hubspot/existing.png)

## 后续步骤

通过学习本教程，您已建立与[!DNL HubSpot]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将营销自动化系统数据引入 [!DNL Experience Platform]](../../dataflow/marketing-automation.md)。
