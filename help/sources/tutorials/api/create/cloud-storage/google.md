---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建Google Cloud存储连接器
topic: overview
translation-type: tm+mt
source-git-commit: 96be7084d5d2efb86b7bba27f1a92bd9c0055fba

---


# 使用Flow Service API创建Google Cloud存储连接器

Flow Service用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Experience Platform连接到Google Cloud存储帐户的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用流服务API成功连接到Google Cloud存储帐户。

### 收集所需的凭据

要使流服务与您的Google Cloud存储帐户连接，您必须为以下连接属性提供值：

| 凭证 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 您的Google Cloud存储帐户的访问密钥ID。 |
| `secretAccessKey` | 您的Google Cloud存储帐户的秘密访问密钥。 |

有关快速入门的信息，请访 [问此Google Cloud文档](https://cloud.google.com/docs/authentication)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于流服务的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标题：

* 内容类型： `application/json`

## 查找连接规范

在将平台连接到Google Cloud存储之前，您必须验证Google Cloud存储是否存在连接规范。 如果连接规范不存在，则无法建立连接。

每个可用源都有其自己唯一的连接规范集，用于描述连接器属性，如身份验证要求。 您可以通过执行GET请求和使用存储参数来查找Google Cloud查询的连接规范。

**API格式**

发送不带查询参数的GET请求将返回所有可用源的连接规范。 您可以包含查询, `property=name=="google-cloud"` 以获取Google Cloud存储的专用信息。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name==google-cloud
```

**请求**

以下请求检索Google Cloud存储的连接规范。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-cloud"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回Google Cloud存储的连接规范，包括其唯一标识符(`id`)。 下一步中需要此ID才能创建基本连接。

```json
{
    "items": [
        {
            "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
            "name": "google-cloud",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for google-cloud",
                    "type": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to google-cloud storage connector.",
                        "properties": {
                            "accessKeyId": {
                                "type": "string",
                                "description": "Access Key Id for the user account"
                            },
                            "secretAccessKey": {
                                "type": "string",
                                "description": "Secret Access Key for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "accessKeyId",
                            "secretAccessKey"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## 创建基本连接

基本连接指定一个源并包含该源的凭据。 每个Google Cloud存储帐户只需要一个基本连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google Cloud Storage base connection",
        "description": "Base connector for Google Cloud Storage",
        "auth": {
            "specName": "Basic Authentication for google-cloud",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretAccessKey": "secretAccessKey"
            }
        },
        "connectionSpec": {
            "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.accessKeyId` | 与您的Google Cloud存储帐户关联的访问密钥ID。 |
| `auth.params.secretAccessKey` | 与您的Google Cloud存储帐户关联的机密访问密钥。 |
| `connectionSpec.id` | 在上一步 `id` 中检索的Google Cloud存储帐户的连接规范。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览您的云存储数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

通过本教程，您已使用API创建了Google Cloud存储连接，并且作为响应体的一部分获得了唯一ID。 您可以使用此连接ID来 [探索使用Flow Service API的云存储](../../explore/cloud-storage.md) ，或 [使用Flow Service API获取拼花数据](../../cloud-storage-parquet.md)。