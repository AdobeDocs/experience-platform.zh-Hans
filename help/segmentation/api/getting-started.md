---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 分段服务开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: bbca6d8f4ab7a684e8bfb1d39b538d937a99244f
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---


# 分段服务开发人员指南

细分允许您在Adobe Experience Platform中根据实时客户受众数据构建细分并生成用户档案。

## 入门指南

本指南需要对使用分段所涉及的各种Adobe Experience Platform服务有充分的了解。

- [细分](../home.md): 允许您根据实时受众数据构建用户档案细分。
- [体验数据模型(XDM)系统](../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
- [实时客户用户档案](../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
- [沙箱](../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成功使用分段。

### 读取示例API调用

Segmentation Service API文档提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的部分。

### 所需的标题

API文档还要求您完成身份验证教 [程](../../tutorials/authentication.md) ，以便成功调用平台端点。 完成身份验证教程后，将为Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱相隔离。 对平台API的所有请求都需要一个标头，它指定将在其中执行操作的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关在Experience Platform中使用沙箱的更多信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

<!-- ## Estimates

Estimates provides statistical information for a segment definition, such as projected audience size and confidence interval. You can use the `/estimate` endpoint to view an estimate of a segment definition. 

For more information on using this endpoint, please read the [estimates developer guide](./estimates.md). 

## Export jobs

Export jobs are asynchronous processes that are used to persist audience segment members to datasets. You can use the `/export/jobs` endpoint to retrieve all export jobs, create a new export job, retrieve details of a specific export job, or cancel a specific export job.

For more information on using this endpoint, please read the [export jobs developer guide](./export-jobs.md).

## Previews

Previews provide a paginated list of qualifying profiles for a segment definition, allowing you to compare the results against what you expect. You can use the `/preview` endpoint to create a new preview job, look up results of a specific preview job, or delete a specific preview job.

For more information on using this endpoint, please read the [previews developer guide](./previews.md).

## PQL conversions

Profile Query Language (PQL) conversions allows you to convert your formatting between `pql/text` and `pql/json`. You can do this by using the `/segment/conversion` endpoint.

For more information on using this endpoint, please read the [PQL conversions developer guide](./pql-conversions.md).

## Schedules

Schedules are a tool that can be used to automatically run export jobs once a day. You can use the `/config/schedules` endpoint to retrieve a list of schedules, create a new schedule, retrieve details of a specific schedule, update a specific schedule, or delete a specific schedule. 

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md). -->

## 细分定义

区段定义定义哪些用户档案将成为哪些受众区段的一部分。 您可以使用端点 `/segment/definitions` 检索段定义的列表、创建新段定义、检索特定段定义的详细信息、删除特定段定义或覆盖特定段定义的详细信息。

有关使用此端点的详细信息，请阅读段定 [义开发人员指南](./segment-definitions.md)。

## 细分作业

细分作业流程以前建立的细分定义以生成受众细分。 您可以使用端 `/segment/jobs` 点来检索区段作业的列表、创建新的区段作业、检索特定区段作业的详细信息或删除特定区段作业。

有关使用此端点的详细信息，请阅读段作 [业开发人员指南](./segment-jobs.md)。

## 区段搜索

段搜索用于搜索和索引包含在各种数据源中的可配置字段，并近乎实时地返回它们。 要开始使用区段搜索，请参阅搜索开 [发人员指南](segment-search.md)

## 后续步骤

要开始使用分段API进行调用，请选择其中一个子指南来了解如何使用特定的分段相关端点。 要进一步了解如何使用平台UI处理区段，请参阅 [分段用户指南](../ui/overview.md)。