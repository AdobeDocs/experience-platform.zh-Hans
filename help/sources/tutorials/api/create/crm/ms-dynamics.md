---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建Microsoft Dynamics连接器
topic: overview
translation-type: tm+mt
source-git-commit: 6c86cec91774f3444dc90042cd7ad5c71429aabd

---


# 使用Flow Service API创建Microsoft Dynamics连接器

Flow Service用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Platform连接到Microsoft Dynamics（以下简称“Dynamics”）帐户以收集CRM数据的步骤。

如果您希望使用Experience Platform中的用户界面， [Dynamics或Salesforce源连接器UI教程将提供执行类似操作的分步说明](../../../ui/create/crm/dynamics-salesforce.md) 。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用Flow Service API将平台成功连接到Dynamics帐户。

### 收集所需的凭据

要使Flow Service连接到Dynamics，您必须为以下连接属性提供值：

| 凭证 | 描述 |
| ---------- | ----------- |
| `serviceUri` | 您的Dynamics实例的服务URL。 |
| `username` | 您的Dynamics用户帐户的用户名。 |
| `password` | 您的Dynamics帐户的密码。 |

有关快速入门的更多信息，请访 [问此Dynamics文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

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

在将平台连接到Dynamics帐户之前，必须验证Dynamics是否存在连接规范。 如果连接规范不存在，则无法建立连接。

每个可用源都有其自己唯一的连接规范集，用于描述连接器属性，如身份验证要求。 您可以通过执行GET请求和使用查询参数来查找Dynamics的连接规范。

**API格式**

发送不带查询参数的GET请求将返回所有可用源的连接规范。 您可以包含查询, `property=name=="dynamics-online"` 以获取Dynamics的专用信息。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**请求**

以下请求检索Dynamics的连接规范。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回Dynamics的连接规范，包括其唯一标识符(`id`)。 下一步中需要此ID才能创建基本连接。

```json
{
    "items": [
        {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "name": "dynamics-online",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for Dynamics-Online",
                    "settings": {
                        "authenticationType": "Office365",
                        "deploymentType": "Online"
                    },
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to dynamics-online",
                        "properties": {
                            "serviceUri": {
                                "type": "string",
                                "description": "The service URL of your Dynamics instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "serviceUri"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## 创建基本连接

基本连接指定一个源并包含该源的凭据。 每个Dynamics帐户只需要一个基本连接，因为它可用于创建多个源连接器以导入不同的数据。

执行以下POST请求以创建基本连接。

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
        "name": "Dynamics Base Connection",
        "description": "Base connection for Dynamics account",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.serviceUri` | 与您的Dynamics实例关联的服务URI。 |
| `auth.params.username` | 与您的Dynamics帐户关联的用户名。 |
| `auth.params.password` | 与您的Dynamics帐户关联的密码。 |
| `connectionSpec.id` | 在上一步 `id` 中检索的Dynamics帐户的连接规范。 |

**响应**

成功的响应包含基本连接的唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 后续步骤

通过本教程，您已使用API为Dynamics帐户创建了基本连接，并且作为响应体的一部分获得了唯一ID。 在下一个教程中，您可以使用此基本连接ID，因为您将学习如何 [使用Flow Service API浏览CRM系统](../../explore/crm.md)。