---
title: 为Experience PlatformWeb SDK配置数据流
description: '了解如何配置数据流。 '
keywords: 配置；数据流；数据流ID；边缘；边缘配置ID；环境设置；边缘配置ID；标识；启用ID同步；ID同步容器ID；沙盒；流入口；事件数据集；目标；客户端代码；资产令牌；目标环境ID;Cookie目标；URL目标；Analytics设置阻止报表包ID;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---


# 配置数据流

Adobe Experience Platform Web SDK的配置分为两个位置。 SDK中的[configure命令](configuring-the-sdk.md)控制必须在客户端上处理的事项，如`edgeDomain`。 数据流处理SDK的所有其他配置。 将请求发送到Adobe Experience Platform边缘网络时， `edgeConfigId`用于引用服务器端配置。 这样，您就无需在网站上进行代码更改即可更新配置。

您的组织必须配置此功能。 请联系您的客户成功经理(CSM)以加入允许列表。

## 创建数据流配置

可以使用数据流配置工具在Adobe[!DNL Experience Platform Launch]中创建数据流。

![datastreams工具导航](../../assets/datastreams_config.png)

>[!NOTE]
>
>无论客户是否使用[!DNL Experience Platform Launch]作为标签管理器，允许列表上的客户都可以使用数据流配置工具。 此外，用户需要在[!DNL Experience Platform Launch]中拥有开发权限。 有关更多详细信息，请参阅[!DNL Experience Platform Launch]文档中的[用户权限](../../tags/ui/administration/user-permissions.md)文章。

单击屏幕右上方的&#x200B;**[!UICONTROL 新建数据流]**&#x200B;来创建数据流。 提供名称和描述后，系统会要求您为每个环境提供默认设置。 下面详细介绍了可用设置。

创建数据流时，会自动使用相同的设置创建三个环境。 这三个环境包括&#x200B;*dev*、*stage*&#x200B;和&#x200B;*prod*。 它们与[!DNL Experience Platform Launch]中的三个默认环境相匹配。 在将[!DNL Experience Platform Launch]库构建到开发环境时，库会自动使用您配置中的开发环境。 您可以根据需要，编辑各个环境中的设置。

SDK中用作`edgeConfigId`的ID是一个复合ID，用于指定配置和环境（例如，`1c86778b-cdba-4684-9903-750e52912ad1:stage`）。 如果复合ID中不存在任何环境（例如，上一个示例中的`stage`），则会使用生产环境。

以下是每个配置环境的可用设置。 大多数部分都可以启用或禁用。 禁用后，您的设置会保存，但处于非活动状态。

## [!UICONTROL 第三方] IDettings

第三方ID部分是唯一始终打开的部分。 它有两个可用的设置：&quot;[!UICONTROL 已启用第三方ID同步]&quot;和&quot;[!UICONTROL 第三方ID同步容器ID]&quot;。

![配置UI的标识部分](../../assets/edge_configuration_identity.png)

### [!UICONTROL 已启用第三方ID同步]

控制SDK是否执行与第三方合作伙伴的身份同步。

### [!UICONTROL 第三方ID同步容器ID]

ID同步可以分组到容器中，以允许在不同时间运行不同的ID同步。 这可控制为给定配置ID运行哪个ID同步容器。

## Adobe Experience Platform设置

通过此处列出的设置，您可以将数据发送到Adobe Experience Platform。 仅当您购买了Adobe Experience Platform时，才应启用此部分。

![Adobe Experience Platform设置块](../../assets/edge_configuration_aep.png)

### [!UICONTROL 沙盒]

沙盒是Adobe Experience Platform中的一些位置，允许客户相互隔离其数据和实施。 有关这些沙盒工作方式的更多详细信息，请参阅[沙盒文档](../../sandboxes/home.md)。

### [!UICONTROL 流入口]

流入口是Adobe Experience Platform中的HTTP源。 这些API是在Adobe Experience Platform的“[!UICONTROL Sources]”选项卡下创建的，作为HTTP API。

### [!UICONTROL 事件数据集]

数据流支持将数据发送到具有类[!UICONTROL Experience Event]架构的数据集。

## Adobe Target设置

要配置Adobe Target，必须提供客户端代码。 其他字段为可选字段。

![Adobe Target设置块](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>与客户端代码关联的组织必须与创建配置ID的组织匹配。

### [!UICONTROL 客户端代码]

目标帐户的唯一ID。 要找到此内容，您可以导航到[!UICONTROL Adobe Target] > [!UICONTROL [!UICONTROL >实施] > [!UICONTROL 编辑[!UICONTROL 下载]按钮旁边的[!UICONTROL at.js]或[!UICONTROL mbox.js]]]

### [!UICONTROL 资产令牌]

[!DNL Target] 允许客户通过使用资产来控制权限。有关详细信息，请参阅[!DNL Target]文档的[企业权限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html)部分。

资产令牌可在[!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]中找到

### [!UICONTROL Target环境ID]

[](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Adobe Target中的环境可帮助您在开发的所有阶段中管理实施。此设置指定要在每个环境中使用的环境。

Adobe建议对`dev`、`stage`和`prod`数据流环境分别设置不同的设置方式，以保持操作简单。 但是，如果您已经定义了Adobe Target环境，则可以使用这些环境。

## Adobe Audience Manager设置

将数据发送到Adobe Audience Manager所需的一切就是启用此部分。 其他设置是可选的，但鼓励使用。

![Adobe受众管理设置块](../../assets/edge_configuration_aam.png)

### [!UICONTROL Cookie目标已启用]

允许SDK通过[Cookie目标](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)从[!DNL Audience Manager]共享区段信息。

### [!UICONTROL 启用URL目标]

允许SDK通过[URL目标](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)共享区段信息。 这些配置在[!DNL Audience Manager]中。

## Adobe Analytics设置

控制数据是否被发送到Adobe Analytics。 有关更多详细信息，请参阅[Analytics概述](../data-collection/adobe-analytics/analytics-overview.md)。

![Adobe Analytics设置块](../../assets/edge_configuration_aa.png)

### [!UICONTROL 报表包 ID]

报表包位于[!UICONTROL 管理员> ReportSuites]下的Adobe Analytics管理员部分。 如果指定了多个报表包，则数据会复制到每个报表包。
