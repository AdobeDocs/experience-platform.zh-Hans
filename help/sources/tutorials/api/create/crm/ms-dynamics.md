---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: 使用Flow Service API创建Microsoft Dynamics连接器
topic: overview
type: Tutorial
description: 本教程使用Flow Service API指导您完成将Platform连接到Microsoft Dynamics（以下简称“Dynamics”）帐户以收集CRM数据的步骤。
translation-type: tm+mt
source-git-commit: d332226541685108b58d88096146ed6048606774
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 1%

---


# 使用 [!DNL Microsoft Dynamics] API创建连 [!DNL Flow Service] 接器

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成连接到用于收 [!DNL Platform] 集CRM [!DNL Microsoft Dynamics] 数据的帐户（以下简称“Dynamics”）的步骤。

如果您希望在中使用用户界 [!DNL Experience Platform]面， [Dynamics源连接器UI教程将提供执行类似操作的分步说明](../../../ui/create/crm/dynamics.md) 。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md):E[!DNL xperience Platform] 提供虚拟沙箱，将单个实例分 [!DNL Platform] 为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用 [!DNL Platform] API成功连接到Dynamics帐 [!DNL Flow Service] 户。

### 收集所需的凭据

要连接 [!DNL Flow Service] 到，您 [!DNL Dynamics]必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUri` | 实例的服务 [!DNL Dynamics] URL。 |
| `username` | 您的用户帐户 [!DNL Dynamics] 的用户名。 |
| `password` | 帐户的密 [!DNL Dynamics] 码。 |

有关快速入门的更多信息，请访 [问此Dynamics文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

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

在连接 [!DNL Platform] 到帐户 [!DNL Dynamics] 之前，必须验证是否存在的连接规范 [!DNL Dynamics]。 如果连接规范不存在，则无法建立连接。

每个可用源都有其自己的唯一连接规范集，用于描述连接器属性，如身份验证要求。 您可以通过执行GET请求 [!DNL Dynamics] 和使用查询参数来查找连接规范。

**API格式**

发送不带GET参数的查询请求将返回所有可用源的连接规范。 您可以包含查询 `property=name=="dynamics-online"` 以获取专门用于的信息 [!DNL Dynamics]。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**请求**

以下请求检索的连接规范 [!DNL Dynamics]。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回的连接规范 [!DNL Dynamics]，包括其唯一标识符(`id`)。 下一步需要此ID才能创建基本连接。

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

## 为API创建连接

API连接指定源并包含该源的凭据。 每个帐户只需要一个API连接， [!DNL Dynamics] 因为它可用于创建多个源连接器以导入不同的数据。

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
| `auth.params.serviceUri` | 与您的实例关联的服务 [!DNL Dynamics] URI。 |
| `auth.params.username` | 与您的帐户关联的 [!DNL Dynamics] 用户名。 |
| `auth.params.password` | 与您的帐户关联的 [!DNL Dynamics] 密码。 |
| `connectionSpec.id` | 在上一步 `id` 中检索 [!DNL Dynamics] 到的帐户的连接规范。 |

**响应**

成功的响应包含基连接的唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 后续步骤

通过本教程，您已使用API为您的 [!DNL Dynamics] 帐户创建了连接，并且作为响应主体的一部分获得了唯一ID。 在下一个教程中，您可以使用此连接ID，因为您将学 [习如何使用流服务API浏览CRM系统](../../explore/crm.md)。