---
title: 高级数据生命周期管理概述
description: 高级数据生命周期管理允许您通过更新或清除过时或不准确的记录来管理数据的生命周期。
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 9ffd2db5555a4c157171d488deb9641aadbb08b4
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 1%

---

# Adobe Experience Platform中的高级数据生命周期管理

Adobe Experience Platform提供了一套强大的工具来管理大型复杂的数据操作，以编排消费者体验。 随着时间推移数据被摄取到系统中，管理数据存储变得越来越重要，以便数据按预期使用，在不正确的数据需要更正时更新，并在组织策略认为必要时删除。

<!-- Experience Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

可以使用[[!UICONTROL 数据生命周期] UI工作区](#ui)或[数据卫生API](#api)执行这些活动。 当数据生命周期作业执行时，系统会在流程的每个步骤提供透明度更新。 有关系统中每种作业类型的表示方式的更多信息，请参阅[时间线和透明度](#timelines-and-transparency)部分。

>[!NOTE]
>
>高级数据生命周期管理支持通过[数据集到期终结点](./api/dataset-expiration.md)进行数据集删除，以及通过[工作单终结点](./api/workorder.md)使用主标识进行ID删除（行级数据）。 您还可以通过Experience Platform UI管理[数据集过期](./ui/dataset-expiration.md)和[记录删除](./ui/record-delete.md)。 有关更多信息，请参阅链接的文档。 请注意，数据生命周期不支持批量删除。

## [!UICONTROL 数据生命周期] UI工作区 {#ui}

Experience Platform UI中的[!UICONTROL 数据生命周期]工作区允许您配置和计划数据生命周期操作，从而确保您的记录按预期维护。

有关在UI中管理数据生命周期任务的详细步骤，请参阅[数据生命周期UI指南](./ui/overview.md)。

## 数据卫生API {#api}

[!UICONTROL 数据生命周期] UI基于数据卫生API构建，如果您希望自动执行数据生命周期活动，则可以直接使用该API的端点。 有关详细信息，请参阅[数据卫生API指南](./api/overview.md)。

## 时间表和透明度 {#timelines-and-transparency}

[记录删除](./ui/record-delete.md)和数据集过期请求都有各自的处理时间表，并在各自工作流程中的关键点提供透明度更新。

>[!TIP]
>
>若要监视当前使用量是否符合配额限制，请参阅[配额参考指南](./api/quota.md)。\
>有关权利规则、每月上限、SLA时间表和异常处理策略，请参阅[记录删除(UI)](./ui/record-delete.md#quotas)和[工作单(API)](./api/workorder.md#quotas)文档。

创建[数据集过期请求](./ui/dataset-expiration.md)时会发生以下情况：

| 暂存 | 计划到期后的时间 | 描述 |
| --- | --- | --- |
| 已提交请求 | 0 小时 | 数据管理员或隐私分析人员提交数据集在给定时间到期的请求。 提交请求后，该请求将显示在[!UICONTROL 数据生命周期UI]中，并一直处于待处理状态，直到计划的过期时间（该时间之后将执行请求）。 |
| 数据集已标记为删除 | 0-2小时 | 执行请求后，数据集将标记为删除。 如果使用Amazon Web Services (AWS)数据存储，此过程最多需要两个小时。 在此期间，批处理分段和流式分段、预览或估计、导出和访问等操作会忽略此数据集。 |
| 数据集已删除 | 3 小时 | **在数据集被标记为删除的一小时后**，它已从系统中完全删除。 此时，会从UI中的[数据集清单页面](../catalog/datasets/user-guide.md)中删除数据集。 但是，数据湖中的数据在此阶段仅被软删除，并且将在硬删除过程完成之前保持软删除状态。 |
| 配置文件计数已更新 | 30 小时 | 根据要删除的数据集的内容，如果某些用户档案的所有组件属性都与该数据集关联，则可能会从系统中删除该用户档案。 数据集被删除30小时后，所有配置文件计数中产生的任何更改都会反映在[仪表板小组件](../dashboards/guides/profiles.md#profile-count-trend)和其他报表中。 |
| 已更新受众 | 48 小时 | 更新所有受影响的配置文件后，将更新所有相关的[受众](../segmentation/home.md)以反映其新大小。 根据删除的数据集以及您进行分段的属性，每个受众的大小可能会因删除而增加或减少。 |
| 已更新历程和目标 | 50 小时 | 已根据相关区段中的更改更新[历程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html)、[促销活动](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)和[目标](../destinations/home.md)。 |
| 硬删除完成 | 15 天 | 与数据集相关的所有数据都会从数据湖中硬删除。 已删除数据集的数据生命周期作业](./ui/browse.md#view-details)的[状态已更新以反映此情况。 |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>在完全应用更改之前，Amazon Web Services (AWS)中的数据集删除操作大约会延迟三个小时。 这最多包括标记要删除的数据集需要两个小时，随后是从系统中完全删除之前的一个小时。 相反，使用Azure数据湖的Experience Platform实例的删除请求会导致跨业务功能的立即更改。
>
>对于AWS用户，此延迟可能会影响批量分段、流式分段、预览、估算、导出和数据访问。 此延迟仅影响使用AWS的客户，因为Azure Data Lake用户会体验到即时更新。 对于AWS用户，删除请求可能需要长达三个小时才能完全传播到所有受影响的系统中。 相应地调整您的预期。


<!-- ### Record deletes {#record-delete-transparency}

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Lifecycle UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the lifecycle job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## 后续步骤

本文档概述了Experience Platform的数据生命周期功能。 要开始在UI中提出数据卫生请求，请参阅[UI指南](./ui/overview.md)。 要了解如何以编程方式创建数据生命周期作业，请参阅[数据卫生API指南](./api/overview.md)
