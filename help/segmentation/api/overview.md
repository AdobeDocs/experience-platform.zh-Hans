---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；API；API；
title: 分段服务API指南
description: 分段服务API允许开发人员以编程方式管理Adobe Experience Platform中的分段操作。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---

# 分段服务API指南

[!DNL Adobe Experience Platform Segmentation Service] 允许您在中构建区段并生成受众 [!DNL Adobe Experience Platform] 来自您的 [!DNL Real-Time Customer Profile] 数据。

此 [!DNL Segmentation Service] API提供了多个端点，允许您以编程方式管理以下位置的分段操作： [!DNL Experience Platform]. 此概述文档提供了其中每个端点的概要介绍，以及指向其关联端点指南的链接以了解详细信息。 在阅读各个端点指南之前，请参阅 [快速入门指南](./getting-started.md) 有关所需标头的重要信息，请阅读示例API调用等。

要查看所有可用的端点和CRUD操作，请参阅 [Segmentation Service API参考](https://www.adobe.io/experience-platform-apis/references/segmentation/).

<!-- ## Audiences

Audiences are a collection of people who share similar behaviors and/or characteristics. These can be generated either by using Platform or from external sources. You can use the `/audiences` endpoint to retrieve all audiences, create a new audience, retrieve details of a specific audience, update a specific audience, or delete a specific audience.

For more information on using this endpoint, please read the [audiences endpoint guide](./audiences.md). -->

## 导出作业

导出作业是异步流程，用于将受众区段成员保留到数据集。 您可以使用 `/export/jobs` 端点，用于检索所有导出作业、创建新的导出作业、检索特定导出作业的详细信息，或取消特定导出作业。

有关使用此端点的更多信息，请阅读 [导出作业端点指南](./export-jobs.md).

## 预览和估计

预览会提供符合区段定义的用户档案分页列表，以便您将结果与预期结果进行比较。 您可以使用 `/preview` 端点，用于创建新的预览作业或查找特定预览作业的结果。

估算可提供区段定义的统计信息，例如预计受众规模、置信区间和误差标准偏差。 您可以使用 `/estimate` 端点，以查看区段定义的估计值。

有关使用这些端点的详细信息，请阅读 [预览和估计端点指南](./previews-and-estimates.md).

## 时间表

计划是一种可用于每天自动运行一次批处理分段作业的工具。 您可以使用 `/config/schedules` 端点检索计划列表、创建新计划、检索特定计划的详细信息、更新特定计划或删除特定计划。

有关使用此端点的更多信息，请阅读 [计划端点指南](./schedules.md).

## 区段定义

区段定义定义哪些配置文件将成为哪些受众区段的一部分。 您可以使用 `/segment/definitions` 端点以管理区段定义。

有关使用此端点的更多信息，请阅读 [区段定义端点指南](./segment-definitions.md).

## 区段作业

区段作业会处理以前建立的区段定义以生成受众区段。 您可以使用 `/segment/jobs` 端点以管理区段作业。

有关使用此端点的更多信息，请阅读 [区段作业端点指南](./segment-jobs.md).

## 区段搜索

区段搜索用于搜索各种数据源中包含的字段并近乎实时地返回它们。 要开始使用区段搜索，请参阅 [搜索端点指南](segment-search.md)

## 后续步骤

要开始使用 [!DNL Segmentation Service] API，请查看不同的端点指南，以了解有关如何调用服务的各种端点的详细步骤。 要了解有关使用区段的更多信息，请使用 [!DNL Platform] UI，请参阅 [分段用户指南](../ui/overview.md).
