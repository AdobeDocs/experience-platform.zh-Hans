---
keywords: Experience Platform;home;popular topics;hubspot;Hubspot
solution: Experience Platform
title: 使用Flow Service API创建HubSpot连接器
topic: overview
description: 本教程使用Flow Service API指导您完成将Experience Platform连接到HubSpot的步骤。
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---


# 使用 [!DNL HubSpot] API创建连 [!DNL Flow Service] 接器

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成连接到的 [!DNL Experience Platform] 步骤 [!DNL HubSpot]。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了成功连接到使用API所需了解的其 [!DNL HubSpot] 他信 [!DNL Flow Service] 息。

### 收集所需的凭据

要连接 [!DNL Flow Service] ，必须 [!DNL HubSpot]提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientId` | 与您的应用程序关联的客户 [!DNL HubSpot] 端ID。 |
| `clientSecret` | 与您的应用程序关联的客户端 [!DNL HubSpot] 机密。 |
| `accessToken` | 最初验证您的OAuth集成时获得的访问令牌。 |
| `refreshToken` | 最初验证您的OAuth集成时获取的刷新令牌。 |

有关快速入门的详细信息，请参阅此 [HubSpot文档](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资源 [!DNL Flow Service]的资源)都隔离到特定虚拟沙箱。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 查找连接规范

要创建连接， [!DNL HubSpot] 必须在中存 [!DNL HubSpot] 在一组连接规范 [!DNL Flow Service]。 连接到的第一步 [!DNL Platform] 是 [!DNL HubSpot] 检索这些规范。

**API格式**

每个可用源都有其自己的唯一连接规范集，用于描述连接器属性，如身份验证要求。 向端点发送GET请 `/connectionSpecs` 求将返回所有可用源的连接规范。 您还可以包含查询, `property=name=="hubspot"` 以获取专门用于的信息 [!DNL HubSpot]。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="hubspot"
```

**请求**

以下请求检索的连接规范 [!DNL HubSpot]。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="hubspot"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回的连接规 [!DNL HubSpot]范，包括其唯一标识符(`id`)。 下一步中需要此ID才能创建API连接。

```json
{
    "items": [
        {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "name": "hubspot",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to HubSpot",
                        "properties": {
                            "clientId": {
                                "type": "string",
                                "description": "The client ID associated with your HubSpot application."
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret associated with your HubSpot application.",
                                "format": "password"
                            },
                            "accessToken": {
                                "type": "string",
                                "description": "The access token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientId",
                            "clientSecret",
                            "accessToken",
                            "refreshToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## 为API创建连接

API连接指定源并包含该源的凭据。 每个帐户只需要一个API连接， [!DNL HubSpot] 因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.clientId` | 与您的应用程序关联的客户 [!DNL HubSpot] 端ID。 |
| `auth.params.clientSecret` | 与您的应用程序关联的客户端 [!DNL HubSpot] 机密。 |
| `auth.params.accessToken` | 最初验证您的OAuth集成时获得的访问令牌。 |
| `auth.params.refreshToken` | 最初验证您的OAuth集成时获取的刷新令牌。 |

**响应**

成功的响应会返回新创建的API连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "2eb9c78b-e8b8-4400-b9c7-8be8b86400b2",
    "etag": "\"05026cf5-0000-0200-0000-5e4c42920000\""
}
```

通过本教程，您已使用 [!DNL HubSpot] API创建了 [!DNL Flow Service] 一个连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您将学 [习如何使用流服务API浏览CRM系统](../../explore/crm.md)。