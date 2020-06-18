---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建ServiceNow连接器
topic: overview
translation-type: tm+mt
source-git-commit: cada7c7eff7597015caa7333559bef16a59eab65
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 1%

---


# 使用Flow Service API创建ServiceNow连接器

>[!NOTE]
>ServiceNow连接器处于测试状态。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

流服务用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Experience Platform连接到ServiceNow服务器的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md): Experience Platform允许从各种来源摄取数据，同时使您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了使用流服务API成功连接到ServiceNow服务器所需了解的其他信息。

### 收集所需的凭据

要使流服务连接到ServiceNow，您必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | ServiceNow服务器的端点。 |
| `username` | 用于连接到ServiceNow服务器进行身份验证的用户名。 |
| `password` | 连接到ServiceNow服务器进行身份验证的口令。 |

有关快速入门的详细信息，请参 [阅此ServiceNow文档](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

### 收集所需标题的值

要调用PlatformAPI，您必须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于流服务的资源）都与特定虚拟沙箱隔离。 对PlatformAPI的所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 查找连接规范

要创建ServiceNow连接，流服务中必须存在一组ServiceNow连接规范。 将Platform连接到ServiceNow的第一步是检索这些规范。

**API格式**

每个可用源都有其自己的唯一连接规范集，用于描述连接器属性，如身份验证要求。 向端点发送GET请求 `/connectionSpecs` 将返回所有可用源的连接规范。 您还可以包含查询, `property=name=="service-now"` 以获取ServiceNow的专用信息。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="service-now"
```

**请求**

以下请求检索ServiceNow的连接规范。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="service-now"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回ServiceNow的连接规范，包括其唯一标识符(`id`)。 下一步需要此ID才能创建基本连接。

```json
{
    "items": [
        {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "name": "service-now",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to ServiceNow server",
                        "properties": {
                            "endpoint": {
                                "type": "string",
                                "description": "The endpoint of the ServiceNow server (http://<instance>.service-now.com)."
                            },
                            "username": {
                                "type": "string",
                                "description": "The user name used to connect to the ServiceNow server for authentication."
                            },
                            "password": {
                                "type": "string",
                                "description": "password to connect to the ServiceNow server for authentication.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "endpoint",
                            "username",
                            "password"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## 创建基本连接

基本连接指定源并包含该源的凭据。 每个ServiceNow帐户只需要一个基本连接，因为它可用于创建多个源连接器以导入不同的数据。

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
        "name": "Base connection for service-now",
        "description": "Base connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| ------------- | --------------- |
| `auth.params.server` | ServiceNow服务器的端点。 |
| `auth.params.username` | 用于连接到ServiceNow服务器进行身份验证的用户名。 |
| `auth.params.password` | 连接到ServiceNow服务器进行身份验证的口令。 |
| `connectionSpec.id` | 与ServiceNow关联的连接规范ID。 |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 需要此ID才能在下一步探索您的CRM。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 后续步骤

通过本教程，您已使用Flow Service API创建了ServiceNow基连接，并获得了该连接的唯一ID值。 在下一个教程中，您可以使用此基本连接ID，因为您将学习如 [何使用流服务API探索客户成功系统](../../explore/customer-success.md)。