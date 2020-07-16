---
title: 边缘配置
seo-title: Experience PlatformWeb SDK的边缘配置
description: '了解如何配置Experience Platform边缘网络。 '
seo-description: '了解如何配置Experience Platform边缘网络。 '
translation-type: tm+mt
source-git-commit: 2d47a00c91000c68c7331f88015264259a4e6323
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 2%

---


# 配置Edge

Adobe Experience PlatformWeb SDK的配置分为两个位置。 SDK [中的](configuring-the-sdk.md) configure命令控制必须在客户端处理的事项，如 `edgeDomain`。 边缘配置处理SDK的所有其他配置。 向Adobe Experience Platform边缘网络发送请求时， `edgeConfigId` 将引用服务器端配置。 这样，您无需在网站上更改代码即可更新配置。

## 创建边缘配置ID

可在Adobe中使用边缘配 [!DNL Launch] 置工具创建边缘配置ID。 此工具允许您创建边缘配置以及这些配置中的环境。

![边缘配置工具导航](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>
>
>无论客户是否使用标签管理器，允许列表上的客户都可 [!DNL Launch] 以使用边缘配置工具。 此外，用户需要中的“开发”权 [!DNL Launch]限。 有关更多 [详细信息](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/admin/user-permissions.html) ，请参 [!DNL Launch] 阅文档中的“用户权限”文章。

单击屏幕右上方区域的“ **[!UICONTROL 新建边缘配置]** ”可创建边缘配置。 提供名称和说明后，系统会要求您为每个环境提供默认设置。

### 默认环境设置

这些默认设置用于创建设置相同的前三个环境。 这三个环境 *是* dev *、* stage *和* prod。 它们与中的三个默认环境匹 [!DNL Launch]配。 在为开发环境 [!DNL Launch] 构建库时，库会自动使用配置中的开发环境。 您可以根据自己的喜好在各个环境中编辑设置。

SDK中使用的ID，作为 `edgeConfigId` 一个指定配置和环境的复合ID。 如果没有环境，则使用生产环境。

### 环境设置

以下是环境可用的各项设置。 大多数部分都可以启用或禁用。 禁用后，将保存您的设置，但不处于活动状态。

#### [!UICONTROL 身份]

标识部分是始终打开的唯一部分。 它有两个可用设置： [!UICONTROL ID同步已启用][!UICONTROL ,]ID同步容器ID。

![配置UI的标识部分](../../assets/edge_configuration_identity.png)

##### [!UICONTROL 已启用ID同步]

控制SDK是否与第三方合作伙伴执行身份同步。

##### [!UICONTROL ID同步容器ID]

ID同步可以分组为容器，以允许在不同时间运行不同的ID同步。 此控制为给定配置ID运行哪个容器的ID同步。

#### Adobe Experience Platform

此处列出的设置允许您向Adobe Experience Platform发送数据。 您只应在已购买Adobe Experience Platform时启用此部分。

![Adobe Experience Platform设置块](../../assets/edge_configuration_aep.png)

##### [!UICONTROL 沙箱]

沙箱是Adobe Experience Platform中允许客户将其数据和实施彼此隔离的位置。 有关它们如何工作的更多详细信息，请参 [阅沙箱文档](../../sandboxes/home.md)。

##### [!UICONTROL Streaming Inlet]

流入口是Adobe Experience Platform中的HTTP源。 这些API在Adobe Experience Platform [!UICONTROL 的] “源”选项卡下创建为HTTP API。

##### [!UICONTROL 事件数据集]

边缘配置支持将数据发送到具有类体验模式 [!UICONTROL 的事件]。

#### Adobe Target

要配置Adobe Target，必须提供客户端代码。 其他字段为可选字段。

![Adobe Target设置块](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>
>
>与客户端代码关联的组织必须与创建配置ID的组织匹配。

##### [!UICONTROL 客户端代码]

目标帐户的唯一ID。 要找到此项，您可以导航到 [!UICONTROL Adobe Target] >设置 [!UICONTROL >安装]> [!UICONTROL 实施] > [!UICONTROL 下一个到的下][!UICONTROL 载按钮的“编辑”按钮，该按钮用于。js或mbox.js]

##### [!UICONTROL 属性令牌]

目标允许客户通过使用属性来控制权限。 详细信息可在目标文 [档的“企业](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) 权限”部分找到。

可以在“Adobe Target”>“设置” [!UICONTROL >“属性] ” [!UICONTROL 中找到属] 性令 [!UICONTROL 牌]

##### [!UICONTROL 目标环境ID]

[环境](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) -Adobe Target-帮助您管理整个开发阶段的实施。 此设置指定要与每个环境一起使用的环境。

Adobe建议对每个配置环境、 `dev``stage`和边 `prod` 缘配置设置不同的设置。 但是，如果您已经定 [!UICONTROL 义了Adobe Target] 环境，则可以使用这些。

#### Adobe Audience Manager

向Adobe Audience Manager发送数据所需的一切就是启用此部分。 其他设置是可选的，但鼓励使用。

![Adobe受众管理设置块](../../assets/edge_configuration_aam.png)

##### [!UICONTROL 已启用Cookie目标]

允许SDK通过Audience Manager中的Cookie目 [标共享](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 段信息。

##### [!UICONTROL 已启用URL目标]

允许SDK通过URL目标共享区 [段信息](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)。 这些配置采用Audience Manager。

#### Adobe Analytics

控制数据是否发送到AdobeAnalytics。 更多详细信息请参 [阅Analytics概述](../solution-specific/analytics/analytics-overview.md)。

![AdobeAnalytics设置块](../../assets/edge_configuration_aa.png)

##### [!UICONTROL 报表包 ID]

报表包位于AdobeAnalytics管理员区域的“管理员”>“ [!UICONTROL 报表包”下]。 如果指定了多个报表包，则数据将复制到每个报表包。
