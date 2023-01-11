---
keywords: Experience Platform；主页；热门主题；Azure AzureData Explorer;AzureData Explorer;AzureData Explorer
solution: Experience Platform
title: 使用流服务API创建Azure AzureData Explorer库连接
type: Tutorial
description: 了解如何使用流程服务API将Azure AzureData Explorer连接到Adobe Experience Platform。
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# 创建 [!DNL Azure Azure Data Explorer] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Azure Data Explorer] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Azure Data Explorer] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Azure Data Explorer]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | 的端点 [!DNL Azure Data Explorer] 服务器。 |
| `database` | 的名称 [!DNL Azure Data Explorer] 数据库。 |
| `tenant` | 用于连接到的唯一租户ID [!DNL Azure Data Explorer] 数据库。 |
| `servicePrincipalId` | 用于连接到的唯一服务主体ID [!DNL Azure Data Explorer] 数据库。 |
| `servicePrincipalKey` | 用于连接到的唯一服务主体键 [!DNL Azure Data Explorer] 数据库。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Azure Data Explorer] is `0479cc14-7651-4354-b233-7480606c2ac3`. |

有关入门的更多信息，请参阅此 [[!DNL Azure Data Explorer] 文档](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Azure Data Explorer] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Azure Data Explorer]:

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
| `auth.params.endpoint` | 的端点 [!DNL Azure Data Explorer] 服务器。 |
| `auth.params.database` | 的名称 [!DNL Azure Data Explorer] 数据库。 |
| `auth.params.tenant` | 用于连接到的唯一租户ID [!DNL Azure Data Explorer] 数据库。 |
| `auth.params.servicePrincipalId` | 用于连接到的唯一服务主体ID [!DNL Azure Data Explorer] 数据库。 |
| `auth.params.servicePrincipalKey` | 用于连接到的唯一服务主体键 [!DNL Azure Data Explorer] 数据库。 |
| `connectionSpec.id` | 的 [!DNL Azure Data Explorer] 连接规范ID: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Azure Data Explorer] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
