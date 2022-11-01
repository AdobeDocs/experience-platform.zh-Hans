---
title: 数据卫生概述
description: Adobe Experience Platform数据卫生功能允许您通过更新或清除过时或不准确的记录来管理数据的生命周期。
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 6453ec6c98d90566449edaa0804ada260ae12bf6
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 3%

---

# Adobe Experience Platform数据卫生

>[!IMPORTANT]
>
>目前，数据卫生仅适用于已购买的组织 **Adobe医疗保健盾** 或 **Adobe隐私和安全防护**.

Adobe Experience Platform提供了一组功能强大的工具来管理大型、复杂的数据操作，以编排客户体验。 随着数据逐渐被摄取到系统中，管理数据存储变得越来越重要，这样数据就可以按预期使用，错误数据需要更正时会更新，组织策略认为有必要时会删除。

Platform的数据卫生功能允许您通过以下方式管理存储的消费者数据：

* 计划自动数据集过期
* 根据摄取的身份删除消费者数据

这些活动可以使用 [[!UICONTROL 数据卫生] UI工作区](#ui) 或 [数据卫生API](#api). 当执行数据卫生作业时，系统会在处理的每个步骤中提供透明度更新。 请参阅 [时间表和透明度](#timelines-and-transparency) 有关每个作业类型在系统中如何表示的详细信息。

## [!UICONTROL 数据卫生] UI工作区 {#ui}

的 [!UICONTROL 数据卫生] 平台UI中的工作区允许您配置和计划数据卫生操作，这有助于确保记录按预期进行维护。

有关在UI中管理数据卫生任务的详细步骤，请参阅 [数据卫生UI指南](./ui/overview.md).

## 数据卫生API {#api}

的 [!UICONTROL 数据卫生] UI是基于数据卫生API构建的，如果您希望自动执行数据卫生活动，则可以直接使用其端点。 请参阅 [数据卫生API指南](./api/overview.md) 以了解更多信息。

## 时间表和透明度

消费者删除和数据集过期请求各自具有各自的处理时间轴，并在各自工作流的关键点提供透明度更新。 有关每种作业类型的详细信息，请参阅以下部分。

### 数据集过期 {#dataset-expiration-transparency}

在 [数据集过期请求](./ui/dataset-expiration.md) 已创建：

| 暂存 | 计划过期后的时间 | 描述 |
| --- | --- | --- |
| 请求已提交 | 0 小时 | 数据管理员或隐私分析员提交了一个请求，要求数据集在给定时间过期。 请求显示在 [!UICONTROL 数据卫生UI] 提交请求后，该请求将保持挂起状态，直到计划过期时间（之后将执行请求）为止。 |
| 数据集已删除 | 1 小时 | 数据集将从 [数据集库页面](../catalog/datasets/user-guide.md) 中。 数据湖中的数据只会被软删除，并且会一直保留到过程结束，之后将会硬删除。 |
| 更新了用户档案计数 | 30 小时 | 数据集过期导致的配置文件计数更改反映在 [功能板小组件](../dashboards/guides/profiles.md#profile-count-trend) 和其他报告。 |
| 区段已更新 | 48 小时 | 删除用户档案后，所有相关 [区段](../segmentation/home.md) 会更新以反映其新大小。 |
| 历程和目标已更新 | 50 小时 | [历程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [营销活动](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)和 [目标](../destinations/home.md) 会根据相关区段的更改进行更新。 |
| 硬删除完成 | 14 天 | 与数据集相关的所有数据都将从数据湖中硬删除。 的 [卫生工作状况](./ui/browse.md#view-details) 会更新删除数据集的内容，以反映这一点。 |

{style=&quot;table-layout:auto&quot;}

### 消费者删除 {#consumer-delete-transparency}

在 [消费者删除请求](./ui/delete-consumer.md) 已创建：

| 暂存 | 请求提交后的时间 | 描述 |
| --- | --- | --- |
| 请求已提交 | 0 小时 | 数据管理员或隐私分析员提交消费者删除请求。 请求显示在 [!UICONTROL 数据卫生UI] 在提交之后。 |
| 配置文件查找已更新 | 3 小时 | 删除身份导致的用户档案计数更改将反映在 [功能板小组件](../dashboards/guides/profiles.md#profile-count-trend) 和其他报告。 |
| 区段已更新 | 24 小时 | 删除用户档案后，所有相关 [区段](../segmentation/home.md) 会更新以反映其新大小。 |
| 历程和目标已更新 | 26 小时 | [历程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [营销活动](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)和 [目标](../destinations/home.md) 会根据相关区段的更改进行更新。 |
| 在数据湖中删除记录软项 | 7 天 | 数据会从数据湖中软删除。 |
| 数据抽真空完成 | 14 天 | 的 [卫生工作状况](./ui/browse.md#view-details) 更新以指示作业已完成，这意味着数据湖上的数据抽真空已完成，相关记录已被硬删除。 |

{style=&quot;table-layout:auto&quot;}

## 后续步骤

本文档概述了Platform的数据卫生功能。 要开始在UI中发出数据卫生请求，请参阅 [UI指南](./ui/overview.md). 要了解如何以编程方式创建数据卫生作业，请参阅 [数据卫生API指南](./api/overview.md)
