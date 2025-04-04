---
keywords: Experience Platform；主页；热门主题；云存储；云存储
title: 使用流服务API浏览云存储文件夹
description: 本教程使用流服务API来探索第三方云存储系统。
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API浏览云存储文件夹

本教程提供了有关如何使用[[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API浏览和预览云存储的结构和内容的步骤。

>[!NOTE]
>
>要探索云存储，您必须已拥有云存储源的有效基本连接ID。 如果您没有此ID，请参阅[源概述](../../../home.md#cloud-storage)，以了解可创建基础连接的云存储源的列表。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../landing/api-guide.md)指南。

## 浏览您的云存储文件夹

您可以在提供源的基本连接ID的同时，通过向[!DNL Flow Service] API发出GET请求来检索有关云存储文件夹结构的信息。

执行GET请求以浏览云存储时，必须包括下表列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `objectType` | 您希望探索的对象类型。 将此值设置为： <ul><li>`folder`：浏览特定目录</li><li>`root`：浏览根目录。</li></ul> |
| `object` | 只有在查看特定目录时才需要此参数。 其值表示您希望浏览的目录的路径。 |


**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 云存储源的基本连接ID。 |
| `{PATH}` | 目录的路径。 |

**请求**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回在查询的目录中找到的文件和文件夹数组。 请记下希望上传的文件的`path`属性，因为您需要在下一步中提供该属性以检查其结构。

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## 检查文件的结构

要检查云存储中的数据文件结构，请在提供文件路径和类型作为查询参数的同时执行GET请求。

您可以通过在提供文件路径和类型的同时执行GET请求来检查云存储源中数据文件的结构。 您还可以检查不同的文件类型，如CSV、TSV或压缩JSON和分隔文件，方法是将其文件类型指定为查询参数的一部分。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&fileType=delimited&encoding=ISO-8859-1;
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 云存储源连接器的连接ID。 |
| `{FILE_PATH}` | 要检查的文件的路径。 |
| `{FILE_TYPE}` | 文件的类型。 支持的文件类型包括：<ul><li><code>已分隔</code>：以分隔符分隔的值。 DSV文件必须以逗号分隔。</li><li><code>JSON</code>：JavaScript对象表示法。 JSON文件必须符合XDM</li><li><code>PARQUET</code>：Apache Parquet。 Parquet文件必须符合XDM。</li></ul> |
| `{QUERY_PARAMS}` | 可用于筛选结果的可选查询参数。 有关详细信息，请参阅[查询参数](#query)上的部分。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回查询文件的结构，包括表名和数据类型。

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## 使用查询参数 {#query}

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)支持使用查询参数预览和检查不同的文件类型。

| 参数 | 描述 |
| --------- | ----------- |
| `columnDelimiter` | 指定为列分隔符以检查CSV或TSV文件的单个字符值。 如果未提供该参数，则值默认为逗号`(,)`。 |
| `compressionType` | 预览压缩的分隔文件或JSON文件所需的查询参数。 支持的压缩文件包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | 定义在呈现预览时使用的编码类型。 支持的编码类型为： `UTF-8`和`ISO-8859-1`。 **注意**： `encoding`参数仅在摄取分隔的CSV文件时可用。 将使用默认编码`UTF-8`摄取其他文件类型。 |

## 后续步骤

通过完成本教程，您已探索云存储系统，找到要引入[!DNL Experience Platform]的文件的路径，并查看其结构。 您可以在下一个教程中使用此信息从云存储中[收集数据并将其引入Experience Platform](../collect/cloud-storage.md)。
