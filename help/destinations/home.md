---
keywords: 目标；adobe experience platform；平台；目标概述；激活数据；激活
title: 目标概述
description: 目标是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用Adobe Experience Platform中的目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# [!DNL Destinations] 概述 {#overview}

![目标概述横幅](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 目标和来源 {#destinations-and-sources}

Platform的核心功能之一是摄取第一方数据并根据业务需求对其进行激活。 使用 [来源](../sources/home.md) 将数据摄取到平台和目标以从平台导出数据。

## 目标步骤 {#steps}

* 从 [自助目录](./catalog/overview.md) 平台中所有可用目标的目标数量。
* 使用目标将用户档案或区段发送到营销自动化平台、数字广告平台等。
* 计划定期向首选目标导出数据。

## 控件 {#controls}

中的控件 [目标工作区](./ui/destinations-workspace.md) 允许您：

* 浏览可激活数据的目标平台目录；
* 创建、编辑、激活和禁用数据流到目录中目标的数据流；
* 在存储位置创建帐户或将平台链接到目标平台中的帐户；
* 选择应激活到目标的区段；
* 选择 [体验数据模型(XDM)字段](../xdm/home.md) 用于在将区段激活到电子邮件营销目标时导出。

## 目标类型和类别 {#types-and-categories}

通过Experience Platform，您可以将数据激活到各种类型的目标，以满足您的激活用例。 目标范围从基于API的集成到与文件接收系统的集成、配置文件查找目标等。 有关所有可用目标的详细信息，请参阅 [目标类型和类别概述](./destination-types.md).

## 目标和访问控制 {#access-controls}

Platform中的目标功能可与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以查看、管理和激活目标。 有关各个权限的信息，请参阅 [Adobe Experience Platform中的访问控制](../access-control/home.md) 并向下滚动到页面底部。

下表概述了对目标执行某些操作所需的权限和权限组合：

| 权限级别 | 描述 |
| ---- | ----|
| **[!UICONTROL 管理目标]** | 要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). |
| **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** | 将区段激活到目标并启用 [映射步骤](ui/activate-batch-profile-destinations.md#mapping) 工作流中，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). |
| **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 在无映射的情况下激活区段]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** | 将区段激活到目标并隐藏 [映射步骤](ui/activate-batch-profile-destinations.md#mapping) 工作流中，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 在无映射的情况下激活区段]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). |

{style="table-layout:auto"}

有关访问控制的更多信息，请参阅 [访问控制用户指南](../access-control/ui/overview.md).

### 目标基于属性的访问控制 {#attribute-based-access}

通过Adobe Experience Platform中基于属性的访问控制，管理员可以基于属性控制对特定对象和/或功能的访问。

通过基于属性的访问控制，您可以将映射配置应用到您有权访问的字段。 此外，如果您无权访问数据集中的所有字段，则无法将数据导出到目标。

有关目标如何使用基于属性的访问控制的更多信息，请阅读 [基于属性的访问控制概述](../access-control/abac/overview.md#destinations).

## 目标监控 {#destinations-monitoring}

在建立与目标的连接并完成激活工作流后，您可以监控向接收系统导出的数据。 阅读 [在UI中监控数据流到目标的指南](/help/dataflows/ui/monitor-destinations.md) 以了解更多信息。

您还可以验证数据是否成功传入您的目标。 目录中的大多数目标文档页面都具有 *验证数据导出部分*，指示如何在目标平台中检查数据是否从Experience Platform成功导入。

## 在将数据激活到目标方面的数据管理限制 {#data-governance}

通过以下方式为Platform目标强制实施数据管理：

* *营销操作* ，您可以在创建目标工作流中选择；
* *数据使用策略* 将包含某些使用标签的数据限制为通过特定营销操作激活到目标。

有关 [营销行动](../data-governance/policies/overview.md) 和 [解决数据策略违规问题](../data-governance/enforcement/auto-enforcement.md).

有关在创建目标工作流中选择营销操作的更多信息，请参阅Platform中不同目标类型的以下页面：

* [广告目标 — Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [广告目标 — Google广告](./catalog/advertising/google-ads-destination.md)
* [广告目标 — Google显示和视频360 ](./catalog/advertising/google-dv360.md)
* [云存储目标](./catalog/cloud-storage/overview.md)
* [电子邮件营销目标](./catalog/email-marketing/overview.md)
* [社交目标](./catalog/social/overview.md)

有关区段激活工作流中违反数据策略的更多信息，请参阅 **[!UICONTROL 审阅]** 步骤：

* [将受众数据激活到流区段导出目标](./ui/activate-segment-streaming-destinations.md#review)
* [将受众数据激活到流配置文件导出目标](./ui/activate-streaming-profile-destinations.md#review)
* [激活受众数据以批量配置文件导出目标](./ui/activate-batch-profile-destinations.md#review)
