---
title: 数据卫生概述
description: Adobe Experience Platform数据卫生允许您通过更新或清除过时或不准确的记录来管理数据的生命周期。
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: e59def7a05862ad880d0b6ada13b1c69c655ff90
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Adobe Experience Platform中的数据卫生

>[!IMPORTANT]
>
>数据卫生当前仅适用于已购买的组织 **AdobeHealth Shield** 或 **Adobe隐私和安全防护**. 这些功能将在不久的将来正式发布。 有关其即将推出的详细信息，请咨询您的Adobe服务代表。 但是，您可以立即 [删除数据集 [!UICONTROL 数据集] UI](../catalog/datasets/user-guide.md#delete).

Adobe Experience Platform提供了一套强大的工具来管理大型复杂的数据操作，以编排消费者体验。 随着时间推移数据被摄取到系统中，管理数据存储变得越来越重要，以便数据按预期使用，在不正确的数据需要更正时更新，并在组织策略认为有必要时删除。

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

这些活动可以使用执行 [[!UICONTROL 数据卫生] UI工作区](#ui) 或 [数据卫生API](#api). 当执行数据卫生作业时，系统提供每个处理步骤的透明度更新。 请参阅以下部分： [时间轴和透明度](#timelines-and-transparency) 有关每种作业类型在系统中的表示方式的更多信息。

## [!UICONTROL 数据卫生] UI工作区 {#ui}

此 [!UICONTROL 数据卫生] Platform UI中的工作区允许您配置和计划数据卫生操作，这有助于确保您的记录按预期维护。

有关在UI中管理数据卫生任务的详细步骤，请参阅 [数据卫生UI指南](./ui/overview.md).

## 数据卫生API {#api}

此 [!UICONTROL 数据卫生] UI基于数据卫生API构建，如果您希望自动执行数据卫生活动，则可以直接使用该API的端点。 请参阅 [数据卫生API指南](./api/overview.md) 了解更多信息。

## 时间轴和透明度

记录删除和数据集过期请求都有各自的处理时间表，并在各自工作流程中的关键点提供透明度更新。

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

在以下情况下 [数据集过期请求](./ui/dataset-expiration.md) 创建时间：

| 暂存 | 计划到期后的时间 | 描述 |
| --- | --- | --- |
| 已提交请求 | 0 小时 | 数据管理员或隐私分析人员提交数据集在给定时间到期的请求。 该请求在中可见 [!UICONTROL 数据卫生UI] 之后，将保持挂起状态，直到计划的到期时间，在此时间之后将执行请求。 |
| 数据集已删除 | 1 小时 | 数据集将从以下位置删除： [数据集清单页面](../catalog/datasets/user-guide.md) 在UI中。 数据湖中的数据仅被软删除，并将保持软删除直到进程结束，之后这些数据将被硬删除。 |
| 配置文件计数已更新 | 30 小时 | 根据要删除的数据集的内容，如果某些用户档案的所有组件属性都与该数据集关联，则可能会将其从系统中删除。 数据集删除后30小时，任何对总体用户档案计数产生的更改都会反映在 [仪表板小组件](../dashboards/guides/profiles.md#profile-count-trend) 和其他报告。 |
| 已更新受众 | 48 小时 | 更新所有受影响的配置文件后，所有相关的 [受众](../segmentation/home.md) 将更新以反映其新大小。 根据删除的数据集和您进行分段的属性，每个受众的大小可能会因删除而增加或减少。 |
| 已更新历程和目标 | 50 小时 | [历程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html)， [营销活动](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)、和 [目标](../destinations/home.md) 会根据相关区段中的更改进行更新。 |
| 硬删除完成 | 14 天 | 与数据集相关的所有数据都会从数据湖中硬删除。 此 [保健作业的状态](./ui/browse.md#view-details) 随即会更新已删除的数据集以反映这一点。 |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

>[!IMPORTANT]
>
>Record deletes are only available for organizations that have purchased Adobe Healthcare Shield.

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Hygiene UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the hygiene job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## 后续步骤

本文档概述了Platform的数据卫生功能。 要开始在UI中提出数据卫生请求，请参阅 [UI指南](./ui/overview.md). 要了解如何以编程方式创建数据卫生作业，请参阅 [数据卫生API指南](./api/overview.md)
