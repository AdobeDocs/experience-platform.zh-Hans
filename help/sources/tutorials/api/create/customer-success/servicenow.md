---
keywords: Experience Platform;home;popular topics;servicenow;ServiceNow
solution: Experience Platform
title: 使用Flow Service API创建ServiceNow连接器
topic: overview
description: 本教程使用Flow Service API指导您完成将Experience Platform连接到ServiceNow服务器的步骤。
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 1%

---


# 使用 [!DNL ServiceNow] API创建连 [!DNL Flow Service] 接器

>[!NOTE]
>
>连接 [!DNL ServiceNow] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成连接到服务 [!DNL Experience Platform] 器的步 [!DNL ServiceNow] 骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成 [!DNL ServiceNow] 功连接到服 [!DNL Flow Service] 务器。

### 收集所需的凭据

要连接 [!DNL Flow Service] 到，您 [!DNL ServiceNow]必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | The endpoint of the [!DNL ServiceNow] server. |
| `username` | 用于连接到服务器进行身 [!DNL ServiceNow] 份验证的用户名。 |
| `password` | 连接到服务器进行身 [!DNL ServiceNow] 份验证的口令。 |

有关快速入门的详细信息，请参 [阅此ServiceNow文档](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资 [!DNL Flow Service]源)都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 查找连接规范

要创建连接， [!DNL ServiceNow] 必须在中存 [!DNL ServiceNow] 在一组连接规范 [!DNL Flow Service]。 连接到的第一步 [!DNL Platform] 是 [!DNL ServiceNow] 检索这些规范。

**API格式**

每个可用源都有其自己的唯一连接规范集，用于描述连接器属性，如身份验证要求。 向端点发送GET请 `/connectionSpecs` 求将返回所有可用源的连接规范。 您还可以包含查询, `property=name=="service-now"` 以获取专门用于的信息 [!DNL ServiceNow]。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="service-now"
```

**请求**

以下请求检索的连接规范 [!DNL ServiceNow]。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="service-now"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回的连接规范 [!DNL ServiceNow]，包括其唯一标识符(`id`)。 下一步需要此ID才能创建基本连接。

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

基本连接指定源并包含该源的凭据。 每个帐户只需要一个基 [!DNL ServiceNow] 本连接，因为它可用于创建多个源连接器以导入不同的数据。

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
| `auth.params.server` | 服务器的端 [!DNL ServiceNow] 点。 |
| `auth.params.username` | 用于连接到服务器进行身 [!DNL ServiceNow] 份验证的用户名。 |
| `auth.params.password` | 连接到服务器进行身 [!DNL ServiceNow] 份验证的口令。 |
| `connectionSpec.id` | 与关联的连接规范ID [!DNL ServiceNow]。 |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 需要此ID才能在下一步探索您的CRM。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 后续步骤

通过本教程，您已使用 [!DNL ServiceNow] API创建了基本 [!DNL Flow Service] 连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此基本连接ID，因为您将学习如 [何使用流服务API探索客户成功系统](../../explore/customer-success.md)。