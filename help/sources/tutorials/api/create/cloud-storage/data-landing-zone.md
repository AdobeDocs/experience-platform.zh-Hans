---
keywords: Experience Platform；主页；热门主题；
solution: Experience Platform
title: 使用流量服务API将数据登陆区连接到Adobe Experience Platform
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到数据登陆区。
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: d57060ddeed64d3863f71ac1ea34ccc5c97265ea
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 4%

---

# 连接 [!DNL Data Landing Zone] 到Adobe Experience Platform

>[!IMPORTANT]
>
>此页面专用于 [!DNL Data Landing Zone] *来源* 连接器Experience Platform。 有关连接到的信息 [!DNL Data Landing Zone] *目标* 连接器，请参阅 [[!DNL Data Landing Zone] 目标文档页面](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] 是一个安全、基于云的文件存储工具，用于将文件导入Adobe Experience Platform。 数据会自动从 [!DNL Data Landing Zone] 七天后。

本教程将指导您完成有关如何创建 [!DNL Data Landing Zone] 源连接使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). 本教程还提供了有关如何检索 [!DNL Data Landing Zone]，以及查看和刷新凭据。

## 快速入门

本指南需要对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了成功创建 [!DNL Data Landing Zone] 源连接使用 [!DNL Flow Service] API。

本教程还要求您阅读 [Platform API快速入门](../../../../../landing/api-guide.md) 了解如何对Platform API进行身份验证并解释文档中提供的示例调用。

## 检索可用的登陆区域

使用API访问的第一步 [!DNL Data Landing Zone] 是向GET请求 `/landingzone` 的端点 [!DNL Connectors] API，同时提供 `type=user_drop_zone` 作为请求标头的一部分。

**API格式**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| 标头 | 描述 |
| --- | --- |
| `user_drop_zone` | 的 `user_drop_zone` 类型允许API将登陆区域容器与可供您使用的其他类型容器区分开。 |

**请求**

以下请求可检索现有登陆区域。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**响应**

以下响应会返回有关登陆区域的信息，包括其相应的 `containerName` 和 `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 属性 | 描述 |
| --- | --- |
| `containerName` | 您检索到的登陆区域的名称。 |
| `containerTTL` | 登陆区域内对数据应用的过期时间（以天为单位）。 给定登陆区内的任何内容将在七天后被删除。 |

## 检索 [!DNL Data Landing Zone] 凭据

检索凭据 [!DNL Data Landing Zone]，向发送GET请求 `/credentials` 的端点 [!DNL Connectors] API。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**请求**

以下请求示例检索现有登陆区的凭据。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

以下响应会返回登陆区的凭据信息，包括您当前的 `SASToken` 和 `SASUri`，以及 `storageAccountName` 对应于登陆区域容器。

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| 属性 | 描述 |
| --- | --- |
| `containerName` | 您的登陆区域的名称。 |
| `SASToken` | 登陆区域的共享访问签名令牌。 此字符串包含授权请求所需的所有信息。 |
| `SASUri` | 登陆区的共享访问签名URI。 此字符串是您要对其进行身份验证的登陆区域的URI及其相应的SAS令牌的组合。 |


## 更新 [!DNL Data Landing Zone] 凭据

您可以更新 `SASToken` 通过向 `/credentials` 的端点 [!DNL Connectors] API。

**API格式**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 标头 | 描述 |
| --- | --- |
| `user_drop_zone` | 的 `user_drop_zone` 类型允许API将登陆区域容器与可供您使用的其他类型容器区分开。 |
| `refresh` | 的 `refresh` 操作允许您重置登陆区域凭据并自动生成新凭据 `SASToken`. |

**请求**

以下请求会更新您的登陆区域凭据。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

以下响应会为 `SASToken` 和 `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## 浏览登陆区文件结构和内容

您可以通过向 `connectionSpecs` 的端点 [!DNL Flow Service] API。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 与 [!DNL Data Landing Zone]. 此固定ID是： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
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
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## 预览登陆区文件结构和内容

要检查登陆区中文件的结构，请在提供文件路径并键入作为查询参数时执行GET请求。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | 与 [!DNL Data Landing Zone]. 此固定ID是： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | 要访问的对象的类型。 | `file` |
| `{OBJECT}` | 要访问的对象的路径和名称。 | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | 文件的类型。 | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | 布尔值，用于定义是否支持文件预览。 | </ul><li>`true`</li><li>`false`</li></ul> |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回查询文件的结构，包括文件名和数据类型。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

### 使用 `determineProperties` 自动检测 [!DNL Data Landing Zone]

您可以使用 `determineProperties` 用于自动检测文件内容属性信息的参数 [!DNL Data Landing Zone] 进行GET调用以探索源的内容和结构时，覆盖分类。

#### `determineProperties` 用例

下表概述了在使用 `determineProperties` 查询参数或手动提供有关文件的信息。

| `determineProperties` | `queryParams` | 响应 |
| --- | --- | --- |
| True | 不适用 | 如果 `determineProperties` 作为查询参数提供，则会进行文件属性检测，并且响应会返回一个新的 `properties` 键，其中包含有关文件类型、压缩类型和列分隔符的信息。 |
| 不适用 | True | 如果文件类型、压缩类型和列分隔符的值是作为 `queryParams`，则会使用它们生成架构，并在响应中返回相同的属性。 |
| True | True | 如果同时完成两个选项，则会返回一个错误。 |
| 不适用 | 不适用 | 如果两个选项都未提供，则会返回一个错误，因为无法获取响应的属性。 |

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `determineProperties` | 此查询参数允许 [!DNL Flow Service] 用于检测有关文件属性的信息的API，包括有关文件类型、压缩类型和列分隔符的信息。 | `true` |

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回查询文件的结构（包括文件名和数据类型），以及 `properties` 键，其中包含 `fileType`, `compressionType`和 `columnDelimiter`.

+++单击这里

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| 属性 | 描述 |
| --- | --- |
| `properties.fileType` | 查询文件的对应文件类型。 支持的文件类型包括： `delimited`, `json`和 `parquet`. |
| `properties.compressionType` | 用于查询文件的相应压缩类型。 支持的压缩类型包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | 用于查询文件的相应列分隔符。 任何单个字符值都是允许的列分隔符。 默认值为逗号 `(,)`. |


## 创建源连接

源连接创建并管理从中摄取数据的外部源的连接。 源连接由数据源、数据格式和创建数据流所需的源连接ID等信息组成。 源连接实例特定于租户和IMS组织。

要创建源连接，请向 `/sourceConnections` 的端点 [!DNL Flow Service] API。


**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 您的 [!DNL Data Landing Zone] 源连接。 |
| `data.format` | 要引入平台的数据格式。 |
| `params.path` | 要引入平台的文件的路径。 |
| `connectionSpec.id` | 与 [!DNL Data Landing Zone]. 此固定ID是： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**响应**

成功的响应会返回唯一标识符(`id`)。 在下一个教程中，需要此ID才能创建数据流。

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 后续步骤

通过阅读本教程，您已检索到 [!DNL Data Landing Zone] 凭据、探索其文件结构以查找要引入平台的文件，并创建源连接以开始将数据引入平台。 您现在可以继续下一个教程，其中将学习如何 [创建数据流，以使用 [!DNL Flow Service] API](../../collect/cloud-storage.md).
