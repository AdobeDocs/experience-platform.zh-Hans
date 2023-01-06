---
keywords: Experience Platform；主页；热门主题；数据访问；数据访问API；查询数据访问
solution: Experience Platform
title: 使用数据访问API查看数据集数据
type: Tutorial
description: 了解如何使用Adobe Experience Platform中的数据访问API查找、访问和下载数据集中存储的数据。 此外，还将介绍数据访问API的一些独特功能，如分页和部分下载。
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 3%

---

# 使用查看数据集数据 [!DNL Data Access] API

本文档提供了分步教程，其中介绍了如何使用 [!DNL Data Access] Adobe Experience Platform中的API。 此外，您还将了解 [!DNL Data Access] API，例如分页和部分下载。

## 快速入门

本教程要求您对如何创建和填充数据集有一定的了解。 请参阅 [数据集创建教程](../../catalog/datasets/create.md) 以了解更多信息。

以下部分提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- Content-Type:application/json

## 序列图

本教程将遵循以下序列图中概述的步骤，其中重点介绍了 [!DNL Data Access] API。</br>
![](../images/sequence_diagram.png)

的 [!DNL Catalog] API允许您检索有关批次和文件的信息。 的 [!DNL Data Access] API允许您通过HTTP访问和下载这些文件，以执行完整或部分下载，具体取决于文件的大小。

## 查找数据

在开始使用 [!DNL Data Access] API中，您需要识别要访问的数据的位置。 在 [!DNL Catalog] API中，您可以使用两个端点来浏览组织的元数据并检索要访问的批处理或文件的ID:

- `GET /batches`:返回组织下的批列表
- `GET /dataSetFiles`:返回您组织下的文件列表

有关 [!DNL Catalog] API，请参阅 [API参考](https://www.adobe.io/experience-platform-apis/references/catalog/).

## 在IMS组织下检索批列表

使用 [!DNL Catalog] API中，您可以返回组织下的批列表：

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

响应包括一个对象，其中列出了与IMS组织相关的所有批次，每个顶级值代表一个批次。 单个批处理对象包含该特定批处理的详细信息。 对于空间，以下响应已最小化。

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

### 过滤批列表

筛选器通常需要查找特定批次，才能针对特定用例检索相关数据。 参数可以添加到 `GET /batches` 请求来筛选返回的响应。 以下请求将返回在指定时间后在特定数据集内创建的所有批次，这些批次在创建时按照创建时进行排序。

**API格式**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{START_TIMESTAMP}` | 以毫秒为单位的开始时间戳(例如，1514836799000)。 |
| `{DATASET_ID}` | 数据集标识符。 |
| `{SORT_BY}` | 按提供的值对响应进行排序。 例如， `desc:created` 按创建日期以降序方式对对象进行排序。 |

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

有关参数和过滤器的完整列表，请参阅 [目录API参考](https://www.adobe.io/experience-platform-apis/references/catalog/).

## 检索属于特定批次的所有文件的列表

现在，您已拥有要访问的批次ID，接下来可以使用 [!DNL Data Access] 用于获取属于该批次的文件列表的API。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 您尝试访问的批次的批次标识符。 |

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

响应包含一个数据数组，其中列出了指定批处理中的所有文件。 文件由其文件ID引用，该ID位于 `dataSetFileId` 字段。

## 使用文件ID访问文件

拥有唯一的文件ID后，您可以使用 [!DNL Data Access] 用于访问有关文件的特定详细信息的API，包括其名称、大小（以字节为单位）以及用于下载该文件的链接。

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

根据文件ID是指向单个文件还是目录，返回的数据数组可能包含一个条目或属于该目录的文件列表。 每个文件元素都将包含详细信息，如文件名、大小（以字节为单位）以及用于下载文件的链接。

**用例1:文件ID指向单个文件**

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

**用例2:文件ID指向目录**

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

此响应会返回一个包含两个单独文件(ID)的目录 `{FILE_ID_2}` 和 `{FILE_ID_3}`. 在此方案中，您需要遵循每个文件的URL才能访问该文件。

## 检索文件的元数据

您可以通过发出HEAD请求来检索文件的元数据。 这会返回文件的元数据标头，包括其大小（字节）和文件格式。

**API格式**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 文件的标识符。 |
| `{FILE_NAME}` | 文件名（例如profiles.parquet） |

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
- `Content-Length`:指示有效负载的大小（以字节为单位）
- `Content-Type`:指示文件的类型。

## 访问文件的内容

您还可以使用 [!DNL Data Access] API。

**API格式**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 文件的标识符。 |
| `{FILE_NAME}` | 文件名（例如profiles.parquet）。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回文件的内容。

## 下载文件的部分内容

的 [!DNL Data Access] API允许下载以块为单位的文件。 可以在 `GET /files/{FILE_ID}` 请求从文件下载特定范围的字节。 如果未指定范围，则API将默认下载整个文件。

中的HEAD示例 [上一部分](#retrieve-the-metadata-of-a-file) 指定特定文件的大小（以字节为单位）。

**API格式**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID} ` | 文件的标识符。 |
| `{FILE_NAME}` | 文件名（例如profiles.parquet） |

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
| `Range: bytes=0-99` | 指定要下载的字节范围。 如果未指定，则API将下载整个文件。 在本例中，将下载前100字节。 |

**响应**

响应主体包括文件的前100字节（由请求中的“范围”标头指定）和HTTP状态206（部分内容）。 响应还包括以下标头：

- Content-Length:100（返回的字节数）
- 内容类型：application/parquet(请求了Parquet文件，因此响应内容类型为 `parquet`)
- 内容范围：字节0-99/249058(请求的范围(0-99)，占字节总数(249058)

## 配置API响应分页

在 [!DNL Data Access] API已分页。 默认情况下，每页的最大条目数为100。 分页参数可用于修改默认行为。

- `limit`:您可以使用“limit”参数根据您的要求指定每页的条目数。
- `start`:偏移量可由“start”查询参数设置。
- `&`:您可以使用与号在单个调用中组合多个参数。

**API格式**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 您尝试访问的批次的批次标识符。 |
| `{OFFSET}` | 用于启动结果数组的指定索引（例如，start=0） |
| `{LIMIT}` | 控制在结果数组中返回多少个结果（例如，limit=1） |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**:

响应包含 `"data"` 数组，由请求参数指定 `limit=1`. 此元素是一个对象，其中包含由 `start=0` 参数（请记住，在从零开始的编号中，第一个元素为“0”）。

的 `_links.next.href` 值包含指向下一页响应的链接，您可以在该页面中看到 `start` 参数已高级为 `start=1`.

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
