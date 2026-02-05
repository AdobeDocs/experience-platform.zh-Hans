---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API；预览；示例
title: 预览示例状态（配置文件预览） API端点
description: 实时客户个人资料API的预览示例状态端点允许您预览个人资料数据的最新成功示例，按数据集和身份列出个人资料分发，并生成显示数据集重叠、身份重叠和未拼接个人资料的报告。
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 399b76f260732015f691fd199c977d6f7e772b01
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 1%

---

# 预览示例状态端点（配置文件预览）

Adobe Experience Platform允许您从多个来源摄取客户数据，以便为每位客户构建强大、统一的配置文件。 当数据被摄取到Experience Platform中时，将运行示例作业以更新用户档案计数和其他实时客户档案数据相关量度。

此示例作业的结果可以使用实时客户个人资料API的`/previewsamplestatus`端点进行查看。 此端点还可用于同时按数据集和身份命名空间列出配置文件分发，以及生成多个报告，以了解您组织的配置文件存储的组成。 本指南将介绍使用`/previewsamplestatus` API端点查看这些量度所需的步骤。

>[!NOTE]
>
>在Adobe Experience Platform分段服务API中提供了一些估计和预览端点，通过这些端点可查看有关区段定义的摘要级别信息，从而帮助您隔离预期的受众。 要查找使用预览和估计端点的详细步骤，请访问[预览和估计端点指南](../../segmentation/api/previews-and-estimates.md)，它是[!DNL Segmentation] API开发人员指南的一部分。

## 快速入门

本指南中使用的API端点是[[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en)的一部分。 在继续之前，请查看[快速入门指南](getting-started.md)，以获取相关文档的链接、此文档中示例API调用的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需的所需标头的重要信息。

## 配置文件片段与合并的配置文件

本指南参考了“配置文件片段”和“合并的配置文件”。 在继续操作之前，请务必了解这些术语之间的差异。

每个单独的客户配置文件都由多个配置文件片段组成，这些片段已合并以形成该客户的单一视图。 例如，如果客户跨多个渠道与您的品牌互动，则您的组织可能具有多个与出现在多个数据集中的单个客户相关的配置文件片段。

将配置文件片段摄取到Experience Platform后，它们会合并在一起（根据合并策略），以便为该客户创建单个配置文件。 因此，配置文件片段的总数可能始终大于合并的配置文件总数，因为每个配置文件都由多个片段组成。

要了解有关配置文件及其在Experience Platform中的角色的更多信息，请先阅读[实时客户配置文件概述](../home.md)。

## 如何触发示例作业

启用实时客户资料的数据被摄取到[!DNL Experience Platform]后，将存储在资料数据存储中。 当将记录摄取到配置文件存储中增加或减少总配置文件计数超过3%时，将触发取样作业以更新计数。 触发示例的方式取决于所使用的摄取类型：

* 对于&#x200B;**流式数据工作流**，每小时进行一次检查，以确定是否已达到3%的增加或减少阈值。 如果有，则会自动触发示例作业以更新计数。
* 对于&#x200B;**批次摄取**，在成功将批次摄取到配置文件存储区后15分钟内，如果达到3%的增加或减少阈值，则会运行作业以更新计数。 使用配置文件API，您可以预览最新成功的示例作业，以及按数据集和身份命名空间列出配置文件分发。

Experience Platform UI的[!UICONTROL Profiles]部分中也提供了按命名空间量度列出的配置文件计数和配置文件。 有关如何使用UI访问配置文件数据的信息，请访问[[!DNL Profile] UI指南](../ui/user-guide.md)。

## 查看上一个示例状态 {#view-last-sample-status}

通过向`/previewsamplestatus`端点发出GET请求，可查看为您的组织运行的上一个成功示例作业的详细信息。 此报表包括示例中的配置文件总数，以及配置文件计数量度，或您的组织在Experience Platform中拥有的配置文件总数。

配置文件计数是在将多个配置文件片段合并在一起，为每个单独的客户形成一个配置文件后生成的。 换言之，当配置文件片段合并在一起时，它们会返回“1”配置文件计数，因为它们都与同一个人相关。

配置文件计数还包括具有属性（记录数据）的用户档案，以及仅包含时间序列（事件）数据(如Adobe Analytics配置文件)的用户档案。 样本作业在摄取用户档案数据时定期刷新，以便在Experience Platform中提供最新的用户档案总数。

**API格式**

```http
GET /previewsamplestatus
```

**请求**

+++ 查看上一个示例状态的示例请求。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**响应**

成功响应会返回HTTP状态200，并包含为组织运行的最后一个成功示例作业的详细信息。

+++ 包含最后一个示例状态的示例响应。

>[!NOTE]
>
>在此示例响应中，`numRowsToRead`和`totalRows`彼此相等。 根据贵组织在Experience Platform中的配置文件数，可能会出现这种情况。 但是，通常这两个数字是不同的，`numRowsToRead`是较小的数字，因为它表示样本为配置文件总数(`totalRows`)的子集。

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "docCount": "\"300803\"",
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
| -------- | ----------- |
| `numRowsToRead` | 示例中合并的配置文件总数。 |
| `sampleJobRunning` | 一个布尔值，当示例作业正在进行时返回`true`。 将批处理文件实际添加到配置文件存储区后，可以透明地反映将文件上传到时发生的延迟。 |
| `docCount` | 数据库中的文档总数。 |
| `totalFragmentCount` | 配置文件存储中的配置文件片段总数。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批次摄取时间戳。 |
| `streamingDriven` | *此字段已弃用，对响应没有意义。* |
| `totalRows` | Experience Platform中合并的用户档案总数，也称为用户档案计数。 |
| `lastBatchId` | 上次批次摄取ID。 |
| `status` | 上一个示例的状态。 |
| `samplingRatio` | 采样的合并配置文件(`numRowsToRead`)与合并配置文件总数(`totalRows`)的比率，以小数格式表示。 |
| `mergeStrategy` | 示例中使用的合并策略。 |
| `lastSampledTimestamp` | 上次成功的示例时间戳。 |

+++

## 按数据集列出配置文件分发

您可以通过向`/previewsamplestatus/report/dataset`端点发出GET请求来按数据集查看用户档案的分布。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 查询参数 | 描述 | 示例 |
| --------------- | ----------- | ------- |
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报告，则返回该日期的最新报告。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报告。 格式：YYYY-MM-DD。 | `date=2024-12-31` |

**请求**

以下请求使用`date`参数返回指定日期的最新报告。

+++ 按数据集检索用户档案分布的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**响应**

>[!NOTE]
>
>如果该日期存在多个报表，则仅返回最新的报表。 如果提供的日期不存在数据集报告，则会返回HTTP状态404 （未找到）。

成功的响应返回HTTP状态200，并包含包含包含数据集对象列表的`data`数组。

+++ 包含最新数据集对象的示例响应。

>[!NOTE]
>
>以下显示的响应已被截断以显示三个数据集。

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
| -------- | ----------- |
| `sampleCount` | 具有此数据集ID的采样合并用户档案总数。 |
| `samplePercentage` | 以小数格式表示的`sampleCount`占抽样合并配置文件总数的百分比（在`numRowsToRead`上次采样状态[中返回的](#view-last-sample-status)值）。 |
| `fullIDsCount` | 具有此数据集ID的合并用户档案总数。 |
| `fullIDsPercentage` | `fullIDsCount`占合并配置文件总数的百分比（在`totalRows`上次采样状态[中返回的](#view-last-sample-status)值），以小数格式表示。 |
| `name` | 数据集的名称，在数据集创建期间提供。 |
| `description` | 数据集的描述，在数据集创建期间提供。 |
| `value` | 数据集的ID。 |
| `streamingIngestionEnabled` | 是否已为数据集启用流式摄取。 |
| `createdUser` | 创建数据集的用户的用户ID。 |
| `reportTimestamp` | 报表的时间戳。 如果在请求期间提供了`date`参数，则返回的报告将对应于提供的日期。 如果未提供`date`参数，则返回最新报告。 |

+++

## 按身份命名空间列出配置文件分发

您可以对`/previewsamplestatus/report/namespace`端点执行GET请求，以查看按身份命名空间对配置文件存储中所有合并配置文件的细分。 这包括Adobe提供的标准身份以及由您的组织定义的自定义身份。

身份命名空间是Adobe Experience Platform Identity Service的重要组成部分，充当与客户数据相关的上下文指示器。 要了解更多信息，请先阅读[身份命名空间概述](../../identity-service/features/namespaces.md)。

>[!NOTE]
>
>按命名空间列出的配置文件总数（将每个命名空间显示的值相加）可能高于配置文件计数量度，因为一个配置文件可能与多个命名空间关联。 例如，如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个人客户关联。

**API格式**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 查询参数 | 描述 | 示例 |
| --------------- | ----------- | ------- |
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报告，则返回该日期的最新报告。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报告。 格式： `YYYY-MM-DD`。 | `date=2025-6-20` |

**请求**

以下请求未指定`date`参数，将返回最新报告。

+++ 返回按命名空间列出的配置文件分发的最新报告的示例请求。 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**响应**

成功的响应返回HTTP状态200并包含`data`数组，其中各个对象包含每个命名空间的详细信息。 显示的响应已被截断以显示四个命名空间。

+++ 示例响应包含有关按命名空间列出的配置文件分布的信息。

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
| -------- | ----------- |
| `sampleCount` | 命名空间中采样的合并配置文件总数。 |
| `samplePercentage` | `sampleCount`以采样合并配置文件的百分比表示（在`numRowsToRead`上次采样状态[中返回的](#view-last-sample-status)值），以十进制格式表示。 |
| `reportTimestamp` | 报表的时间戳。 如果在请求期间提供了`date`参数，则返回的报告将对应于提供的日期。 如果未提供`date`参数，则返回最新报告。 |
| `fullIDsFragmentCount` | 命名空间中的配置文件片段总数。 |
| `fullIDsCount` | 命名空间中合并的配置文件总数。 |
| `fullIDsPercentage` | `fullIDsCount`占合并配置文件总数的百分比（在`totalRows`上次采样状态[中返回的](#view-last-sample-status)值），以小数格式表示。 |
| `code` | 命名空间的`code`。 使用[Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md)处理命名空间时可以找到此项，在Experience Platform UI中也称为[!UICONTROL Identity symbol]。 若要了解详细信息，请访问[身份命名空间概述](../../identity-service/features/namespaces.md)。 |
| `value` | 命名空间的`id`值。 使用[Identity服务API](../../identity-service/api/list-namespaces.md)处理命名空间时可以找到此项。 |

+++

## 列出数据集统计信息 {#dataset-stats}

通过向`/previewsamplestatus/report/dataset_stats`端点发出GET请求，可生成提供数据集统计信息的报表。

**API格式**

```http
GET /previewsamplestatus/report/dataset_stats
```

**请求**

+++ 生成数据集统计信息报告的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset_stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关数据集统计信息的信息。

+++ 包含有关数据集统计信息的示例响应。

>[!NOTE]
>
>以下响应已被截断以显示三个数据集。

```json
{
    "data": [
        {
            "120days": 4,
            "14days": 4,
            "30days": 4,
            "365days": 4,
            "60days": 4,
            "7days": 4,
            "90days": 4,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 1,
            "records": 4,
            "totalProfiles": 1
        },
        {
            "120days": 155435837,
            "14days": 32888631,
            "30days": 66496282,
            "365days": 155435837,
            "60days": 116433804,
            "7days": 18202004,
            "90days": 155435837,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 16.0,
            "percentProfiles": 0.0,
            "profileFragments": 5410745,
            "records": 155435837,
            "totalProfiles": 4524723
        },
        {
            "120days": 0,
            "14days": 0,
            "30days": 0,
            "365days": 0,
            "60days": 0,
            "7days": 0,
            "90days": 0,
            "datasetId": "{DATASET_ID}",
            "datasetType": "Profiles",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 3589,
            "records": 3589,
            "totalProfiles": 3589
        }
    ],
    "reportTimestamp": "2025-10-29T16:20:18.956"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `120days` | 数据过期120天后保留在数据集中的记录数。 |
| `14days` | 数据过期14天后保留在数据集中的记录数。 |
| `30days` | 数据过期30天后保留在数据集中的记录数。 |
| `365days` | 数据过期365天后保留在数据集中的记录数。 |
| `60days` | 数据过期60天后保留在数据集中的记录数。 |
| `7days` | 数据过期7天后保留在数据集中的记录数。 |
| `90days` | 数据过期90天后保留在数据集中的记录数。 |
| `datasetId` | 数据集的ID。 |
| `datasetType` | 数据集类型。 此值可以是`Profiles`或`ExperienceEvents`。 |
| `percentEvents` | 数据集内体验事件记录的百分比。 |
| `percentProfiles` | 数据集内配置文件记录的百分比。 |
| `profileFragments` | 数据集中存在的配置文件片段总数。 |
| `records` | 引入数据集的配置文件记录总数。 |
| `totalProfiles` | 引入数据集的配置文件总数。 |

+++

## 后续步骤

现在您知道如何在配置文件存储中预览样本数据并对数据运行多个报告了，您还可以使用分段服务API的估计和预览端点查看有关区段定义的摘要级别信息。 此信息可帮助您确保隔离预期的受众。 要了解有关使用分段API处理预览和估算的更多信息，请访问[预览和估算端点指南](../../segmentation/api/previews-and-estimates.md)。

