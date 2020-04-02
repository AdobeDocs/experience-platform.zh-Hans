---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 分段服务开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: 38762fa57188ed018c4347c07765f3d09daef2e6

---


# 分段服务开发人员指南

细分允许您在Adobe Experience Platform中根据实时客户用户档案数据构建细分并生成受众。

## 入门指南

本指南需要了解与使用分段相关的各种Adobe Experience Platform服务。

- [细分](../home.md):允许您根据实时客户用户档案数据构建受众细分。
- [体验数据模型(XDM)系统](../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
- [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
- [沙箱](../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成功使用分段。

### 读取示例API调用

Segmentation Service API文档提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 必需的标题

API文档还要求您完成身份验证教 [程](../../tutorials/authentication.md) ，以成功调用平台端点。 完成身份验证教程后，Experience Platform API调用中每个所需标头的值将显示如下：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定要在其中执行操作的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>**注意：** 有关在Experience Platform中使用沙箱的更多信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

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

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md).

## Segment definitions

Segment definitions define which profiles will be part of which audience segments. You can use the `/segment/definitions` endpoint to retrieve a list of segment definitions, create a new segment definition, retrieve details of a specific segment definition, delete a specific segment definition, or overwrite details of a specific segment definition.

For more information on using this endpoint, please read the [segment definitions developer guide](./segment-definitions.md). -->

## 细分作业

区段作业会处理先前建立的区段定义，以生成受众区段。 您可以使用端 `/segment/jobs` 点检索区段作业的列表、创建新的区段作业、检索特定区段作业的详细信息或删除特定区段作业。

有关使用此端点的详细信息，请阅读区段作 [业开发人员指南](./segment-jobs.md)。

## 后续步骤

要开始使用分段API进行调用，请选择其中一个子指南，以了解如何使用特定的分段相关端点。 要进一步了解如何使用平台UI处理区段，请参阅分 [段用户指南](../ui/overview.md)。