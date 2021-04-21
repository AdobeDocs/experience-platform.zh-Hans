---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API;预览；示例
title: 预览示例状态(用户档案预览)API端点
description: 使用预览示例状态端点(实时客户用户档案API的一部分)，您可以预览最新成功的用户档案数据示例，以及按数据集和Adobe Experience Platform内的身份命名空间按列表用户档案分发。
topic-legacy: guide
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1652'
ht-degree: 1%

---

# 预览示例状态端点(用户档案预览)

Adobe Experience Platform使您能够从多个来源收集客户数据，从而为各个客户构建强大的统一用户档案。 当为实时客户用户档案启用的数据被引入[!DNL Platform]时，它存储在用户档案数据存储中。

当将记录引入用户档案存储中时，将总用户档案计数增加或减少5%以上时，将触发采样作业以更新该计数。 触发样本的方式取决于所使用的摄取类型：

* 对于&#x200B;**流数据工作流**，每小时检查以确定是否达到5%增加或减少阈值。 如果已触发，则会自动触发示例作业以更新计数。
* 对于&#x200B;**批处理摄取**，在成功将批处理摄取到用户档案存储区的15分钟内，如果达到5%增加或减少阈值，则运行作业以更新计数。 使用用户档案 API，您可以预览最新成功的示例作业，以及按数据集和身份命名空间列表用户档案分发。

这些量度也可在Experience Platform UI的[!UICONTROL Profiles]部分中使用。 有关如何使用UI访问用户档案数据的信息，请访问[[!DNL Profile] 用户指南](../ui/user-guide.md)。

>[!NOTE]
>
>Adobe Experience Platform分段服务API中提供了一些估计和预览端点，允许您视图有关区段定义的摘要级别信息，以帮助确保隔离预期受众。 要查找使用区段预览和估计端点的详细步骤，请访问[预览和估计端点指南](../../segmentation/api/previews-and-estimates.md)（[!DNL Segmentation] API开发人员指南的一部分）。

## 入门指南

本指南中使用的API端点是[[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en)的一部分。 在继续之前，请查阅[快速入门指南](getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南以及成功调用任何[!DNL Experience Platform] API所需标头的重要信息。

## 用户档案片段与合并用户档案

本指南同时引用“用户档案片段”和“合并用户档案”。 在继续之前，必须了解这些术语之间的差异。

每个客户用户档案都由多个用户档案片段组成，这些片段已合并，以形成该客户的单个视图。 例如，如果一个渠道跨多个用户档案与您的品牌互动，则您的组织将在多个数据集中显示与该单个客户相关的多个片段。 当这些片段被引入平台时，它们会合并在一起（基于合并策略），以便为该客户创建单一用户档案。 因此，用户档案片段的总数可能始终高于合并用户档案的总数，因为每个用户档案由多个片段组成。

## 视图上次示例状态{#view-last-sample-status}

您可以向`/previewsamplestatus`端点执行GET请求，以视图为IMS组织运行的上次成功示例作业的详细信息。 这包括示例中的用户档案总数，以及用户档案计数量度，或您的组织在Experience Platform中拥有的用户档案总数。 用户档案计数在合并用户档案片段后生成，以便为每个单独的客户形成单个用户档案。 换句话说，您的组织可能有多个用户档案片段与跨不同渠道与您的品牌进行交互的单个客户相关，但这些片段将合并在一起（根据默认合并策略），并将返回“1”个用户档案计数，因为它们都与同一个人相关。

用户档案计数还包括具有属性（记录数据）的用户档案和仅包含时间序列(事件)数据的用户档案，如Adobe Analytics用户档案。 在摄取用户档案数据时，将定期刷新示例作业，以便在平台内提供最新的用户档案总数。

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

响应包括为IMS组织运行的上次成功示例作业的详细信息。

>[!NOTE]
>
>在此示例响应中，`numRowsToRead`和`totalRows`彼此相等。 根据您的组织在Experience Platform中拥有的用户档案数，情况可能是这样。 但是，这两个数字通常不同，`numRowsToRead`是较小的数字，因为它将样本表示为用户档案总数(`totalRows`)的子集。

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
| `numRowsToRead` | 样本中合并用户档案的总数。 |
| `sampleJobRunning` | 一个布尔值，当示例作业正在进行时返回`true`。 为从批处理文件上传到实际添加到用户档案存储时的延迟提供透明度。 |
| `cosmosDocCount` | Cosmos中的文档总数。 |
| `totalFragmentCount` | 用户档案存储中的用户档案片段总数。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批摄取时间戳。 |
| `streamingDriven` | *此字段已弃用，且不包含对响应的重要性。* |
| `totalRows` | Experience Platform中合并用户档案的总数，也称为“用户档案计数”。 |
| `lastBatchId` | 上次批量摄取ID。 |
| `status` | 上一个示例的状态。 |
| `samplingRatio` | 采样的合并用户档案(`numRowsToRead`)与合并用户档案(`totalRows`)的比率，以小数格式表示为百分比。 |
| `mergeStrategy` | 示例中使用的合并策略。 |
| `lastSampledTimestamp` | 上次成功的示例时间戳。 |

## 列表用户档案分布（按数据集）

要按用户档案集查看GET分布，可以向`/previewsamplestatus/report/dataset`端点执行请求。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报表，则将返回该日期的最新报表。 如果在指定日期不存在报表，则将返回404错误。 如果未指定日期，则将返回最近的报表。 格式：YYYY-MM-DD。 示例: `date=2024-12-31` |

**请求**

以下请求使用`date`参数返回指定日期的最新报表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括`data`数组，其中包含数据集对象的列表。 显示的响应已截断，以显示三个数据集。

>[!NOTE]
>
>如果该日期存在多个报表，则只返回最新的报表。 如果提供的日期不存在数据集报告，则将返回“HTTP状态404（未找到）”。

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
| `sampleCount` | 使用此数据集ID的采样合并用户档案总数。 |
| `samplePercentage` | `sampleCount`作为采样合并用户档案总数的百分比（在[最后一个采样状态](#view-last-sample-status)中返回的`numRowsToRead`值），以十进制格式表示。 |
| `fullIDsCount` | 具有此用户档案集ID的合并数据集总数。 |
| `fullIDsPercentage` | `fullIDsCount`作为合并用户档案总数的百分比（在[最后一个示例状态](#view-last-sample-status)中返回的`totalRows`值），以十进制格式表示。 |
| `name` | 数据集的名称，在创建数据集时提供。 |
| `description` | 数据集的描述，在创建数据集时提供。 |
| `value` | 数据集的ID。 |
| `streamingIngestionEnabled` | 是否启用了数据集以进行流摄取。 |
| `createdUser` | 创建数据集的用户的用户ID。 |
| `reportTimestamp` | 报表的时间戳。 如果在请求期间提供了`date`参数，则返回的报表为提供的日期。 如果未提供`date`参数，则返回最近的报告。 |

## 列表用户档案按命名空间分发

您可以对`/previewsamplestatus/report/namespace`端点执行GET请求，以在用户档案存储中的所有合并用户档案上按标识命名空间视图划分。 身份命名空间是Adobe Experience Platform Identity Service的一个重要组件，可作为与客户数据相关的上下文的指示器。 要了解更多信息，请访问[标识命名空间概述](../../identity-service/namespaces.md)。

>[!NOTE]
>
>按命名空间划分的用户档案总数(将每个命名空间显示的值相加)将始终高于用户档案计数量度，因为一个用户档案可能与多个命名空间关联。 例如，如果一个客户在多个渠道上与您的品牌互动，则多个命名空间将与该个别客户关联。

**API格式**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报表，则将返回该日期的最新报表。 如果在指定日期不存在报表，则将返回404错误。 如果未指定日期，则将返回最近的报表。 格式：YYYY-MM-DD。 示例: `date=2024-12-31` |

**请求**

以下请求未指定`date`参数，因此将返回最近的报告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括`data`数组，其中各个对象包含每个命名空间的详细信息。 显示的响应已截断，显示四个命名空间。

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
| `sampleCount` | 命名空间中采样合并用户档案的总数。 |
| `samplePercentage` | `sampleCount`作为采样合并用户档案的百分比（在[最后一个采样状态](#view-last-sample-status)中返回的`numRowsToRead`值），以十进制格式表示。 |
| `reportTimestamp` | 报表的时间戳。 如果在请求期间提供了`date`参数，则返回的报表为提供的日期。 如果未提供`date`参数，则返回最近的报告。 |
| `fullIDsFragmentCount` | 命名空间中的用户档案片段总数。 |
| `fullIDsCount` | 命名空间中的合并用户档案总数。 |
| `fullIDsPercentage` | `fullIDsCount`作为合并用户档案总数的百分比（在[最后一个示例状态](#view-last-sample-status)中返回的`totalRows`值），以十进制格式表示。 |
| `code` | 该命名空间的`code`。 这在使用[Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md)处理命名空间时可找到，在Experience PlatformUI中也称为[!UICONTROL Identity symbol]。 要了解更多信息，请访问[标识命名空间概述](../../identity-service/namespaces.md)。 |
| `value` | 命名空间的`id`值。 使用[Identity Service API](../../identity-service/api/list-namespaces.md)处理命名空间时，可以找到这一点。 |

## 后续步骤

现在，您知道如何在用户档案存储中预览样本数据，还可以使用分段服务API的估计和预览端点来视图有关区段定义的摘要级信息。 此信息有助于确保您隔离区段中的预期受众。 要了解有关使用分段API处理区段预览和估计的更多信息，请访问[预览和估计终结点指南](../../segmentation/api/previews-and-estimates.md)。
