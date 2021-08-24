---
keywords: Experience Platform；主页；热门主题；日期范围
title: 警报概述
description: 了解Adobe Experience Platform中的警报，包括警报规则的定义结构。
source-git-commit: 5fabf5fa12f0a117a50bf694dea5118e5ea03500
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---


# 警报概述

Adobe Experience Platform允许您订阅有关Adobe Experience Platform活动的基于事件的警报。 警报可减少或消除轮询[[!DNL Observability Insights] API](../api/overview.md)的需要，以便检查作业是否已完成、是否已到达工作流中的某个里程碑，或是否发生任何错误。

当您的Platform操作达到一组特定条件（例如，当系统超出阈值时可能出现问题）时，Platform可以向组织中订阅了这些条件的任何用户发送警报消息。 这些消息可以在预定义的时间间隔内重复，直到警报得到解析。

本文档概述了Adobe Experience Platform中的警报，包括如何定义警报规则的结构。

## 一次性警报与重复警报

平台警报可以发送一次，也可以在预定义的间隔内重复，直到它们得到解析。 这些选项的用例在以下方面有所不同：

| 一次性警报 | 重复警报 |
| --- | --- |
| 不一定表示问题。 | 表示可能不需要的状态。 |
| 不重复。 | 如果异常情况持续存在，可以重复上述步骤。 |
| 示例包括：<ul><li>数据摄取已成功完成。</li><li>查询执行已完成。</li><li>数据已删除。</li></ul> | 示例包括：<ul><li>摄取持续时间超过服务级别协议(SLA)。</li><li>过去24小时内未发生每日摄取。</li><li>流处理器的错误率高于配置的阈值。</li><li>用户档案总数超过授权。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 警报解剖

警报可以划分为以下组件：

| Component | 描述 |
| --- | --- |
| **量度** | 可观察性[量度](../api/metrics.md#available-metrics)，其值会触发警报，如失败的批量摄取事件数(`timeseries.ingestion.dataset.batchfailed.count`)。 |
| **条件** | 与量度相关的条件，如果量度解析为true，则会触发警报，例如超过特定数字的计数量度。 此条件可能与预定义的时间窗口相关联。 |
| **窗口** | （可选）警报条件可限制为预定义的时间窗口。 例如，根据过去五分钟中失败批次的数量，可能会触发警报。 |
| **操作** | 触发警报时，会执行一项操作。 具体而言，通过投放渠道(如预配置的Webhook或Experience PlatformUI)向适用的收件人发送消息。 |
| **频度** | （可选）如果警报的条件仍为true或未解析，则可以将其配置为以定义的间隔重复其操作。 |

{style=&quot;table-layout:auto&quot;}

## 接收和管理警报

可通过两个渠道接收和管理警报：

* [Adobe I/O事件](#events)
* [平台UI](#ui)

### I/O事件 {#events}

警报可发送到配置的Webhook，以促进活动监控的高效自动化。 要通过WebHook接收警报，您必须在Adobe开发人员控制台中为平台警报注册WebHook。 有关具体步骤，请参阅[订阅Adobe I/O事件通知](./subscribe.md)的指南。

### 平台UI {#ui}

要在Platform UI中处理警报，您必须通过Adobe Admin Console启用以下访问控制权限：

| 权限 | 描述 |
| --- | --- |
| 查看警报 | 用于查看已接收的警报消息。 |
| 查看警报历史记录* | 用于通过[!UICONTROL 警报]选项卡查看接收警报的历史记录。 |
| 管理警报* | 允许您通过[!UICONTROL 警报]选项卡启用和禁用警报规则。 |
| 解决警报* | 用于通过[!UICONTROL 警报]选项卡解析触发的警报。 |

{style=&quot;table-layout:auto&quot;}

**要访问[!UICONTROL 警报]选项卡，您还必须获得“查看警报”权限，并同时获得其中一个权限。*

>[!NOTE]
>
>有关如何管理Platform中权限的更多信息，请参阅[访问控制文档](../../access-control/ui/overview.md)。

具有“查看警报”权限时，可以通过选择右上角的铃铛图标（![铃铛图标](../images/alerts/overview/icon.png)）来查看收到的警报。

![](../images/alerts/overview/ui.png)

此外， UI中的[!UICONTROL 警报]选项卡允许个人用户订阅特定的警报类型，并允许管理员完全启用或禁用警报规则。 有关管理警报的更多信息，请参阅[ UI指南](./ui.md) 。

## 后续步骤

通过阅读本文档，您已被介绍到Platform警报及其在Platform生态系统中的角色。 请参阅在整个概述中链接到的流程文档，了解如何接收和管理警报。