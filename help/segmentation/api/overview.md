---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；API;API;
title: Segmentation Service API指南
topic-legacy: guide
description: Segmentation Service API允许开发人员以编程方式管理Adobe Experience Platform中的分段操作。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: b48ead4255d50585cd315436ccb9727d86142d4c
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 2%

---

# Segmentation Service API指南

[!DNL Adobe Experience Platform Segmentation Service] 允许您在 [!DNL Adobe Experience Platform] 从 [!DNL Real-time Customer Profile] 数据。

的 [!DNL Segmentation Service] API提供了多个端点，允许您以编程方式在中管理分段操作 [!DNL Experience Platform]. 此概述文档提供了每个端点的高级简介，以及指向其关联端点指南的链接以了解详细信息。 在阅读各个端点指南之前，请参阅 [入门指南](./getting-started.md) 有关所需标头、读取示例API调用等的重要信息。

要查看所有可用的端点和CRUD操作，请参阅 [分段服务API参考](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## 受众

受众是指具有相似行为和/或特征的人员的集合。 这些量度既可以使用Platform生成，也可以从外部源生成。 您可以使用 `/audiences` 用于检索所有受众、创建新受众、检索特定受众的详细信息、更新特定受众或删除特定受众的端点。

有关使用此端点的更多信息，请阅读 [audiences endpoint guide](./audiences.md).

## 导出作业

导出作业是用于将受众区段成员保留到数据集的异步进程。 您可以使用 `/export/jobs` 用于检索所有导出作业、创建新导出作业、检索特定导出作业的详细信息或取消特定导出作业的端点。

有关使用此端点的更多信息，请阅读 [导出作业端点指南](./export-jobs.md).

## 预览和估计

“预览”为区段定义提供符合条件的用户档案的分页列表，允许您将结果与预期结果进行比较。 您可以使用 `/preview` 端点来创建新的预览作业或查找特定预览作业的结果。

估计值提供区段定义的统计信息，如预计受众规模、置信区间和误差标准偏差。 您可以使用 `/estimate` 端点来查看区段定义的估计值。

有关使用这些端点的更多信息，请阅读 [预览和估计端点指南](./previews-and-estimates.md).

## 计划

计划是一种工具，可用于每天自动运行一次批量分段作业。 您可以使用 `/config/schedules` 端点来检索计划列表、创建新计划、检索特定计划的详细信息、更新特定计划或删除特定计划。

有关使用此端点的更多信息，请阅读 [schedules endpoint guide](./schedules.md).

## 区段定义

区段定义定义哪些用户档案将属于哪些受众区段。 您可以使用 `/segment/definitions` 用于管理区段定义的端点。

有关使用此端点的更多信息，请阅读 [segment definitions endpoint buide](./segment-definitions.md).

## 区段作业

区段作业会处理之前已建立的区段定义，以生成受众区段。 您可以使用 `/segment/jobs` 用于管理区段作业的端点。

有关使用此端点的更多信息，请阅读 [segment jobs endpoint wide](./segment-jobs.md).

## 区段搜索

区段搜索用于搜索跨各种数据源包含的字段，并近乎实时地返回它们。 要开始使用区段搜索，请参阅 [search endpoint指南](segment-search.md)

## 后续步骤

要开始使用 [!DNL Segmentation Service] 有关如何调用服务各种端点的详细步骤，请参阅不同端点指南。 要了解有关使用 [!DNL Platform] UI，请参阅 [分段用户指南](../ui/overview.md).
