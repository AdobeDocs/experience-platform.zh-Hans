---
title: 边缘配置
seo-title: Experience Platform Web SDK的边缘配置
description: '了解如何配置Experience Platform Edge Network。 '
seo-description: '了解如何配置Experience Platform Edge Network。 '
translation-type: tm+mt
source-git-commit: efbc080117754cee01f21c9f9ec409204648e757

---


# （测试版）边缘配置

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Platfrom Web SDK的配置分为两个位置。 SDK [中的](configuring-the-sdk.md) configure命令控制必须在客户端处理的事项，如 `edgeDomain`。 边缘配置处理SDK的所有其他配置。 当请求发送到Adobe Experience Platform Edge Network时， `edgeConfigId` 将引用服务器端配置。 这样，您无需在网站上更改代码即可更新配置。

## 创建边缘配置ID

可以在启动中使用边缘配置工具创建边缘配置ID。 此工具允许您创建边缘配置以及这些配置中的环境。

![边缘配置工具导航](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>无论客户是否将Launch用作标签管理器，白名单客户都可以使用边缘配置工具。 此外，用户需要在Launch中具有“开发”权限。 有关更多 [详细信息](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/admin/user-permissions.html) ，请参阅启动文档中的用户权限文章。

单击屏幕右上角的“UICONTROL **[新边缘配置]** ”可创建边缘配置。 提供名称和说明后，系统会要求您为每个环境提供默认设置。

### 默认环境设置

这些默认设置用于创建设置相同的前三个环境。 这三个环境是dev、stage和prod。 它们与启动项中的三个默认环境匹配。 在将启动库构建为开发环境时，库会自动使用配置中的开发环境。 您可以根据自己的喜好在各个环境中编辑设置。

SDK中使用的ID，作为 `edgeConfigId` 一个指定配置和环境的复合ID。 如果没有环境，则使用生产环境。

### 环境设置

以下是环境可用的各项设置。 大多数部分都可以启用或禁用。 禁用后，将保存您的设置，但不处于活动状态。

#### [!UICONTROL Identity]

标识部分是始终打开的唯一部分。 它有两个可用设置： ID同步已启用和ID同步容器ID。

![配置UI的标识部分](../../assets/edge_configuration_identity.png)

##### [!UICONTROL ID Sync Enabled]

控制SDK是否与第三方合作伙伴执行身份同步。

##### [!UICONTROL ID Sync Container ID]

ID同步可以分组为容器，以允许在不同时间运行不同的ID同步。 此控制为给定配置ID运行哪个容器的ID同步。

#### Adobe Experience Platform

此处列出的设置允许您将数据发送到Adobe Experience Platform。 只有在购买了Adobe Experience Platform后，您才应启用此部分。

![Adobe Experience Platform设置块](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Sandbox]

沙箱是Adobe Experience Platform中的位置，允许客户将其数据和实施相互隔离。 沙箱文档中提供了有关它们工作方式的更 [多详细信息](../../sandboxes/home.md)。

##### [!UICONTROL Streaming Inlet]

流入口是Adobe Experience Platform中的HTTP源。 这些API在Adobe [!UICONTROL Sources] Experience Platform的选项卡下创建为HTTP API。

##### [!UICONTROL Event Dataset]

边缘配置支持将数据发送到具有类模式的数据集 [!UICONTROL Experience Event]。

#### Adobe Target

要配置Adobe目标，必须提供客户端代码。 其他字段为可选字段。

![Adobe目标设置块](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>与客户端代码关联的组织必须与创建配置ID的组织匹配。

##### [!UICONTROL Client Code]

目标帐户的唯一ID。 要找到此项，您可以导 [!UICONTROL Adobe Target] 航到> [!UICONTROL Setup]> [!UICONTROL Implementation] > [!UICONTROL edit settings] Button旁 [!UICONTROL download][!UICONTROL at.js] 边，或者 [!UICONTROL mbox.js]

##### [!UICONTROL Property Token]

目标允许客户通过使用属性来控制权限。 详细信息可在目标文 [档的“企业](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) 权限”部分找到。

可以在> > UICONTROL属性中 [!UICONTROL Adobe Target] 找 [!UICONTROL setup] 到属 [性令牌]

##### [!UICONTROL Target Environment ID]

[Adobe](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) 目标中的环境可帮助您管理整个开发阶段的实施。 此设置指定要与每个环境一起使用的环境。

Adobe建议对每个配置环境、 `dev``stage`和边 `prod` 缘配置设置不同的设置。 但是，如果您已经定 [!UICONTROL Adobe Target environments] 义了，则可以使用这些。

#### Adobe Audience Manager

向Adobe受众管理器发送数据所需的全部功能就是启用此部分。 其他设置是可选的，但鼓励使用。

![Adobe受众管理设置块](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Cookie Destinations Enabled]

允许SDK通过受众管理器中的 [Cookie目标](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 共享区段信息。

##### [!UICONTROL URL Destinations Enabled]

允许SDK通过URL目标共享区 [段信息](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)。 这些配置在受众管理器中。

#### Adobe Analytics

控制数据是否发送到Adobe Analytics。 更多详细信息请参 [阅分析概述](../solution-specific/analytics/analytics-overview.md)。

![Adobe Analytics设置块](../../assets/edge_configuration_aa.png)

##### [!UICONTROL Report Suite ID]

报表包位于下方的“Adobe Analytics管理员”部分 [!UICONTROL Admin > ReportSuites]。 如果指定了多个报表包，则数据将复制到每个报表包。
