---
keywords: Experience Platform；主页；热门主题；数据访问；数据访问API；查询数据访问
solution: Experience Platform
title: 使用数据访问API查看数据集数据
type: Tutorial
description: 了解如何使用Adobe Experience Platform中的数据访问API查找、访问和下载存储在数据集中的数据。 本文档介绍数据访问API的一些独特功能，例如分页和部分下载。
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 9%

---

# 使用[!DNL Data Access] API查看数据集数据

使用本分步教程了解如何使用Adobe Experience Platform中的[!DNL Data Access] API查找、访问和下载存储在数据集中的数据。 本文档介绍[!DNL Data Access] API的一些独特功能，例如分页和部分下载。

## 快速入门

本教程需要对如何创建和填充数据集有一定的了解。 有关详细信息，请参阅[数据集创建教程](../../catalog/datasets/create.md)。

以下部分提供了成功调用Experience Platform API时需要了解的其他信息。

### 正在读取示例 API 调用 {#reading-sample-api-calls}

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例 API 调用的文档中所用惯例的信息，请参阅故障排除指南中的[如何读取示例 API 调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) [!DNL Experience Platform]。

### 收集所需标头的值

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](../../landing/api-authentication.md)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- 授权：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，该标头指定执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

- Content-Type： application/json

## 序列图

本教程遵循以下顺序图中所列的步骤，其中重点介绍了[!DNL Data Access] API的核心功能。

![数据访问API核心功能的顺序图。](../images/sequence_diagram.png)

要检索有关批次和文件的信息，请使用[!DNL Catalog] API。 要通过HTTP访问和下载这些文件，或者完全下载，或者部分下载，具体取决于文件的大小，请使用[!DNL Data Access] API。

## 查找数据

在开始使用[!DNL Data Access] API之前，您必须确定要访问的数据的位置。 在[!DNL Catalog] API中，有两个端点可用于浏览组织的元数据并检索要访问的批次或文件的ID：

- `GET /batches`：返回组织下的批次列表
- `GET /dataSetFiles`：返回组织下的文件列表

有关[!DNL Catalog] API中端点的完整列表，请参阅[API引用](https://developer.adobe.com/experience-platform-apis/references/catalog/)。

## 检索组织内的批次列表

使用[!DNL Catalog] API，您可以返回组织下的批次列表：

**API格式**

```http
GET /batches
```

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包括一个对象，该对象列出与组织相关的所有批次，每个顶级值表示一个批次。 单个批次对象包含该特定批次的详细信息。 下面的响应已最小化，占用空间。

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### 筛选批次列表 {#filter-batches-list}

通常，需要过滤器来查找特定批次，以检索特定用例的相关数据。 可将参数添加到`GET /batches`请求以筛选返回的响应。 以下请求返回指定时间后在特定数据集中创建的所有批次，按其创建时间排序。

**API格式**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{START_TIMESTAMP}` | 开始时间戳，以毫秒为单位(例如，1514836799000)。 |
| `{DATASET_ID}` | 数据集标识符。 |
| `{SORT_BY}` | 按提供的值对响应进行排序。 例如，`desc:created`按创建日期降序排列对象。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{ORG_ID}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

可在[目录API引用](https://developer.adobe.com/experience-platform-apis/references/catalog/)中找到参数和筛选器的完整列表。

## 检索属于特定批次的所有文件的列表

现在您有了要访问的批次的ID，可以使用[!DNL Data Access] API获取属于该批次的文件的列表。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 尝试访问的批次的批次标识符。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `data._links.self.href` | 用于访问此文件的URL。 |

响应包含一个数据数组，其中列出了指定批次中的所有文件。 文件通过其文件ID引用，该文件位于`dataSetFileId`字段下。

## 使用文件ID访问文件 {#access-file-with-file-id}

一旦您拥有了唯一的文件ID，您就可以使用[!DNL Data Access] API访问有关文件的特定详细信息，包括其名称、大小（字节）和下载链接。

**API格式**

```http
GET /files/{FILE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 要访问的文件的标识符。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

根据文件ID指向单个文件或目录，返回的数据阵列可能包含单个条目或属于该目录的文件列表。 每个文件元素都包含详细信息，例如文件名、字节大小以及用于下载文件的链接。

**案例1：文件ID指向单个文件**

**响应**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | 文件的名称。 |
| `_links.self.href` | 用于下载文件的URL。 |

**案例2：文件ID指向目录**

**响应**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

| 属性 | 描述 |
| -------- | ----------- | 
| `data._links.self.href` | 用于下载关联文件的URL。 |

此响应返回包含两个单独文件的目录，ID为`{FILE_ID_2}`和`{FILE_ID_3}`。 在此方案中，必须遵循每个文件的URL才能访问该文件。

## 检索文件的元数据

您可以通过发出HEAD请求来检索文件的元数据。 这将返回文件的元数据标头，包括其大小（以字节和文件格式表示）。

**API格式**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 文件的标识符。 |
| `{FILE_NAME}` | 文件名（例如，profiles.parquet） |

**请求**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应标头包含查询文件的元数据，包括：

- `Content-Length`：指示有效负载的大小（以字节为单位）
- `Content-Type`：指示文件的类型。

## 访问文件的内容

您还可以使用[!DNL Data Access] API访问文件的内容。

**API格式**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 文件的标识符。 |
| `{FILE_NAME}` | 文件名（例如，profiles.parquet）。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回文件的内容。

## 下载文件的部分内容 {#download-partial-file-contents}

要从文件下载特定范围的字节，请在`GET /files/{FILE_ID}`请求[!DNL Data Access] API期间指定范围标头。 如果未指定范围，默认情况下，API会下载整个文件。

[上一节](#retrieve-the-metadata-of-a-file)中的HEAD示例给出了特定文件的大小（以字节为单位）。

**API格式**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 文件的标识符。 |
| `{FILE_NAME}` | 文件名（例如，profiles.parquet） |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| 属性 | 描述 |
| -------- | ----------- | 
| `Range: bytes=0-99` | 指定要下载的字节范围。 如果未指定，则API下载整个文件。 在此示例中，下载前100个字节。 |

**响应**

响应正文包括文件的前100个字节（由请求中的“Range”标头指定）以及HTTP状态206（部分内容）。 响应还包括以下标头：

- Content-Length： 100（返回的字节数）
- Content-type： application/parquet （请求了Parquet文件，因此响应内容类型为`parquet`）
- Content-Range：字节0-99/249058(请求的范围(0-99)，总字节数(249058))

## 配置API响应分页 {#configure-response-pagination}

[!DNL Data Access] API中的响应将分页。 默认情况下，每页的最大条目数为100。 您可以使用分页参数修改缺省行为。

- `limit`：您可以使用“limit”参数，根据自己的要求指定每页的条目数。
- `start`：偏移量可由“start”查询参数设置。
- `&`：您可以使用&amp;符号在单个调用中组合多个参数。

**API格式**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 尝试访问的批次的批次标识符。 |
| `{OFFSET}` | 用于启动结果数组的指定索引（例如，start=0） |
| `{LIMIT}` | 控制结果数组中返回的结果数量（例如，limit=1） |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**：

响应包含具有单个元素的`"data"`数组，如请求参数`limit=1`所指定。 此元素是一个对象，其中包含第一个可用文件的详细信息，如请求中的`start=0`参数所指定（请记住，在从零开始的编号中，第一个元素为“0”）。

`_links.next.href`值包含指向下一页响应的链接，您可以在该页中看到`start`参数已前进到`start=1`。

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```
