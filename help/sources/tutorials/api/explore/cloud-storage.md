---
keywords: Experience Platform;home;popular topics;cloud storage;Cloud storage
solution: Experience Platform
title: 使用Flow Service API浏览云存储系统
topic: overview
description: 本教程使用Flow Service API探索第三方云存储系统。
translation-type: tm+mt
source-git-commit: 026007e5f80217f66795b2b53001b6cf5e6d2344
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 2%

---


# 使用API浏览云存储系 [!DNL Flow Service] 统

本教程使用 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) 来探索第三方云存储系统。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成功连接到云存储 [!DNL Flow Service] 系统。

### 获取连接ID

要使用API探索第三方云存储, [!DNL Platform] 您必须拥有有效的连接ID。 如果您尚未连接要使用的存储，则可以通过以下教程创建一个连接：

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azure数据湖存储Gen2](../create/cloud-storage/adls-gen2.md)
* [Azure文件存储](../create/cloud-storage/azure-file-storage.md)
* [Google Cloud商店](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [SFTP](../create/cloud-storage/sftp.md)

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资 [!DNL Flow Service]源)都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 浏览您的云存储

使用云存储的连接ID，您可以通过执行GET请求浏览文件和目录。 在执行GET请求以浏览您的云存储时，您必须包括下表中列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `objectType` | 要浏览的对象类型。 将此值设置为： <ul><li>`folder`:浏览特定目录</li><li>`root`:浏览根目录。</li></ul> |
| `object` | 仅当查看特定目录时，才需要此参数。 它的值表示要浏览的目录的路径。 |

使用以下调用查找要引入的文件的路径 [!DNL Platform]:

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{CONNECTION_ID}` | 云存储源连接器的连接ID。 |
| `{PATH}` | 目录的路径。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
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

要从云存储检查GET文件的结构，请在提供文件的路径和类型作为查询参数时执行数据请求。

可以通过将自定义分隔符指定为查询周长来检查CSV或TSV文件的结构。 任何单个字符值都是允许的列分隔符。 如果未提供， `(,)` 则使用逗号作为默认值。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=;
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=\t
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 云存储源连接器的连接ID。 |
| `{FILE_PATH}` | 要检查的文件的路径。 |
| `{FILE_TYPE}` | 文件的类型。 支持的文件类型包括：<ul><li>分隔</code>:分隔符分隔的值。 DSV文件必须以逗号分隔。</li><li>JSON</code>:JavaScript对象表示法。 JSON文件必须符合XDM</li><li>镶木</code>:阿帕奇镶木地板。 拼花文件必须符合XDM标准。</li></ul> |
| `columnDelimiter` | 指定为列分隔符以检查CSV或TSV文件的单个字符值。 如果未提供该参数，则值默认为逗号 `(,)`。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
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