---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；API;API;
title: Segmentation Service API指南
topic-legacy: guide
description: Segmentation Service API允许开发人员以编程方式管理Adobe Experience Platform中的分段操作。 请阅读本指南，了解如何使用API执行关键操作。
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Segmentation Service API指南

[!DNL Adobe Experience Platform Segmentation Service] 允许您在中根据数据生成区 [!DNL Adobe Experience Platform] 段和 [!DNL Real-time Customer Profile] 受众。

[!DNL Segmentation Service] API提供了多个端点，允许您以编程方式管理[!DNL Experience Platform]中的分段操作。 此概述文档提供了每个端点的高级简介，以及指向其关联端点指南的链接以了解详细信息。 在阅读各个端点指南之前，请参阅[快速入门指南](./getting-started.md) ，以了解有关所需标头、读取示例API调用等的重要信息。

要查看所有可用的端点和CRUD操作，请参阅[Segmentation Service API引用](https://www.adobe.io/experience-platform-apis/references/segmentation/)。

## 导出作业

导出作业是用于将受众区段成员保留到数据集的异步进程。 您可以使用`/export/jobs`端点检索所有导出作业、创建新导出作业、检索特定导出作业的详细信息或取消特定导出作业。

有关使用此端点的更多信息，请阅读[导出作业端点指南](./export-jobs.md)。

## 预览和估计

“预览”为区段定义提供符合条件的用户档案的分页列表，允许您将结果与预期结果进行比较。 您可以使用`/preview`端点创建新的预览作业或查找特定预览作业的结果。

估计值提供区段定义的统计信息，如预计受众规模、置信区间和误差标准偏差。 您可以使用`/estimate`端点来查看区段定义的估计值。

有关使用这些端点的更多信息，请阅读[预览和估计端点指南](./previews-and-estimates.md)。

## 调度程序

计划是一种工具，可用于每天自动运行一次批量分段作业。 您可以使用`/config/schedules`端点来检索计划列表、创建新计划、检索特定计划的详细信息、更新特定计划或删除特定计划。

有关使用此端点的更多信息，请阅读[计划端点指南](./schedules.md)。

## 区段定义

区段定义定义哪些用户档案将属于哪些受众区段。 您可以使用`/segment/definitions`端点管理区段定义。

有关使用此端点的更多信息，请阅读[区段定义端点指南](./segment-definitions.md)。

## 区段作业

区段作业会处理之前已建立的区段定义，以生成受众区段。 您可以使用`/segment/jobs`端点管理区段作业。

有关使用此端点的更多信息，请阅读[segment作业端点指南](./segment-jobs.md)。

## 区段搜索

区段搜索用于搜索跨各种数据源包含的字段，并近乎实时地返回它们。 要开始使用区段搜索，请参阅[search endpoint guide](segment-search.md)

## 后续步骤

要开始使用[!DNL Segmentation Service] API，请查看不同的端点指南，以详细了解如何调用服务的各种端点。 要了解有关使用[!DNL Platform] UI处理区段的更多信息，请参阅[分段用户指南](../ui/overview.md)。
