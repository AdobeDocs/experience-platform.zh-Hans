---
title: 数据卫生概述
description: Adobe Experience Platform数据卫生功能允许您通过更新或清除过时或不准确的记录来管理数据的生命周期。
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 2913e9e687843e566db4ebf2031e610d1891d4c9
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Adobe Experience Platform数据卫生

>[!IMPORTANT]
>
>目前，数据卫生仅适用于已购买的组织 **Adobe医疗保健盾** 或 **Adobe隐私和安全防护**. 这些功能将在不久的将来正式发布。 有关这些服务即将发布的更多信息，请联系您的Adobe服务代表。 但是，您可以立即 [通过删除数据集 [!UICONTROL 数据集] UI](../catalog/datasets/user-guide.md#delete).

Adobe Experience Platform提供了一组功能强大的工具来管理大型、复杂的数据操作，以编排客户体验。 随着数据逐渐被摄取到系统中，管理数据存储变得越来越重要，这样数据就可以按预期使用，错误数据需要更正时会更新，组织策略认为有必要时会删除。

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

这些活动可以使用 [[!UICONTROL 数据卫生] UI工作区](#ui) 或 [数据卫生API](#api). 当执行数据卫生作业时，系统会在处理的每个步骤中提供透明度更新。 请参阅 [时间表和透明度](#timelines-and-transparency) 有关每个作业类型在系统中如何表示的详细信息。

## [!UICONTROL 数据卫生] UI工作区 {#ui}

的 [!UICONTROL 数据卫生] 平台UI中的工作区允许您配置和计划数据卫生操作，这有助于确保记录按预期进行维护。

有关在UI中管理数据卫生任务的详细步骤，请参阅 [数据卫生UI指南](./ui/overview.md).

## 数据卫生API {#api}

的 [!UICONTROL 数据卫生] UI是基于数据卫生API构建的，如果您希望自动执行数据卫生活动，则可以直接使用其端点。 请参阅 [数据卫生API指南](./api/overview.md) 以了解更多信息。

## 时间表和透明度

记录删除请求和数据集过期请求每个请求都有各自的处理时间轴，并在各自工作流的关键点提供透明度更新。

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

在 [数据集过期请求](./ui/dataset-expiration.md) 已创建：

| 暂存 | 计划过期后的时间 | 描述 |
| --- | --- | --- |
| 请求已提交 | 0 小时 | 数据管理员或隐私分析员提交了一个请求，要求数据集在给定时间过期。 请求显示在 [!UICONTROL 数据卫生UI] 提交请求后，该请求将保持挂起状态，直到计划过期时间（之后将执行请求）为止。 |
| 数据集已删除 | 1 小时 | 数据集将从 [数据集库页面](../catalog/datasets/user-guide.md) 中。 数据湖中的数据只会被软删除，并且会一直保留到过程结束，之后将会硬删除。 |
| 更新了用户档案计数 | 30 小时 | 根据所删除数据集的内容，如果某些配置文件的所有组件属性都与该数据集绑定，则这些配置文件可能会从系统中删除。 在删除数据集30小时后，对整体用户档案计数所做的任何更改都会反映在 [功能板小组件](../dashboards/guides/profiles.md#profile-count-trend) 和其他报告。 |
| 区段已更新 | 48 小时 | 更新所有受影响的用户档案后，所有相关 [区段](../segmentation/home.md) 会更新以反映其新大小。 根据删除的数据集以及您进行分段的属性，每个区段的大小可能会因删除而增加或减少。 |
| 历程和目标已更新 | 50 小时 | [历程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [营销活动](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)和 [目标](../destinations/home.md) 会根据相关区段的更改进行更新。 |
| 硬删除完成 | 14 天 | 与数据集相关的所有数据都将从数据湖中硬删除。 的 [卫生工作状况](./ui/browse.md#view-details) 会更新删除数据集的内容，以反映这一点。 |

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

本文档概述了Platform的数据卫生功能。 要开始在UI中发出数据卫生请求，请参阅 [UI指南](./ui/overview.md). 要了解如何以编程方式创建数据卫生作业，请参阅 [数据卫生API指南](./api/overview.md)
