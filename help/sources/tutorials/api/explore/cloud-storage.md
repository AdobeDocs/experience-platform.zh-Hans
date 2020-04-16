---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API浏览云存储系统
topic: overview
translation-type: tm+mt
source-git-commit: 7cd9bec7336d0e1d9f3036cf862633f498002af8

---


# 使用Flow Service API浏览云存储系统

Flow Service用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API探索第三方云存储系统。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用流服务API成功连接到云存储系统。

### 获取基本连接

要使用Platform API探索第三方云存储，您必须拥有有效的基本连接ID。 如果您还没有要处理的存储的基本连接，则可以通过以下教程创建一个：

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azure Data Lake Gen2存储](../create/cloud-storage/adls-gen2.md)
* [Google Cloud商店](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于Flow Service的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标题：

* 内容类型： `application/json`

## 浏览您的云存储

使用云存储的基本连接，您可以通过执行GET请求来浏览文件和目录。 在执行GET请求以浏览您的云存储时，必须包括下表中列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `objectType` | 要浏览的对象类型。 将此值设置为： <ul><li>`folder`:浏览特定目录</li><li>`root`:浏览根目录。</li></ul> |
| `object` | 此参数仅在查看特定目录时才是必需的。 其值表示要浏览的目录的路径。 |

使用以下调用查找要引入平台的文件的路径：

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 云存储基础连接的ID。 |
| `{PATH}` | 目录的路径。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回在查询的目录中找到的一组文件和文件夹。 请注意您希 `path` 望上传的文件的属性，因为您需要在下一步中提供该属性以检查其结构。

```json
[
    {
        "type": "File",
        "name": "data.csv",
        "path": "/some/path/data.csv"
    },
    {
        "type": "Folder",
        "name": "foobar",
        "path": "/some/path/foobar"
    }
]
```

## 检查文件的结构

要从云存储检查数据文件的结构，请在提供文件路径作为查询参数时执行GET请求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 云存储基础连接的ID。 |
| `{FILE_PATH}` | 文件路径。 |
| `{FILE_TYPE}` | 文件的类型。 支持的文件类型包括：<ul><li>分隔</code>:分隔符分隔的值。 DSV文件必须以逗号分隔。</li><li>JSON</code>:JavaScript对象表示法。 JSON文件必须符合XDM规范</li><li>镶木</code>:阿帕奇拼花。 拼花文件必须符合XDM规范。</li></ul> |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回所查询文件的结构，包括表名和数据类型。

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

## 后续步骤

通过本教程，您探索了您的云存储系统，找到了要导入平台的文件的路径，并查看了其结构。 您可以在下一个教程中使用此信息从 [您的云存储收集数据并将其引入平台](../collect/cloud-storage.md)。