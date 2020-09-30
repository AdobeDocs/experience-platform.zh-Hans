---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;API;api;
title: Adobe Experience Platform分段服务开发人员指南
topic: guide
description: 此概述文档提供了每个Segmentation Service API端点的高级介绍，以及指向相关端点指南的链接以获取详细信息。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Segmentation Service] API开发人员指南

[!DNL Adobe Experience Platform Segmentation Service] 允许您根据数据构建细分 [!DNL Adobe Experience Platform] 和生成 [!DNL Real-time Customer Profile] 受众。

API提 [!DNL Segmentation Service] 供多个端点，允许您在中以编程方式管理您的分段操作 [!DNL Experience Platform]。 此概述文档提供了每个端点的高级介绍，以及指向其关联端点指南的链接以获取详细信息。 在阅读各个端点指南之前，请参 [阅入门指南](./getting-started.md) ，了解有关所需标题、读取示例API调用等的重要信息。

要视图所有可用的端点和CRUD操作，请参阅分段 [服务API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)。

## 导出作业

导出作业是异步进程，用于将受众段成员保留到数据集。 您可以使用端点 `/export/jobs` 来检索所有导出作业、创建新导出作业、检索特定导出作业的详细信息或取消特定导出作业。

有关使用此端点的详细信息，请阅读导 [出作业端点指南](./export-jobs.md)。

## 预览和估计

预览为区段定义提供符合条件的用户档案的分页列表，允许您将结果与预期进行比较。 您可以使用终 `/preview` 结点创建新预览作业或查找特定预览作业的结果。

估计提供细分定义的统计信息，如预测受众大小、置信区间和误差标准偏差。 您可以使用端 `/estimate` 点来视图段定义的估计。

有关使用这些端点的更多信息，请阅读 [预览和估计端点指南](./previews-and-estimates.md)。

## 计划

计划是一种工具，可用于每天自动运行一次批处理分段作业。 您可以使用端点 `/config/schedules` 检索列表、创建新计划、检索特定计划的详细信息、更新特定计划或删除特定计划。

有关使用此端点的更多信息，请阅读 [计划端点指南](./schedules.md)。

## 细分定义

区段定义定义哪些用户档案将成为哪些受众区段的一部分。 您可以使用端 `/segment/definitions` 点管理段定义。

有关使用此端点的详细信息，请阅读段定 [义端点指南](./segment-definitions.md)。

## 细分作业

细分作业流程以前建立的细分定义以生成受众细分。 您可以使用端 `/segment/jobs` 点管理段作业。

有关使用此端点的详细信息，请阅读段作 [业端点指南](./segment-jobs.md)。

## 区段搜索

区段搜索用于搜索包含在各种数据源中的字段，并近乎实时地返回它们。 要开始使用段搜索，请参阅搜索 [端点指南](segment-search.md)

## 后续步骤

要开始使用API, [!DNL Segmentation Service] 请查看不同的端点指南，了解有关如何调用服务的各个端点的详细步骤。 要进一步了解如何使用UI处理 [!DNL Platform] 区段，请参阅 [分段用户指南](../ui/overview.md)。