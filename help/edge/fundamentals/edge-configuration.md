---
title: 边缘配置
seo-title: Experience PlatformWeb SDK的边缘配置
description: '了解如何配置Experience Platform边缘网络。 '
seo-description: '了解如何配置Experience Platform边缘网络。 '
keywords: configuration;edge;edge configuration id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite id;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 1%

---


# 配置Edge

Adobe Experience PlatformWeb SDK的配置分为两个位置。 SDK [中的](configuring-the-sdk.md) configure命令控制必须在客户端处理的事项，如 `edgeDomain`。 边缘配置处理SDK的所有其他配置。 向Adobe Experience Platform边缘网络发送请求时， `edgeConfigId` 将引用服务器端配置。 这样，您无需在网站上更改代码即可更新配置。

您的组织必须配置此功能。 请联系您的认证软件经理(CSM)，开始允许列表。

## 创建边缘配置

可使用边配置工具在Adobe [!DNL Experience Platform Launch] 中创建边配置。

![边缘配置工具导航](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>无论客户是否使用标签管理器，允许列表上的客户都可 [!DNL Experience Platform Launch] 以使用边缘配置工具。 此外，用户需要中的“开发”权 [!DNL Experience Platform Launch]限。 有关更多 [详细信息](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/admin/user-permissions.html) ，请参 [!DNL Experience Platform Launch] 阅文档中的“用户权限”文章。

通过单击屏幕右上方区 **[!UICONTROL 域的“新建边]** ”(New Edge Configuration)创建边配置。 提供名称和说明后，系统会要求您为每个环境提供默认设置。 可用设置详见下文。

创建边缘配置时，会自动创建三个环境，设置相同。 这三个环境 *是* dev *、* stage *和* prod。 它们与中的三个默认环境匹 [!DNL Experience Platform Launch]配。 在为开发环境 [!DNL Experience Platform Launch] 构建库时，库会自动使用配置中的开发环境。 您可以根据自己的喜好在各个环境中编辑设置。

SDK中使用的ID(作为 `edgeConfigId` 一个复合ID)，它指定配置和环境(例如 `1c86778b-cdba-4684-9903-750e52912ad1:stage`)。 如果复合ID中没有环境(例如，在上 `stage` 一个示例中)，则使用生产环境。

在下面，您将找到每个配置环境的可用设置。 大多数部分都可以启用或禁用。 禁用后，将保存您的设置，但不处于活动状态。

## [!UICONTROL 身份设置]

标识部分是始终打开的唯一部分。 它有两个可用设置：“[!UICONTROL ID Sync Enabled]”和“[!UICONTROL ID Sync容器ID]”。

![配置UI的标识部分](../../assets/edge_configuration_identity.png)

### [!UICONTROL 已启用ID同步]

控制SDK是否与第三方合作伙伴执行身份同步。

### [!UICONTROL ID同步容器ID]

ID同步可以分组为容器，以允许在不同时间运行不同的ID同步。 此控制为给定配置ID运行哪个容器的ID同步。

## Adobe Experience Platform设置

此处列出的设置允许您将数据发送到Adobe Experience Platform。 只有在购买了Adobe Experience Platform时，才应启用此部分。

![Adobe Experience Platform设置块](../../assets/edge_configuration_aep.png)

### [!UICONTROL 沙箱]

沙箱是位于Adobe Experience Platform的一个位置，它允许客户将其数据和实施相互隔离。 有关它们如何工作的更多详细信息，请参 [阅沙箱文档](../../sandboxes/home.md)。

### [!UICONTROL Streaming Inlet]

流入口是Adobe Experience Platform的HTTP源。 这些API在Adobe Experience Platform[!UICONTROL 的]“源”选项卡下创建为HTTP API。

### [!UICONTROL 事件数据集]

边缘配置支持将数据发送到具有类体验模式 [!UICONTROL 的事件]。

## Adobe Target设置

要配置Adobe Target，必须提供客户端代码。 其他字段为可选字段。

![Adobe Target设置块](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>与客户端代码关联的组织必须与创建配置ID的组织匹配。

### [!UICONTROL 客户端代码]

目标帐户的唯一ID。 要找到此项，您可以导航到 [!UICONTROL Adobe Target] >设置 [!UICONTROL >实施]>下一步， [!UICONTROL 到下载按] 钮中编辑按钮( [!UICONTROL 用于。js或mbox.js)。]

### [!UICONTROL 属性令牌]

[!DNL Target] 允许客户通过使用属性来控制权限。 详细信息可在文档的 [“企业权限](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) ”部分 [!DNL Target] 找到。

属性令牌可在Adobe Target [!UICONTROL >设置] > [!UICONTROL 属性][!UICONTROL 中]

### [!UICONTROL 目标环境ID]

[环境](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) (Adobe Target)的可帮助您管理整个开发阶段的实施。 此设置指定要与每个环境一起使用的环境。

Adobe建议对每个配置、 `dev`和边 `stage`缘配置 `prod` 环境进行不同的设置，以简化操作。 但是，如果您已定义了Adobe Target环境，则可以使用这些。

## Adobe Audience Manager设置

向Adobe Audience Manager发送数据所需的一切就是启用本节。 其他设置是可选的，但鼓励使用。

![Adobe受众管理设置块](../../assets/edge_configuration_aam.png)

### [!UICONTROL 已启用Cookie目标]

允许SDK通过Cookie目标共 [享区段信息](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)[!DNL Audience Manager]。

### [!UICONTROL 已启用URL目标]

允许SDK通过URL目标共享区 [段信息](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)。 这些配置在 [!DNL Audience Manager]。

## Adobe Analytics设置

控制数据是否发送到Adobe Analytics。 更多详细信息请参 [阅分析概述](../data-collection/adobe-analytics/analytics-overview.md)。

![Adobe Analytics设置块](../../assets/edge_configuration_aa.png)

### [!UICONTROL 报表包 ID]

报表包位于“管理员”>“报表包”下的“Adobe Analytics [!UICONTROL 管理员”部分]。 如果指定了多个报表包，则数据将复制到每个报表包。
