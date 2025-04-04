---
keywords: Experience Platform；主页；热门主题；Azure Azure Data Explorer；Azure Data Explorer；Azure Data Explorer
solution: Experience Platform
title: 使用流服务API创建Azure Azure Data Explorer基本连接
type: Tutorial
description: 了解如何使用流服务API将Azure Azure Data Explorer连接到Adobe Experience Platform。
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL Azure Azure Data Explorer]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Azure Data Explorer]创建基本连接的步骤。


## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Azure Data Explorer]所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Azure Data Explorer]连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | [!DNL Azure Data Explorer]服务器的终结点。 |
| `database` | [!DNL Azure Data Explorer]数据库的名称。 |
| `tenant` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一租户ID。 |
| `servicePrincipalId` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一服务主体ID。 |
| `servicePrincipalKey` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一服务主体密钥。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Azure Data Explorer]的连接规范ID为`0479cc14-7651-4354-b233-7480606c2ac3`。 |

有关入门的详细信息，请参阅此[[!DNL Azure Data Explorer] 文档](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Azure Data Explorer]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Azure Data Explorer]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
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
| `auth.params.endpoint` | [!DNL Azure Data Explorer]服务器的终结点。 |
| `auth.params.database` | [!DNL Azure Data Explorer]数据库的名称。 |
| `auth.params.tenant` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一租户ID。 |
| `auth.params.servicePrincipalId` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一服务主体ID。 |
| `auth.params.servicePrincipalKey` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一服务主体密钥。 |
| `connectionSpec.id` | [!DNL Azure Data Explorer]连接规范ID： `0479cc14-7651-4354-b233-7480606c2ac3`。 |

**响应**

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Azure Data Explorer]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将数据库数据引入Experience Platform](../../collect/database-nosql.md)
