---
title: 边缘配置
seo-title: Experience PlatformWeb SDK的边缘配置
description: '了解如何配置Experience Platform边缘网络。 '
seo-description: '了解如何配置Experience Platform边缘网络。 '
keywords: configuration;edge;edge configuration id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite id;
translation-type: tm+mt
source-git-commit: 94b3faf3157f4e1f4e46b6055914a04883dc44fa
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 1%

---


# 配置Edge

Adobe Experience PlatformWeb SDK的配置分为两个位置。 SDK中的[configure命令](configuring-the-sdk.md)控制必须在客户端处理的事项，如`edgeDomain`。 边缘配置处理SDK的所有其他配置。 向Adobe Experience Platform边缘网络发送请求时，`edgeConfigId`用于引用服务器端配置。 这样，您无需在网站上更改代码即可更新配置。

您的组织必须配置此功能。 请联系您的客户成功经理(CSM)，开始允许列表。

## 创建边缘配置

可以使用边缘配置工具在Adobe[!DNL Experience Platform Launch]中创建边缘配置。

![边缘配置工具导航](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>无论客户是否使用[!DNL Experience Platform Launch]作为标签管理器，允许列表上的客户都可以使用边缘配置工具。 此外，用户需要[!DNL Experience Platform Launch]中的“开发”权限。 有关详细信息，请参阅[!DNL Experience Platform Launch]文档中的[用户权限](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/admin/user-permissions.html)文章。

通过单击屏幕右上角的&#x200B;**[!UICONTROL 新建边缘配置]**&#x200B;创建边缘配置。 提供名称和说明后，系统会要求您为每个环境提供默认设置。 可用设置详见下文。

创建边缘配置时，会自动创建三个环境，设置相同。 这三个环境是&#x200B;*dev*、*stage*&#x200B;和&#x200B;*prod*。 它们与[!DNL Experience Platform Launch]中的三个默认环境匹配。 当您为开发环境构建[!DNL Experience Platform Launch]库时，库会自动使用配置中的开发环境。 您可以根据自己的喜好在各个环境中编辑设置。

SDK中使用的ID（作为`edgeConfigId`）是指定配置和环境（例如`1c86778b-cdba-4684-9903-750e52912ad1:stage`）的复合ID。 如果复合ID中不存在环境（例如，上一个示例中的`stage`），则使用生产环境。

在下面，您将找到每个配置环境的可用设置。 大多数部分都可以启用或禁用。 禁用后，将保存您的设置，但不处于活动状态。

## [!UICONTROL 身份] 设置

标识部分是始终打开的唯一部分。 它有两个可用设置：&quot;[!UICONTROL ID同步已启用]&quot;和&quot;[!UICONTROL ID同步容器ID]&quot;。

![配置UI的标识部分](../../assets/edge_configuration_identity.png)

### [!UICONTROL 已启用ID同步]

控制SDK是否与第三方合作伙伴执行身份同步。

### [!UICONTROL ID同步容器ID]

ID同步可以分组为容器，以允许在不同时间运行不同的ID同步。 此控制为给定配置ID运行哪个容器的ID同步。

## Adobe Experience Platform设置

此处列出的设置允许您将数据发送到Adobe Experience Platform。 只有在购买了Adobe Experience Platform时，才应启用此部分。

![Adobe Experience Platform设置块](../../assets/edge_configuration_aep.png)

### [!UICONTROL 沙箱]

沙箱是位于Adobe Experience Platform的一个位置，它允许客户将其数据和实施相互隔离。 有关它们如何工作的详细信息，请参阅[沙箱文档](../../sandboxes/home.md)。

### [!UICONTROL Streaming Inlet]

流入口是Adobe Experience Platform的HTTP源。 这些API在Adobe Experience Platform的“[!UICONTROL 源]”选项卡下创建为HTTP API。

### [!UICONTROL 事件数据集]

边缘配置支持将数据发送到具有[!UICONTROL 体验事件]类模式的数据集。

## Adobe Target设置

要配置Adobe Target，必须提供客户端代码。 其他字段为可选字段。

![Adobe Target设置块](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>与客户端代码关联的组织必须与创建配置ID的组织匹配。

### [!UICONTROL 客户端代码]

目标帐户的唯一ID。 要找到此问题，您可以导航到[!UICONTROL at.js]或&lt;a11/>的&lt;a8/>下载]按钮旁边的[!UICONTROL Adobe Target]>[!UICONTROL 安装][!UICONTROL >实施]>[!UICONTROL 编辑设置]2/>mbox.js][!UICONTROL [!UICONTROL 

### [!UICONTROL 属性令牌]

[!DNL Target] 允许客户通过使用属性来控制权限。有关详细信息，请参阅[!DNL Target]文档的[企业权限](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html)部分。

属性令牌可在[!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL 属性]中找到

### [!UICONTROL 目标环境ID]

[adobe target](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) 的环境可以帮助您管理整个开发阶段的实施。此设置指定要与每个环境一起使用的环境。

Adobe建议对`dev`、`stage`和`prod`边缘配置环境以不同方式设置此选项，以简化操作。 但是，如果您已定义了Adobe Target环境，则可以使用这些。

## Adobe Audience Manager设置

向Adobe Audience Manager发送数据所需的一切就是启用本节。 其他设置是可选的，但鼓励使用。

![Adobe受众管理设置块](../../assets/edge_configuration_aam.png)

### [!UICONTROL 已启用Cookie目标]

允许SDK通过[Cookie目标](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)从[!DNL Audience Manager]共享段信息。

### [!UICONTROL 已启用URL目标]

允许SDK通过[URL目标](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)共享段信息。 这些配置在[!DNL Audience Manager]中。

## Adobe Analytics设置

控制数据是否发送到Adobe Analytics。 其他详细信息请参阅[分析概述](../data-collection/adobe-analytics/analytics-overview.md)。

![Adobe Analytics设置块](../../assets/edge_configuration_aa.png)

### [!UICONTROL 报表包 ID]

报表包位于[!UICONTROL 管理> ReportSuites]下的“Adobe Analytics管理员”部分。 如果指定了多个报表包，则数据将复制到每个报表包。
