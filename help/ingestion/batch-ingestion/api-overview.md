---
keywords: Experience Platform；主页；热门主题；批量摄取；批量摄取；开发人员指南；API指南；上传；摄取Parquet；摄取json;
solution: Experience Platform
title: 批量摄取API指南
topic-legacy: developer guide
description: 本文档全面概述了使用批量摄取API。
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '2552'
ht-degree: 6%

---

# 批量摄取API指南

本文档全面概述了如何使用[批量摄取API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)。

本文档的附录提供了用于摄取](#data-transformation-for-batch-ingestion)的[格式化数据的信息，包括示例CSV和JSON数据文件。

## 快速入门

数据摄取提供了一个RESTful API，通过该API，您可以对支持的对象类型执行基本的CRUD操作。

以下部分提供了为成功调用批量摄取API而需要了解或掌握的其他信息。

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [批量摄取](./overview.md):允许您将数据作为批处理文件导入到Adobe Experience Platform中。
- [[!DNL Experience Data Model (XDM)] 系统](../../xdm/home.md):用于组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源均与特定虚拟沙箱隔离。 对[!DNL Platform] API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

包含有效负载(POST、PUT、PATCH)的请求可能需要额外的`Content-Type`标头。 每个调用的接受值都在调用参数中提供。

## 类型

在摄取数据时，务必要了解[!DNL Experience Data Model](XDM)模式的工作方式。 有关XDM字段类型如何映射到不同格式的更多信息，请阅读[架构注册开发人员指南](../../xdm/api/getting-started.md)。

在摄取数据时具有一定的灵活性 — 如果类型与目标架构中的内容不匹配，则数据将转换为表示的目标类型。 如果不能，则使用`TypeCompatibilityException`的批处理将失败。

例如，JSON和CSV都没有日期或日期时间类型。 因此，这些值使用[ISO 8061格式化字符串](https://www.iso.org/iso-8601-date-and-time-format.html)(&quot;2018-07-10T15:05:59.000-08:00&quot;)或Unix时间（以毫秒为单位）格式化，并在摄取时转换为目标XDM类型。

下表显示了摄取数据时支持的转化。

| 入站（行）与目标（列） | 字符串 | 字节 | 短 | 整数 | 长 | 双精度 | 日期 | Date-Time | 对象 | 地图 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 字符串 | X | X | X | X | X | X | X | X |  |  |
| 字节 | X | X | X | X | X | X |  |  |  |  |
| 短 | X | X | X | X | X | X |  |  |  |  |
| 整数 | X | X | X | X | X | X |  |  |  |  |
| 长 | X | X | X | X | X | X | X | X |  |  |
| 双精度 | X | X | X | X | X | X |  |  |  |  |
| 日期 |  |  |  |  |  |  | X |  |  |  |
| Date-Time |  |  |  |  |  |  |  | X |  |  |
| 对象 |  |  |  |  |  |  |  |  | X | X |
| 地图 |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>布尔值和数组无法转换为其他类型。

## 摄取约束

批量数据摄取具有一些限制：
- 每批文件的最大数量：1500
- 最大批次大小：100 GB
- 每行属性或字段的最大数量：10000
- 每个用户每分钟的最大批数：138

## 摄取JSON文件

>[!NOTE]
>
>以下步骤适用于小文件（256 MB或更小）。 如果遇到网关超时或请求正文大小错误，则需要切换到大文件上传。

### 创建批处理

首先，您需要创建一个以JSON作为输入格式的批处理。 创建批处理时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的XDM架构。

>[!NOTE]
>
>以下示例适用于单行JSON。 要摄取多行JSON，需要设置`isMultiLineJson`标记。 有关更多信息，请阅读[批量摄取疑难解答指南](./troubleshooting.md)。

**API格式**

```http
POST /batches
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
    "imsOrg": "{IMS_ORG}",
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

现在，您已创建批处理，接下来可以使用之前的`batchId`将文件上传到该批处理。 您可以将多个文件上传到批。

>[!NOTE]
>
>有关格式正确的JSON数据文件](#data-transformation-for-batch-ingestion)的示例，请参阅附录部分。[

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批处理的ID。 |
| `{DATASET_ID}` | 批次引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 此文件路径是文件在Adobe端保存的位置。 |

**请求**

>[!NOTE]
>
>API支持单步上传。 确保content-type为application/八位字节流。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如`Users/sample-user/Downloads/sample.json`。 |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```http
200 OK
```

## 摄取Parquet文件

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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
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
    "imsOrg": "{IMS_ORG}",
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

现在，您已创建批处理，接下来可以使用之前的`batchId`将文件上传到该批处理。 您可以将多个文件上传到批。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批处理的ID。 |
| `{DATASET_ID}` | 批次引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 此文件路径是文件在Adobe端保存的位置。 |

**请求**

>[!CAUTION]
>
>此API支持单步上传。 确保content-type为application/八位字节流。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如`Users/sample-user/Downloads/sample.json`。 |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
    "imsOrg": "{IMS_ORG}",
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{FILE_NAME}` | 要上传的文件的名称。 此文件路径是文件在Adobe端保存的位置。 |

**请求**

>[!CAUTION]
>
>此API支持单步上传。 确保content-type为application/八位字节流。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONTENT_RANGE}` | 在整数中，请求范围的开头和结尾。 |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如`Users/sample-user/Downloads/sample.json`。 |


**响应**

```http
200 OK
```

### 完整大文件

现在，您已创建批处理，接下来可以使用之前的`batchId`将文件上传到该批处理。 您可以将多个文件上传到批。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 摄取CSV文件

要摄取CSV文件，您需要创建一个支持CSV的类、架构和数据集。 有关如何创建必需类和模式的详细信息，请按照[ad-hoc模式创建教程](../../xdm/api/ad-hoc.md)中提供的说明进行操作。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
    "imsOrg": "{IMS_ORG}",
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

现在，您已创建批处理，接下来可以使用之前的`batchId`将文件上传到该批处理。 您可以将多个文件上传到批。

>[!NOTE]
>
>有关格式正确的CSV数据文件](#data-transformation-for-batch-ingestion)的示例，请参阅附录部分。[

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批处理的ID。 |
| `{DATASET_ID}` | 批次引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 此文件路径是文件在Adobe端保存的位置。 |

**请求**

>[!CAUTION]
>
>此API支持单步上传。 确保content-type为application/八位字节流。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如`Users/sample-user/Downloads/sample.json`。 |


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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 删除批处理 {#delete-a-batch}

可以通过对要删除的批的ID执行以下POST请求（使用`action=REVERT`查询参数）来删除批。 该批标记为“不活动”，以便符合垃圾收集的条件。 将异步收集该批次，届时该批次将标记为“已删除”。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 重播批处理

如果要替换已摄取的批处理，可以通过“批重播”执行此操作 — 此操作等同于删除旧批处理并摄取新批处理。

### 创建批处理

首先，您需要创建一个以JSON作为输入格式的批处理。 创建批处理时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的XDM架构。 此外，您还需要在重播部分中提供旧批次作为引用。 在以下示例中，您正在重播ID为`batchIdA`和`batchIdB`的批次。

**API格式**

```http
POST /batches
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
    "imsOrg": "{IMS_ORG}",
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

现在，您已创建批处理，接下来可以使用之前的`batchId`将文件上传到该批处理。 您可以将多个文件上传到批。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批处理的ID。 |
| `{DATASET_ID}` | 批次引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 此文件路径是文件在Adobe端保存的位置。 |

**请求**

>[!CAUTION]
>
>此API支持单步上传。 确保content-type为application/八位字节流。 请勿使用curl -F选项，因为它默认为与API不兼容的多部分请求。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如`Users/sample-user/Downloads/sample.json`。 |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```http
200 OK
```

## 附录

### 用于批量摄取的数据转换

要将数据文件摄取到[!DNL Experience Platform]中，文件的层次结构必须符合与上传到的数据集关联的[体验数据模型(XDM)](../../xdm/home.md)架构。

有关如何映射CSV文件以符合XDM架构的信息，请参阅[示例转换](../../etl/transformations.md)文档，以及格式正确的JSON数据文件的示例。 文档中提供的示例文件可在此处找到：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
