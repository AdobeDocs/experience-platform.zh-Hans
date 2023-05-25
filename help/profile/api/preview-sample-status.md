---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；预览；示例
title: 预览示例状态（配置文件预览） API端点
description: 通过Real-time Customer Profile API的预览示例状态端点，可预览配置文件数据的最新成功示例、按数据集和身份列出配置文件分发，并生成显示数据集重叠、身份重叠和未拼合配置文件的报告。
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2873'
ht-degree: 1%

---

# 预览示例状态端点（配置文件预览）

Adobe Experience Platform允许您从多个来源摄取客户数据，以便为每位客户构建强大、统一的配置文件。 当数据被摄取到Platform中时，将运行一个示例作业来更新用户档案计数和其他与实时客户档案数据相关的量度。

可以使用查看此示例作业的结果 `/previewsamplestatus` 端点，实时客户个人资料API的一部分。 此端点还可用于按数据集和身份命名空间列出配置文件分发，以及生成多个报告，以了解贵组织的配置文件存储区的组成。 本指南将介绍使用查看这些指标所需的步骤。 `/previewsamplestatus` API端点。

>[!NOTE]
>
>在Adobe Experience Platform分段服务API中提供了一些估算和预览端点，利用这些端点，可查看有关区段定义的摘要级别信息，以帮助确保隔离预期受众。 要查找使用区段预览和估计端点的详细步骤，请访问 [预览和估计端点指南](../../segmentation/api/previews-and-estimates.md)，的一部分 [!DNL Segmentation] API开发人员指南。

## 快速入门

本指南中使用的API端点是 [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). 在继续之前，请查看 [快速入门指南](getting-started.md) 有关相关文档的链接，请参阅本文档中的示例API调用指南，以及有关成功调用任何组件所需的所需标头的重要信息 [!DNL Experience Platform] API。

## 配置文件片段与合并的配置文件

本指南同时引用了“配置文件片段”和“合并的配置文件”。 在继续操作之前，请务必了解这些术语之间的差异。

每个客户配置文件都由多个配置文件片段组成，这些片段已合并以形成该客户的单一视图。 例如，如果客户跨多个渠道与您的品牌互动，则您的组织可能具有多个与该单个客户相关的配置文件片段，这些片段出现在多个数据集中。

在将配置文件片段摄取到Platform时，将它们（根据合并策略）合并在一起，以便为该客户创建单个配置文件。 因此，配置文件片段的总数可能始终大于合并的配置文件总数，因为每个配置文件都由多个片段组成。

要了解有关用户档案及其在Experience Platform中的角色的更多信息，请从阅读 [Real-time Customer Profile概述](../home.md).

## 如何触发示例作业

随着为Real-time Customer Profile启用的数据被摄取 [!DNL Platform]，它存储在配置文件数据存储中。 当将记录摄取到配置文件存储区增加或减少总配置文件计数超过5%时，将触发取样作业以更新计数。 触发示例的方式取决于所使用的摄取类型：

* 对象 **流数据工作流**，每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果有，则会自动触发示例作业以更新计数。
* 对象 **批量摄取**，在成功将批次摄取到配置文件存储区后15分钟内，如果满足5%的增加或减少阈值，则会运行作业以更新计数。 使用配置文件API，您可以预览最新成功的示例作业，以及按数据集和身份命名空间列出配置文件分发。

按命名空间量度列出的配置文件计数和配置文件也可在中找到 [!UICONTROL 配置文件] Experience PlatformUI的部分。 有关如何使用UI访问配置文件数据的信息，请访问 [[!DNL Profile] UI指南](../ui/user-guide.md).

## 查看上一个示例状态 {#view-last-sample-status}

GET您可以向 `/previewsamplestatus` 端点，用于查看为您的组织运行的最后一个成功示例作业的详细信息。 这包括示例中的配置文件总数，以及配置文件计数量度，或您的组织在Experience Platform内拥有的配置文件总数。

配置文件计数是在将多个配置文件片段合并在一起，以便为每个单独的客户形成一个配置文件后生成的。 换句话说，当配置文件片段合并在一起时，它们会返回“1”配置文件计数，因为它们都与同一个人相关。

配置文件计数还包括具有属性（记录数据）的用户档案，以及仅包含时间序列（事件）数据(如Adobe Analytics配置文件)的用户档案。 在摄取用户档案数据时，示例作业会定期刷新，以便提供平台内最新的用户档案总数。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包含为组织运行的最后一个成功示例作业的详细信息。

>[!NOTE]
>
>在此示例响应中， `numRowsToRead` 和 `totalRows` 彼此相等。 根据贵组织在Experience Platform中的用户档案数，情况可能会如此。 但是，通常这两个数字是不同的，因为 `numRowsToRead` 是较小的数字，因为它表示样本为配置文件总数的子集(`totalRows`)。

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
| `numRowsToRead` | 示例中合并的配置文件总数。 |
| `sampleJobRunning` | 返回布尔值 `true` 当示例作业正在进行时。 使批处理文件实际添加到配置文件存储区时发生的延迟透明化。 |
| `cosmosDocCount` | Cosmos中的文档总数。 |
| `totalFragmentCount` | 配置文件存储区中的配置文件片段总数。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批量摄取时间戳。 |
| `streamingDriven` | *此字段已弃用，对响应没有任何意义。* |
| `totalRows` | Experience Platform中合并的配置文件总数，也称为“配置文件计数”。 |
| `lastBatchId` | 上次批次摄取ID。 |
| `status` | 上一个示例的状态。 |
| `samplingRatio` | 已采样的合并配置文件的比率(`numRowsToRead`)到合并的配置文件总数(`totalRows`)，以小数格式表示的百分比。 |
| `mergeStrategy` | 示例中使用的合并策略。 |
| `lastSampledTimestamp` | 上一个成功的示例时间戳。 |

## 按数据集列出配置文件分发

GET要按数据集查看用户档案分布，您可以对 `/previewsamplestatus/report/dataset` 端点。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报告，则会返回该日期的最新报告。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最新的报告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下请求使用 `date` 用于返回指定日期的最新报表的参数。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括 `data` 数组，包含数据集对象的列表。 显示的响应已被截断以显示三个数据集。

>[!NOTE]
>
>如果日期存在多个报表，则仅返回最新的报表。 如果提供的日期不存在数据集报告，则会返回HTTP状态404 （未找到）。

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
| `sampleCount` | 具有此数据集ID的采样合并配置文件总数。 |
| `samplePercentage` | 此 `sampleCount` 占抽样合并配置文件总数的百分比( `numRowsToRead` 中返回的值 [上一个示例状态](#view-last-sample-status))，以十进制格式表示。 |
| `fullIDsCount` | 具有此数据集ID的合并用户档案总数。 |
| `fullIDsPercentage` | 此 `fullIDsCount` 占合并的配置文件总数的百分比( `totalRows` 中返回的值 [上一个示例状态](#view-last-sample-status))，以十进制格式表示。 |
| `name` | 数据集的名称，在数据集创建期间提供。 |
| `description` | 数据集的描述，在数据集创建期间提供。 |
| `value` | 数据集的ID。 |
| `streamingIngestionEnabled` | 是否已为数据集启用流式摄取。 |
| `createdUser` | 创建数据集的用户的用户ID。 |
| `reportTimestamp` | 报表的时间戳。 如果 `date` 参数是在请求期间提供的，返回的报告是针对提供的日期。 如果否 `date` 参数时，返回最新的报告。 |

## 按身份命名空间列出配置文件分发

GET您可以向 `/previewsamplestatus/report/namespace` 端点，用于查看按身份命名空间对配置文件存储中的所有合并配置文件进行的划分。 这包括Adobe提供的标准身份以及由贵组织定义的自定义身份。

身份命名空间是Adobe Experience Platform Identity Service的重要组成部分，充当与客户数据相关的上下文指示器。 要了解更多信息，请从阅读 [身份命名空间概述](../../identity-service/namespaces.md).

>[!NOTE]
>
>按命名空间列出的配置文件总数（将每个命名空间显示的值相加）可能高于配置文件计数量度，因为一个配置文件可能与多个命名空间关联。 例如，如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个人客户关联。

**API格式**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报告，则会返回该日期的最新报告。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下请求未指定 `date` 参数，因此将返回最新的报告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括 `data` 数组，其中单个对象包含每个命名空间的详细信息。 显示的响应已被截断以显示四个命名空间。

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
| `sampleCount` | 命名空间中采样的合并配置文件总数。 |
| `samplePercentage` | 此 `sampleCount` 占抽样合并配置文件的百分比( `numRowsToRead` 中返回的值 [上一个示例状态](#view-last-sample-status))，以十进制格式表示。 |
| `reportTimestamp` | 报表的时间戳。 如果 `date` 参数是在请求期间提供的，返回的报告是针对提供的日期。 如果否 `date` 参数时，返回最新的报告。 |
| `fullIDsFragmentCount` | 命名空间中的配置文件片段总数。 |
| `fullIDsCount` | 命名空间中合并的配置文件总数。 |
| `fullIDsPercentage` | 此 `fullIDsCount` 占合并配置文件总数的百分比( `totalRows` 中返回的值 [上一个示例状态](#view-last-sample-status))，以十进制格式表示。 |
| `code` | 此 `code` 用于命名空间。 当使用命名空间时，可以找到它 [Adobe Experience Platform Identity服务API](../../identity-service/api/list-namespaces.md) 也称为 [!UICONTROL 身份符号] 在Experience PlatformUI中。 要了解更多信息，请访问 [身份命名空间概述](../../identity-service/namespaces.md). |
| `value` | 此 `id` 命名空间的值。 当使用命名空间时，可以找到它 [身份服务API](../../identity-service/api/list-namespaces.md). |

## 生成数据集重叠报告

数据集重叠报表通过公开对可寻址受众贡献最大的数据集（合并的用户档案），提供了对组织配置文件存储构成的可见性。 除了提供数据洞察，此报表还可以帮助您采取措施优化许可证使用，如设置特定数据集的过期时间。

GET您可以通过对 `/previewsamplestatus/report/dataset/overlap` 端点。

有关分步说明，其中概述了如何使用命令行或Postman UI生成数据集重叠报告，请参阅 [生成数据集重叠报表教程](../tutorials/dataset-overlap-report.md).

**API格式**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在同一日期运行了多个报告，则会返回该日期的最新报告。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最新的报告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下请求使用 `date` 用于返回指定日期的最新报表的参数。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的请求会返回HTTP状态200 （正常）和数据集重叠报表。

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| 属性 | 描述 |
|---|---|
| `data` | 此 `data` 对象包含以逗号分隔的数据集列表及其各自的配置文件计数。 |
| `reportTimestamp` | 报表的时间戳。 如果 `date` 参数是在请求期间提供的，返回的报告是针对提供的日期。 如果否 `date` 参数时，返回最新的报告。 |

### 解释数据集重叠报表

报表的结果可以从响应中的数据集和配置文件计数中解释。 考虑以下示例报告 `data` 对象：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此报表提供以下信息：

* 共有123个配置文件，包含来自以下数据集的数据： `5d92921872831c163452edc8`， `5da7292579975918a851db57`， `5eb2cdc6fa3f9a18a7592a98`.
* 共有454,412个用户档案包含来自以下两个数据集的数据： `5d92921872831c163452edc8` 和 `5eb2cdc6fa3f9a18a7592a98`.
* 有107个配置文件仅由数据集中的数据组成 `5eeda0032af7bb19162172a7`.
* 该组织共有454,642个用户档案。

## 生成身份命名空间重叠报告 {#identity-overlap-report}

身份命名空间重叠报表通过公开对可寻址受众贡献最大的身份命名空间（合并的配置文件），提供了对贵组织配置文件存储区构成的可见性。 这包括Adobe提供的标准身份命名空间以及贵组织定义的自定义身份命名空间。

您可以通过向以下对象执行GET请求来生成身份命名空间重叠报表： `/previewsamplestatus/report/namespace/overlap` 端点。

**API格式**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在同一日期运行了多个报告，则会返回该日期的最新报告。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最新的报告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下请求使用 `date` 用于返回指定日期的最新报表的参数。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的请求会返回HTTP状态200 （正常）和身份命名空间重叠报表。

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| 属性 | 描述 |
|---|---|
| `data` | 此 `data` 对象包含以逗号分隔的列表，这些列表具有身份命名空间代码及其各自配置文件计数的唯一组合。 |
| 命名空间代码 | 此 `code` 是每个身份命名空间名称的简短形式。 每个项目的映射 `code` 到其 `name` 可使用找到 [Adobe Experience Platform Identity服务API](../../identity-service/api/list-namespaces.md). 此 `code` 也称为 [!UICONTROL 身份符号] 在Experience PlatformUI中。 要了解更多信息，请访问 [身份命名空间概述](../../identity-service/namespaces.md). |
| `reportTimestamp` | 报表的时间戳。 如果 `date` 参数是在请求期间提供的，返回的报告是针对提供的日期。 如果否 `date` 参数时，返回最新的报告。 |

### 解释身份命名空间重叠报告

可以从响应中的身份和配置文件计数解释报表的结果。 每行的数值可告知您有多少个配置文件由标准和自定义身份命名空间的精确组合组成。

考虑以下摘录自 `data` 对象：

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

此报表提供以下信息：

* 有142个配置文件包含 `AAID`， `ECID`、和 `Email` 标准身份以及来自自定义的身份 `crmid` 身份命名空间。
* 有24个配置文件包含 `AAID` 和 `ECID` 身份命名空间。
* 有6,565个配置文件仅包含 `ECID` 身份。

## 生成未拼合的用户档案报告

您可以通过未拼合的用户档案报表进一步了解组织用户档案存储区的构成。 “未拼合”配置文件是仅包含一个配置文件片段的配置文件。 “未知”配置文件是与假名身份命名空间关联的配置文件，例如 `ECID` 和 `AAID`. 未知配置文件处于非活动状态，这意味着它们在指定的时间段内未添加新事件。 未拼合的用户档案报表提供了7、30、60、90和120天的用户档案细目。

您可以通过对执行GET请求来生成未拼接的用户档案报表 `/previewsamplestatus/report/unstitchedProfiles` 端点。

**API格式**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**请求**

以下请求返回未拼合的用户档案报表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的请求会返回HTTP状态200 （正常）和未拼合的用户档案报表。

>[!NOTE]
>
>出于本指南的目的，报告已被截断为仅包含 `"120days"` 和&quot;`7days`“时段。 完整的未拼合用户档案报表提供了7、30、60、90和120天的用户档案细目。

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| 属性 | 描述 |
|---|---|
| `data` | 此 `data` 对象包含为未拼合的用户档案报告返回的信息。 |
| `totalNumberOfProfiles` | 配置文件存储区中的独特配置文件总数。 这相当于可寻址受众计数。 它包括已知和未拼接的用户档案。 |
| `totalNumberOfEvents` | 配置文件存储区中的ExperienceEvents总数。 |
| `unstitchedProfiles` | 一个对象，其中包含按时间段划分的未拼接用户档案。 未拼合的用户档案报表提供了7、30、60、90和120天时间段的用户档案细目。 |
| `countOfProfiles` | 时间段内未拼接配置文件的计数或命名空间未拼接配置文件的计数。 |
| `eventsAssociated` | 时间范围的ExperienceEvents数或命名空间的事件数。 |
| `nsDistribution` | 一个对象，其中包含各个身份命名空间，每个命名空间均分配有未拼接的用户档案和事件。 注意：将合计合计 `countOfProfiles` 中每个身份命名空间 `nsDistribution` 对象等于 `countOfProfiles` 时间段。 同样的情况也适用于 `eventsAssociated` 每个命名空间和总计 `eventsAssociated` 每个时段。 |
| `reportTimestamp` | 报表的时间戳。 |

### 解释未拼合的用户档案报告

该报告的结果可以让您深入了解您的组织在其配置文件存储区中有多少个未拼合的和不活动的配置文件。

考虑以下摘录自 `data` 对象：

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

此报表提供以下信息：

* 有1,782个配置文件仅包含一个配置文件片段，并且过去7天中没有新事件。
* 有29,151个ExperienceEvents与1,782个未拼接的用户档案关联。
* 有1,734个未拼接的用户档案，其中包含来自ECID身份命名空间的单个用户档案片段。
* 有28,591个事件与1,734个未拼接配置文件关联，这些配置文件包含来自ECID身份命名空间的单个配置文件片段。

## 后续步骤

现在，您已了解如何在配置文件存储中预览样本数据并对数据运行多个报告，您还可以使用分段服务API的估计和预览端点来查看有关区段定义的摘要级别信息。 此信息有助于确保隔离区段中的预期受众。 要了解有关使用分段API处理区段预览和估计的更多信息，请访问 [预览和评估端点指南](../../segmentation/api/previews-and-estimates.md).

