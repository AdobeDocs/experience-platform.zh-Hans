---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API
title: 用户档案系统作业API端点
topic: guide
type: Documentation
description: Adobe Experience Platform允许您从用户档案商店删除数据集或批，以删除不再需要或错误添加的实时客户用户档案数据。 这需要使用用户档案API创建用户档案系统作业或删除请求。
translation-type: tm+mt
source-git-commit: d2ace7cadb06f77bdf14b6a4ef83e879c4ca88fd
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 2%

---


# 用户档案系统作业端点（删除请求）

Adobe Experience Platform使您能够从多个来源收集数据，并为各个客户构建强大的用户档案。 引入[!DNL Platform]的数据存储在[!DNL Data Lake]中，如果已启用用户档案集，该数据也存储在[!DNL Real-time Customer Profile]数据存储中。 有时可能需要从用户档案库中删除数据集或批处理，以删除不再需要或错误添加的数据。 这需要使用[!DNL Real-time Customer Profile] API创建[!DNL Profile]系统作业或`delete request`，如果需要，还可以修改、监视或删除该作业。

>[!NOTE]
>
>如果您尝试从[!DNL Data Lake]删除数据集或批，请访问[目录服务概述](../../catalog/home.md)以了解更多信息。

## 入门指南

本指南中使用的API端点是[[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)的一部分。 在继续之前，请查看[入门指南](getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何Experience PlatformAPI所需的重要头信息。

## 视图删除请求

删除请求是一个长时间运行的异步进程，这意味着您的组织可能同时运行多个删除请求。 为了视图您的组织当前正在运行的所有删除请求，您可以对`/system/jobs`端点执行GET请求。

您还可以使用可选的查询参数来筛选响应中返回的删除请求的列表。 要使用多个参数，请使用和号(`&`)分隔每个参数。

**API格式**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `start` | 根据请求的创建时间，偏移返回的结果页面。 示例: `start=4` |
| `limit` | 限制返回的结果数。 示例: `limit=10` |
| `page` | 按照请求的创建时间返回特定的结果页面。 示例: `page=2` |
| `sort` | 按特定字段按升序(`asc`)或降序(`desc`)顺序对结果进行排序。 返回多页结果时，排序参数不起作用。 示例: `sort=batchId:asc` |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

该响应包括一个“子项”数组，每个删除请求都有一个对象，其中包含该请求的详细信息。

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| 属性 | 描述 |
|---|---|
| `_page.count` | 请求总数。 此响应已被截断为空间。 |
| `_page.next` | 如果存在其他结果页，则通过将[查找请求](#view-a-specific-delete-request)中的ID值替换为提供的`"next"`值来视图下一页结果。 |
| `jobType` | 所创建作业的类型。 在这种情况下，它将始终返回`"DELETE"`。 |
| `status` | 删除请求的状态。 可能的值为`"NEW"`、`"PROCESSING"`、`"COMPLETED"`、`"ERROR"`。 |
| `metrics` | 一个对象，包括已处理的记录数(`"recordsProcessed"`)和请求已处理的时间（以秒为单位），或完成请求所用的时间(`"timeTakenInSec"`)。 |

## 创建删除请求{#create-a-delete-request}

通过向`/systems/jobs`端点发出POST请求来启动新的删除请求，其中，要删除的数据集或批处理的ID在请求主体中提供。

### 删除数据集

要从用户档案商店删除数据集，数据集ID必须包含在POST请求的正文中。 此操作将删除给定数据集的ALL数据。 [!DNL Experience Platform] 允许您根据记录和时间序列模式删除数据集。

**API格式**

```http
POST /system/jobs
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| 属性 | 描述 |
|---|---|
| `dataSetId` | **（必需）** 要删除的数据集的ID。 |

**响应**

成功的响应会返回新创建的删除请求的详细信息，包括该请求的唯一、由系统生成的只读ID。 这可用于查找请求并检查其状态。 创建时请求的`status`为`"NEW"`，直到开始处理。 响应中的`dataSetId`应与请求中发送的`dataSetId`匹配。

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| 属性 | 描述 |
|---|---|
| `id` | 删除请求的唯一、由系统生成的只读ID。 |
| `dataSetId` | 数据集的ID，在POST请求中指定。 |

### 删除批

要删除批，批ID必须包含在POST请求主体中。 请注意，不能根据记录模式删除数据集的批。 只能删除基于时间序列模式的数据集的批次。

>[!NOTE]
>
> 无法根据记录模式删除数据集批的原因是记录类型数据集批覆盖以前的记录，因此无法“撤消”或删除。 要消除基于记录模式的数据集中错误批次的影响，唯一的方法是使用正确的数据重新收录批次，以覆盖错误的记录。

有关记录和时间序列行为的详细信息，请查看[!DNL XDM System]概述中有关XDM数据行为](../../xdm/home.md#data-behaviors)的[部分。

**API格式**

```http
POST /system/jobs
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| 属性 | 描述 |
|---|---|
| `batchId` | **(必需** )要删除的批的ID。 |

**响应**

成功的响应会返回新创建的删除请求的详细信息，包括该请求的唯一、由系统生成的只读ID。 这可用于查找请求并检查其状态。 创建时请求的`"status"`为`"NEW"`，直到开始处理。 响应中的`"batchId"`值应与请求中发送的`"batchId"`值匹配。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| 属性 | 描述 |
|---|---|
| `id` | 删除请求的唯一、由系统生成的只读ID。 |
| `batchId` | 批的ID，在POST请求中指定。 |

如果尝试为“记录”数据集批启动删除请求，您将遇到400级错误，如下所示：

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## 视图特定的删除请求{#view-a-specific-delete-request}

要视图特定的删除请求（包括其状态等详细信息），可以对`/system/jobs`端点执行查找(GET)请求，并在路径中包含删除请求的ID。

**API格式**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 参数 | 描述 |
|---|---|
| `{DELETE_REQUEST_ID}` | **（必需）** 您要视图的删除请求的ID。 |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应提供删除请求的详细信息，包括其更新状态。 响应中删除请求的ID（`"id"`值）应与请求路径中发送的ID匹配。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| 属性 | 描述 |
|---|---|
| `jobType` | 正在创建的作业类型，在此例中，它将始终返回`"DELETE"`。 |
| `status` | 删除请求的状态。 可能的值：`"NEW"`、`"PROCESSING"`、`"COMPLETED"`、`"ERROR"`。 |
| `metrics` | 一个数组，包括已处理的记录数(`"recordsProcessed"`)和请求已处理的时间（以秒为单位），或请求完成所用的时间(`"timeTakenInSec"`)。 |

删除请求状态为`"COMPLETED"`后，您可以通过尝试使用数据访问API访问已删除的数据来确认该数据已被删除。 有关如何使用数据访问API访问数据集和批次的说明，请查阅[数据访问文档](../../data-access/home.md)。

## 删除删除请求

[!DNL Experience Platform] 允许您删除以前的请求，这可能由于许多原因（包括删除作业未完成或在处理阶段卡住）而有用。要删除删除请求，您可以对`/system/jobs`端点执行DELETE请求，并将要删除请求的ID包含到请求路径。

**API格式**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 参数 | 描述 |
|---|---|
| {DELETE_请求_ID} | 要删除的删除请求的ID。 |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功删除请求将返回HTTP状态200(OK)和空的响应主体。 您可以通过执行GET请求来按删除请求的ID视图该请求，以确认该请求已被删除。 这应返回“HTTP状态404（未找到）”，表示删除请求已被删除。

## 后续步骤

现在，您已了解从[!DNL Experience Platform]中的[!DNL Profile Store]删除数据集和批处理时涉及的步骤，因此您可以安全地删除错误添加的数据，或者删除您的组织不再需要的数据。 请注意，删除请求无法撤消，因此您应仅删除您确信现在不需要且将来不需要的数据。