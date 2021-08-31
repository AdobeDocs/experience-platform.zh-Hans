---
keywords: Experience Platform；主页；热门主题；Azure AzureData Explorer;AzureData Explorer;AzureData Explorer
solution: Experience Platform
title: 使用流服务API创建Azure AzureData Explorer库连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流程服务API将Azure AzureData Explorer连接到Adobe Experience Platform。
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Azure Azure Data Explorer]基本连接

>[!NOTE]
>
>[!DNL Azure Azure Data Explorer]连接器处于测试阶段。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Azure Data Explore]创建基本连接的步骤。


## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL Azure Data Explorer]。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Azure Data Explorer]连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | [!DNL Azure Data Explorer]服务器的端点。 |
| `database` | [!DNL Azure Data Explorer]数据库的名称。 |
| `tenant` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一租户ID。 |
| `servicePrincipalId` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一服务主体ID。 |
| `servicePrincipalKey` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一服务主体键。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Azure Data Explorer]的连接规范ID为`0479cc14-7651-4354-b233-7480606c2ac3`。 |

有关入门的详细信息，请参阅此[[!DNL Azure Data Explorer] 文档](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Azure Data Explorer]身份验证凭据时，向`/connections`端点发出POST请求。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.endpoint` | [!DNL Azure Data Explorer]服务器的端点。 |
| `auth.params.database` | [!DNL Azure Data Explorer]数据库的名称。 |
| `auth.params.tenant` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一租户ID。 |
| `auth.params.servicePrincipalId` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一服务主体ID。 |
| `auth.params.servicePrincipalKey` | 用于连接到[!DNL Azure Data Explorer]数据库的唯一服务主体键。 |
| `connectionSpec.id` | [!DNL Azure Data Explorer]连接规范ID:`0479cc14-7651-4354-b233-7480606c2ac3`。 |

**响应**

成功的响应返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Azure Data Explorer]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流服务API](../../explore/database-nosql.md)浏览数据库。
