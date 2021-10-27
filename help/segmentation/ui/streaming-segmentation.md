---
keywords: Experience Platform；主页；热门主题；流式分段；分段；分段服务；分段服务；用户界面指南；
solution: Experience Platform
title: 流分段UI指南
topic-legacy: ui guide
description: 通过Adobe Experience Platform上的流式分段，您可以近乎实时地进行分段，同时重点关注数据的丰富性。 使用流式分段，区段鉴别现在会在数据登陆平台时进行，从而缓解了计划和运行分段作业的需求。 借助此功能，大多数区段规则现在都可以在数据传递到平台时进行评估，这意味着区段成员资格将保持为最新状态，而无需运行计划的分段作业。
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: bb5a56557ce162395511ca9a3a2b98726ce6c190
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# 流分段

>[!NOTE]
>
>以下文档说明了如何使用UI使用流分段。 有关使用API的流式分段的信息，请阅读 [流分段API指南](../api/streaming-segmentation.md).

流式分段 [!DNL Adobe Experience Platform] 允许客户近乎实时地进行分段，同时重点关注数据的丰富性。 通过流式客户细分，现在，当流数据进入 [!DNL Platform]，以缓解计划和运行分段作业的需求。 使用此功能，现在可以在数据被传递到时评估大多数区段规则 [!DNL Platform]，这意味着区段成员资格将保持为最新状态，而不运行计划的分段作业。

>[!NOTE]
>
>流分段只能用于评估流入平台的数据。 换言之，通过批量摄取摄取摄取的数据将不会通过流式分段进行评估，而是会与夜间计划的区段作业一起进行评估。
>
>此外，如果使用流分段评估的区段基于使用批处理分段评估的另一个区段，则该区段可能会在理想成员资格与实际成员资格之间产生漂移。 例如，如果区段A基于区段B，并且区段B使用批量分段进行评估，因为区段B仅每24小时更新一次，因此区段A将远离实际数据，直到它与区段B更新重新同步为止。

## 流分段查询类型

>[!NOTE]
>
>为了使流式客户细分正常工作，您需要为组织启用计划客户细分。 有关启用计划分段的详细信息，请参阅 [分段用户指南中的流分段部分](./overview.md#scheduled-segmentation).

如果查询满足以下任一条件，则将自动使用流分段来评估该查询：

| 查询类型 | 详细信息 | 示例 |
| ---------- | ------- | ------- |
| 单个事件 | 任何引用无时间限制的单个传入事件的区段定义。 | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| 相对时间窗口内的单个事件 | 引用单个传入事件的任何区段定义。 | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| 包含时间窗口的单个事件 | 引用带有时间窗口的单个传入事件的任何区段定义。 | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| 仅配置文件 | 仅引用配置文件属性的任何区段定义。 |  |
| 具有配置文件属性的单个事件 | 任何引用单个传入事件（无时间限制）和一个或多个用户档案属性的区段定义。 **注意：** 事件发生时，将立即评估查询。 但是，对于用户档案事件，必须等待24小时才能合并。 | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| 相对时间窗口内具有配置文件属性的单个事件 | 引用单个传入事件和一个或多个用户档案属性的任何区段定义。 | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| 区段 | 包含一个或多个批处理或流式处理区段的任何区段定义。 **注意：** 如果使用区段区段，则会发生配置文件取消资格事件 **每24小时**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| 具有配置文件属性的多个事件 | 引用多个事件的任何区段定义 **过去24小时内** 和（可选）具有一个或多个配置文件属性。 | ![](../images/ui/streaming-segmentation/event-history-success.png) |

区段定义将 **not** 在以下情况下启用流分段：

- 区段定义包括Adobe Audience Manager(AAM)区段或特征。
- 区段定义包括多个实体（多实体查询）。

此外，执行流式分段时还应遵循以下准则：

| 查询类型 | 准则 |
| ---------- | -------- |
| 单个事件查询 | 回顾窗口没有限制。 |
| 包含事件历史记录的查询 | <ul><li>回顾窗口限制为 **一天**.</li><li>严格的时间排序条件 **必须** 事件之间存在。</li><li>支持具有至少一个否定事件的查询。 但是，整个事件 **无法** 是否定。</li></ul> |

如果修改了区段定义，使其不再符合流式分段的标准，则区段定义将自动从“流式”切换为“批处理”。

## 流分段区段详细信息

创建启用流式传输的区段后，您可以查看该区段的详细信息。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

具体而言， **[!UICONTROL 合格受众总大小]** 中。 的 **[!UICONTROL 合格受众总数]** 显示上次完成区段作业运行中符合条件的受众的总数。 如果区段作业在过去24小时内未完成，则将从估计中获取受众数量。

下面是一个折线图，显示过去24小时内符合条件且被取消资格的区段数量。 可以调整下拉菜单以显示最近24小时、上周或最近30天。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

通过选择信息气泡，可以找到有关最后一个区段评估的其他信息。

![](../images/ui/streaming-segmentation/info-bubble.png)

有关区段定义的更多信息，请阅读 [区段定义详细信息](#segment-details).

## 后续步骤

本用户指南介绍启用流的区段定义如何在Adobe Experience Platform上工作，以及如何监视启用流的区段。

要了解有关使用Adobe Experience Platform用户界面的更多信息，请阅读 [分段用户指南](./overview.md).
