---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；预览；示例
title: 预览示例状态（配置文件预览）API端点
description: 使用预览示例状态端点（实时客户配置文件API的一部分），您可以预览配置文件数据的最新成功示例、按数据集和身份列出配置文件分发，以及生成显示数据集重叠、身份重叠和未知配置文件的报表。
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2882'
ht-degree: 1%

---

# 预览示例状态端点（配置文件预览）

Adobe Experience Platform允许您从多个来源摄取客户数据，以便为每个单独的客户构建一个强大、统一的配置文件。 将数据摄取到Platform后，将运行一个示例作业以更新用户档案计数和其他与实时客户档案数据相关的量度。

可以使用 `/previewsamplestatus` 端点，实时客户配置文件API的一部分。 此端点还可用于按数据集和身份命名空间列出配置文件分配，以及生成多个报表，以便查看您组织的配置文件存储的组成。 本指南将逐步介绍使用 `/previewsamplestatus` API端点。

>[!NOTE]
>
>Adobe Experience Platform Segmentation Service API提供了一些可用的预估和预览端点，通过这些端点可以查看有关区段定义的摘要级别信息，以帮助确保隔离预期受众。 要查找有关使用区段预览和评估端点的详细步骤，请访问 [预览和估计端点指南](../../segmentation/api/previews-and-estimates.md), [!DNL Segmentation] API开发人员指南。

## 快速入门

本指南中使用的API端点是 [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). 在继续之前，请查看 [入门指南](getting-started.md) 有关相关文档的链接、本文档中的API调用示例指南，以及有关成功调用任何代码所需标头的重要信息 [!DNL Experience Platform] API。

## 配置文件片段与合并的配置文件

本指南同时引用“配置文件片段”和“合并的配置文件”。 在继续操作之前，务必要了解这些术语之间的差异。

每个客户配置文件都由多个配置文件片段组成，这些片段已合并，以形成该客户的单一视图。 例如，如果客户跨多个渠道与您的品牌进行交互，则贵组织可能在多个数据集中显示与该单个客户相关的多个配置文件片段。

将配置文件片段摄取到Platform后，它们会合并在一起（基于合并策略），以便为该客户创建单个配置文件。 因此，由于每个配置文件都由多个片段组成，因此配置文件片段的总数可能始终高于合并的配置文件的总数。

要进一步了解用户档案及其在Experience Platform中的角色，请首先阅读 [实时客户资料概述](../home.md).

## 示例作业的触发方式

由于实时客户资料启用的数据会被摄取到 [!DNL Platform]，则会存储在配置文件数据存储中。 当将记录摄取到用户档案存储区时，如果用户档案总计数增加或减少5%以上，则会触发取样作业以更新计数。 触发示例的方式取决于所使用的摄取类型：

* 对于 **流式数据工作流**，则会每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果已执行此操作，则会自动触发示例作业以更新计数。
* 对于 **批量摄取**，在成功将批处理摄取到用户档案存储的15分钟内，如果满足5%的增加或减少阈值，则会运行一个作业以更新计数。 使用配置文件API，您可以预览最新成功的示例作业，以及按数据集和身份命名空间列出配置文件分发。

在 [!UICONTROL 用户档案] Experience PlatformUI的部分。 有关如何使用UI访问用户档案数据的信息，请访问 [[!DNL Profile] UI指南](../ui/user-guide.md).

## 查看最后一个示例状态 {#view-last-sample-status}

您可以对 `/previewsamplestatus` 端点来查看为IMS组织运行的上一个成功示例作业的详细信息。 这包括示例中的用户档案总数，以及用户档案计数量度，或您的组织在Experience Platform中拥有的用户档案总数。

将配置文件片段合并到一起后，会生成配置文件计数，以便为每个单独的客户形成一个配置文件。 换言之，当配置文件片段合并在一起时，它们会返回“1”个配置文件的计数，因为它们都与同一个人相关。

用户档案计数还包含具有属性（记录数据）的用户档案，以及仅包含时间系列（事件）数据的用户档案，如Adobe Analytics用户档案。 在摄取用户档案数据时，将定期刷新示例作业，以便在Platform中提供最新的用户档案总数。

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
>在此示例响应中， `numRowsToRead` 和 `totalRows` 彼此相等。 根据贵组织在Experience Platform中拥有的用户档案数，情况可能如此。 但是，通常这两个数字是不同的， `numRowsToRead` 数字越小，因为它表示示例是用户档案总数的子集(`totalRows`)。

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
| `numRowsToRead` | 示例中合并的用户档案总数。 |
| `sampleJobRunning` | 返回的布尔值 `true` 正在进行示例作业时。 为从上传批处理文件到将其实际添加到配置文件存储区的延迟提供透明度。 |
| `cosmosDocCount` | Cosmos中的文档总计数。 |
| `totalFragmentCount` | 配置文件存储中的配置文件片段总数。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批量摄取时间戳。 |
| `streamingDriven` | *此字段已弃用，且不包含对响应的显着性。* |
| `totalRows` | Experience Platform中合并的用户档案总数，也称为“用户档案计数”。 |
| `lastBatchId` | 上次批量摄取ID。 |
| `status` | 最后一个示例的状态。 |
| `samplingRatio` | 采样的合并用户档案的比率(`numRowsToRead`)到合并用户档案总数(`totalRows`)，以小数格式以百分比表示。 |
| `mergeStrategy` | 示例中使用的合并策略。 |
| `lastSampledTimestamp` | 上次成功的示例时间戳。 |

## 按数据集列出配置文件分发

要按GET集查看用户档案的分布，您可以向 `/previewsamplestatus/report/dataset` 端点。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报表，则会返回该日期的最新报表。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报表。 格式：YYYY-MM-DD。 示例: `date=2024-12-31` |

**请求**

以下请求使用 `date` 参数来返回指定日期的最新报表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括 `data` 数组，包含数据集对象列表。 显示的响应已被截断，以显示三个数据集。

>[!NOTE]
>
>如果日期存在多个报表，则只会返回最新的报表。 如果提供的日期不存在数据集报表，则会返回“HTTP状态404（未找到）”。

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
| `samplePercentage` | 的 `sampleCount` 按采样合并用户档案总数的百分比( `numRowsToRead` 值 [上次示例状态](#view-last-sample-status))，以小数格式表示。 |
| `fullIDsCount` | 具有此数据集ID的合并用户档案总数。 |
| `fullIDsPercentage` | 的 `fullIDsCount` 合并用户档案总数( `totalRows` 值 [上次示例状态](#view-last-sample-status))，以小数格式表示。 |
| `name` | 数据集的名称，在数据集创建期间提供。 |
| `description` | 数据集的描述，在数据集创建期间提供。 |
| `value` | 数据集的ID。 |
| `streamingIngestionEnabled` | 是否为流摄取启用了数据集。 |
| `createdUser` | 创建数据集的用户的用户ID。 |
| `reportTimestamp` | 报表的时间戳。 如果 `date` 参数，则返回的报表为提供的日期。 如果否 `date` 参数时，将返回最新的报表。 |

## 按身份命名空间列出配置文件分发

您可以对 `/previewsamplestatus/report/namespace` 端点来查看“配置文件存储”中所有合并配置文件中按身份命名空间划分的内容。 这包括由Adobe提供的标准身份以及由您的组织定义的自定义身份。

身份命名空间是Adobe Experience Platform Identity Service的重要组件，充当与客户数据相关的上下文指示器。 要了解更多信息，请首先阅读 [身份命名空间概述](../../identity-service/namespaces.md).

>[!NOTE]
>
>按命名空间划分的配置文件总数（将每个命名空间显示的值相加）可能高于配置文件计数量度，因为一个配置文件可能与多个命名空间关联。 例如，如果客户在多个渠道上与您的品牌进行交互，则多个命名空间将与该个别客户关联。

**API格式**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报表，则会返回该日期的最新报表。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报表。 格式：YYYY-MM-DD。 示例: `date=2024-12-31` |

**请求**

以下请求未指定 `date` 参数和将因此返回最新的报表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括 `data` 数组，其中各个对象包含每个命名空间的详细信息。 显示的响应已被截断为显示四个命名空间。

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
| `sampleCount` | 命名空间中取样的合并配置文件总数。 |
| `samplePercentage` | 的 `sampleCount` 按采样合并用户档案的百分比( `numRowsToRead` 值 [上次示例状态](#view-last-sample-status))，以小数格式表示。 |
| `reportTimestamp` | 报表的时间戳。 如果 `date` 参数，则返回的报表为提供的日期。 如果否 `date` 参数时，将返回最新的报表。 |
| `fullIDsFragmentCount` | 命名空间中的配置文件片段总数。 |
| `fullIDsCount` | 命名空间中合并的配置文件总数。 |
| `fullIDsPercentage` | 的 `fullIDsCount` 合并用户档案总数的百分比( `totalRows` 值 [上次示例状态](#view-last-sample-status))，以小数格式表示。 |
| `code` | 的 `code` 的子域。 使用命名空间时，可以找到该值 [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md) 和也称为 [!UICONTROL 身份符号] 在Experience PlatformUI中。 要了解更多信息，请访问 [身份命名空间概述](../../identity-service/namespaces.md). |
| `value` | 的 `id` 值。 使用命名空间时，可以找到该值 [Identity Service API](../../identity-service/api/list-namespaces.md). |

## 生成数据集重叠报表

数据集重叠报表通过公开对可寻址受众（合并的配置文件）贡献最大的数据集，可以显示贵组织的配置文件存储的构成。 除了提供对数据的分析之外，此报表还可以帮助您采取措施来优化许可证使用情况，例如为某些数据集设置TTL。

您可以通过向 `/previewsamplestatus/report/dataset/overlap` 端点。

有关如何使用命令行或Postman UI生成数据集重叠报表的分步说明，请参阅 [生成数据集重叠报表教程](../tutorials/dataset-overlap-report.md).

**API格式**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在同一日期运行多个报表，则会返回该日期的最新报表。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报表。 格式：YYYY-MM-DD。 示例: `date=2024-12-31` |

**请求**

以下请求使用 `date` 参数来返回指定日期的最新报表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的请求会返回“HTTP状态200（确定）”和数据集重叠报表。

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
| `data` | 的 `data` 对象包含以逗号分隔的数据集列表及其各自的配置文件计数。 |
| `reportTimestamp` | 报表的时间戳。 如果 `date` 参数，则返回的报表为提供的日期。 如果否 `date` 参数时，将返回最新的报表。 |

### 解释数据集重叠报表

可以从响应中的数据集和用户档案计数来解释报表结果。 请考虑以下示例报表 `data` 对象：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此报表提供以下信息：

* 共有123个用户档案，其中包含来自以下数据集的数据： `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* 共有454,412个用户档案，包含来自以下两个数据集的数据： `5d92921872831c163452edc8` 和 `5eb2cdc6fa3f9a18a7592a98`.
* 有107个配置文件只包含来自数据集的数据 `5eeda0032af7bb19162172a7`.
* 组织共有454,642个用户档案。

## 生成身份命名空间重叠报表

身份命名空间重叠报表通过公开对可寻址受众（合并的配置文件）贡献最大的身份命名空间，来提供对贵组织配置文件存储区构成的可见性。 这包括由Adobe提供的标准身份命名空间，以及由您的组织定义的自定义身份命名空间。

您可以通过执行对 `/previewsamplestatus/report/namespace/overlap` 端点。

**API格式**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在同一日期运行多个报表，则会返回该日期的最新报表。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报表。 格式：YYYY-MM-DD。 示例: `date=2024-12-31` |

**请求**

以下请求使用 `date` 参数来返回指定日期的最新报表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的请求会返回HTTP状态200（确定）和身份命名空间重叠报表。

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
| `data` | 的 `data` 对象包含以逗号分隔的列表，其中包含身份命名空间代码及其相应配置文件计数的唯一组合。 |
| 命名空间代码 | 的 `code` 是每个身份命名空间名称的短格式。 每个 `code` 到 `name` 可以使用 [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md). 的 `code` 也称为 [!UICONTROL 身份符号] 在Experience PlatformUI中。 要了解更多信息，请访问 [身份命名空间概述](../../identity-service/namespaces.md). |
| `reportTimestamp` | 报表的时间戳。 如果 `date` 参数，则返回的报表为提供的日期。 如果否 `date` 参数时，将返回最新的报表。 |

### 解释身份命名空间重叠报表

报告的结果可以从响应中的标识和用户档案计数来解释。 每行的数字值可告知您有多少个配置文件由标准和自定义身份命名空间的确切组合组成。

请考虑以下摘自 `data` 对象：

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

此报表提供以下信息：

* 共有142个用户档案，由 `AAID`, `ECID`和 `Email` 标准身份，以及来自自定义 `crmid` 身份命名空间。
* 共有24个用户档案，其中 `AAID` 和 `ECID` 身份命名空间。
* 有6,565个用户档案仅包含 `ECID` 身份。

## 生成未知的用户档案报告

您可以通过未知的用户档案报表进一步了解贵组织的用户档案存储的构成。 “未知配置文件”是指在给定时间段内未拼合和不活动的任何配置文件。 “未拼合”配置文件是只包含一个配置文件片段的配置文件，而“不活动”配置文件是指在指定时间段内未添加新事件的任何配置文件。 未知用户档案报表提供7、30、60、90和120天的用户档案细目。

您可以通过向执行GET请求来生成未知的用户档案报告 `/previewsamplestatus/report/unknownProfiles` 端点。

**API格式**

```http
GET /previewsamplestatus/report/unknownProfiles
```

**请求**

以下请求会返回未知的用户档案报表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unknownProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的请求会返回HTTP状态200（确定）和未知的用户档案报告。

>[!NOTE]
>
>就本指南而言，报表已被截断为仅包含 `"120days"` 和&quot;`7days`“时间段”。 完整的未知用户档案报表提供7、30、60、90和120天的用户档案细目。

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unknownProfiles": {
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
| `data` | 的 `data` 对象包含为未知用户档案报告返回的信息。 |
| `totalNumberOfProfiles` | 配置文件存储区中独特配置文件的总数。 这等同于可寻址受众计数。 它包括已知和未知的用户档案。 |
| `totalNumberOfEvents` | 配置文件存储中的ExperienceEvents总数。 |
| `unknownProfiles` | 包含按时间段划分未知用户档案（未拼合和不活动）的对象。 “未知用户档案”报表提供7天、30天、60天、90天和120天时间段的用户档案细目。 |
| `countOfProfiles` | 时间段内未知配置文件的计数或命名空间中未知配置文件的计数。 |
| `eventsAssociated` | 时间范围的ExperienceEvents数量或命名空间的事件数。 |
| `nsDistribution` | 一个对象，其中包含单个身份命名空间以及每个命名空间的未知配置文件和事件的分布。 注意：合计总计 `countOfProfiles` (对于 `nsDistribution` 对象等于 `countOfProfiles` 在时间段内。 同样的情况也适用于 `eventsAssociated` 每个命名空间和总计 `eventsAssociated` 每个时段。 |
| `reportTimestamp` | 报表的时间戳。 |

### 解释未知用户档案报表

报表结果可以让您分析贵组织在其配置文件存储区中拥有多少个未拼合和非活动的配置文件。

请考虑以下摘自 `data` 对象：

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

* 有1,782个用户档案，其中仅包含一个用户档案片段，且过去七天内没有新事件。
* 有29,151个ExperienceEvent与1,782个未知用户档案关联。
* 有1,734个未知配置文件，其中包含ECID标识命名空间中的单个配置文件片段。
* 有28,591个事件与1,734个未知配置文件关联，这些未知配置文件包含ECID标识命名空间中的单个配置文件片段。

## 后续步骤

现在，您已了解如何在配置文件存储中预览示例数据并运行有关数据的多个报表，接下来还可以使用分段服务API的估计和预览端点来查看有关区段定义的摘要级别信息。 此信息有助于确保隔离区段中的预期受众。 要了解有关使用分段API进行区段预览和评估的更多信息，请访问 [预览和评估端点指南](../../segmentation/api/previews-and-estimates.md).

