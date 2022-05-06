---
keywords: Experience Platform；主页；热门主题；云存储；云存储
title: 使用流服务API浏览云存储文件夹
description: 本教程使用流程服务API来探索第三方云存储系统。
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

本教程提供了有关如何使用 [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API。

>[!NOTE]
>
>要浏览您的云存储，您必须已拥有云存储源的有效基连接ID。 如果您没有此ID，请参阅 [源概述](../../../home.md#cloud-storage) 有关可创建基本连接的云存储源列表。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../landing/api-guide.md).

## 浏览云存储文件夹

您可以通过向 [!DNL Flow Service] API，同时提供源的基本连接ID。

执行GET请求以浏览云存储时，必须包含下表中列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `objectType` | 要浏览的对象类型。 将此值设置为： <ul><li>`folder`:浏览特定目录</li><li>`root`:浏览根目录。</li></ul> |
| `object` | 仅当查看特定目录时，才需要此参数。 其值表示要浏览的目录的路径。 |


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

成功的响应会返回在查询目录中找到的文件和文件夹数组。 请注意 `path` 要上传的文件的属性，因为需要在下一步中提供该属性以检查其结构。

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

## Inspect文件结构

要从云存储中检查GET文件的结构，请在提供文件路径并键入作为查询参数时执行数据请求。

您可以在提供文件的路径和类型的同时，通过执行GET请求，从云存储源中检查数据文件的结构。 您还可以通过在查询参数中指定不同文件类型来检查不同的文件类型，例如CSV、TSV或压缩的JSON和分隔文件。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 云存储源连接器的连接ID。 |
| `{FILE_PATH}` | 要检查的文件的路径。 |
| `{FILE_TYPE}` | 文件的类型。 支持的文件类型包括：<ul><li>分隔</code>:分隔符分隔值。 DSV文件必须以逗号分隔。</li><li>JSON</code>:JavaScript对象表示法。 JSON文件必须符合XDM</li><li>镶木</code>:阿帕奇拼花。 Parquet文件必须符合XDM。</li></ul> |
| `{QUERY_PARAMS}` | 可用于筛选结果的可选查询参数。 请参阅 [查询参数](#query) 以了解更多信息。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回查询文件的结构，包括表名和数据类型。

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

的 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 支持使用查询参数来预览和检查不同的文件类型。

| 参数 | 描述 |
| --------- | ----------- |
| `columnDelimiter` | 指定为用于检查CSV或TSV文件的列分隔符的单个字符值。 如果未提供参数，则值默认为逗号 `(,)`. |
| `compressionType` | 预览压缩的分隔或JSON文件所需的查询参数。 支持的压缩文件包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## 后续步骤

通过阅读本教程，您探索了云存储系统，找到了要引入的文件的路径 [!DNL Platform]，并查看了其结构。 在下一个教程中，您可以在 [从云存储中收集数据并将其导入平台](../collect/cloud-storage.md).
