---
title: 为Experience Platform Web SDK配置数据流
description: '了解如何配置数据流。 '
keywords: 配置；datastreams;datastreamId;edge;edge配置id;环境设置；edgeConfigId;id同步；启用ID同步容器ID；沙箱；流入；事件数据集；目标；客户端代码；属性令牌；目标环境ID;Cookie目标；url目标；分析设置区块报表包ID;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 5642fa155d487982f01d25fa765bb36ad5c3bb21
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 1%

---


# 配置数据流

Adobe Experience Platform Web SDK的配置分为两个位置。 SDK中的[configure命令](configuring-the-sdk.md)控制必须在客户端上处理的事项，如`edgeDomain`。 数据流处理SDK的所有其他配置。 向Adobe Experience Platform Edge Network发送请求时，`edgeConfigId`用于引用服务器端配置。 这样，您无需在网站上更改代码即可更新配置。

您的组织必须为此功能设置。 请联系您的客户成功经理(CSM)，以便加入允许列表。

## 创建数据流配置

可以使用Datastream配置工具在Adobe [!DNL Experience Platform Launch]中创建Datastream。

![datastreams工具导航](../../assets/datastreams_config.png)

>[!NOTE]
>
>允许列表上的客户可以使用datastreams配置工具，而不管他们是否使用[!DNL Experience Platform Launch]作为标签管理器。 此外，用户需要[!DNL Experience Platform Launch]中的“开发”权限。 有关详细信息，请参阅[!DNL Experience Platform Launch]文档中的[用户权限](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/admin/user-permissions.html)文章。

单击屏幕右上角的&#x200B;**[!UICONTROL New Datastream]**&#x200B;创建数据流。 提供名称和说明后，系统会要求您为每个环境提供默认设置。 可用设置详见下文。

创建数据流时，会自动创建三个环境，设置相同。 这三个环境是&#x200B;*dev*、*stage*&#x200B;和&#x200B;*prod*。 它们与[!DNL Experience Platform Launch]中的三个默认环境匹配。 在将[!DNL Experience Platform Launch]库构建到开发环境时，库会自动使用配置中的开发环境。 您可以按自己喜欢的任意环境编辑设置。

SDK中用作`edgeConfigId`的ID是指定配置和环境（例如`1c86778b-cdba-4684-9903-750e52912ad1:stage`）的复合ID。 如果复合ID中没有环境（例如，上一个示例中的`stage`），则使用生产环境。

以下是每个配置环境的可用设置。 大多数部分可以启用或禁用。 禁用后，将保存您的设置，但不处于活动状态。

## [!UICONTROL Third Party ID] Settings

第三方ID部分是始终打开的唯一部分。 它有两个可用设置：&quot;[!UICONTROL Third Party ID Sync Enabled]&quot;和&quot;[!UICONTROL Third Party ID Sync Container ID]&quot;。

![配置UI的标识部分](../../assets/edge_configuration_identity.png)

### [!UICONTROL Third Party ID Sync Enabled]

控制SDK是否与第三方合作伙伴执行身份同步。

### [!UICONTROL Third Party ID Sync Container ID]

ID同步可以分组为容器，以允许在不同时间运行不同的ID同步。 这控制为给定配置ID运行哪个容器的ID同步。

## Adobe Experience Platform设置

此处列出的设置允许您将数据发送到Adobe Experience Platform。 您只应在已购买Adobe Experience Platform时启用此部分。

![Adobe Experience Platform设置块](../../assets/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

沙箱是Adobe Experience Platform中允许客户将其数据和实施彼此隔离的位置。 有关它们如何工作的详细信息，请参阅[沙箱文档](../../sandboxes/home.md)。

### [!UICONTROL Streaming Inlet]

流入口是Adobe Experience Platform中的HTTP源。 这些API在Adobe Experience Platform的“[!UICONTROL Sources]”选项卡下创建为HTTP API。

### [!UICONTROL Event Dataset]

数据流支持向具有[!UICONTROL Experience Event]类模式的数据集发送数据。

## Adobe Target设置

要配置Adobe Target，必须提供客户端代码。 其他字段为可选字段。

![Adobe Target设置块](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>与客户端代码关联的组织必须与创建配置ID的组织匹配。

### [!UICONTROL Client Code]

目标帐户的唯一ID。 要找到此问题，您可以导航到[!UICONTROL at.js]或[!UICONTROL mbox.js]的[!UICONTROL download]按钮旁的[!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementation] > [!UICONTROL edit settings]

### [!UICONTROL Property Token]

[!DNL Target] 允许客户通过使用属性来控制权限。有关详细信息，请参阅[!DNL Target]文档的[企业权限](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html)部分。

可以在[!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]中找到属性令牌

### [!UICONTROL Target Environment ID]

[Adobe Target](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) 中的环境可帮助您管理整个开发阶段的实施。此设置指定将与每个环境一起使用的环境。

Adobe建议对`dev`、`stage`和`prod`数据流环境分别设置不同的设置，以使操作变得简单。 但是，如果您已经定义了Adobe Target环境，则可以使用这些。

## Adobe Audience Manager设置

向Adobe Audience Manager发送数据所需的一切就是启用此部分。 其他设置是可选的，但鼓励使用。

![Adobe受众管理设置块](../../assets/edge_configuration_aam.png)

### [!UICONTROL Cookie Destinations Enabled]

允许SDK通过[!DNL Audience Manager]的Cookie目标](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)共享区段信息。[

### [!UICONTROL URL Destinations Enabled]

允许SDK通过[URL目标](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)共享区段信息。 这些配置在[!DNL Audience Manager]中。

## Adobe Analytics设置

控制是否将数据发送到Adobe Analytics。 其他详细信息请参阅[分析概述](../data-collection/adobe-analytics/analytics-overview.md)。

![Adobe Analytics设置块](../../assets/edge_configuration_aa.png)

### [!UICONTROL Report Suite ID]

报表包位于[!UICONTROL Admin > ReportSuites]下的“Adobe Analytics管理”部分。 如果指定了多个报表包，则数据将复制到每个报表包。
