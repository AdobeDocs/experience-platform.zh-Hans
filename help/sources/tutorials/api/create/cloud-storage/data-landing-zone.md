---
keywords: Experience Platform；主页；热门主题；
solution: Experience Platform
title: 使用流量服务API将数据登陆区连接到Adobe Experience Platform
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到数据登陆区。
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 3%

---

# 使用流服务API将[!DNL Data Landing Zone]连接到Adobe Experience Platform

[!DNL Data Landing Zone] 是一个基于云的数据存储设施，可用于配置有Adobe Experience Platform的临时文件存储。7天后，数据将自动从[!DNL Data Landing Zone]中删除。

本教程将指导您完成有关如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)创建[!DNL Data Landing Zone]源连接的步骤。 本教程还提供了有关如何检索[!DNL Data Landing Zone]以及查看和刷新凭据的说明。

## 快速入门

本指南需要对Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功创建[!DNL Data Landing Zone]源连接。

此外，本教程还要求您阅读[Platform API入门指南](../../../../../landing/api-guide.md)，了解如何对Platform API进行身份验证并解释文档中提供的示例调用。

## 检索可用的登陆区域

使用API访问[!DNL Data Landing Zone]的第一步是向[!DNL Connectors] API的`/landingzone`端点发出GET请求，同时提供`type=user_drop_zone`作为请求标头的一部分。

**API格式**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| 标头 | 描述 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone`类型允许API将登陆区域容器与可供您使用的其他类型容器区分开来。 |

**请求**

以下请求可检索现有登陆区域。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**响应**

以下响应会返回有关登陆区域的信息，包括其对应的`containerName`和`containerTTL`。

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 属性 | 描述 |
| --- | --- |
| `containerName` | 您检索到的登陆区域的名称。 |
| `containerTTL` | 适用于登陆区域内数据的生存时间设置。 给定登陆区内的任何内容将在七天后被删除。 |

## 检索[!DNL Data Landing Zone]凭据

要检索[!DNL Data Landing Zone]的凭据，请向[!DNL Connectors] API的`/credentials`端点发出GET请求。

**API格式**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**请求**

以下请求示例检索现有登陆区的凭据。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

以下响应会返回登陆区的凭据信息，包括当前的`SASToken`和`SASUri`，以及与登陆区容器对应的`storageAccountName`。

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


## 更新[!DNL Data Landing Zone]凭据

您可以通过向[!DNL Connectors] API的`/credentials`端点发出POST请求来更新`SASToken`。

**API格式**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 标头 | 描述 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone`类型允许API将登陆区域容器与可供您使用的其他类型容器区分开来。 |
| `refresh` | `refresh`操作允许您重置登陆区域凭据并自动生成新的`SASToken`。 |

**请求**

以下请求会更新您的登陆区域凭据。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

以下响应会返回`SASToken`和`SASUri`的更新值。

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## 浏览登陆区文件结构和内容

您可以通过向[!DNL Flow Service] API的`connectionSpecs`端点发出GET请求，来浏览登陆区域的文件结构和内容。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 与[!DNL Data Landing Zone]对应的连接规范ID。 此固定ID是：`26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回在查询目录中找到的文件和文件夹数组。 请注意要上传的文件的`path`属性，因为需要在下一步中提供该属性以检查其结构。

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
| `{CONNECTION_SPEC_ID}` | 与[!DNL Data Landing Zone]对应的连接规范ID。 此固定ID是：`26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |
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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回查询文件的结构，包括表名和数据类型。

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

## 创建源连接

源连接创建并管理从中摄取数据的外部源的连接。 源连接由数据源、数据格式和创建数据流所需的源连接ID等信息组成。 源连接实例特定于租户和IMS组织。

要创建源连接，请向[!DNL Flow Service] API的`/sourceConnections`端点发出POST请求。


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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | [!DNL Data Landing Zone]源连接的名称。 |
| `data.format` | 要引入平台的数据格式。 |
| `params.path` | 要引入平台的文件的路径。 |
| `connectionSpec.id` | 与[!DNL Data Landing Zone]对应的连接规范ID。 此固定ID是：`26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |

**响应**

成功的响应会返回新创建源连接的唯一标识符(`id`)。 在下一个教程中，需要此ID才能创建数据流。

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 后续步骤

通过本教程，您已检索了[!DNL Data Landing Zone]凭据，探索了其文件结构以查找要引入平台的文件，并创建了源连接以开始将数据引入平台。 您现在可以继续下一个教程，其中您将学习如何[创建数据流，以使用 [!DNL Flow Service] API](../../collect/cloud-storage.md)将云存储数据引入平台。
