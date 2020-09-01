---
keywords: Experience Platform;home;popular topics;cloud storage;Cloud storage
solution: Experience Platform
title: 使用Flow Service API浏览云存储系统
topic: overview
description: 本教程使用Flow Service API探索第三方云存储系统。
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---


# 使用API浏览云存储系 [!DNL Flow Service] 统

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用 [!DNL Flow Service] API探索第三方云存储系统。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成功连接到云存储 [!DNL Flow Service] 系统。

### 获取基本连接

要使用API探索第三方云存储, [!DNL Platform] 您必须拥有有效的基本连接ID。 如果尚未为要使用的存储建立基本连接，则可通过以下教程创建一个：

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azure数据湖存储Gen2](../create/cloud-storage/adls-gen2.md)
* [Google Cloud商店](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资 [!DNL Flow Service]源)都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 浏览您的云存储

使用云存储的基本连接，您可以通过执行GET请求浏览文件和目录。 在执行GET请求以浏览您的云存储时，您必须包括下表中列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `objectType` | 要浏览的对象类型。 将此值设置为： <ul><li>`folder`:浏览特定目录</li><li>`root`:浏览根目录。</li></ul> |
| `object` | 仅当查看特定目录时，才需要此参数。 它的值表示要浏览的目录的路径。 |

使用以下调用查找要引入的文件的路径 [!DNL Platform]:

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 云存储库连接的ID。 |
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

成功的响应会返回查询的目录中找到的一组文件和文件夹。 请注意您希 `path` 望上传的文件的属性，因为您需要在下一步中提供它来检查其结构。

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

## Inspect文件结构

要从云存储检查GET文件的结构，请在提供文件路径作为查询参数时执行数据请求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 云存储库连接的ID。 |
| `{FILE_PATH}` | 文件的路径。 |
| `{FILE_TYPE}` | 文件的类型。 支持的文件类型包括：<ul><li>分隔</code>:分隔符分隔的值。 DSV文件必须以逗号分隔。</li><li>JSON</code>:JavaScript对象表示法。 JSON文件必须符合XDM</li><li>镶木</code>:阿帕奇镶木地板。 拼花文件必须符合XDM标准。</li></ul> |

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

通过本教程，您探索了您的云存储系统，找到了要导入的文件的路径，并查 [!DNL Platform]看了其结构。 您可以在下一个教程中使用此信 [息从您的云存储收集数据并将其引入平台](../collect/cloud-storage.md)。