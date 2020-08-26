---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用流服务API创建AzureData Explorer连接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 1%

---


# 使用API [!DNL Azure Data Explorer] 创建连接 [!DNL Flow Service] 器

>[!NOTE]
>
>连接 [!DNL Azure Data Explorer] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成将 [!DNL Azure Data Explorer] 其连接(以下称“Data Explorer”)的步骤 [!DNL Experience Platform]。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了成功连接到使用API所需了解的其 [!DNL Data Explorer] 他信 [!DNL Flow Service] 息。

### 收集所需的凭据

要连接 [!DNL Flow Service] ，必须 [!DNL Data Explorer]为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | The endpoint of the [!DNL Data Explorer] server. |
| `database` | The name of the [!DNL Data Explorer] database. |
| `tenant` | 用于连接数据库的唯一租户 [!DNL Data Explorer] ID。 |
| `servicePrincipalId` | 用于连接到数据库的唯一服务主体 [!DNL Data Explorer] ID。 |
| `servicePrincipalKey` | 用于连接到数据库的唯一服务主体 [!DNL Data Explorer] 键。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 连接规范ID [!DNL Data Explorer] 为 `0479cc14-7651-4354-b233-7480606c2ac3`。 |

有关快速入门的详细信息，请参 [阅此Data Explorer文档](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程可为所有E API调用中的每个所需标头提供值[!DNL xperience Platform] ，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资源 [!DNL Flow Service]的资源)都隔离到特定虚拟沙箱。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个帐户只需要一 [!DNL Data Explorer] 个连接器，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建连接， [!DNL Data Explorer] 其唯一连接规范ID必须作为POST请求的一部分提供。 连接规范ID [!DNL Data Explorer] 为 `0479cc14-7651-4354-b233-7480606c2ac3`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Data Explorer connection",
        "description": "A connection for Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.endpoint` | The endpoint of the [!DNL Data Explorer] server. |
| `auth.params.database` | The name of the [!DNL Data Explorer] database. |
| `auth.params.tenant` | 用于连接数据库的唯一租户 [!DNL Data Explorer] ID。 |
| `auth.params.servicePrincipalId` | 用于连接到数据库的唯一服务主体 [!DNL Data Explorer] ID。 |
| `auth.params.servicePrincipalKey` | 用于连接到数据库的唯一服务主体 [!DNL Data Explorer] 键。 |
| `connectionSpec.id` | 连接 [!DNL Data Explorer] 规范ID: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 后续步骤

通过本教程，您已使用 [!DNL Data Explorer] API创建了 [!DNL Flow Service] 一个连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您将学习如 [何使用流服务API浏览数据库](../../explore/database-nosql.md)。
