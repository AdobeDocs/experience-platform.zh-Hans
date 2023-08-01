---
keywords: 目标；adobe experience platform；平台；目标概述；激活数据；激活；
title: 目标概述
description: 目标是预先构建的与目标平台的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用Adobe Experience Platform中的“目标”来激活跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例的已知和未知数据。
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: ce1aec87b827b6e8626018846bc6f438834fff54
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 4%

---

# [!DNL Destinations] 概述 {#overview}

![目标概述横幅](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 目标和源 {#destinations-and-sources}

Platform的核心功能之一是摄取您的第一方数据，并根据您的业务需求激活该数据。 使用 [源](../sources/home.md) 将数据摄取到Platform和目标以从Platform导出数据。

## 目标步骤 {#steps}

* 从 [自助服务目录](./catalog/overview.md) Platform中所有可用的目标。
* 使用目标将用户档案或受众发送到营销自动化平台、数字广告平台等。
* 定期安排数据导出到您的首选目标。

## 控件 {#controls}

中的控件 [目标工作区](./ui/destinations-workspace.md) 允许您：

* 浏览可在其中激活数据的目标平台目录；
* 创建、编辑、激活和禁用流向目录中的目标的数据流；
* 在存储位置中创建帐户或将Platform链接到目标平台中的帐户；
* 选择应将哪些受众激活到目标；
* 选择 [体验数据模型(XDM)字段](../xdm/home.md) 以将受众激活到电子邮件营销目标时导出。

## 目标类型和类别 {#types-and-categories}

借助Experience Platform，您可以将数据激活到各种类型的目标，以满足您的激活用例要求。 目标范围从基于API的集成，到与文件接收系统、配置文件查找目标的集成，等等。 有关所有可用目标的详细信息，请参阅 [目标类型和类别概述](./destination-types.md).

## Adobe构建和合作伙伴构建的目标 {#adobe-and-partner-built-destinations}

Experience Platform目标目录中的某些连接器是由Adobe构建和维护的，而其他连接器是由合作伙伴公司使用构建和维护的 [Destination SDK](/help/destinations/destination-sdk/overview.md). 如果合作伙伴创建并维护了目标，则每个合作伙伴构建的连接器在文档页面顶部的注释会标出。 例如， [Amazon S3连接器](/help/destinations/catalog/cloud-storage/amazon-s3.md) 由Adobe创建，而 [TikTok连接器](/help/destinations/catalog/social/tiktok.md) 由TikTok团队创建和维护。

对于合作伙伴创作并维护的连接器，这意味着连接器问题可能需要由合作伙伴团队解决（文档页面注释中提供的联系方法）。 有关Adobe创作和维护的连接器出现的问题，请联系您的Adobe代表或客户关怀团队。

## 目标和访问控制 {#access-controls}

Platform中的目标功能可与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以查看、管理和激活目标。 有关各个权限的信息，请参阅 [Adobe Experience Platform中的访问控制](../access-control/home.md) 并向下滚动到页面底部。

下表概述了对目标执行某些操作所需的权限和权限组合：

| 权限级别 | 描述 |
| ---- | ---- |
| **[!UICONTROL 管理目标]** | 要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). |
| **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** | 要将受众激活到目标并启用 [映射步骤](ui/activate-batch-profile-destinations.md#mapping) 的工作流中，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). |
| **[!UICONTROL 管理目标]**， **[!UICONTROL 激活没有映射的区段]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** | 要将受众激活到目标并隐藏 [映射步骤](ui/activate-batch-profile-destinations.md#mapping) 的工作流中，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活没有映射的区段]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). |

{style="table-layout:auto"}

有关访问控制的详细信息，请参见 [访问控制用户指南](../access-control/ui/overview.md).

### 目标的基于属性的访问控制 {#attribute-based-access}

Adobe Experience Platform中基于属性的访问控制允许管理员根据属性控制对特定对象和/或权能的访问。

通过基于属性的访问控制，您可以将映射配置应用到您拥有权限的字段。 此外，如果您无权访问数据集中的所有字段，则无法将数据导出到目标。

有关目标如何使用基于属性的访问控制的详细信息，请参阅 [基于属性的访问控制概述](../access-control/abac/overview.md#destinations).

## 目标监控 {#destinations-monitoring}

在建立与目标连接并完成激活工作流后，您可以监控向接收系统导出的数据。 阅读 [关于在UI中监控到目标的数据流的指南](/help/dataflows/ui/monitor-destinations.md) 以了解更多信息。

您还可以验证数据是否已成功到达您的目标。 目录中的大多数目标文档页面都具有 *验证数据导出部分*，以指示您如何在目标平台中检查数据是否已成功从Experience Platform引入。

## 将数据激活到目标的数据治理限制 {#data-governance}

通过以下方式为Platform目标强制执行数据管理：

* *营销活动* 可在创建目标工作流中选择的其他变量；
* *数据使用策略* 通过特定营销操作，限制将包含特定使用标签的数据激活到目标。

有关更多详细信息，请参阅Platform中的数据治理文档 [营销活动](../data-governance/policies/overview.md) 和 [解决数据策略违规](../data-governance/enforcement/auto-enforcement.md).

有关在创建目标工作流中选择营销操作的更多信息，请参阅Platform中不同目标类型的以下页面：

* [广告目标 — Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [广告目标 — Google Ads](./catalog/advertising/google-ads-destination.md)
* [广告目标 — Google显示和视频360](./catalog/advertising/google-dv360.md)
* [云存储目标](./catalog/cloud-storage/overview.md)
* [电子邮件营销目标](./catalog/email-marketing/overview.md)
* [社交目标](./catalog/social/overview.md)

有关受众激活工作流中数据策略违规的更多信息，请参阅 **[!UICONTROL 审核]** 步骤：

* [将受众数据激活到流式受众导出目标](./ui/activate-segment-streaming-destinations.md#review)
* [将受众数据激活到流式配置文件导出目标](./ui/activate-streaming-profile-destinations.md#review)
* [将受众数据激活到批量配置文件导出目标](./ui/activate-batch-profile-destinations.md#review)
