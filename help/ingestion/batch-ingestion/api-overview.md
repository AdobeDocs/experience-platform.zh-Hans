---
keywords: Experience Platform；主页；热门主题；批量摄取；批量摄取；开发人员指南；API指南；上传；摄取Parquet；摄取json；
solution: Experience Platform
title: 批量摄取API指南
description: 本文档为使用Adobe Experience Platform批量摄取API的开发人员提供了全面的指南。
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 4%

---

# 批量摄取开发人员指南

本文档提供了全面的使用指南 [批量摄取API端点](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) 在Adobe Experience Platform中。 有关批量摄取API的概述，包括先决条件和最佳实践，请从阅读 [批量摄取API概述](overview.md).

本文档的附录提供了 [设置用于摄取的数据格式](#data-transformation-for-batch-ingestion)，包括示例CSV和JSON数据文件。

## 快速入门

本指南中使用的API端点是 [批量摄取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). 通过RESTful API提供批量摄取，您可以在其中对支持的对象类型执行基本CRUD操作。

在继续之前，请查看 [批量摄取API概述](overview.md) 和 [快速入门指南](getting-started.md).

## 摄取JSON文件

>[!NOTE]
>
>以下步骤适用于小文件（256 MB或更小）。 如果遇到网关超时或请求正文大小错误，则需要切换到大型文件上传。

### 创建批次

首先，您需要创建一个批次，以JSON作为输入格式。 创建批次时，您需要提供数据集ID。 您还需要确保作为批次的一部分上传的所有文件符合链接到所提供数据集的XDM架构。

>[!NOTE]
>
>以下示例适用于单行JSON。 要摄取多行JSON，请 `isMultiLineJson` 需要设置标志。 欲知更多信息，请阅读 [批量摄取疑难解答指南](./troubleshooting.md).

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
| `{BATCH_ID}` | 新创建的批次的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |

### 上传文件

现在您已经创建了批次，可以使用批次创建响应中的批次ID将文件上传到批次。 您可以将多个文件上载到批处理。

>[!NOTE]
>
>请参阅附录部分，了解 [格式正确的JSON数据文件示例](#data-transformation-for-batch-ingestion).

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批次的ID。 |
| `{DATASET_ID}` | 批次的引用数据集的ID。 |
| `{FILE_NAME}` | 要上载的文件的名称。 确保使用唯一的文件名，以便它不会与要提交的批量文件的另一个文件冲突。 |

**请求**

>[!NOTE]
>
>API支持单部分上传。 确保内容类型为application/octet-stream。

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
| `{FILE_PATH_AND_NAME}` | 尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，例如 `acme/customers/campaigns/summer.json`. |

**响应**

```http
200 OK
```

### 完成批处理

上传完文件的所有不同部分后，您需要表明数据已完全上传，并且批次已准备好进行升级。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批次的ID。 |

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
>以下步骤适用于小文件（256 MB或更小）。 如果遇到网关超时或请求正文大小错误，则需要切换到大型文件上传。

### 创建批次

首先，需要创建一个批次，以Parquet作为输入格式。 创建批次时，您需要提供数据集ID。 您还需要确保作为批次的一部分上传的所有文件符合链接到所提供数据集的XDM架构。

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
| `{BATCH_ID}` | 新创建的批次的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |
| `{USER_ID}` | 创建批次的用户的ID。 |

### 上传文件

现在您已经创建了批次，接下来可以使用 `batchId` 从之前将文件上传到批处理。 您可以将多个文件上载到批处理。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批次的ID。 |
| `{DATASET_ID}` | 批次的引用数据集的ID。 |
| `{FILE_NAME}` | 要上载的文件的名称。 确保使用唯一的文件名，以便它不会与要提交的批量文件的另一个文件冲突。 |

**请求**

>[!CAUTION]
>
>此API支持单部分上传。 确保内容类型为application/octet-stream。

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
| `{FILE_PATH_AND_NAME}` | 尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，例如 `acme/customers/campaigns/summer.parquet`. |

**响应**

```http
200 OK
```

### 完成批处理

上传完文件的所有不同部分后，您需要表明数据已完全上传，并且批次已准备好进行升级。

**API格式**

```http
POST /batches/{BATCH_ID}?action=complete
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要发出信号的批次ID已准备好完成。 |

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

## 摄取大型Parquet文件

>[!NOTE]
>
>本节详细介绍如何上载大于256 MB的文件。 将大文件上传为块，然后通过API信号拼合。

### 创建批次

首先，需要创建一个批次，以Parquet作为输入格式。 创建批次时，您需要提供数据集ID。 您还需要确保作为批次的一部分上传的所有文件符合链接到所提供数据集的XDM架构。

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
| `{BATCH_ID}` | 新创建的批次的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |
| `{USER_ID}` | 创建批次的用户的ID。 |

### 初始化大文件

创建批次后，您需要先初始化大文件，然后再将块上传到批次。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建的批次的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |
| `{FILE_NAME}` | 即将初始化的文件的名称。 |

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

### 上载大文件块

现在文件已创建，可以通过重复的PATCH请求（文件的每个部分各一个）上传所有后续块。

**API格式**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批次的ID。 |
| `{DATASET_ID}` | 批次的引用数据集的ID。 |
| `{FILE_NAME}` | 要上载的文件的名称。 确保使用唯一的文件名，以便它不会与要提交的批量文件的另一个文件冲突。 |

**请求**

>[!CAUTION]
>
>此API支持单部分上传。 确保内容类型为application/octet-stream。

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
| `{CONTENT_RANGE}` | 在整数中，为请求范围的开始和结束。 |
| `{FILE_PATH_AND_NAME}` | 尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，例如 `acme/customers/campaigns/summer.json`. |


**响应**

```http
200 OK
```

### 完整的大文件

现在您已经创建了批次，接下来可以使用 `batchId` 从之前将文件上传到批处理。 您可以将多个文件上载到批处理。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要表示已完成的批次ID。 |
| `{DATASET_ID}` | 批次的引用数据集的ID。 |
| `{FILE_NAME}` | 要表示已完成的文件的名称。 |

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

### 完成批处理

上传完文件的所有不同部分后，您需要表明数据已完全上传，并且批次已准备好进行升级。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要发出信号的批次的ID已完成。 |


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

为了摄取CSV文件，您需要创建一个支持CSV的类、架构和数据集。 有关如何创建必要类和架构的详细信息，请按照 [临时架构创建教程](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>以下步骤适用于小文件（256 MB或更小）。 如果遇到网关超时或请求正文大小错误，则需要切换到大型文件上传。

### 创建数据集

按照上面的说明创建必要的类和架构后，您将需要创建可支持CSV的数据集。

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
| `{TENANT_ID}` | 此ID用于确保您创建的资源被正确命名并包含在您的组织中。 |
| `{SCHEMA_ID}` | 您已创建的架构的ID。 |

### 创建批次

接下来，您需要创建一个将CSV作为输入格式的批次。 创建批次时，您需要提供数据集ID。 您还需要确保作为批次的一部分上传的所有文件都符合链接到所提供数据集的架构。

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
| `{BATCH_ID}` | 新创建的批次的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |
| `{USER_ID}` | 创建批次的用户的ID。 |

### 上传文件

现在您已经创建了批次，接下来可以使用 `batchId` 从之前将文件上传到批处理。 您可以将多个文件上载到批处理。

>[!NOTE]
>
>请参阅附录部分，了解 [格式正确的CSV数据文件示例](#data-transformation-for-batch-ingestion).

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批次的ID。 |
| `{DATASET_ID}` | 批次的引用数据集的ID。 |
| `{FILE_NAME}` | 要上载的文件的名称。 确保使用唯一的文件名，以便它不会与要提交的批量文件的另一个文件冲突。 |

**请求**

>[!CAUTION]
>
>此API支持单部分上传。 确保内容类型为application/octet-stream。

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
| `{FILE_PATH_AND_NAME}` | 尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，例如 `acme/customers/campaigns/summer.csv`. |


**响应**

```http
200 OK
```

### 完成批处理

完成上载文件的所有不同部分后，您需要发出信号表明数据已完全上载，并且批次已准备好进行升级。

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

## 取消批次

在处理批次时，仍可取消它。 但是，一旦完成批处理（例如成功或失败状态），就无法取消批处理。

**API格式**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要取消的批次ID。 |

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

## 删除批次 {#delete-a-batch}

通过使用执行以下POST请求，可以删除批次 `action=REVERT` 查询要删除的批次ID的参数。 该批次被标记为“不活动”，因此可用于垃圾收集。 将异步收集批次，然后将其标记为“已删除”。

**API格式**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要删除的批次的ID。 |

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

## 修补批次

有时候，可能需要更新您组织的配置文件存储区中的数据。 例如，您可能需要更正记录或更改属性值。 Adobe Experience Platform支持通过更新插入操作或“修补批次”来更新或修补配置文件存储区数据。

>[!NOTE]
>
>这些更新仅允许在配置文件记录中进行，不允许在体验事件中进行。

要修补批次，需要满足以下条件：

- **为配置文件和属性更新启用的数据集。** 这是通过数据集标记完成的，需要特定 `isUpsert:true` 标签添加到 `unifiedProfile` 数组。 有关显示如何创建数据集或配置现有数据集进行更新插入的详细步骤，请阅读的教程 [为配置文件更新启用数据集](../../catalog/datasets/enable-upsert.md).
- **包含要修补的字段和配置文件的标识字段的Parquet文件。** 为批次打补丁的数据格式与常规批次摄取过程类似。 所需的输入是一个Parquet文件，除了要更新的字段外，上传的数据必须包含身份字段，以便与配置文件存储区中的数据匹配。

在为Profile和upsert启用了数据集，并且有一个Parquet文件包含要修补的字段以及必要的标识字段后，您可以执行以下步骤 [正在摄取Parquet文件](#ingest-parquet-files) 以通过批量摄取完成修补程序。

## 重播批次

如果要替换已摄取的批次，可以使用“批量重播”来执行此操作 — 此操作等同于删除旧批次并摄取新批次。

### 创建批次

首先，您需要创建一个批次，以JSON作为输入格式。 创建批次时，您需要提供数据集ID。 您还需要确保作为批次的一部分上传的所有文件符合链接到所提供数据集的XDM架构。 此外，您还需要提供旧批次作为重播部分中的引用。 在下面的示例中，您将使用ID重播批次 `batchIdA` 和 `batchIdB`.

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
| `{BATCH_ID}` | 新创建的批次的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |
| `{USER_ID}` | 创建批次的用户的ID。 |


### 上传文件

现在您已经创建了批次，接下来可以使用 `batchId` 从之前将文件上传到批处理。 您可以将多个文件上载到批处理。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批次的ID。 |
| `{DATASET_ID}` | 批次的引用数据集的ID。 |
| `{FILE_NAME}` | 要上载的文件的名称。 确保使用唯一的文件名，以便它不会与要提交的批量文件的另一个文件冲突。 |

**请求**

>[!CAUTION]
>
>此API支持单部分上传。 确保内容类型为application/octet-stream。 请勿使用curl -F选项，因为它默认为与API不兼容的多部分请求。

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
| `{FILE_PATH_AND_NAME}` | 尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，例如 `acme/customers/campaigns/summer.json`. |

**响应**

```http
200 OK
```

### 完成批处理

上传完文件的所有不同部分后，您需要表明数据已完全上传，并且批次已准备好进行升级。

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

### 批量摄取的数据转换

为了将数据文件摄取到 [!DNL Experience Platform]，文件的层次结构必须符合 [体验数据模型(XDM)](../../xdm/home.md) 与要上载到的数据集关联的架构。

有关如何映射CSV文件以符合XDM架构的信息，请参阅 [示例转换](../../etl/transformations.md) 文档，以及格式正确的JSON数据文件示例。 文档中提供的示例文件可在此处找到：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
