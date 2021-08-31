---
keywords: Experience Platform；主页；热门主题；云存储；云存储
solution: Experience Platform
title: 使用流服务API探索云存储系统
topic-legacy: overview
description: 本教程使用流程服务API来探索第三方云存储系统。
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API浏览云存储系统

本教程使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)来浏览第三方云存储系统。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到云存储系统。

### 获取连接ID

要使用[!DNL Platform] API探索第三方云存储，您必须拥有有效的连接ID。 如果您尚未连接要处理的存储，则可以通过以下教程创建一个：

* [[!DNL Amazon S3]](../create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)
* [[!DNL FTP]](../create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../create/cloud-storage/sftp.md)

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都与特定虚拟沙箱隔离。 对[!DNL Platform] API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 探索云存储

使用云存储的连接ID，您可以通过执行GET请求来浏览文件和目录。 执行GET请求以浏览云存储时，必须包含下表中列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `objectType` | 要浏览的对象类型。 将此值设置为： <ul><li>`folder`:浏览特定目录</li><li>`root`:浏览根目录。</li></ul> |
| `object` | 仅当查看特定目录时，才需要此参数。 其值表示要浏览的目录的路径。 |

使用以下调用查找要引入[!DNL Platform]的文件的路径：

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

成功的响应会返回在查询目录中找到的文件和文件夹数组。 请注意您希望上传的文件的`path`属性，因为需要在下一步中提供该属性以检查其结构。

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

您可以在提供文件路径和类型的同时，通过执行GET请求，从云存储源中检查数据文件的结构。 您还可以通过在查询参数中指定不同文件类型来检查不同的文件类型，例如CSV、TSV或压缩的JSON和分隔文件。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 云存储源连接器的连接ID。 |
| `{FILE_PATH}` | 要检查的文件的路径。 |
| `{FILE_TYPE}` | 文件的类型。 支持的文件类型包括：<ul><li>已分隔</code>:分隔符分隔值。 DSV文件必须以逗号分隔。</li><li>JSON</code>:JavaScript对象表示法。 JSON文件必须符合XDM</li><li>PARQUET</code>:阿帕奇拼花。 Parquet文件必须符合XDM。</li></ul> |
| `{QUERY_PARAMS}` | 可用于筛选结果的可选查询参数。 有关更多信息，请参阅[查询参数](#query)中的部分。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)支持使用查询参数来预览和检查不同的文件类型。

| 参数 | 描述 |
| --------- | ----------- |
| `columnDelimiter` | 指定为用于检查CSV或TSV文件的列分隔符的单个字符值。 如果未提供参数，则值默认为逗号`(,)`。 |
| `compressionType` | 预览压缩的分隔或JSON文件所需的查询参数。 支持的压缩文件包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## 后续步骤

通过阅读本教程，您探索了云存储系统，找到了要导入[!DNL Platform]的文件路径，并查看了其结构。 在下一个教程中，您可以使用此信息从云存储中收集数据，并将其导入Platform](../collect/cloud-storage.md)。[
