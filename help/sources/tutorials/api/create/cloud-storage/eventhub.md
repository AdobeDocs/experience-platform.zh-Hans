---
title: 使用流服务API创建Azure事件中心源连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Azure事件中心帐户。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 3%

---

# 创建 [!DNL Azure Event Hubs] 源连接使用 [!DNL Flow Service] API

>[!IMPORTANT]
>
>此 [!DNL Azure Event Hubs] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

本教程提供了创建 [!DNL Azure Event Hubs] (以下简称“[!DNL Event Hubs]“)Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

- [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下内容构建、标记和增强传入数据： [!DNL Platform] 服务。
- [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL Event Hubs] 到平台，使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以与您的 [!DNL Event Hubs] 帐户，您必须提供以下连接属性的值：

>[!BEGINTABS]

>[!TAB 标准身份验证]

| 凭据 | 描述 |
| --- | --- |
| `sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `sasKey` | 的主键 [!DNL Event Hubs] 命名空间。 此 `sasPolicy` 该 `sasKey` 对应于必须具有 `manage` 权限已配置，用于 [!DNL Event Hubs] 要填充的列表。 |
| `namespace` | 的命名空间 [!DNL Event Hubs] 您正在访问。 An [!DNL Event Hubs] namespace提供了一个唯一的范围容器，您可以在其中创建一个或多个 [!DNL Event Hubs]. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 此 [!DNL Event Hubs] 连接规范ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!TAB SAS身份验证]

| 凭据 | 描述 |
| --- | --- |
| `sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `sasKey` | 的主键 [!DNL Event Hubs] 命名空间。 此 `sasPolicy` 该 `sasKey` 对应于必须具有 `manage` 权限已配置，用于 [!DNL Event Hubs] 要填充的列表。 |
| `namespace` | 的命名空间 [!DNL Event Hubs] 您正在访问。 An [!DNL Event Hubs] namespace提供了一个唯一的范围容器，您可以在其中创建一个或多个 [!DNL Event Hubs]. |
| `eventHubName` | 您的名称 [!DNL Event Hubs] 源。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 此 [!DNL Event Hubs] 连接规范ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!ENDTABS]

有关这些值的更多信息，请参阅 [此事件中心文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

>[!TIP]
>
>创建后，便无法更改的身份验证类型 [!DNL Event Hubs] 基本连接。 要更改身份验证类型，必须创建新的基本连接。

创建源连接的第一步是验证您的 [!DNL Event Hubs] 并生成基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并识别要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Event Hubs] 作为请求参数一部分的身份验证凭据。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 标准身份验证]

POST要使用标准身份验证创建帐户，请向 `/connections` 端点，同时为提供值 `sasKeyName`， `sasKey`、和 `namespace`.

+++请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.namespace` | 的命名空间 [!DNL Event Hubs] 您正在访问。 |
| `connectionSpec.id` | 此 [!DNL Event Hubs] 连接规范ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++响应

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此连接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB SAS身份验证]

POST要使用SAS身份验证创建帐户，请向 `/connections` 端点，同时为提供值 `sasKeyName`， `sasKey`，`namespace`、和 `eventHubName`.

+++请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
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
| `auth.params.namespace` | 的命名空间 [!DNL Event Hubs] 您正在访问。 |
| `params.eventHubName` | 您的名称 [!DNL Event Hubs] 源。 |
| `connectionSpec.id` | 此 [!DNL Event Hubs] 连接规范ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++响应

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此连接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## 创建源连接

>[!TIP]
>
>An [!DNL Event Hubs] 使用者组只能在给定时间用于单个流。

源连接创建和管理与摄取数据的外部源的连接。 源连接由数据源、数据格式和创建数据流所需的源连接ID等信息组成。 源连接实例特定于租户和组织。

POST要创建源连接，请向 `/sourceConnections` 的端点 [!DNL Flow Service] API。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
          "eventHubName": "{EVENT_HUB_NAME}",
          "dataType": "raw",
          "reset": "latest",
          "consumerGroup": "{CONSUMER_GROUP}"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可提供的可选值，用于包含有关源连接的更多信息。 |
| `baseConnectionId` | 的连接ID [!DNL Event Hubs] 上一步中生成的源。 |
| `connectionSpec.id` | 的固定连接规范ID [!DNL Event Hubs]. 此ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | 的格式 [!DNL Event Hubs] 要摄取的数据。 目前，唯一支持的数据格式为 `json`. |
| `params.eventHubName` | 您的名称 [!DNL Event Hubs] 源。 |
| `params.dataType` | 此参数定义正在摄取的数据的类型。 支持的数据类型包括： `raw` 和 `xdm`. |
| `params.reset` | 此参数定义数据的读取方式。 使用 `latest` 以开始读取最新数据，并使用 `earliest` 以开始读取流中的第一个可用数据。 此参数为可选参数，默认为 `earliest` 如果未提供。 |
| `params.consumerGroup` | 要使用的发布或订阅机制 [!DNL Event Hubs]. 此参数为可选参数，默认为 `$Default` 如果未提供。 请参阅此 [[!DNL Event Hubs] 事件使用者指南](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) 以了解更多信息。 **注意**：一个 [!DNL Event Hubs] 使用者组只能在给定时间用于单个流。 |

## 后续步骤

在本教程之后，您已创建一个 [!DNL Event Hubs] 源连接使用 [!DNL Flow Service] API。 您可以在下一教程中使用此源连接ID [使用创建流数据流 [!DNL Flow Service] API](../../collect/streaming.md).
