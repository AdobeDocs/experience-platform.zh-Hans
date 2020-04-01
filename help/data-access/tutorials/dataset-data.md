---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据访问概述
topic: tutorial
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# 使用Data Access API查询数据集数据

本文档提供了一个分步教程，其中涵盖如何使用Adobe Experience Platform中的Data Access API查找、访问和下载数据集中存储的数据。 您还将介绍Data Access API的一些独特功能，如分页和部分下载。

## 入门指南

本教程旨在了解如何创建和填充数据集。 有关详细 [信息，请参阅数据集创建教程](../../catalog/datasets/create.md) 。

以下各节提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：承载人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

## 序列图

本教程遵循以下序列图中概述的步骤，突出显示Data Access API的核心功能。</br>
![](../images/sequence_diagram.png)

Catalog API允许您检索有关批处理和文件的信息。 数据访问API允许您通过HTTP访问和下载这些文件，作为完整或部分下载，具体取决于文件的大小。

## 定位数据

在开始使用数据访问API之前，您需要先确定要访问的数据的位置。 在目录API中，您可以使用两个端点浏览组织的元数据并检索要访问的批处理或文件的ID:

- `GET /batches`:返回组织下的批列表
- `GET /dataSetFiles`:返回单位下的列表文件

有关目录API中端点的全面列表，请参阅 [API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

## 检索IMS组织下的批列表

使用目录API，您可以返回组织下的一列表批：

**API格式**

```http
GET /batches
```

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包括一个对象，该对象列表与IMS组织相关的所有批，每个顶级值表示一个批。 单个批处理对象包含该特定批处理的详细信息。 以下响应已最小化为空间。

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{IMS_ORG}",
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

### 筛选批列表

过滤器通常需要查找特定批次才能检索特定用例的相关数据。 可以将参数添加到请 `GET /batches` 求中以过滤返回的响应。 以下请求将返回在指定时间后创建的所有批，这些批在特定数据集中按创建时间排序。

**API格式**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{START_TIMESTAMP}` | 开始时间戳（以毫秒为单位）（例如，1514836799000）。 |
| `{DATASET_ID}` | 数据集标识符。 |
| `{SORT_BY}` | 按提供的值对响应进行排序。 例如，按 `desc:created` 创建日期以降序对对象排序。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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

可在目录API参考中找到参数和过滤器的完 [整列表](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

## 检索属于特定批次的所有文件的列表

现在，您拥有要访问的批次的ID，您可以使用数据访问API获取属于该批次的一列表文件。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 您尝试访问的批的批的批标识符。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `data._links.self.href` | 访问此文件的URL。 |

响应包含一个数据数组，它列表指定批次中的所有文件。 文件由其文件ID引用，该文件ID位于字段 `dataSetFileId` 下。

## 使用文件ID访问文件

获得唯一的文件ID后，您可以使用Data Access API访问有关该文件的特定详细信息，包括其名称、大小（以字节为单位）以及用于下载该文件的链接。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

根据文件ID指向单个文件还是目录，返回的数据数组可能包含属于该目录的单个条目或一列表文件。 每个文件元素都将包含详细信息，如文件名、大小（以字节为单位）以及用于下载文件的链接。

**案例1:文件ID指向单个文件**

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

**案例2:文件ID指向目录**

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

此响应返回一个包含两个单独文件（ID和）的 `{FILE_ID_2}` 目录 `{FILE_ID_3}`。 在此方案中，您需要按照每个文件的URL访问该文件。

## 检索文件的元数据

您可以通过发出HEAD请求来检索文件的元数据。 这将返回文件的元数据标题，包括其大小（以字节为单位）和文件格式。

**API格式**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 文件的标识符。 |
| `{FILE_NAME`} | 文件名(例如，用户档案.parce) |

**请求**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应标题包含查询的文件的元数据，包括：
- `Content-Length`:指示有效负荷的大小（以字节为单位）
- `Content-Type`:指示文件的类型。

## 访问文件内容

您还可以使用数据访问API访问文件的内容。

**API格式**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 文件的标识符。 |
| `{FILE_NAME`} | 文件名(例如，用户档案.parce)。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回文件的内容。

## 下载文件的部分内容

Data Access API允许以块为单位下载文件。 在请求从文件下载特定范围的字 `GET /files/{FILE_ID}` 节时，可以指定范围标题。 如果未指定范围，则默认情况下，API将下载整个文件。

上一节中的HEAD示 [例给出特定文件的大小](#retrieve-the-metadata-of-a-file) （以字节为单位）。

**API格式**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID} ` | 文件的标识符。 |
| `{FILE_NAME}` | 文件名(例如，用户档案.parce) |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| 属性 | 描述 |
| -------- | ----------- | 
| `Range: bytes=0-99` | 指定要下载的字节范围。 如果未指定，API将下载整个文件。 在此示例中，将下载前100字节。 |

**响应**

响应主体包括文件的前100字节（由请求中的“范围”标题指定）和HTTP状态206（部分内容）。 响应还包括以下标题：

- 内容长度：100（返回的字节数）
- 内容类型：application/parke（请求的是镶木文件，因此响应内容类型为镶木）
- 内容范围：字节0-99/249058(在总字节数中请求的范围(0-99)(249058))

## 配置API响应分页

数据访问API中的响应将分页。 默认情况下，每页最多可输入100个条目。 分页参数可用于修改默认行为。

- `limit`:您可以使用“limit”参数根据您的要求指定每页的条目数。
- `start`:偏移量可以由“开始”查询参数设置。
- `&`:您可以使用“和号”在单个调用中组合多个参数。

**API格式**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 您尝试访问的批的批的批标识符。 |
| `{OFFSET}` | 用于开始结果数组的指定索引(例如，开始=0) |
| `{LIMIT}` | 控制在结果数组中返回的结果数（例如，limit=1） |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**:

响应包含一个 `"data"` 具有单个元素的数组，由request参数指定 `limit=1`。 此元素是包含第一个可用文件的详细信息的对象，如请求中的参数所指定（请记住，在从零开始的编号中，第一个元素是“0”）。 `start=0`

该 `_links.next.href` 值包含指向下一页响应的链接，您可以在该页看到该参 `start` 数已高级到 `start=1`。

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
