---
keywords: Experience Platform;home;popular topics;Salesforce;salesforce
solution: Experience Platform
title: 使用流服务API创建Salesforce连接器
topic: overview
type: Tutorial
description: 本教程使用Flow Service API指导您完成将平台连接到Salesforce帐户以收集CRM数据的步骤。
translation-type: tm+mt
source-git-commit: d332226541685108b58d88096146ed6048606774
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 1%

---


# 使用 [!DNL Salesforce] API创建连 [!DNL Flow Service] 接器

Flow Service用于收集和集中来自Adobe Experience Platform不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成连接到用于收集CRM [!DNL Platform] 数据的 [!DNL Salesforce] 帐户的步骤。

如果您希望在中使用用户界 [!DNL Experience Platform]面， [Salesforce源连接器UI教程提供了执行类似操作的分步说明](../../../ui/create/crm/salesforce.md) 。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API [!DNL Platform] 成功连 [!DNL Salesforce] 接到帐户 [!DNL Flow Service] 。

### 收集所需的凭据

要连接 [!DNL Flow Service] 到，您 [!DNL Salesforce]必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | 源实例 [!DNL Salesforce] 的URL。 |
| `username` | 用户帐户的 [!DNL Salesforce] 用户名。 |
| `password` | 用户帐户的 [!DNL Salesforce] 口令。 |
| `securityToken` | 用户帐户的安 [!DNL Salesforce] 全令牌。 |

有关快速入门的详细信息，请访 [问此Salesforce文档](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)。

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

在连接 [!DNL Platform] 到帐户 [!DNL Salesforce] 之前，必须验证是否存在的连接规范 [!DNL Salesforce]。 如果连接规范不存在，则无法建立连接。

每个可用源都有其自己的唯一连接规范集，用于描述连接器属性，如身份验证要求。 您可以通过执行GET请求 [!DNL Salesforce] 和使用查询参数来查找连接规范。

**API格式**

发送不带GET参数的查询请求将返回所有可用源的连接规范。 您可以包含查询 `property=name=="salesforce"` 以获取专门用于的信息 [!DNL Salesforce]。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce"
```

**请求**

以下请求检索的连接规范 [!DNL Salesforce]。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name==%22salesforce%22' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回的连接规范 [!DNL Salesforce]，包括其唯一标识符(`id`)。 下一步需要此ID才能创建基本连接。

```json
{
    "items": [
        {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "name": "salesforce",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "Basic_Authentication",
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
            ]
        }
    ]
}
```

## 为API创建连接

API连接指定源并包含该源的凭据。 每个帐户只需要一个API连接， [!DNL Salesforce] 因为它可用于创建多个源连接器以导入不同的数据。

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
        "name": "Salesforce Base Connection",
        "description": "Base connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.username` | 与您的帐户关联的 [!DNL Salesforce] 用户名。 |
| `auth.params.password` | 与您的帐户关联的 [!DNL Salesforce] 密码。 |
| `auth.params.securityToken` | 与您的帐户关联的安全 [!DNL Salesforce] 令牌。 |
| `connectionSpec.id` | 在上一步 `id` 中检索 [!DNL Salesforce] 到的帐户的连接规范。 |

**响应**

成功的响应包含基连接的唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## 后续步骤

通过本教程，您已使用API为您的 [!DNL Salesforce] 帐户创建了连接，并且作为响应主体的一部分获得了唯一ID。 在下一个教程中，您可以使用此连接ID，因为您将学 [习如何使用流服务API浏览CRM系统](../../explore/crm.md)。