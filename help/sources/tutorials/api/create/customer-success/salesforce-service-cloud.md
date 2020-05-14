---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用流服务API创建Salesforce Service Cloud连接器
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 1%

---


# 使用流服务API创建Salesforce Service Cloud连接器

>[!NOTE]
>Salesforce Service Cloud连接器处于测试状态。 功能和文档可能会发生更改。

Flow Service用于在Adobe Experience Platform内收集和集中来自不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Experience Platform连接到Salesforce Service Cloud（以下简称“SSC”）的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md): Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供了使用流服务API成功连接到SSC所需了解的其他信息。

### 收集所需的凭据

要使流服务与SSC连接，您必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `username` | 用户帐户的用户名。 |
| `password` | 用户帐户的密码。 |
| `securityToken` | 用户帐户的安全令牌。 |

有关快速入门的详细信息，请 [参阅此Salesforce服务云文档](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的部分。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程后，将提供所有Experience Platform API调用中每个所需标头的值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于流服务的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 查找连接规范

要创建SSC连接，流服务中必须存在一组SSC连接规范。 将平台连接到SSC的第一步是检索这些规范。

**API格式**

每个可用源都有其自己的唯一连接规范集，用于描述连接器属性，如身份验证要求。 向端点发送GET请求 `/connectionSpecs` 将返回所有可用源的连接规范。 您还可以包含查询, `property=name=="salesforce-service-cloud"` 以获取专门用于SSC的信息。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce-service-cloud"
```

**请求**

以下请求检索SSC的连接规范。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="mysql"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回SSC的连接规范，包括其唯一标识符(`id`)。 在下一步创建基本连接时需要此ID。

```json
{
    "items": [
        {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "name": "salesforce-service-cloud",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "BasicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "environmentUrl": {
                                "type": "string",
                                "description": "URL of the source instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "securityToken": {
                                "type": "string",
                                "description": "Security token for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "securityToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## 创建基本连接

基本连接指定源并包含该源的凭据。 每个SSC帐户只需要一个基本连接，因为它可用于创建多个源连接器以导入不同的数据。

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
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.username` | 与您的SSC帐户关联的用户名。 |
| `auth.params.password` | 与您的SSC帐户关联的密码。 |
| `auth.params.securityToken` | 与您的SSC帐户关联的安全令牌。 |
| `connectionSpec.id` | 在上一步 `id` 中检索的SSC帐户的连接规范。 |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 后续步骤

通过本教程，您已使用Flow Service API创建了SSC基本连接，并获得了该连接的唯一ID值。 在下一个教程中，您可以使用此基本连接ID，因为您将学习如 [何使用流服务API探索客户成功系统](../../explore/customer-success.md)。
