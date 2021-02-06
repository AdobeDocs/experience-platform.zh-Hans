---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；API;api;
title: 分段服务API指南
topic: guide
description: Segmentation Service API允许开发人员以编程方式管理Adobe Experience Platform的分段操作。 请按照本指南学习如何使用API执行关键操作。
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# 分段服务API指南

[!DNL Adobe Experience Platform Segmentation Service] 允许您根据数据构建细 [!DNL Adobe Experience Platform] 分和生 [!DNL Real-time Customer Profile] 成受众

[!DNL Segmentation Service] API提供多个端点，允许您以编程方式管理[!DNL Experience Platform]中的分段操作。 此概述文档提供了每个端点的高级介绍，以及指向其关联端点指南的链接以获取详细信息。 在阅读各个端点指南之前，请参阅[快速入门指南](./getting-started.md)，了解有关所需标头、读取示例API调用等的重要信息。

要视图所有可用的端点和CRUD操作，请参阅[分段服务API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)。

## 导出作业

导出作业是异步进程，用于将受众段成员保留到数据集。 您可以使用`/export/jobs`端点检索所有导出作业、创建新导出作业、检索特定导出作业的详细信息或取消特定导出作业。

有关使用此端点的详细信息，请阅读[导出作业端点指南](./export-jobs.md)。

## 预览和估计

预览为区段定义提供符合条件的用户档案的分页列表，允许您将结果与预期进行比较。 您可以使用`/preview`端点创建新的预览作业或查找特定预览作业的结果。

估计提供细分定义的统计信息，如预测受众大小、置信区间和误差标准偏差。 您可以使用`/estimate`端点视图段定义的估计值。

有关使用这些端点的详细信息，请阅读[预览和估计端点指南](./previews-and-estimates.md)。

## 计划

计划是一种工具，可用于每天自动运行一次批处理分段作业。 您可以使用`/config/schedules`端点检索列表、创建新计划、检索特定计划的详细信息、更新特定计划或删除特定计划。

有关使用此端点的详细信息，请阅读[计划端点指南](./schedules.md)。

## 细分定义

区段定义定义哪些用户档案将成为哪些受众区段的一部分。 您可以使用`/segment/definitions`端点管理段定义。

有关使用此端点的详细信息，请阅读[段定义端点指南](./segment-definitions.md)。

## 细分作业

细分作业流程以前建立的细分定义以生成受众细分。 您可以使用`/segment/jobs`端点管理段作业。

有关使用此端点的详细信息，请阅读[段作业端点指南](./segment-jobs.md)。

## 区段搜索

区段搜索用于搜索包含在各种数据源中的字段，并近乎实时地返回它们。 要开始使用段搜索，请参阅[搜索端点指南](segment-search.md)

## 后续步骤

要开始使用[!DNL Segmentation Service] API，请查看不同的端点指南，了解有关如何调用服务的各个端点的详细步骤。 要进一步了解如何使用[!DNL Platform] UI处理区段，请参阅[分段用户指南](../ui/overview.md)。