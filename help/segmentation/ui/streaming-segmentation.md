---
keywords: Experience Platform;home;popular topics;streaming segmentation;Segmentation;Segmentation Service;segmentation service;ui guide;
solution: Experience Platform
title: 流细分
topic: ui guide
description: Adobe Experience Platform的流式细分使您能够近乎实时地进行细分，同时专注于数据的丰富性。 利用流细分，当数据进入平台时，现在会发生细分资格，从而减轻计划和运行细分作业的需求。 借助此功能，现在可以在数据传入平台时评估大多数细分规则，这意味着，在不运行计划的细分作业的情况下，细分成员资格将保持最新。
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---


# 流细分

>[!NOTE]
>
>以下文档说明了如何使用UI使用流式分段。 有关使用API的流分段的信息，请阅读流 [分段API指南](../api/streaming-segmentation.md)。

基于的流 [!DNL Adobe Experience Platform] 式细分允许客户在关注数据丰富性的同时近乎实时地进行细分。 利用流细分，流数据进入时即会发生细分资格 [!DNL Platform]，从而减轻计划和运行细分作业的需求。 借助此功能，现在可以在数据传入时评估大多数细分规则， [!DNL Platform]这意味着，在不运行计划的细分作业的情况下，区段成员关系将保持最新状态。

>[!NOTE]
>
>流分段只能用于评估流入平台的数据。 换言之，通过批量摄取摄取的数据不会通过流分段进行评估，而需要触发批量评估。

## 流分段查询类型

>[!NOTE]
>
>为了使流分段正常工作，您需要为组织启用计划分段。 有关启用计划分段的详细信息，请参 [阅分段用户指南中的流分段部分](./overview.md#scheduled-segmentation)。

如果查询符合以下任何条件，则将使用流分段自动评估该数据：

| 查询类型 | 详细信息 | 示例 |
| ---------- | ------- | ------- |
| 传入点击 | 任何区段定义，指没有时间限制的单个传入事件。 | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| 相对时间窗口内的传入点击 | 指过去七天内单个传入事件 **的任何区段定义**。 | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| 仅用户档案 | 只引用用户档案属性的任何区段定义。 |  |
| 指用户档案 | 引用单个传入事件（无时间限制）和一个或多个用户档案属性的任何区段定义。 | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| 指相对时间窗口内用户档案的传入点击 | 在过去七天内引用单个传入事件和一个或多个属性 **的任何用户档案定义**。 | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| 引用事件的多个用户档案 | 任何引用过去24小时内的多个事件 **并且(可选** )具有一个或多个用户档案属性的定义。 | ![](../images/ui/streaming-segmentation/event-history-success.png) |

下节列表段定义示例，这些示例将 **不启** 用流分段功能。

| 查询类型 | 详细信息 | 示例 |
| ---------- | ------- | ------- |
| 相对时间窗口内的传入点击 | 如果区段定义引用的事件不 **是** 在最 **近七天的时间段内**。 例如，在过去 **两周内**。 | ![](../images/ui/streaming-segmentation/relative-hit-failure.png) |
| 指相对窗口中的用户档案的传入点击 | 以下选项将不 **支持** 流分段：<ul><li>未在最 **后** 七 **天内到达的事件**。</li><li>包括区段或特征 [!DNL Adobe Audience Manager (AAM)] 的区段定义。</li></ul> | ![](../images/ui/streaming-segmentation/profile-relative-failure.png) |
| 引用事件的多个用户档案 | 以下选项将不 **支持** 流分段：<ul><li>在过去24 **小时** 内 **不发生的事件**。</li><li>包括Adobe Audience Manager(AAM)区段或特征的区段定义。</li></ul> | ![](../images/ui/streaming-segmentation/event-history-failure.png) |
| 多实体查询 | 整体而言，多实体查询不 **受流** 分段支持。 |  |

此外，执行流分段时还会应用一些准则：

| 查询类型 | 准则 |
| ---------- | -------- |
| 单事件查询 | 回顾窗限于 **七天**。 |
| 查询事件历史 | <ul><li>回顾窗限于一 **天**。</li><li>事件之间必 **须存** 在严格的时间排序条件。</li><li>只允许在事件之间进行简单的时间排序（前后）。</li><li>不能否定 **个别事件** 。 但是，整个查询 **可以** 被否定。</li></ul> |

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