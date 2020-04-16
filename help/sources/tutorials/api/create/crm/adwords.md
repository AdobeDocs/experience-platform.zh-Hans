---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建Google AdWords连接器
topic: overview
translation-type: tm+mt
source-git-commit: a456dce58c32348c9e680cd672b71dd7bbdc1a04

---


# 使用Flow Service API创建Google AdWords连接器

Flow Service用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Experience Platform连接到Google AdWords（以下简称“AdWords”）的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了使用Flow Service API成功连接到AdWords时需要了解的其他信息。

### 收集所需的凭据

要使Flow Service与AdWords连接，您必须为以下连接属性提供值：

| **凭证** | **描述** |
| -------------- | --------------- |
| `clientCustomerID` | 与目标Google AdWords关联的客户ID | account. |
| `developerToken` | 用于标识AdWords API开发人员的字符串。 |
| `refreshToken` | 从Google获取的用于授权访问AdWords的刷新令牌。 |
| `clientID` | 用于生成刷新令牌的应用程序的ID。 |
| `clientSecret` | 用于生成刷新令牌的应用程序的客户端机密。 |

有关这些值的详细信息，请参阅此 [Google AdWords文档](https://developers.google.com/adwords/api/docs/guides/authentication)。

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

要创建AdWords连接，流服务中必须存在一组AdWords连接规范。 将平台连接到AdWords的第一步是检索这些规范。

**API格式**

每个可用源都有其自己唯一的连接规范集，用于描述连接器属性，如身份验证要求。 您可以通过执行GET请求和使用查询参数来查找AdWords的连接规范。

发送不带查询参数的GET请求将返回所有可用源的连接规范。 您可以包含获取AdWords `property=name=="google-adwords"` 专用信息的查询。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="google-adwords"
```

**请求**

以下请求检索AdWords的连接规范。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?{QUERY_PARAMS}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回AdWords的连接规范，包括其唯一标识符(`id`)。 下一步中需要此ID才能创建基本连接。

```json
{
    "items": [
        {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "name": "google-adwords",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for google-adwords",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "clientCustomerID": {
                                "type": "string",
                                "description": "The Client customer ID of the AdWords account"
                            },
                            "developerToken": {
                                "type": "string",
                                "description": "The developer token associated with the manager account",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained from Google for authorizing access to AdWords",
                                "format": "password"
                            },
                            "clientId": {
                                "type": "string",
                                "description": "The client ID of the Google application used to acquire the refresh token"
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret of the google application used to acquire the refresh token",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientCustomerID",
                            "developerToken",
                            "refreshToken",
                            "clientId",
                            "clientSecret"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## 创建基本连接

基本连接指定一个源并包含该源的凭据。 每个AdWords帐户只需要一个基本连接，因为它可用于创建多个源连接器以引入不同的数据。

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
        "name": "google-adwords base connection",
        "description": "Base connection for google-adwords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.clientCustomerID` | 您的AdWords帐户的客户客户ID。 |
| `auth.params.developerToken` | 您的AdWords帐户的开发人员令牌。 |
| `auth.params.refreshToken` | 您的AdWords帐户的刷新令牌。 |
| `auth.params.clientID` | 您的AdWords帐户的客户端ID。 |
| `auth.params.clientSecret` | AdWords帐户的客户端机密。 |
| `connectionSpec.id` | 在上一步 `id` 中检索的AdWords帐户的连接规范。 |

**响应**

成功的响应会返回新创建的基本连接`id`的唯一标识符()。 在下一个教程中浏览您的AdWords数据时需要此ID。

```json
{
    "id": "e6ce1eab-416b-4a20-8e1e-ab416b1a206f",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 后续步骤

通过本教程，您使用Flow Service API创建了一个AdWords基本连接，并获得了该连接的唯一ID值。 在下一个教程中，您可以使用此基本连接ID，因为您将学习如何 [使用Flow Service API浏览CRM系统](../../explore/crm.md)。
