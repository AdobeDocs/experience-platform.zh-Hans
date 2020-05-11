---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据访问概述
topic: overview
translation-type: tm+mt
source-git-commit: d9aa21a7439a6c40f6f51dfbdf5c7b3690c4593a
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 4%

---


# 数据访问概述

Data Access API为用户提供RESTful界面，侧重于Experience Platform内所摄取数据集的可发现性和可访问性，从而支持Adobe Experience Platform。

![体验平台上的数据访问](images/Data_Access_Experience_Platform.png)

## API规范参考

Swagger API参考文档可在此处 [找到](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)。

## 术语

本文档中一些常用术语的说明。

| 搜索词 | 描述 |
| ----- | ------------ |
| 数据集 | 包含模式和字段的数据集合。 |
| 批 | 在一段时间内收集的一组数据，并作为单个单元一起处理。 |

## 检索批中文件的列表

通过使用批处理标识符(batchID)，数据访问API可以检索属于该特定批处理的一列表文件。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 指定批的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
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

数 `"data"` 组包含指定批次中所有文件的列表。 返回的每个文件在字段中都包`{FILE_ID}`含其自己的唯一 `"dataSetFileId"` ID()。 此唯一ID随后可用于访问或下载文件。

| 属性 | 描述 |
| -------- | ----------- |
| `data.dataSetFileId` | 指定批次中每个文件的文件ID。 |
| `data._links.self.href` | 访问文件的url。 |

## 批量访问和下载文件

通过使用文件标`{FILE_ID}`识符()，数据访问API可用于访问文件的特定详细信息，包括文件名称、大小（以字节为单位）和要下载的链接。

响应将包含一个数据数组。 根据ID所指向的文件是单个文件还是目录，返回的数据数组可能包含属于该目录的单个条目或一列表文件。 每个文件元素都将包含文件的详细信息。

**API格式**

```http
GET /files/{FILE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 与要访 `"dataSetFileId"`问的文件的ID相等。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `data.name` | 文件的名称(例如用户档案.csv)。 |
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

返回目录时，它包含该目录内所有文件的数组。

| 属性 | 描述 |
| -------- | ----------- |
| `data.name` | 文件的名称(例如用户档案.csv)。 |
| `data._links.self.href` | 用于下载文件的URL。 |

## 访问文件内容

数据访问API还可用于访问文件的内容。 然后，这可用于将内容下载到外部源。

**API格式**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_NAME}` | 您尝试访问的文件的名称。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 数据集中文件的ID。 |
| `{FILE_NAME}` | 文件的完整名称(例如用户档案.csv)。 |

**响应**

```
Contents of the file
```

## 其他代码范例

有关其他示例，请参阅数 [据访问教程](tutorials/dataset-data.md)。

## 订阅数据获取事件

平台通过Adobe开发人员控制台提供特定的高价 [值事件供订阅](https://www.adobe.com/go/devs_console_ui)。 例如，您可以订阅数据获取事件，以便收到潜在延迟和故障的通知。 有关详细信息，请 [参阅有关订阅数据获取通知](../ingestion/quality/subscribe-events.md) 的教程。