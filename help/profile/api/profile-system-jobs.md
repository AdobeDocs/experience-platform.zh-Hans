---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API
title: 配置文件系统作业API端点
type: Documentation
description: Adobe Experience Platform允许您从配置文件存储中删除数据集或批次，以便删除不再需要或添加错误的实时客户配置文件数据。 这需要使用配置文件API创建配置文件系统作业或删除请求。
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: 42c83c7449a14eec5b91f82811bce4234e47cb51
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 2%

---

# 配置文件系统作业端点（删除请求）

Adobe Experience Platform允许您从多个源摄取数据，并为个别客户构建可靠的配置文件。 数据被引入 [!DNL Platform] 存储在 [!DNL Data Lake]，并且如果为配置文件启用了数据集，则该数据将存储在 [!DNL Real-Time Customer Profile] 数据存储区。 有时候，可能有必要从配置文件存储中删除与数据集关联的配置文件数据，以便删除不再需要或添加错误的数据。 这需要使用 [!DNL Real-Time Customer Profile] 用于创建应用程序的API [!DNL Profile] 系统作业，或 `delete request`，如有必要，还可以修改、监视或移除这些组件。

>[!NOTE]
>
>如果您尝试从以下位置删除数据集或批次： [!DNL Data Lake]，请访问 [目录服务概述](../../catalog/home.md) 以了解更多信息。

## 快速入门

本指南中使用的API端点是 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 在继续之前，请查看 [快速入门指南](getting-started.md) 有关相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 查看删除请求

删除请求是一个长期运行的异步过程，这意味着您的组织可能同时运行多个删除请求。 要查看贵组织当前运行的所有删除请求，您可以向以下网站执行GET请求： `/system/jobs` 端点。

您还可以使用可选的查询参数来筛选响应中返回的删除请求列表。 要使用多个参数，请使用&amp;符号(`&`)。

**API格式**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `start` | 根据请求的创建时间，偏移返回的结果页面。 示例：`start=4` |
| `limit` | 限制返回的结果数。 示例：`limit=10` |
| `page` | 根据请求的创建时间，返回结果的特定页面。 示例：`page=2` |
| `sort` | 按特定字段对结果进行升序排序(`asc`)或降序(`desc`)。 返回多个结果页面时，排序参数不起作用。 示例：`sort=batchId:asc` |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包括“子项”数组，每个删除请求都有一个对象，其中包含该请求的详细信息。

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
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
| `_page.count` | 请求总数。 此响应的空间已被截断。 |
| `_page.next` | 如果存在额外的结果页面，请通过替换 [查找请求](#view-a-specific-delete-request) 使用 `"next"` 提供的值。 |
| `jobType` | 正在创建的作业类型。 在这种情况下，它将始终返回 `"DELETE"`. |
| `status` | 删除请求的状态。 可能的值包括 `"NEW"`， `"PROCESSING"`， `"COMPLETED"`， `"ERROR"`. |
| `metrics` | 包含已处理的记录数的对象(`"recordsProcessed"`)以及处理请求所用的时间（以秒为单位）或完成请求所用的时间(`"timeTakenInSec"`)。 |

## 创建删除请求 {#create-a-delete-request}

新删除请求是通过向发出的POST请求来启动的 `/systems/jobs` 端点，其中在请求正文中提供要删除的数据集或批次的ID。

### 删除数据集和关联的配置文件数据

要从配置文件存储中删除数据集及与该数据集关联的所有配置文件数据，数据集ID必须包含在POST请求正文中。 此操作将删除给定数据集的所有数据。 [!DNL Experience Platform] 允许您同时基于记录和时间序列架构删除数据集。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| 属性 | 描述 |
|---|---|
| `dataSetId` | **（必需）** 要删除的数据集的ID。 |

**响应**

成功的响应会返回新创建的删除请求的详细信息，包括系统生成的唯一只读ID请求。 这可用于查找请求并检查其状态。 此 `status` 对于创建时的请求，为 `"NEW"` 直到它开始处理。 此 `dataSetId` 在响应中应匹配 `dataSetId` 在请求中发送。

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| 属性 | 描述 |
|---|---|
| `id` | 删除请求的唯一、系统生成的只读ID。 |
| `dataSetId` | 数据集的ID，在POST请求中指定。 |

### 删除批次

要删除批次，批次ID必须包含在POST请求正文中。 请注意，您无法删除基于记录架构的数据集的批次。 只能删除基于时间序列架构的数据集的批次。

>[!NOTE]
>
> 无法删除基于记录架构的数据集的批次，因为记录类型数据集批次会覆盖以前的记录，因此无法“撤消”或删除。 在基于记录架构的数据集中消除错误批次影响的唯一方法是使用正确的数据重新摄取批次，以覆盖错误的记录。

有关记录和时间序列行为的更多信息，请查阅 [有关XDM数据行为的部分](../../xdm/home.md#data-behaviors) 在 [!DNL XDM System] 概述。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| 属性 | 描述 |
|---|---|
| `batchId` | **（必需）** 要删除的批次的ID。 |

**响应**

成功的响应会返回新创建的删除请求的详细信息，包括系统生成的唯一只读ID请求。 这可用于查找请求并检查其状态。 此 `"status"` 对于创建时的请求，为 `"NEW"` 直到它开始处理。 此 `"batchId"` 响应中的值应与 `"batchId"` 请求中发送的值。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| 属性 | 描述 |
|---|---|
| `id` | 删除请求的唯一、系统生成的只读ID。 |
| `batchId` | 在POST请求中指定的批次ID。 |

如果尝试启动记录数据集批次的删除请求，您将遇到400级错误，如下所示：

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

## 查看特定的删除请求 {#view-a-specific-delete-request}

要查看特定删除请求（包括其状态等详细信息），您可以向以下地址执行查找(GET)请求： `/system/jobs` 端点并在路径中包含删除请求的ID。

**API格式**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 参数 | 描述 |
|---|---|
| `{DELETE_REQUEST_ID}` | **（必需）** 要查看的删除请求的ID。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应会提供删除请求的详细信息，包括其更新状态。 响应中的删除请求的ID (响应中的 `"id"` 值)应与请求路径中发送的ID匹配。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
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
| `jobType` | 正在创建的作业类型，在这种情况下，将始终返回 `"DELETE"`. |
| `status` | 删除请求的状态。 可能的值： `"NEW"`， `"PROCESSING"`， `"COMPLETED"`， `"ERROR"`. |
| `metrics` | 一个数组，其中包含已处理的记录数(`"recordsProcessed"`)以及处理请求所用的时间（以秒为单位）或完成请求所用的时间(`"timeTakenInSec"`)。 |

一旦删除请求状态为 `"COMPLETED"` 您可以通过尝试使用数据访问API访问已删除的数据来确认数据已被删除。 有关如何使用数据访问API访问数据集和批次的说明，请查看 [数据访问文档](../../data-access/home.md).

## 删除删除请求

[!DNL Experience Platform] 允许您删除以前的请求，删除请求可能由于许多原因非常有用，包括删除作业未完成或停滞在处理阶段。 要删除删除请求，您可以对执行DELETE请求 `/system/jobs` 端点，并包括要删除到请求路径的删除请求的ID。

**API格式**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 参数 | 描述 |
|---|---|
| {DELETE_REQUEST_ID} | 要删除的删除请求的ID。 |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的删除请求返回HTTP状态200 （正常）和空响应正文。 您可以通过执行GET请求来确认请求已删除，以按其ID查看删除请求。 此操作应返回HTTP状态404（未找到），指示删除请求已被删除。

## 后续步骤

现在您已经知道了从中删除数据集和批次所涉及的步骤 [!DNL Profile Store] 范围 [!DNL Experience Platform]，您可以安全地删除错误添加或您的组织不再需要的数据。 请注意，删除请求无法撤消，因此您应该只删除确信现在不需要且将来不需要的数据。
