---
keywords: Experience Platform；主页；热门主题；数据访问；python sdk；spark sdk；数据访问api；导出；导出
solution: Experience Platform
title: Data Access API指南
description: 数据访问API通过为开发人员提供RESTful接口来支持Adobe Experience Platform，该接口侧重于在Experience Platform中摄取的数据集的可发现性和可访问性。
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 78dbb735bad70e2115cbbaabb6cf74bf38983460
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 4%

---

# Data Access API指南

>[!IMPORTANT]
>
>数据访问API现在&#x200B;**已弃用**。 建议使用目标从Adobe Experience Platform导出数据。 有关详细信息，请参阅[数据集导出目标文档](../destinations/destination-types.md#dataset-export-destinations)。

数据访问API通过向用户提供侧重于在[!DNL Experience Platform]内摄取的数据集的可发现性和可访问性的RESTful接口来支持Adobe Experience Platform。

![数据访问如何促进Experience Platform中已摄取数据集的可发现性和可访问性的图表。](images/Data_Access_Experience_Platform.png)

## API规范参考

请参阅[数据访问OpenAPI参考文档](https://developer.adobe.com/experience-platform-apis/references/data-access/)，查看易于集成、测试和探索的机器可读的标准化格式。

## 术语 {#terminology}

该表提供了本文档中常用的一些术语的说明。

| 搜索词 | 描述 |
| ----- | ------------ |
| 数据集 | 包含架构和字段的数据集合。 |
| 批次 | 一段时间内收集的一组数据，并作为一个单元一起处理。 |

## 检索批次中的文件列表 {#retrieve-list-of-files-in-a-batch}

要检索属于特定批次的文件列表，请将批次标识符(batchID)与数据访问API一起使用。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 指定批次的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
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
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

`"data"`数组包含指定批次中所有文件的列表。 返回的每个文件都有其自己的唯一ID (`{FILE_ID}`)，该ID包含在`"dataSetFileId"`字段中。 您可以使用此唯一ID来访问或下载文件。

| 属性 | 描述 |
| -------- | ----------- |
| `data.dataSetFileId` | 指定批次中每个文件的文件ID。 |
| `data._links.self.href` | 用于访问文件的url。 |

## 访问和下载批量文件

要访问文件的特定详细信息，请将文件标识符(`{FILE_ID}`)与数据访问API一起使用，包括其名称、字节大小以及要下载的链接。

响应包含数据数组。 根据ID指向的文件是单个文件还是目录，返回的数据阵列可能包含单个条目或属于该目录的文件列表。 每个文件元素都包含文件的详细信息。

**API格式**

```http
GET /files/{FILE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 等于`"dataSetFileId"`，即要访问的文件的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**单个文件响应**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
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
| `data.name` | 文件的名称（例如，`profiles.parquet`）。 |
| `data.length` | 文件的大小（以字节为单位）。 |
| `data._links.self.href` | 用于下载文件的URL。 |

**目录响应**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
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

当返回目录时，它包含目录中所有文件的数组。

| 属性 | 描述 |
| -------- | ----------- |
| `data.name` | 文件的名称（例如，`profiles.parquet`）。 |
| `data._links.self.href` | 用于下载文件的URL。 |

## 访问文件的内容 {#access-file-contents}

您还可以使用[!DNL Data Access] API访问文件的内容。 然后，您可以将内容下载到外部源。

**API格式**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_NAME}` | 尝试访问的文件的名称。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 数据集内文件的ID。 |
| `{FILE_NAME}` | 文件的全名（例如，`profiles.parquet`）。 |

**响应**

`Contents of the file`

## 其他代码示例

有关其他示例，请参阅[数据访问教程](tutorials/dataset-data.md)。

## 订阅数据摄取事件 {#subscribe-to-data-ingestion-events}

您可以通过[Adobe Developer Console](https://developer.adobe.com/console/)订阅特定的高价值事件。 例如，您可以订阅数据摄取事件，以接收潜在延迟和失败的通知。 有关详细信息，请参阅有关[订阅Adobe事件通知](../observability/alerts/subscribe.md)的教程。
