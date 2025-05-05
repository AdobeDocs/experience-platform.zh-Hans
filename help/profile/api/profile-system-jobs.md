---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 配置文件系统作业API端点
type: Documentation
description: Adobe Experience Platform允许您从配置文件存储中删除数据集或批次，以便删除不再需要或添加错误的实时客户配置文件数据。 这需要使用配置文件API创建配置文件系统作业或删除请求。
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 2%

---

# 配置文件系统作业端点（删除请求）

>[!IMPORTANT]
>
>在Microsoft Azure上运行的Adobe Experience Platform实施与Amazon Web Services (AWS)上运行的实施之间可能存在以下端点。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/landing/multi-cloud)。

Adobe Experience Platform允许您从多个源摄取数据，并为个别客户构建可靠的配置文件。 摄取到[!DNL Experience Platform]的数据存储在[!DNL Data Lake]中，如果为配置文件启用了数据集，则该数据也存储在[!DNL Real-Time Customer Profile]数据存储中。 有时候，可能有必要从配置文件存储中删除与数据集关联的配置文件数据，以便删除不再需要或添加错误的数据。 这需要使用[!DNL Real-Time Customer Profile] API创建[!DNL Profile]系统作业或“删除请求”。

>[!NOTE]
>
>如果您尝试从[!DNL Data Lake]中删除数据集或批次，请访问[目录服务概述](../../catalog/home.md)以了解更多信息。

## 快速入门

本指南中使用的API终结点是[[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 在继续之前，请查看[快速入门指南](getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience Platform API所需的所需标头的重要信息。

## 查看删除请求 {#view}

删除请求是一个长期运行的异步过程，这意味着您的组织可能同时运行多个删除请求。 要查看您的组织当前运行的所有删除请求，您可以对`/system/jobs`端点执行GET请求。

您还可以使用可选的查询参数来筛选响应中返回的删除请求列表。 若要使用多个参数，请使用&amp;符号(`&`)分隔每个参数。

**API格式**

>[!AVAILABILITY]
>
>在Microsoft Azure上使用Experience Platform时，以下查询参数仅&#x200B;**可用**。
>
>在AWS上使用此端点时，前100个系统作业将根据其创建日期以降序返回。

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `start` | 根据请求的创建时间，偏移返回的结果页面。 | `start=4` |
| `limit` | 限制返回的结果数。 | `limit=10` |
| `page` | 根据请求的创建时间，返回结果的特定页面。 | `page=2` |
| `sort` | 按特定字段对结果进行升序(`asc`)或降序(`desc`)排序。 返回多个结果页面时，排序参数不起作用。 | `sort=batchId:asc` |

**请求**

>[!IMPORTANT]
>
>以下请求在Azure实例和AWS实例之间有所不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ 查看系统作业的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>在将此端点与AWS结合使用时，您&#x200B;**必须**&#x200B;使用`x-sandbox-id`请求标头，而不是`x-sandbox-name`请求标头。

+++ 查看系统作业的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
```

+++

>[!ENDTABS]

**响应**

>[!IMPORTANT]
>
>以下响应在Azure实例和AWS实例之间有所不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

成功的响应包括“子项”数组，每个删除请求都有一个对象，其中包含该请求的详细信息。

+++ 查看删除请求的成功响应

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
| -------- | ----------- |
| `_page.count` | 请求总数。 此响应的空间已被截断。 |
| `_page.next` | 如果存在额外的结果页，请将[查找请求](#view-a-specific-delete-request)中的ID值替换为提供的`"next"`值，以查看下一页的结果。 |
| `jobType` | 正在创建的作业类型。 在这种情况下，它将始终返回`"DELETE"`。 |
| `status` | 删除请求的状态。 可能的值包括`"NEW"`、`"PROCESSING"`、`"COMPLETED"`和`"ERROR"`。 |
| `metrics` | 一个对象，其中包含已处理的记录数(`"recordsProcessed"`)、请求已处理的时间（以秒为单位）或完成请求所需的时间(`"timeTakenInSec"`)。 |

+++

>[!TAB Amazon Web Services (AWS)]

成功的响应会返回一个数组，其中包含每个系统请求的对象。

+++ 查看系统请求的成功响应

```json
{
    [
        {
            "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
            "requestType": "DELETE_EE_BATCH",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        },
        {
            "requestId": "38a835eb-b491-4864-902b-be07fa4d6a6d",
            "requestType": "TRUNCATE_DATASET",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        }        
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `requestId` | 系统作业的ID。 |
| `requestType` | 系统作业的类型。 可能的值包括`BACKFILL_TTL`、`DELETE_EE_BATCH`和`TRUNCATE_DATASET`。 |
| `status` | 系统作业的状态。 可能的值包括`NEW`、`SUCCESS`、`ERROR`、`FAILED`和`IN-PROGRESS`。 |
| `properties` | 包含系统作业的批次和/或数据集ID的对象。 |

+++

>[!ENDTABS]

## 创建删除请求 {#create-a-delete-request}

启动新的删除请求是通过POST请求完成到`/systems/jobs`端点的操作，其中要删除的数据集或批次的ID会包含在请求正文中。

### 删除数据集和关联的配置文件数据

要从配置文件存储中删除数据集以及与数据集关联的所有配置文件数据，数据集ID必须包含在POST请求正文中。 此操作将删除给定数据集的所有数据。 [!DNL Experience Platform]允许您同时基于记录和时间序列架构删除数据集。

**API格式**

```http
POST /system/jobs
```

**请求**

>[!IMPORTANT]
>
>以下请求在Azure实例和AWS实例之间有所不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ 删除数据集的示例请求。

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

+++

| 属性 | 描述 |
| -------- | ----------- |
| `dataSetId` | 要删除的数据集的ID。 |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>在将此端点与AWS结合使用时，您&#x200B;**必须**&#x200B;使用`x-sandbox-id`请求标头，而不是`x-sandbox-name`请求标头。

+++ 删除数据集的示例请求。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| 属性 | 描述 |
| -------- | ----------- |
| `dataSetId` | 要删除的数据集的ID。 |

>[!ENDTABS]

**响应**

>[!IMPORTANT]
>
>以下响应在Azure实例和AWS实例之间有所不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

成功的响应会返回新创建的删除请求的详细信息，包括系统生成的唯一只读ID请求。 这可用于查找请求并检查其状态。 创建请求时的`status`为`"NEW"`，直到开始处理为止。 响应中的`dataSetId`应与请求中发送的`dataSetId`匹配。

+++ 创建删除请求的成功响应。

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
| -------- | ----------- |
| `id` | 删除请求的唯一、系统生成的只读ID。 |
| `dataSetId` | 数据集的ID，在POST请求中指定。 |

+++

>[!TAB Amazon Web Services (AWS)]

成功的响应会返回新创建的系统请求的详细信息。

+++ 创建删除请求的成功响应。

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `requestId` | 系统作业的ID。 |
| `requestType` | 系统作业的类型。 可能的值包括`BACKFILL_TTL`、`DELETE_EE_BATCH`和`TRUNCATE_DATASET`。 |
| `status` | 系统作业的状态。 可能的值包括`NEW`、`SUCCESS`、`ERROR`、`FAILED`和`IN-PROGRESS`。 |
| `properties` | 包含系统作业的批次和/或数据集ID的对象。 |

+++

>[!ENDTABS]

### 删除批次

要删除批次，批次ID必须包含在POST请求正文中。 请注意，您无法删除基于记录架构的数据集的批次。 只能删除基于时间序列架构的数据集的批次。

>[!NOTE]
>
> 无法删除基于记录架构的数据集的批次，因为记录类型数据集批次会覆盖以前的记录，因此无法“撤消”或删除。 在基于记录架构的数据集中消除错误批次影响的唯一方法是使用正确的数据重新摄取批次，以覆盖错误的记录。

有关记录和时序行为的更多信息，请查看[!DNL XDM System]概述中有关XDM数据行为[&#128279;](../../xdm/home.md#data-behaviors)的部分。

**API格式**

```http
POST /system/jobs
```

**请求**

>[!IMPORTANT]
>
>以下请求在Azure实例和AWS实例之间有所不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ 删除批次的示例请求。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| 属性 | 描述 |
| -------- | ----------- |
| `datasetId` | 要删除的批次的数据集的ID。 |
| `batchId` | 要删除的批次的ID。 |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>在将此端点与AWS结合使用时，您&#x200B;**必须**&#x200B;使用`x-sandbox-id`请求标头，而不是`x-sandbox-name`请求标头。

+++ 删除批次的示例请求。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| 属性 | 描述 |
| -------- | ----------- |
| `datasetId` | 要删除的批次的数据集的ID。 |
| `batchId` | 要删除的批次的ID。 |

>[!ENDTABS]

**响应**

>[!IMPORTANT]
>
>以下响应在Azure实例和AWS实例之间有所不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

成功的响应会返回新创建的删除请求的详细信息，包括系统生成的唯一只读ID请求。 这可用于查找请求并检查其状态。 创建请求时的`"status"`为`"NEW"`，直到开始处理为止。 响应中的`"batchId"`值应与请求中发送的`"batchId"`值匹配。

+++ 创建删除请求的成功响应。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "66a92c5910df2d1767de13f3",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 删除请求的唯一、系统生成的只读ID。 |
| `datasetId` | 指定数据集的ID。 |
| `batchId` | POST请求中指定的批次ID。 |

+++

>[!TAB Amazon Web Services (AWS)]

成功的响应会返回新创建的系统请求的详细信息。

+++ 创建删除请求的成功响应。

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `requestId` | 系统作业的ID。 |
| `requestType` | 系统作业的类型。 可能的值包括`BACKFILL_TTL`、`DELETE_EE_BATCH`和`TRUNCATE_DATASET`。 |
| `status` | 系统作业的状态。 可能的值包括`NEW`、`SUCCESS`、`ERROR`、`FAILED`和`IN-PROGRESS`。 |
| `properties` | 包含系统作业的批次和/或数据集ID的对象。 |

+++

>[!ENDTABS]

>[!AVAILABILITY]
>
>在Microsoft Azure上使用Experience Platform时，以下功能仅&#x200B;**可用**。

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

要查看特定删除请求，包括其状态等详细信息，您可以对`/system/jobs`端点执行查找(GET)请求，并在路径中包含删除请求的ID。

**API格式**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DELETE_REQUEST_ID}` | 要查看的删除请求的ID。 |

**请求**

>[!IMPORTANT]
>
>以下请求在Azure实例和AWS实例之间有所不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ 查看配置文件作业的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>在将此端点与AWS结合使用时，您&#x200B;**必须**&#x200B;使用`x-sandbox-id`请求标头，而不是`x-sandbox-name`请求标头。

+++ 查看配置文件作业的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

+++

>[!ENDTABS]


**响应**

>[!IMPORTANT]
>
>以下响应在Azure实例和AWS实例之间有所不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

响应会提供删除请求的详细信息，包括其更新状态。 响应中的删除请求的ID（`"id"`值）应与请求路径中发送的ID匹配。

+++ 查看删除请求的成功响应。

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
| ---------- | ----------- |
| `jobType` | 正在创建的作业类型，在这种情况下，它将始终返回`"DELETE"`。 |
| `status` | 删除请求的状态。 可能的值包括`NEW`、`PROCESSING`、`COMPLETED`和`ERROR`。 |
| `metrics` | 一个数组，其中包含已处理的记录数(`"recordsProcessed"`)以及处理请求所用的时间（以秒为单位）或完成请求所用的时间(`"timeTakenInSec"`)。 |

+++

>[!TAB Amazon Web Services (AWS)]

成功的响应将返回指定系统请求的详细信息。

+++ 查看删除请求的成功响应。

```json
{
    "requestId": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `requestId` | 系统作业的ID。 |
| `requestType` | 系统作业的类型。 可能的值包括`BACKFILL_TTL`、`DELETE_EE_BATCH`和`TRUNCATE_DATASET`。 |
| `status` | 系统作业的状态。 可能的值包括`NEW`、`SUCCESS`、`ERROR`、`FAILED`和`IN-PROGRESS`。 |
| `properties` | 包含系统作业的批次和/或数据集ID的对象。 |

+++

>[!ENDTABS]

删除请求状态为`"COMPLETED"`后，您可以通过尝试使用数据访问API访问已删除的数据来确认数据已被删除。 有关如何使用数据访问API访问数据集和批次的说明，请查看[数据访问文档](../../data-access/home.md)。

## 删除删除请求

>[!AVAILABILITY]
>
>此终结点在Adobe Experience Platform的Azure实例中是&#x200B;**only**&#x200B;受支持的，在AWS实例中是&#x200B;**不支持**。

[!DNL Experience Platform]允许您删除以前的请求，这可能对许多原因有用，包括删除作业未完成或卡在处理阶段。 要删除删除请求，您可以对`/system/jobs`端点执行DELETE请求，并包含要删除到请求路径的删除请求的ID。

**API格式**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| {DELETE_REQUEST_ID} | 要删除的删除请求的ID。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的删除请求返回HTTP状态200 （正常）和空响应正文。 您可以通过执行GET请求来确认请求已删除，以按其ID查看删除请求。 此操作应返回HTTP状态404（未找到），指示删除请求已被删除。

## 后续步骤

现在您已经知道从[!DNL Experience Platform]中的[!DNL Profile store]删除数据集和批次所涉及的步骤，您可以安全地删除已错误添加或您的组织不再需要的数据。 请注意，删除请求无法撤消，因此您应该只删除确信现在不需要且将来不需要的数据。
