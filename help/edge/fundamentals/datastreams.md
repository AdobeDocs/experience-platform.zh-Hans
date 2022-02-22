---
title: 为Experience PlatformWeb SDK配置数据流
description: '了解如何配置数据流。 '
keywords: 配置；数据流；数据流ID；边缘；数据流ID；环境设置；edgeConfigId；身份；启用ID同步的容器ID；沙盒；流入口；事件数据集；目标；客户端代码；资产令牌；目标环境ID;Cookie目标；URL目标；Analytics设置阻止报表包ID;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 74c19bb0498002b81f93954d4d8e40f0df36c97d
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 1%

---


# 配置数据流

Adobe Experience Platform Web SDK的配置分为两个位置。 的 [配置命令](configuring-the-sdk.md) 中的控制必须在客户端上处理的事项，例如 `edgeDomain`. 数据流处理SDK的所有其他配置。 请求发送至Adobe Experience Platform边缘网络时， `edgeConfigId` 用于引用服务器端配置。 这样，您就无需在网站上进行代码更改即可更新配置。

您的组织必须配置此功能。 请联系您的客户成功经理(CSM)以加入允许列表。

## 创建数据流配置

您可以通过选择 **[!UICONTROL 数据流]** 中。

![datastreams工具导航](../images/datastreams/config.png)

>[!NOTE]
>
>而您可以 [!UICONTROL 数据流] 选项卡无论您是否使用Platform的标签管理功能，都必须拥有开发人员权限来自行管理数据流。 请参阅 [用户权限](../../tags/ui/administration/user-permissions.md) 有关更多详细信息，请参阅标记文档中的文章。

通过单击 **[!UICONTROL 新数据流]** 中。 提供名称和描述后，系统会要求您为每个环境提供默认设置。 下面详细介绍了可用设置。

创建数据流时，会自动使用相同的设置创建三个环境。 这三个环境包括 *开发*, *阶段*&#x200B;和 *prod*. 它们与标记的三个默认环境相匹配。 在将标记库构建到开发环境时，该库会自动使用您配置中的开发环境。 您可以根据需要，编辑各个环境中的设置。

SDK中用作 `edgeConfigId` 是一个复合ID，用于指定配置和环境(例如， `1c86778b-cdba-4684-9903-750e52912ad1:stage`)。 如果复合ID中不存在环境(例如， `stage` 在上一个示例中)，则会使用生产环境。

以下是每个配置环境的可用设置。 大多数部分都可以启用或禁用。 禁用后，您的设置会保存，但处于非活动状态。

## [!UICONTROL 第三方ID] 设置

第三方ID部分是唯一始终打开的部分。 它有两个可用的设置：&quot;[!UICONTROL 已启用第三方ID同步]&quot;和&quot;[!UICONTROL 第三方ID同步容器ID]&quot;

![配置UI的标识部分](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL 已启用第三方ID同步]

控制SDK是否执行与第三方合作伙伴的身份同步。

### [!UICONTROL 第三方ID同步容器ID]

ID同步可以分组到容器中，以允许在不同时间运行不同的ID同步。 这可控制为给定配置ID运行哪个ID同步容器。

## Adobe Experience Platform设置

通过此处列出的设置，您可以将数据发送到Adobe Experience Platform。 仅当您购买了Adobe Experience Platform时，才应启用此部分。

![Adobe Experience Platform设置块](../images/datastreams/platform-config.png)

| 字段 | 描述 |
| --- | --- |
| [!UICONTROL 沙盒] | **（必需）** 选择要将数据发送到的平台沙盒。 沙盒是Adobe Experience Platform中的虚拟分区，允许您将数据和实施与组织中的其他人员隔离开来。<br><br>如果在不选择沙盒的情况下创建数据流，则以后仍可以选择沙盒。<br><br>创建数据流并选择沙盒后，便无法更改沙盒。 的 [!UICONTROL 沙盒] 因此，在编辑具有选定沙箱的现有数据流时，选择字段不可用。<br><br> 的 [!UICONTROL 沙盒] 因此，在编辑现有数据流时，选择字段不可用。<br><br>有关沙箱在Experience Platform中角色的更多详细信息，请参阅 [沙盒文档](../../sandboxes/home.md). |
| [!UICONTROL 事件数据集] | **（必需）** 选择将客户事件数据流式传输到的Platform数据集。 此架构必须使用 [XDM ExperienceEvent类](../../xdm/classes/experienceevent.md). |
| [!UICONTROL 配置文件数据集] | 选择要将客户属性数据发送到的Platform数据集。 此架构必须使用 [XDM个人配置文件类](../../xdm/classes/individual-profile.md). |
| [!UICONTROL 优惠决策] | 选中此复选框可启用Platform Web SDK实施的Offer decisioning。 请参阅 [将Offer decisioning与Platform Web SDK结合使用](../personalization/offer-decisioning/offer-decisioning-overview.md) 以了解更多实施详细信息。 有关Offer decisioning功能的更多信息，请参阅 [Adobe Journey Optimizer文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=zh-Hans). |
| [!UICONTROL 边缘分割] | 选中此复选框可启用 [边缘分割](../../segmentation/ui/edge-segmentation.md) 数据流。 当Platform Web SDK通过启用了边缘分段的数据流发送数据时，相关用户档案的任何更新区段成员关系都将在响应中发送回。<br><br>此选项可与 [!UICONTROL 个性化目标] 表示 [下一页个性化用例](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL 个性化目标] | 与 [!UICONTROL 边缘分割] 复选框，此选项允许数据流连接到个性化引擎，如Adobe Target。 有关的具体步骤，请参阅目标文档 [配置个性化目标](../../destinations/ui/configure-personalization-destinations.md). |

## Adobe Target设置

要配置Adobe Target，必须提供客户端代码。 其他字段为可选字段。

![Adobe Target设置块](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>与客户端代码关联的组织必须与创建配置ID的组织匹配。

### [!UICONTROL 客户端代码]

目标帐户的唯一ID。 要查找此内容，您可以导航到 [!UICONTROL Adobe Target] > [!UICONTROL 设置]> [!UICONTROL 实施] > [!UICONTROL 编辑设置] 旁边 [!UICONTROL 下载] 按钮 [!UICONTROL at.js] 或 [!UICONTROL mbox.js]

### [!UICONTROL 资产令牌]

[!DNL Target] 允许客户通过使用资产来控制权限。 有关详细信息可在 [企业权限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 部分 [!DNL Target] 文档。

资产令牌可在 [!UICONTROL Adobe Target] > [!UICONTROL 设置] > [!UICONTROL 属性]

### [!UICONTROL Target环境ID]

[环境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 在Adobe Target中，帮助您管理所有开发阶段的实施。 此设置指定要在每个环境中使用的环境。

Adobe建议对您的 `dev`, `stage`和 `prod` 数据流环境，使事情保持简单。 但是，如果您已经定义了Adobe Target环境，则可以使用这些环境。

## Adobe Audience Manager设置

将数据发送到Adobe Audience Manager所需的一切就是启用此部分。 其他设置是可选的，但鼓励使用。

![Adobe受众管理设置块](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Cookie目标已启用]

允许SDK通过 [Cookie目标](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 从 [!DNL Audience Manager].

### [!UICONTROL 启用URL目标]

允许SDK通过 [URL目标](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). 这些配置在 [!DNL Audience Manager].

## Adobe Analytics设置

控制数据是否被发送到Adobe Analytics。 其他详细信息位于 [Analytics概述](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics设置块](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL 报表包 ID]

报表包可在Adobe Analytics管理员部分的下方找到 [!UICONTROL 管理员>报表包]. 如果指定了多个报表包，则数据会复制到每个报表包。
