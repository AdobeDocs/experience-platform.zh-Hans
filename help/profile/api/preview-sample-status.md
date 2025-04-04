---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API；预览；示例
title: 预览示例状态（配置文件预览） API端点
description: 实时客户个人资料API的预览示例状态端点允许您预览个人资料数据的最新成功示例，按数据集和身份列出个人资料分发，并生成显示数据集重叠、身份重叠和未拼接个人资料的报告。
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2909'
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

启用实时客户资料的数据被摄取到[!DNL Experience Platform]后，将存储在资料数据存储中。 当将记录摄取到配置文件存储中增加或减少总配置文件计数超过5%时，将触发取样作业以更新计数。 触发示例的方式取决于所使用的摄取类型：

* 对于&#x200B;**流式数据工作流**，每小时进行一次检查，以确定是否已达到5%的增加或减少阈值。 如果有，则会自动触发示例作业以更新计数。
* 对于&#x200B;**批次摄取**，在成功将批次摄取到配置文件存储区后15分钟内，如果达到5%的增加或减少阈值，则会运行作业以更新计数。 使用配置文件API，您可以预览最新成功的示例作业，以及按数据集和身份命名空间列出配置文件分发。

在Experience Platform UI的[!UICONTROL 配置文件]部分中，还提供了按命名空间量度列出的配置文件计数和配置文件。 有关如何使用UI访问配置文件数据的信息，请访问[[!DNL Profile] UI指南](../ui/user-guide.md)。

## 查看上一个示例状态 {#view-last-sample-status}

您可以对`/previewsamplestatus`端点执行GET请求，以查看为您的组织运行的上一个成功示例作业的详细信息。 这包括示例中的配置文件总数，以及配置文件计数量度，或您的组织在Experience Platform中拥有的配置文件总数。

配置文件计数是在将多个配置文件片段合并在一起，为每个单独的客户形成一个配置文件后生成的。 换言之，当配置文件片段合并在一起时，它们会返回“1”配置文件计数，因为它们都与同一个人相关。

配置文件计数还包括具有属性（记录数据）的用户档案，以及仅包含时间序列（事件）数据(如Adobe Analytics配置文件)的用户档案。 样本作业在摄取用户档案数据时定期刷新，以便在Experience Platform中提供最新的用户档案总数。

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
|---|---|
| `numRowsToRead` | 示例中合并的配置文件总数。 |
| `sampleJobRunning` | 一个布尔值，当示例作业正在进行时返回`true`。 将批处理文件实际添加到配置文件存储区后，可以透明地反映将文件上传到时发生的延迟。 |
| `docCount` | 数据库中的文档总数。 |
| `totalFragmentCount` | 配置文件存储中的配置文件片段总数。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批次摄取时间戳。 |
| `streamingDriven` | *此字段已弃用，对响应没有意义。* |
| `totalRows` | Experience Platform中合并的用户档案总数，也称为“用户档案计数”。 |
| `lastBatchId` | 上次批次摄取ID。 |
| `status` | 上一个示例的状态。 |
| `samplingRatio` | 采样的合并配置文件(`numRowsToRead`)与合并配置文件总数(`totalRows`)的比率，以小数格式表示。 |
| `mergeStrategy` | 示例中使用的合并策略。 |
| `lastSampledTimestamp` | 上次成功的示例时间戳。 |

## 按数据集列出配置文件分发

要查看按数据集分发的用户档案，您可以对`/previewsamplestatus/report/dataset`端点执行GET请求。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报告，则返回该日期的最新报告。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下请求使用`date`参数返回指定日期的最新报告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包含一个`data`数组，其中包含数据集对象列表。 显示的响应已被截断以显示三个数据集。

>[!NOTE]
>
>如果该日期存在多个报表，则仅返回最新的报表。 如果提供的日期不存在数据集报告，则会返回HTTP状态404 （未找到）。

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
| `sampleCount` | 具有此数据集ID的采样合并用户档案总数。 |
| `samplePercentage` | 以小数格式表示的`sampleCount`占抽样合并配置文件总数的百分比（在[上次采样状态](#view-last-sample-status)中返回的`numRowsToRead`值）。 |
| `fullIDsCount` | 具有此数据集ID的合并用户档案总数。 |
| `fullIDsPercentage` | `fullIDsCount`占合并配置文件总数的百分比（在[上次采样状态](#view-last-sample-status)中返回的`totalRows`值），以小数格式表示。 |
| `name` | 数据集的名称，在数据集创建期间提供。 |
| `description` | 数据集的描述，在数据集创建期间提供。 |
| `value` | 数据集的ID。 |
| `streamingIngestionEnabled` | 是否已为数据集启用流式摄取。 |
| `createdUser` | 创建数据集的用户的用户ID。 |
| `reportTimestamp` | 报表的时间戳。 如果在请求期间提供了`date`参数，则返回的报告将对应于提供的日期。 如果未提供`date`参数，则返回最新报告。 |

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

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报告，则返回该日期的最新报告。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下请求未指定`date`参数，因此将返回最新报告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括`data`数组，其中单个对象包含每个命名空间的详细信息。 显示的响应已被截断以显示四个命名空间。

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
| `samplePercentage` | `sampleCount`以采样合并配置文件的百分比表示（在[上次采样状态](#view-last-sample-status)中返回的`numRowsToRead`值），以十进制格式表示。 |
| `reportTimestamp` | 报表的时间戳。 如果在请求期间提供了`date`参数，则返回的报告将对应于提供的日期。 如果未提供`date`参数，则返回最新报告。 |
| `fullIDsFragmentCount` | 命名空间中的配置文件片段总数。 |
| `fullIDsCount` | 命名空间中合并的配置文件总数。 |
| `fullIDsPercentage` | `fullIDsCount`占合并配置文件总数的百分比（在[上次采样状态](#view-last-sample-status)中返回的`totalRows`值），以小数格式表示。 |
| `code` | 命名空间的`code`。 使用[Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md)处理命名空间时可找到此项，在Experience Platform UI中也称为[!UICONTROL Identity符号]。 若要了解详细信息，请访问[身份命名空间概述](../../identity-service/features/namespaces.md)。 |
| `value` | 命名空间的`id`值。 使用[Identity服务API](../../identity-service/api/list-namespaces.md)处理命名空间时可以找到此项。 |

## 生成数据集重叠报告

数据集重叠报表通过公开对可寻址受众贡献最大的数据集（合并的用户档案），提供了对组织用户档案存储构成的可见性。 除了提供数据见解外，此报表还可以帮助您采取措施优化许可证使用，如设置特定数据集的过期时间。

您可以通过对`/previewsamplestatus/report/dataset/overlap`端点执行GET请求来生成数据集重叠报表。

有关分步说明，其中概述了如何使用命令行或Postman UI生成数据集重叠报告，请参阅[生成数据集重叠报告教程](../tutorials/dataset-overlap-report.md)。

**API格式**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在同一日期运行了多个报告，则会返回该日期的最新报告。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下请求使用`date`参数返回指定日期的最新报告。

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
| `data` | `data`对象包含以逗号分隔的数据集列表及其各自的配置文件计数。 |
| `reportTimestamp` | 报表的时间戳。 如果在请求期间提供了`date`参数，则返回的报告将对应于提供的日期。 如果未提供`date`参数，则返回最新报告。 |

### 解释数据集重叠报表

报表的结果可以从响应中的数据集和配置文件计数进行解释。 请考虑以下示例报表`data`对象：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此报表提供以下信息：

* 有123个配置文件包含来自以下数据集的数据： `5d92921872831c163452edc8`、`5da7292579975918a851db57`、`5eb2cdc6fa3f9a18a7592a98`。
* 有454,412个配置文件包含来自这两个数据集的数据：`5d92921872831c163452edc8`和`5eb2cdc6fa3f9a18a7592a98`。
* 有107个配置文件仅包含来自数据集`5eeda0032af7bb19162172a7`的数据。
* 该组织共有454,642个用户档案。

## 生成身份命名空间重叠报告 {#identity-overlap-report}

身份命名空间重叠报表通过公开对可寻址受众贡献最大的身份命名空间（合并的用户档案），提供了对组织配置文件存储构成的可见性。 这包括Adobe提供的标准身份命名空间以及由贵组织定义的自定义身份命名空间。

您可以通过向`/previewsamplestatus/report/namespace/overlap`端点执行GET请求来生成身份命名空间重叠报表。

**API格式**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在同一日期运行了多个报告，则会返回该日期的最新报告。 如果指定日期不存在报表，则会返回404（未找到）错误。 如果未指定日期，则返回最近的报告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下请求使用`date`参数返回指定日期的最新报告。

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
| `data` | `data`对象包含以逗号分隔的列表，这些列表具有身份命名空间代码及其各自配置文件计数的唯一组合。 |
| 命名空间代码 | `code`是每个身份命名空间名称的简短形式。 可以使用[Adobe Experience Platform Identity服务API](../../identity-service/api/list-namespaces.md)找到每个`code`到其`name`的映射。 在Experience Platform UI中，`code`也称为[!UICONTROL 标识符号]。 若要了解详细信息，请访问[身份命名空间概述](../../identity-service/features/namespaces.md)。 |
| `reportTimestamp` | 报表的时间戳。 如果在请求期间提供了`date`参数，则返回的报告将对应于提供的日期。 如果未提供`date`参数，则返回最新报告。 |

### 解释身份命名空间重叠报表

报表的结果可以从响应中的身份和配置文件计数中解释。 每行的数值可告知您有多少个配置文件由标准和自定义身份命名空间的精确组合组成。

请考虑以下来自`data`对象的摘录：

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

此报表提供以下信息：

* 有142个配置文件由`AAID`、`ECID`和`Email`标准身份以及从自定义`crmid`身份命名空间组成。
* 有24个配置文件由`AAID`和`ECID`身份命名空间组成。
* 有6,565个配置文件仅包含`ECID`标识。

## 生成未拼合的用户档案报告

您可以通过未拼合的用户档案报告进一步了解组织用户档案存储区的构成。 “未拼合”配置文件是仅包含一个配置文件片段的配置文件。 “未知”配置文件是与假名身份命名空间（如`ECID`和`AAID`）关联的配置文件。 未知配置文件处于不活动状态，这意味着它们在指定的时间段内未添加新事件。 未拼合的用户档案报表提供了7、30、60、90和120天的用户档案细目。

您可以通过对`/previewsamplestatus/report/unstitchedProfiles`端点执行GET请求来生成未拼合配置文件报表。

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

成功的请求会返回HTTP状态200 （正常）以及“未拼合的用户档案”报表。

>[!NOTE]
>
>出于本指南的目的，报告已被截断为仅包含`"120days"`和“`7days`”个时间段。 完整的未拼合用户档案报表提供了7、30、60、90和120天的用户档案细目。

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
| `data` | `data`对象包含为未拼合的用户档案报告返回的信息。 |
| `totalNumberOfProfiles` | 配置文件存储中的唯一配置文件总数。 这相当于可寻址受众计数。 它包括已知和未拼接的用户档案。 |
| `totalNumberOfEvents` | 配置文件存储区中的ExperienceEvents总数。 |
| `unstitchedProfiles` | 一个对象，其中包含按时间段划分的未拼接用户档案。 未拼合的用户档案报表提供了7、30、60、90和120天时间段的配置文件细目。 |
| `countOfProfiles` | 时间段内未拼接用户档案的计数或命名空间未拼接用户档案的计数。 |
| `eventsAssociated` | 时间范围的ExperienceEvents数或命名空间的事件数。 |
| `nsDistribution` | 一个对象，其中包含各个身份命名空间，每个命名空间均分配有未拼接的用户档案和事件。 注意：将`nsDistribution`对象中每个身份命名空间的总和`countOfProfiles`相加等于时间段内的`countOfProfiles`。 每个命名空间的`eventsAssociated`和每个时段的总数`eventsAssociated`也是如此。 |
| `reportTimestamp` | 报表的时间戳。 |

### 解释未拼合的用户档案报告

该报表的结果可以让您深入了解您的组织在其配置文件存储区中有多少个未拼合和不活动的配置文件。

请考虑以下来自`data`对象的摘录：

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

* 有1,782个配置文件仅包含一个配置文件片段，并且过去7天没有新事件。
* 有29,151个ExperienceEvents与1,782个未拼接的用户档案关联。
* 有1,734个未拼接的用户档案，其中包含来自ECID身份命名空间的单个用户档案片段。
* 有28,591个事件与1,734个未拼接配置文件关联，其中包含来自ECID身份命名空间的单个配置文件片段。

## 后续步骤

现在您知道如何在配置文件存储中预览样本数据并对数据运行多个报告了，您还可以使用分段服务API的估计和预览端点查看有关区段定义的摘要级别信息。 此信息可帮助您确保隔离预期的受众。 要了解有关使用分段API处理预览和估算的更多信息，请访问[预览和估算端点指南](../../segmentation/api/previews-and-estimates.md)。

