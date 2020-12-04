---
keywords: Experience Platform;home;popular topics;streaming segmentation;Segmentation;Segmentation Service;segmentation service;ui guide;
solution: Experience Platform
title: 流细分
topic: ui guide
description: Adobe Experience Platform的流式细分使您能够近乎实时地进行细分，同时专注于数据的丰富性。 利用流细分，当数据进入平台时，现在会发生细分资格，从而减轻计划和运行细分作业的需求。 借助此功能，现在可以在数据传入平台时评估大多数细分规则，这意味着，在不运行计划的细分作业的情况下，细分成员资格将保持最新。
translation-type: tm+mt
source-git-commit: 2bd4b773f7763ca408b55e3b0e2d0bbe9e7b66ba
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---


# 流细分

>[!NOTE]
>
>以下文档说明了如何使用UI使用流式分段。 有关使用API的流分段的信息，请阅读流 [分段API指南](../api/streaming-segmentation.md)。

基于的流 [!DNL Adobe Experience Platform] 式细分允许客户在关注数据丰富性的同时近乎实时地进行细分。 利用流细分，流数据进入时即会发生细分资格 [!DNL Platform]，从而减轻计划和运行细分作业的需求。 借助此功能，现在可以在数据传入时评估大多数细分规则， [!DNL Platform]这意味着，在不运行计划的细分作业的情况下，区段成员关系将保持最新状态。

>[!NOTE]
>
>流分段只能用于评估流入平台的数据。 换言之，通过批处理摄取的数据将不会通过流分段进行评估，并将与晚间计划的分段作业一起进行评估。

## 流分段查询类型

>[!NOTE]
>
>为了使流分段正常工作，您需要为组织启用计划分段。 有关启用计划分段的详细信息，请参 [阅分段用户指南中的流分段部分](./overview.md#scheduled-segmentation)。

如果查询符合以下任何条件，则将使用流分段自动评估该数据：

| 查询类型 | 详细信息 | 示例 |
| ---------- | ------- | ------- |
| 传入点击 | 任何区段定义，指没有时间限制的单个传入事件。 | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| 相对时间窗口内的传入点击 | 引用单个传入事件的任何区段定义。 | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| 仅用户档案 | 只引用用户档案属性的任何区段定义。 |  |
| 指用户档案 | 引用单个传入事件（无时间限制）和一个或多个用户档案属性的任何区段定义。 | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| 指相对时间窗口内用户档案的传入点击 | 引用单个传入事件和一个或多个用户档案属性的任何区段定义。 | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| 引用事件的多个用户档案 | 任何引用过去24小时内的多个事件 **并且(可选** )具有一个或多个用户档案属性的定义。 | ![](../images/ui/streaming-segmentation/event-history-success.png) |

在以下情况下 **** ，将不会为流分段启用段定义：

- 区段定义包括Adobe Audience Manager(AAM)区段或特征。
- 段定义包括多个实体(多实体查询)。

此外，执行流分段时还会应用一些准则：

| 查询类型 | 准则 |
| ---------- | -------- |
| 单事件查询 | 回顾窗口没有限制。 |
| 查询事件历史 | <ul><li>回顾窗口限于 **一天**。</li><li>事件之间必 **须存** 在严格的时间排序条件。</li><li>支持具有至少一个否定查询的事件。 但是，整个事件 **不能** 是否定的。</li></ul> |

如果修改了区段定义，使其不再符合流式分段的条件，则区段定义将自动从“流式”切换为“批处理”。

## 流细分细分细分

创建支持流式播放的区段后，您可以视图该区段的详细信息。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

具体而言，将显示有关 **[!UICONTROL 合格受众总大小的]** 详细信息。 “ **[!UICONTROL 合格受众总数]** ”显示上次完成的区段作业运行中合格受众的总数。 如果在过去24小时内未完成细分作业，则将从估计中获取受众数。

下面是一个线形图，显示过去24小时内合格和被取消资格的区段数。 可以调整下拉列表以显示最近24小时、上周或最近30天。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

通过选择信息气泡，可以找到有关最后一个细分评估的其他信息。

![](../images/ui/streaming-segmentation/info-bubble.png)

有关区段定义的更多信息，请阅读上一节有关区段定 [义的详细信息](#segment-details)。

## 流分段视频演示

以下视频旨在支持您对流细分的理解。 它展示了一个客户体验示例，然后快速浏览界面中的主要 [!DNL Platform] 功能。

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## 后续步骤

本用户指南介绍支持流的细分定义如何在Adobe Experience Platform运行以及如何监控支持流的细分。

要了解有关使用Adobe Experience Platform用户界面的更多信息，请阅 [读分段用户指南](./overview.md)。