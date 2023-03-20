---
keywords: Experience Platform；主页；热门主题；日期范围
title: 警报概述
description: 了解 Adobe Experience Platform 中的警报，包括有关如何定义警报规则的结构。
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: 37700c3b3b728b59083fd51cabf1d8e4b8213580
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 3%

---

# 警报概述

>[!NOTE]
>
>非生产沙箱不支持警报。 要订阅警报，您必须确保使用的是生产沙盒。

Adobe Experience Platform允许您订阅有关Adobe Experience Platform活动的基于事件的警报。 警报可减少或消除轮询 [[!DNL Observability Insights] API](../api/overview.md) 为了检查作业是否已完成、是否已到达工作流中的某个里程碑，或是否发生任何错误。

当您的Platform操作达到一组特定条件（例如，当系统超出阈值时可能出现问题）时，Platform可以向组织中订阅了这些条件的任何用户发送警报消息。 这些消息可以在预定义的时间间隔内重复，直到警报得到解析。

本文档概述了Adobe Experience Platform中的警报，包括如何定义警报规则的结构。

## 一次性警报与重复警报

平台警报可以发送一次，也可以在预定义的间隔内重复，直到它们得到解析。 这些选项的用例在以下方面有所不同：

| 一次性警报 | 重复警报 |
| --- | --- |
| 不一定表示问题。 | 表示可能不需要的状态。 |
| 不重复。 | 如果异常情况持续存在，可以重复上述步骤。 |
| 示例包括：<ul><li>数据摄取已成功完成。</li><li>查询执行已完成。</li><li>数据已删除。</li></ul> | 示例包括：<ul><li>摄取持续时间超过服务级别协议(SLA)。</li><li>过去24小时内未发生每日摄取。</li><li>流处理器的错误率高于配置的阈值。</li><li>用户档案总数超过授权。</li></ul> |

{style="table-layout:auto"}

## 警报解剖

警报可以划分为以下组件：

| 组件 | 描述 |
| --- | --- |
| **量度** | 可观测性 [量度](../api/metrics.md#available-metrics) 其值会触发警报，例如失败的批量摄取事件数(`timeseries.ingestion.dataset.batchfailed.count`)。 |
| **条件** | 与量度相关的条件，如果量度解析为true，则会触发警报，例如超过特定数字的计数量度。 此条件可能与预定义的时间窗口相关联。 |
| **窗口** | （可选）警报条件可限制为预定义的时间窗口。 例如，根据过去五分钟中失败批次的数量，可能会触发警报。 |
| **操作** | 触发警报时，会执行一项操作。 具体而言，通过投放渠道(如预配置的Webhook或Experience PlatformUI)向适用的收件人发送消息。 |
| **频度** | （可选）如果警报的条件仍为true或未解析，则可以将其配置为以定义的间隔重复其操作。 |

{style="table-layout:auto"}

## 接收和管理警报

可通过两个渠道接收和管理警报：

* [Adobe I/O事件](#events)
* [平台UI](#ui)

### I/O事件 {#events}

警报可发送到配置的Webhook，以促进活动监控的高效自动化。 要通过Webhook接收警报，您必须在Adobe Developer控制台中为Platform警报注册Webhook。 请参阅 [订阅Adobe I/O事件通知](./subscribe.md) 中。

### 平台UI {#ui}

平台UI允许您查看收到的警报并管理警报规则。 以下视频介绍了这些功能。

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

要在Platform UI中处理警报，您必须通过Adobe Admin Console启用以下访问控制权限：

| 权限 | 描述 |
| --- | --- |
| 查看警报 | 用于查看已接收的警报消息。 |
| 查看警报历史记录* | 允许您通过 [!UICONTROL 警报] 选项卡。 |
| 管理警报* | 允许您通过 [!UICONTROL 警报] 选项卡。 |
| 解决警报* | 允许您通过 [!UICONTROL 警报] 选项卡。 |

{style="table-layout:auto"}

**为了访问 [!UICONTROL 警报] 选项卡，则还必须同时授予您“查看警报”权限和其他权限之一。*

>[!NOTE]
>
>有关如何在Platform中管理权限的更多信息，请参阅 [访问控制文档](../../access-control/ui/overview.md).

具有查看警报权限时，可以通过选择铃铛图标(![钟图标](../images/alerts/overview/icon.png))。

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> 选择警报以导航到相关的功能板，以了解有关触发警报的原因的更多详细信息。

此外， [!UICONTROL 警报] 用户界面中的选项卡允许个人用户订阅特定的警报类型，并允许管理员完全启用或禁用警报规则。 请参阅 [UI指南](./ui.md) 以了解有关管理警报的更多信息。

## 后续步骤

通过阅读本文档，您已被介绍到Platform警报及其在Platform生态系统中的角色。 请参阅在整个概述中链接到的流程文档，了解如何接收和管理警报。
