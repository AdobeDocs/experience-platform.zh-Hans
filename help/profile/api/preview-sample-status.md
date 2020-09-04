---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;preview;sample
solution: Adobe Experience Platform
title: 用户档案预览-实时客户用户档案API
description: Adobe Experience Platform使您能够从多个来源收集客户数据，从而为各个客户构建强大的统一用户档案。 由于实时客户用户档案启用的数据被引入平台，因此它存储在用户档案数据存储中。 随着用户档案存储中记录数的增加或减少，将运行一个示例作业，该示例作业包括关于用户档案片段和合并用户档案在数据存储中的数量的信息。 使用用户档案API，您可以预览最新成功的示例，以及按数据集和身份命名空间列表用户档案分发。
topic: guide
translation-type: tm+mt
source-git-commit: 2edba7cba4892f5c8dd41b15219bf45597bd5219
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 1%

---


# 预览示例状态端点(用户档案预览)

Adobe Experience Platform使您能够从多个来源收集客户数据，从而为各个客户构建强大的统一用户档案。 当实时用户档案启用的数据被引入时，它 [!DNL Platform]会存储在用户档案数据存储中。

当将记录引入用户档案存储中时，将用户档案总计数增加或减少5%以上，将触发作业以更新该计数。 对于流数据工作流，每小时检查一次以确定是否达到5%的增加或减少阈值。 如果已激活，则会自动触发作业以更新计数。 对于批量摄取，在成功将批量摄入用户档案存储的15分钟内，如果达到5%增加或减少阈值，则运行作业以更新计数。 使用用户档案API，您可以预览最新成功的示例作业，以及按数据集和身份命名空间列表用户档案分发。

这些指标也可在用户档案 [!UICONTROL UI] 的Experience Platform部分中找到。 有关如何使用UI访问用户档案数据的信息，请访问 [[!DNL Profile] 用户指南](../ui/user-guide.md)。

## 入门指南

本指南中使用的API端点是API的一 [[!DNL Real-time Customer Profile] 部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。 在继续之前，请查 [看入门指南](getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何API所需标头的重要信 [!DNL Experience Platform] 息。

## 视图上次示例状态 {#view-last-sample-status}

您可以向端点执行GET请 `/previewsamplestatus` 求，以视图为您的IMS组织运行的最后一个成功示例作业的详细信息。 这包括示例中的用户档案总数，以及用户档案计数量度，或您的组织在Experience Platform内拥有的用户档案总数。 用户档案计数在合并用户档案片段后生成，以便为每个单独的客户形成单个用户档案。 换言之，您的组织可能有多个与跨不同渠道与您的品牌进行交互的单个客户相关的用户档案片段，但这些片段将合并在一起（根据默认合并策略），并将返回“1”个用户档案计数，因为它们都与同一个人相关。

用户档案计数还包括具有属性（记录数据）的用户档案以及仅包含时间序列(事件)数据的用户档案，如Adobe Analytics用户档案。 在摄取用户档案数据时，会定期刷新示例作业，以提供平台内最新的用户档案总数。

**API格式**

```http
GET /previewsamplestatus
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括为IMS组织运行的上一个成功示例作业的详细信息。

>[!NOTE]
>
>在此示例响应中， `numRowsToRead` 并 `totalRows` 且彼此相等。 根据您的组织在Experience Platform中拥有的用户档案数，情况可能是这样。 但是，这两个数字通常是不同的， `numRowsToRead` 因为它表示样本是用户档案总数()的子集，所以这两个数字是较小`totalRows`的。

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "cosmosDocCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| 属性 | 描述 |
|---|---|
| `numRowsToRead` | 示例中合并用户档案的总数。 |
| `sampleJobRunning` | 一个布尔值，当 `true` 示例作业正在进行时返回。 为从上传批处理文件到将其实际添加到用户档案存储时发生的延迟提供透明度。 |
| `cosmosDocCount` | Cosmos中的文档总数。 |
| `totalFragmentCount` | 用户档案存储中的用户档案片段总数。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批量摄取时间戳。 |
| `streamingDriven` | *此字段已弃用，且不包含对响应的重要性。* |
| `totalRows` | Experience Platform中合并用户档案的总数，也称为“用户档案数”。 |
| `lastBatchId` | 上次批量摄取ID。 |
| `status` | 最后一个示例的状态。 |
| `samplingRatio` | 采样的合并用户档案()`numRowsToRead`与合并用户档案()总和的比`totalRows`率，以小数格式表示。 |
| `mergeStrategy` | 示例中使用的合并策略。 |
| `lastSampledTimestamp` | 上次成功的示例时间戳。 |

## 列表用户档案分布

要按数据集查看用户档案的分布，可以向端点执行GET请 `/previewsamplestatus/report/dataset` 求。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报告，则将返回该日期的最新报告。 如果指定日期不存在报告，则将返回404错误。 如果未指定日期，则将返回最近的报告。 格式：YYYY-MM-DD。 示例: `date=2024-12-31` |

**请求**

以下请求使用 `date` 参数返回指定日期的最近报告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括一 `data` 个数组，其中包含列表数据集对象。 显示的响应已被截断，以显示三个数据集。

>[!NOTE]
>
>如果该日期存在多个报告，则只返回最新的报告。 如果提供的日期不存在数据集报告，则将返回HTTP状态404（找不到）。

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| 属性 | 描述 |
|---|---|
| `sampleCount` | 使用此数据集ID的采样合并用户档案的总数。 |
| `samplePercentage` | 以 `sampleCount` 十进制格式表示的采样合并用户档案总数( `numRowsToRead` 上一采样状态 [中返回的值](#view-last-sample-status))的百分比表示。 |
| `fullIDsCount` | 此数据集ID的合并用户档案总数。 |
| `fullIDsPercentage` | 合 `fullIDsCount` 并用户档案总数(在上一个示例状态中返回 `totalRows` 的值)的百 [分比，以十进制格式表示](#view-last-sample-status)。 |
| `name` | 数据集的名称，在数据集创建过程中提供。 |
| `description` | 数据集的描述，在数据集创建过程中提供。 |
| `value` | 数据集的ID。 |
| `streamingIngestionEnabled` | 数据集是否启用流摄取。 |
| `createdUser` | 创建数据集的用户ID。 |
| `reportTimestamp` | 报告的时间戳。 如果在 `date` 请求期间提供了参数，则返回的报告为提供的日期。 如果未 `date` 提供参数，则返回最近的报告。 |



## 列表用户档案按命名空间分布

您可以对终结点执行GET请 `/previewsamplestatus/report/namespace` 求，以在用户档案商店中的所有合并用户档案中按标识命名空间视图细分。 身份命名空间是Adobe Experience Platform身份服务的重要组成部分，可作为与客户数据相关的上下文的指标。 要了解更多信息，请访 [问身份命名空间概述](../../identity-service/namespaces.md)。

>[!NOTE]
>
>按命名空间划分的用户档案总数(将每个命名空间显示的值相加)将始终高于用户档案计数量度，因为一个用户档案可能与多个命名空间关联。 例如，如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个别客户关联。

**API格式**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报告，则将返回该日期的最新报告。 如果指定日期不存在报告，则将返回404错误。 如果未指定日期，则将返回最近的报告。 格式：YYYY-MM-DD。 示例: `date=2024-12-31` |

**请求**

以下请求未指定参 `date` 数，因此将返回最近的报告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括一个数 `data` 组，其中各个对象包含每个命名空间的详细信息。 显示的响应已被截断，显示四个命名空间。

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| 属性 | 描述 |
|---|---|
| `sampleCount` | 命名空间中采样的合并用户档案总数。 |
| `samplePercentage` | 以 `sampleCount` 小数格式表示的采样合并用户档案( `numRowsToRead` 上一个采样状态 [中返回的值](#view-last-sample-status))的百分比表示。 |
| `reportTimestamp` | 报告的时间戳。 如果在 `date` 请求期间提供了参数，则返回的报告为提供的日期。 如果未 `date` 提供参数，则返回最近的报告。 |
| `fullIDsFragmentCount` | 用户档案中的命名空间片段总数。 |
| `fullIDsCount` | 命名空间中合并用户档案的总数。 |
| `fullIDsPercentage` | 以 `fullIDsCount` 小数格式表示的合并用户档案总 `totalRows` 数的百分比(上 [一示例状态中返](#view-last-sample-status)回的值)。 |
| `code` | 为 `code` 命名空间。 这在使用 [Adobe Experience PlatformIdentity Service API处理命名空间时](../../identity-service/api/list-namespaces.md) ，也称为 [!UICONTROL Experience PlatformUI中] 的Identity符号。 要了解更多信息，请访 [问身份命名空间概述](../../identity-service/namespaces.md)。 |
| `value` | 命名空间 `id` 的值。 在使用Identity Service API处理命名空间时 [可找到此项](../../identity-service/api/list-namespaces.md)。 |

## 后续步骤

您还可以使用类似的估计和预览来视图有关细分定义的摘要级别信息，以帮助确保隔离预期受众。 要查找使用API处理细分预览和评估的详细步 [!DNL Adobe Experience Platform Segmentation Service] 骤，请访问 [预览和评估终结点指南](../../segmentation/api/previews-and-estimates.md)(API开发人员指南 [!DNL Segmentation] 的一部分)。

