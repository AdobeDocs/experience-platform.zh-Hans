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
>在非生产沙盒中不支持警报。 要订阅警报，您必须确保使用生产沙盒。

通过Adobe Experience Platform，可订阅有关Adobe Experience Platform活动的基于事件的警报。 警报减少或无需轮询 [[!DNL Observability Insights] API](../api/overview.md) 用于检查作业是否已完成、是否已到达工作流中的某个里程碑或者是否已发生任何错误。

当您的Platform操作达到特定条件集时（例如系统违反阈值时出现潜在问题），Platform可以向组织中订阅警报消息的任何用户发送警报消息。 这些消息可在预定义的时间间隔内重复出现，直到警报得到解决为止。

本文档概述了Adobe Experience Platform中的警报，包括如何定义警报规则的结构。

## 一次性警报与重复警报

平台警报可以发送一次，也可以在预定义的时间间隔内重复发送，直到得到解决为止。 每个选项的用例旨在以下列方式有所不同：

| 一次性警报 | 重复警报 |
| --- | --- |
| 不一定表示存在问题。 | 指示可能不受欢迎的状态。 |
| 不重复。 | 如果异常情况持续存在，可以重复此操作。 |
| 示例包括：<ul><li>已成功完成数据摄取。</li><li>查询执行已完成。</li><li>已删除数据。</li></ul> | 示例包括：<ul><li>摄取持续时间超过服务级别协议(SLA)。</li><li>在过去24小时内未发生每日摄取。</li><li>流处理器的错误率高于配置的阈值。</li><li>配置文件总数超过授权。</li></ul> |

{style="table-layout:auto"}

## 警报剖析

警报可以划分为以下组件：

| 组件 | 描述 |
| --- | --- |
| **量度** | 可观察性 [量度](../api/metrics.md#available-metrics) 其值会触发警报，例如失败的批量摄取事件数(`timeseries.ingestion.dataset.batchfailed.count`)。 |
| **条件** | 与度量相关的条件，如果警报解析为true，则会触发警报，例如计数度量超过某个数字。 此条件可以与预定义的时间窗口相关联。 |
| **窗口** | （可选）警报的条件可以限制在预定义的时间范围内。 例如，根据过去5分钟内失败的批次数量，可能会触发警报。 |
| **操作** | 触发警报时，将执行操作。 具体而言，消息通过投放渠道(例如预配置的webhook或Experience PlatformUI)发送给适用的收件人。 |
| **频度** | （可选）可以将警报配置为在定义的间隔内重复其操作（如果其条件为true或未解析）。 |

{style="table-layout:auto"}

## 接收和管理警报

可通过两个渠道接收和管理警报：

* [Adobe I/O事件](#events)
* [平台UI](#ui)

### I/O事件 {#events}

可将警报发送到配置的webhook以促进活动监控的高效自动化。 要通过webhook接收警报，您必须在Adobe Developer控制台中注册用于Platform警报的webhook。 请参阅指南，网址为 [订阅Adobe I/O事件通知](./subscribe.md) 以了解具体步骤。

### 平台UI {#ui}

Platform UI允许您查看收到的警报和管理警报规则。 以下视频介绍了这些功能。

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

要在Platform UI中使用警报，您必须通过Adobe Admin Console启用以下访问控制权限：

| 权限 | 描述 |
| --- | --- |
| 查看警报 | 用于查看已接收的警报消息。 |
| 查看警报历史记录* | 允许您查看已接收警报的历史记录，方法是 [!UICONTROL 警报] 选项卡。 |
| 管理警报* | 允许您通过启用和禁用警报规则 [!UICONTROL 警报] 选项卡。 |
| 解决警报* | 允许您通过 [!UICONTROL 警报] 选项卡。 |

{style="table-layout:auto"}

**要访问 [!UICONTROL 警报] 选项卡上，您还必须被授予查看警报权限以及其他某个权限。*

>[!NOTE]
>
>有关如何在Platform中管理权限的更多信息，请参阅 [访问控制文档](../../access-control/ui/overview.md).

具有“查看警报”权限时，可以通过选择铃铛图标(![铃铛图标](../images/alerts/overview/icon.png))的图标。

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> 选择警报以导航到相关仪表板，了解有关触发警报原因的更多详细信息。

此外， [!UICONTROL 警报] UI中的选项卡允许个人用户订阅特定的警报类型，并允许管理员完全启用或禁用警报规则。 请参阅 [UI指南](./ui.md) 以了解有关管理警报的详细信息。

## 后续步骤

通过阅读本文档，您已经了解了Platform警报及其在平台生态系统中的作用。 请参阅本概述中链接的流程文档，了解如何接收和管理警报。
