---
title: 高级数据生命周期管理概述
description: 高级数据生命周期管理允许您通过更新或清除过时或不准确的记录来管理数据的生命周期。
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: fc71e61fd33fe216f8cd326b9df048958c07077a
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 2%

---

# Adobe Experience Platform中的高级数据生命周期管理

Adobe Experience Platform提供了一套强大的工具来管理大型复杂的数据操作，以编排消费者体验。 随着时间推移数据被摄取到系统中，管理数据存储变得越来越重要，以便数据按预期使用，在不正确的数据需要更正时更新，并在组织策略认为必要时删除。

可以使用[[!UICONTROL Data Lifecycle] UI工作区](#ui)或[数据卫生API](#api)执行这些活动。 当数据生命周期作业执行时，系统会在流程的每个步骤提供透明度更新。 有关系统中每种作业类型的表示方式的更多信息，请参阅[时间线和透明度](#timelines-and-transparency)部分。

>[!NOTE]
>
>高级数据生命周期管理支持通过[数据集到期终结点](./api/dataset-expiration.md)进行数据集删除，以及通过[工作单终结点](./api/workorder.md)使用主标识进行ID删除（行级数据）。 您还可以通过Experience Platform UI管理[数据集过期](./ui/dataset-expiration.md)和[记录删除](./ui/record-delete.md)。 有关更多信息，请参阅链接的文档。 请注意，数据生命周期不支持批量删除。

## [!UICONTROL Data Lifecycle]用户界面工作区 {#ui}

Experience Platform UI中的[!UICONTROL Data Lifecycle]工作区允许您配置和计划数据生命周期操作，这有助于确保您的记录按预期进行维护。

有关在UI中管理数据生命周期任务的详细步骤，请参阅[数据生命周期UI指南](./ui/overview.md)。

## 数据卫生API {#api}

[!UICONTROL Data Lifecycle] UI基于数据卫生API构建，如果您希望自动执行数据生命周期活动，则可以直接使用其端点。 有关详细信息，请参阅[数据卫生API指南](./api/overview.md)。

## 时间表和透明度 {#timelines-and-transparency}

[记录删除](./ui/record-delete.md)和数据集过期请求都有各自的处理时间表，并在各自工作流程中的关键点提供透明度更新。

>[!TIP]
>
>若要监视当前使用量是否符合配额限制，请参阅[配额参考指南](./api/quota.md)。\
>有关权利规则、每月上限、SLA时间表和异常处理策略，请参阅[记录删除(UI)](./ui/record-delete.md#quotas)和[工作单(API)](./api/workorder.md#quotas)文档。

创建[数据集过期请求](./ui/dataset-expiration.md)时会发生以下情况：

| 暂存 | 计划到期后的时间 | 描述 |
| --- | --- | --- |
| 已提交请求 | 0 小时 | 数据管理员或隐私分析人员提交数据集在给定时间到期的请求。 提交请求后，该请求在[!UICONTROL Data Lifecycle UI]中可见，并一直处于待处理状态，直到计划的过期时间（该时间过后，该请求将执行）。 |
| 从数据湖中删除数据集 | 1 小时 | 该数据集从UI中的[数据集清单页面](../catalog/datasets/user-guide.md)中删除。 数据湖中的数据仅被软删除，并将保持软删除直到进程结束，之后这些数据将被硬删除。 |
| 从配置文件服务中删除数据集 | 3 小时 | 从此时起，批处理分段和流式分段、预览或估计、导出和实体访问等操作将不再从此数据集中读取数据。 仅软删除配置文件服务中的数据，并将一直保留到流程结束为止，之后将硬删除这些数据。 |
| 已更新配置文件计数和受众 | 48 小时 | 更新所有受影响的配置文件后，将更新所有相关的[受众](../segmentation/home.md)以反映其新大小。 根据删除的数据集以及您进行分段的属性，每个受众的大小可能会因删除而增加或减少。 此时，[仪表板小组件](../dashboards/guides/profiles.md#profile-count-trend)和其他报表中会反映所有配置文件计数中产生的任何更改。 |
| 已更新历程和目标 | 50 小时 | 已根据相关区段中的更改更新[历程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html)、[促销活动](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)和[目标](../destinations/home.md)。 |
| 硬删除完成 | 15 天 | 与数据集相关的所有数据都会从数据湖和配置文件服务中硬删除。 已删除数据集的数据生命周期作业[的](./ui/browse.md#view-details)状态已更新以反映此情况。 |

{style="table-layout:auto"}

## 后续步骤

本文档概述了Experience Platform的数据生命周期功能。 要开始在UI中提出数据卫生请求，请参阅[UI指南](./ui/overview.md)。 要了解如何以编程方式创建数据生命周期作业，请参阅[数据卫生API指南](./api/overview.md)
