---
keywords: Experience Platform；主页；热门主题；事件中心；Azure事件中心；事件中心
solution: Experience Platform
title: Create an Azure Event Hubs Source Connection Using the Flow Service API
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Azure事件中心帐户。
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 1%

---


# 创建 [!DNL Azure Event Hubs] 源连接使用 [!DNL Flow Service] API

本教程将指导您完成连接的步骤 [!DNL Azure Event Hubs] (以下简称“[!DNL Event Hubs]&quot;)Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
- [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接所需了解的其他信息 [!DNL Event Hubs] 使用 [!DNL Flow Service] API。

### Gather required credentials

为 [!DNL Flow Service] 与 [!DNL Event Hubs] 帐户，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `sasKeyName` | The name of the authorization rule, which is also known as the SAS key name. |
| `sasKey` | 的主键 [!DNL Event Hubs] 命名空间。 的 `sasPolicy` 该 `sasKey` 对应于必须拥有 `manage` 为 [!DNL Event Hubs] 列表。 |
| `namespace` | The namespace of the [!DNL Event Hubs] you are accessing. 安 [!DNL Event Hubs] 命名空间提供了唯一的作用域容器，您可以在其中创建一个或多个 [!DNL Event Hubs]. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的 [!DNL Event Hubs] 连接规范ID是： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

有关这些值的更多信息，请参阅 [此事件中心文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

创建源连接的第一步是验证您的 [!DNL Event Hubs] 源并生成基本连接ID。 A base connection ID allows you to explore and navigate files from within your source and identify specific items that you want to ingest, including information regarding their data types and formats.

要创建基本连接ID，请向 `/connections` 提供 [!DNL Event Hubs] 身份验证凭据作为请求参数的一部分。

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
        "name": "Azure Event Hubs connection",
        "description": "Connector for Azure Event Hubs",
        "auth": {
            "specName": "Azure EventHub authentication credentials",
            "params": {
                "sasKeyName": "{SAS_KEY_NAME}",
                "sasKey": "{SAS_KEY}",
                "namespace": "{NAMESPACE}"
            }
        },
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.sasKeyName` | The name of the authorization rule, which is also known as the SAS key name. |
| `auth.params.sasKey` | 生成的共享访问签名。 |
| `auth.params.namespace` | The namespace of the [!DNL Event Hubs] you are accessing. |
| `connectionSpec.id` | The [!DNL Event Hubs] connection specification ID is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 要创建源连接，需要在下一步中使用此连接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 创建源连接

源连接创建并管理从中摄取数据的外部源的连接。 源连接由创建数据流所需的数据源、数据格式和源连接ID等信息组成。 A source connection instance is specific to a tenant and IMS Organization.

To create a source connection, make a POST request to the `/sourceConnections` endpoint of the [!DNL Flow Service] API.

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'authorization: Bearer {ACCESS_TOKEN}' \
    -H 'content-type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_Org}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Azure Event Hubs source connection",
        "description": "A source connection for Azure Event Hubs",
        "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "eventHubName": "{EVENTHUB_NAME}",
            "dataType": "raw",
            "reset": "latest",
            "consumerGroup": "{CONSUMER_GROUP}"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 确保源连接的名称具有描述性，因为您可以使用该名称查找有关源连接的信息。 |
| `description` | An optional value that you can provide to include more information on your source connection. |
| `baseConnectionId` | The connection ID of your [!DNL Event Hubs] source that was generated in the previous step. |
| `connectionSpec.id` | 的固定连接规范ID [!DNL Event Hubs]. 此ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | 的格式 [!DNL Event Hubs] 要摄取的数据。 目前，唯一支持的数据格式是 `json`. |
| `params.eventHubName` | 您的 [!DNL Event Hubs] 来源。 |
| `params.dataType` | 此参数定义正在摄取的数据的类型。 支持的数据类型包括： `raw` 和 `xdm`. |
| `params.reset` | 此参数定义数据的读取方式。 Use `latest` to start reading from the most recent data, and use `earliest` to start reading from the first available data in the stream. 此参数为可选参数，默认为 `earliest` 如果未提供。 |
| `params.consumerGroup` | 要用于的发布或订阅机制 [!DNL Event Hubs]. 此参数为可选参数，默认为 `$Default` 如果未提供。 请参阅 [[!DNL Event Hubs] 事件消费者指南](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) 以了解更多信息。 |

## 后续步骤

通过阅读本教程，您已创建 [!DNL Event Hubs] 源连接使用 [!DNL Flow Service] API。 在下一个教程中，您可以使用此源连接ID [使用创建流数据流 [!DNL Flow Service] API](../../collect/streaming.md).
