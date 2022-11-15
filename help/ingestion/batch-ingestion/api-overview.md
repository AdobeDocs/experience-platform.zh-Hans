---
keywords: Experience Platform；主页；热门主题；批量摄取；批量摄取；开发人员指南；API指南；上传；摄取Parquet；摄取json;
solution: Experience Platform
title: 批量摄取API指南
description: 本文档为使用适用于Adobe Experience Platform的批量摄取API的开发人员提供了全面的指南。
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 49281d6ef959c84c3da964f0a9e19859fd8901a5
workflow-type: tm+mt
source-wordcount: '2413'
ht-degree: 4%

---

# 批量摄取开发人员指南

本文档提供了使用 [批量摄取API端点](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Batch-Ingestion) 在Adobe Experience Platform。 有关批量摄取API的概述（包括先决条件和最佳实践），请首先阅读 [批量摄取API概述](overview.md).

本文档的附录提供了 [格式化要用于摄取的数据](#data-transformation-for-batch-ingestion)，包括示例CSV和JSON数据文件。

## 快速入门

本指南中使用的API端点是 [数据摄取API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). 数据摄取提供了一个RESTful API，通过该API，您可以对支持的对象类型执行基本的CRUD操作。

在继续之前，请查看 [批量摄取API概述](overview.md) 和 [入门指南](getting-started.md).

## 摄取JSON文件

>[!NOTE]
>
>以下步骤适用于小文件（256 MB或更小）。 如果遇到网关超时或请求正文大小错误，则需要切换到大文件上传。

### 创建批处理

首先，您需要创建一个以JSON作为输入格式的批处理。 创建批处理时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的XDM架构。

>[!NOTE]
>
>以下示例适用于单行JSON。 要摄取多行JSON，请 `isMultiLineJson` 需要设置标记。 欲知更多信息，请阅读 [批量摄取疑难解答指南](./troubleshooting.md).

**API格式**

```http
POST /batches
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 引用数据集的ID。 |

**响应**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批处理的ID。 |
| `{DATASET_ID}` | 引用的数据集的ID。 |

### 上传文件

现在，您已创建批处理，接下来可以使用批处理创建响应中的批处理ID将文件上传到批处理。 您可以将多个文件上传到批。

>[!NOTE]
>
>请参阅附录部分 [格式正确的JSON数据文件的示例](#data-transformation-for-batch-ingestion).

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批处理的ID。 |
| `{DATASET_ID}` | 批次引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 确保使用唯一的文件名，使其与正在提交的批量文件的其他文件不冲突。 |

**请求**

>[!NOTE]
>
>API支持单步上传。 确保content-type为application/八位字节流。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如 `acme/customers/campaigns/summer.json`. |

**响应**

```http
200 OK
```

### 完成批次

上传完文件的所有不同部分后，您将需要发出数据已完全上传以及批处理已准备好升级的信号。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批处理的ID。 |

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```http
200 OK
```

## 摄取Parquet文件 {#ingest-parquet-files}

>[!NOTE]
>
>以下步骤适用于小文件（256 MB或更小）。 如果遇到网关超时或请求正文大小错误，则需要切换到大文件上传。

### 创建批处理

首先，需要创建一个以Parquet为输入格式的批处理。 创建批处理时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的XDM架构。

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| 参数 | 描述 |
| --------- | ------------ |
| `{DATASET_ID}` | 引用数据集的ID。 |

**响应**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批处理的ID。 |
| `{DATASET_ID}` | 引用的数据集的ID。 |
| `{USER_ID}` | 创建批处理的用户ID。 |

### 上传文件

现在，您已创建批处理，接下来可以使用 `batchId` 从之前将文件上传到批处理。 您可以将多个文件上传到批。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批处理的ID。 |
| `{DATASET_ID}` | 批次引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 确保使用唯一的文件名，使其与正在提交的批量文件的其他文件不冲突。 |

**请求**

>[!CAUTION]
>
>此API支持单步上传。 确保content-type为application/八位字节流。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如 `acme/customers/campaigns/summer.parquet`. |

**响应**

```http
200 OK
```

### 完成批次

上传完文件的所有不同部分后，您将需要发出数据已完全上传以及批处理已准备好升级的信号。

**API格式**

```http
POST /batches/{BATCH_ID}?action=complete
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要表示的批的ID已准备就绪，可供完成。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 摄取大型镶木文件

>[!NOTE]
>
>本节详细介绍如何上传大于256 MB的文件。 大文件以块形式上传，然后通过API信号拼合。

### 创建批处理

首先，需要创建一个以Parquet为输入格式的批处理。 创建批处理时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的XDM架构。

**API格式**

```http
POST /batches
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 引用数据集的ID。 |

**响应**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批处理的ID。 |
| `{DATASET_ID}` | 引用的数据集的ID。 |
| `{USER_ID}` | 创建批处理的用户ID。 |

### 初始化大文件

创建批处理后，您需要先初始化大文件，然后再将块上传到批处理。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批处理的ID。 |
| `{DATASET_ID}` | 引用的数据集的ID。 |
| `{FILE_NAME}` | 要初始化的文件的名称。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
201 Created
```

### 上传大文件块

现在，文件已创建完毕，通过发出重复的PATCH请求（对文件的每个部分发出一个请求），可以上传所有后续区块。

**API格式**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批处理的ID。 |
| `{DATASET_ID}` | 批次引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 确保使用唯一的文件名，使其与正在提交的批量文件的其他文件不冲突。 |

**请求**

>[!CAUTION]
>
>此API支持单步上传。 确保content-type为application/八位字节流。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONTENT_RANGE}` | 在整数中，请求范围的开头和结尾。 |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如 `acme/customers/campaigns/summer.json`. |


**响应**

```http
200 OK
```

### 完整大文件

现在，您已创建批处理，接下来可以使用 `batchId` 从之前将文件上传到批处理。 您可以将多个文件上传到批。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要表示完成的批的ID。 |
| `{DATASET_ID}` | 批次引用数据集的ID。 |
| `{FILE_NAME}` | 要表示完成的文件的名称。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
201 Created
```

### 完成批次

上传完文件的所有不同部分后，您将需要发出数据已完全上传以及批处理已准备好升级的信号。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要表示的批次的ID已完成。 |


**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 摄取CSV文件

要摄取CSV文件，您需要创建一个支持CSV的类、架构和数据集。 有关如何创建必需类和架构的详细信息，请按照 [临时模式创建教程](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>以下步骤适用于小文件（256 MB或更小）。 如果遇到网关超时或请求正文大小错误，则需要切换到大文件上传。

### 创建数据集

按照上面创建必需类和架构的说明进行操作后，您将需要创建一个可支持CSV的数据集。

**API格式**

```http
POST /catalog/dataSets
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      }
  }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TENANT_ID}` | 此ID用于确保您创建的资源具有正确命名空间，并包含在您的IMS组织内。 |
| `{SCHEMA_ID}` | 您创建的架构的ID。 |

### 创建批处理

接下来，您将需要创建一个以CSV作为输入格式的批处理。 创建批处理时，您需要提供数据集ID。 您还需要确保作为批次的一部分上传的所有文件都符合链接到提供数据集的架构。

**API格式**

```http
POST /batches
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 引用数据集的ID。 |

**响应**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批处理的ID。 |
| `{DATASET_ID}` | 引用的数据集的ID。 |
| `{USER_ID}` | 创建批处理的用户ID。 |

### 上传文件

现在，您已创建批处理，接下来可以使用 `batchId` 从之前将文件上传到批处理。 您可以将多个文件上传到批。

>[!NOTE]
>
>请参阅附录部分 [格式正确的CSV数据文件示例](#data-transformation-for-batch-ingestion).

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批处理的ID。 |
| `{DATASET_ID}` | 批次引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 确保使用唯一的文件名，使其与正在提交的批量文件的其他文件不冲突。 |

**请求**

>[!CAUTION]
>
>此API支持单步上传。 确保content-type为application/八位字节流。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如 `acme/customers/campaigns/summer.csv`. |


**响应**

```http
200 OK
```

### 完成批次

完成文件所有不同部分的上传后，您将需要发出数据已完全上传以及批处理已准备好升级的信号。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```http
200 OK
```

## 取消批

在批处理过程中，仍可以取消该批处理。 但是，一个批次完成（例如，成功或失败状态）后，便无法取消该批次。

**API格式**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要取消的批次的ID。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 删除批处理 {#delete-a-batch}

通过使用 `action=REVERT` 查询参数到要删除的批的ID。 该批标记为“不活动”，以便符合垃圾收集的条件。 将异步收集该批次，届时该批次将标记为“已删除”。

**API格式**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要删除的批的ID。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 修补批处理

有时可能需要更新贵组织的用户档案存储区中的数据。 例如，您可能需要更正记录或更改属性值。 Adobe Experience Platform支持通过upsert操作或“修补批处理”来更新或修补配置文件存储数据。

>[!NOTE]
>
>这些更新仅允许在用户档案记录中进行，不允许在体验事件中进行。

要对批处理进行修补，需要满足以下条件：

- **为配置文件和属性更新启用的数据集。** 这可通过数据集标记完成，并且需要 `isUpsert:true` 标记 `unifiedProfile` 数组。 有关如何创建数据集或配置现有数据集以进行升级的详细信息步骤，请按照 [启用数据集以进行配置文件更新](../../catalog/datasets/enable-upsert.md).
- **Parquet文件，其中包含要修补的字段和配置文件的标识字段。** 为批处理打补丁的数据格式与常规的批处理摄取过程类似。 所需的输入是Parquet文件，除了要更新的字段外，上传的数据还必须包含标识字段，才能匹配用户档案存储中的数据。

在为Profile和Upsert启用了数据集，并且添加了Parquet文件（其中包含您要修补的字段以及必要的标识字段）后，您可以按照 [摄取Parquet文件](#ingest-parquet-files) 以便通过批量摄取完成修补程序。

## 重播批处理

如果要替换已摄取的批处理，可以通过“批重播”执行此操作 — 此操作等同于删除旧批处理并摄取新批处理。

### 创建批处理

首先，您需要创建一个以JSON作为输入格式的批处理。 创建批处理时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的XDM架构。 此外，您还需要在重播部分中提供旧批次作为引用。 在以下示例中，您正在重播具有ID的批次 `batchIdA` 和 `batchIdB`.

**API格式**

```http
POST /batches
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| 参数 | 描述 |
| --------- | ----------- | 
| `{DATASET_ID}` | 引用数据集的ID。 |

**响应**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批处理的ID。 |
| `{DATASET_ID}` | 引用的数据集的ID。 |
| `{USER_ID}` | 创建批处理的用户ID。 |


### 上传文件

现在，您已创建批处理，接下来可以使用 `batchId` 从之前将文件上传到批处理。 您可以将多个文件上传到批。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批处理的ID。 |
| `{DATASET_ID}` | 批次引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 确保使用唯一的文件名，使其与正在提交的批量文件的其他文件不冲突。 |

**请求**

>[!CAUTION]
>
>此API支持单步上传。 确保content-type为application/八位字节流。 请勿使用curl -F选项，因为它默认为与API不兼容的多部分请求。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如 `acme/customers/campaigns/summer.json`. |

**响应**

```http
200 OK
```

### 完成批次

上传完文件的所有不同部分后，您将需要发出数据已完全上传以及批处理已准备好升级的信号。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要完成的批次的ID。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```http
200 OK
```

## 附录

以下部分包含有关使用批量摄取在Experience Platform中摄取数据的其他信息。

### 用于批量摄取的数据转换

要将数据文件摄取到 [!DNL Experience Platform]，文件的层次结构必须符合 [体验数据模型(XDM)](../../xdm/home.md) 与上传到的数据集关联的架构。

有关如何映射CSV文件以符合XDM架构的信息，请参阅 [示例转换](../../etl/transformations.md) 文档，以及格式正确的JSON数据文件的示例。 文档中提供的示例文件可在此处找到：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
