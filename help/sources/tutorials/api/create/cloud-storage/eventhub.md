---
keywords: Experience Platform；主页；热门主题；事件中心；Azure事件中心；事件中心
solution: Experience Platform
title: 使用流服务API创建Azure事件中心源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Azure事件中心帐户。
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 1%

---


# 使用[!DNL Flow Service] API创建[!DNL Azure Event Hubs]源连接

本教程将指导您完成使用[[!DNL Flow Service]  API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将[!DNL Azure Event Hubs]（以下称“[!DNL Event Hubs]”）连接到Experience Platform的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
- [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功将[!DNL Event Hubs]连接到平台。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Event Hubs]帐户连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `sasKey` | 生成的共享访问签名。 |
| `namespace` | 您正在访问的[!DNL Event Hubs]的命名空间。 [!DNL Event Hubs]命名空间提供了一个唯一的范围界定容器，您可以在其中创建一个或多个[!DNL Event Hubs]。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Event Hubs]连接规范ID为：`bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |

有关这些值的详细信息，请参阅[此事件中心文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

创建源连接的第一步是验证[!DNL Event Hubs]源并生成基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Event Hubs]身份验证凭据时，向`/connections`端点发出POST请求。

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
| `auth.params.sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `auth.params.sasKey` | 生成的共享访问签名。 |
| `auth.params.namespace` | 您正在访问的[!DNL Event Hubs]的命名空间。 |
| `connectionSpec.id` | [!DNL Event Hubs]连接规范ID为：`bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 要创建源连接，需要在下一步中使用此连接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 创建源连接

源连接创建并管理从中摄取数据的外部源的连接。 源连接由创建数据流所需的数据源、数据格式和源连接ID等信息组成。 源连接实例特定于租户和IMS组织。

要创建源连接，请向[!DNL Flow Service] API的`/sourceConnections`端点发出POST请求。

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
| `description` | 可提供的可选值，用于包含有关源连接的更多信息。 |
| `baseConnectionId` | 在上一步中生成的[!DNL Event Hubs]源的连接ID。 |
| `connectionSpec.id` | [!DNL Event Hubs]的固定连接规范ID。 此ID为：`bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |
| `data.format` | 要摄取的[!DNL Event Hubs]数据的格式。 目前，唯一支持的数据格式是`json`。 |
| `params.eventHubName` | [!DNL Event Hubs]源的名称。 |
| `params.dataType` | 此参数定义正在摄取的数据的类型。 支持的数据类型包括：`raw`和`xdm`。 |
| `params.reset` | 此参数定义数据的读取方式。 使用`latest`开始从最新数据中读取数据，使用`earliest`开始从流中的第一个可用数据中读取数据。 此参数是可选的，如果未提供，则默认为`earliest`。 |
| `params.consumerGroup` | 用于[!DNL Event Hubs]的发布或订阅机制。 此参数是可选的，如果未提供，则默认为`$Default`。 有关更多信息，请参阅本[[!DNL Event Hubs] 事件用户指南](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers)。 |

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Event Hubs]源连接。 在下一个教程中，您可以使用此源连接ID来使用 [!DNL Flow Service] API](../../collect/streaming.md)创建流数据流。[
