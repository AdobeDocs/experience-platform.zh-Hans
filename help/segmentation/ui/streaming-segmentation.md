---
keywords: Experience Platform；主页；热门主题；流分段；分段；分段服务；分段服务；用户界面指南；
solution: Experience Platform
title: 流分段UI指南
topic: ui指南
description: Adobe Experience Platform上的流细分使您能够近乎实时地进行细分，同时专注于数据的丰富性。 借助流细分，当数据进入平台时，细分资格现在会发生，从而缓解了计划和运行细分作业的需求。 借助此功能，现在可以在数据传递到平台时评估大多数细分规则，这意味着，在不运行计划的细分作业的情况下，区段成员资格将保持最新。
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
translation-type: tm+mt
source-git-commit: e1ae20412f449c991f53fdd0f095d0c3a6de262c
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# 流细分

>[!NOTE]
>
>以下文档说明了如何使用UI使用流分段。 有关使用API的流分段的信息，请阅读[流分段API指南](../api/streaming-segmentation.md)。

[!DNL Adobe Experience Platform]上的流细分使客户能够近乎实时地进行细分，同时专注于数据的丰富性。 使用流分段，流数据进入[!DNL Platform]时，现在会发生细分资格，从而缓解了计划和运行分段作业的需求。 借助此功能，现在可以在数据传入[!DNL Platform]时评估大多数区段规则，这意味着区段成员资格将保持最新，而不运行计划的分段作业。

>[!NOTE]
>
>流分段只能用于评估流入平台的数据。 换句话说，通过批摄取摄取的数据将不会通过流分段进行评估，并将与晚间计划的区段作业一起进行评估。
>
>此外，如果使用流分段评估的区段基于使用批处理分段评估的另一个区段，则该区段可能会在理想成员和实际成员之间漂移。 例如，如果区段A基于区段B，而区段B是使用批分段进行评估的，因为区段B仅每24小时更新一次，因此区段A将进一步远离实际数据，直至其与区段B更新重新同步。

## 流分段查询类型

>[!NOTE]
>
>为了使流分段正常工作，您需要为组织启用计划分段。 有关启用计划分段的详细信息，请参阅分段用户指南](./overview.md#scheduled-segmentation)中的[流分段部分。

如果查询符合以下任何条件，则将使用流分段自动评估该数据：

| 查询类型 | 详细信息 | 示例 |
| ---------- | ------- | ------- |
| 传入点击 | 任何区段定义，指没有时间限制的单个传入事件。 | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| 在相对时间窗口内传入点击 | 引用单个传入事件的任何区段定义。 | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| 带时间窗口的传入点击 | 任何区段定义，指带时间窗口的单个传入事件。 | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| 仅用户档案 | 只引用用户档案属性的任何区段定义。 |  |
| 指用户档案的传入点击 | 引用单个传入事件（无时间限制）和一个或多个用户档案属性的任何区段定义。 | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| 在相对时间窗口内引用用户档案的传入点击 | 引用单个传入事件和一个或多个用户档案属性的任何区段定义。 | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| 分类 | 包含一个或多个批或流区段的任何区段定义。 | ![](../images/ui/streaming-segmentation/two-batches.png) |
| 引用事件的多个用户档案 | 在过去24小时内引用多个事件&#x200B;**且（可选）具有一个或多个用户档案属性的任何区段定义。** | ![](../images/ui/streaming-segmentation/event-history-success.png) |

在以下情况下，将&#x200B;**不**&#x200B;启用区段定义以进行流分段：

- 区段定义包括Adobe Audience Manager(AAM)区段或特征。
- 区段定义包括多个实体(多实体查询)。

此外，执行流分段时还会应用一些准则：

| 查询类型 | 准则 |
| ---------- | -------- |
| 单个事件查询 | 回顾窗口没有限制。 |
| 查询和事件历史 | <ul><li>回顾窗口限制为&#x200B;**一天**。</li><li>严格的时间排序条件&#x200B;**必须**&#x200B;存在于事件之间。</li><li>支持具有至少一个否定事件的查询。 但是，整个事件&#x200B;**不能**&#x200B;为否定。</li></ul> |

如果修改了区段定义，使其不再符合流式分段的条件，则区段定义将自动从“流式”切换为“批”。

## 流细分细分细分

创建支持流的区段后，您可以视图该区段的详细信息。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

具体而言，将显示有关&#x200B;**[!UICONTROL total qualified audience size]**&#x200B;的详细信息。 **[!UICONTROL Total qualified audience size]**&#x200B;显示上次完成的区段作业运行中合格受众的总数。 如果在过去24小时内未完成区段作业，则将从估计中取得受众数。

下面是一个折线图，显示在过去24小时内被合格和取消资格的区段数。 可以调整下拉列表以显示最近24小时、上周或最近30天。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

通过选择信息气泡，可以找到有关最后一个区段评估的其他信息。

![](../images/ui/streaming-segmentation/info-bubble.png)

有关区段定义的详细信息，请阅读上一节[区段定义详细信息](#segment-details)。

## 后续步骤

本用户指南介绍支持流的细分定义如何在Adobe Experience Platform上工作，以及如何监视支持流的细分。

要了解有关使用Adobe Experience Platform用户界面的更多信息，请阅读[分段用户指南](./overview.md)。
