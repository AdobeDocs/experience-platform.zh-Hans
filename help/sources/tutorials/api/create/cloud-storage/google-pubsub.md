---
title: 使用流服务API创建Google PubSub源连接
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Google PubSub帐户。
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 2b72d384e8edd91c662364dfac31ce4edff79172
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 1%

---

# 创建 [!DNL Google PubSub] 使用流服务API的源连接

本教程将指导您完成连接的步骤 [!DNL Google PubSub] (以下简称“[!DNL PubSub]&quot;)Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接所需了解的其他信息 [!DNL PubSub] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接到 [!DNL PubSub]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `projectId` | 验证所需的项目ID [!DNL PubSub]. |
| `credentials` | 验证所需的凭据或密钥 [!DNL PubSub]. |
| `topicId` | 的ID [!DNL PubSub] 表示消息馈送的资源。 如果要提供对中特定数据流的访问权限，则必须指定主题ID [!DNL Google PubSub] 来源。 |
| `subscriptionId` | 您的 [!DNL PubSub] 订阅。 在 [!DNL PubSub]，则通过订阅已发布消息的主题，可接收消息。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基目标连接和源目标连接相关的验证规范。 的 [!DNL PubSub] 连接规范ID是： `70116022-a743-464a-bbfe-e226a7f8210c`. |

有关这些值的更多信息，请参阅此 [[!DNL PubSub] 身份验证](https://cloud.google.com/pubsub/docs/authentication) 文档。 要使用基于服务帐户的身份验证，请参阅 [[!DNL PubSub] 创建服务帐户指南](https://cloud.google.com/docs/authentication/production#create_service_account) 以了解有关如何生成凭据的步骤。

>[!TIP]
>
>如果您使用基于服务帐户的身份验证，请确保您已向您的服务帐户授予足够的用户访问权限，并且在复制和粘贴凭据时，JSON中没有额外的空格。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

创建源连接的第一步是验证您的 [!DNL PubSub] 源并生成基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL PubSub] 身份验证凭据作为请求参数的一部分。

在此步骤中，您可以通过提供主题ID来定义您的帐户有权访问的数据。 只能访问与该主题ID关联的订阅。

>[!NOTE]
>
>在 [!DNL PubSub] 项目。 如果要添加主体（角色）以有权访问特定主题，则还必须将该主体（角色）添加到该主题的相应订阅中。 有关更多信息，请阅读 [[!DNL PubSub] 访问控制文档](https://cloud.google.com/pubsub/docs/access-control).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Google PubSub authentication credentials",
          "params": {
              "projectId": "acme-project",
              "credentials": "{CREDENTIALS}",
              "topicId": "acmeProjectAPI",
              "subscriptionId": "acme-project-api-new"
          }
      },
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.projectId` | 验证所需的项目ID [!DNL PubSub]. |
| `auth.params.credentials` | 验证所需的凭据或密钥 [!DNL PubSub]. |
| `auth.params.topicId` | 主题ID [!DNL PubSub] 要提供访问权限的源。 |
| `auth.params.subscriptionId` | 针对您的 [!DNL PubSub] 主题。 |
| `connectionSpec.id` | 的 [!DNL PubSub] 连接规范ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此基本连接ID才能创建源连接。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 创建源连接 {#source}

源连接创建并管理从中摄取数据的外部源的连接。 源连接由创建数据流所需的数据源、数据格式和源连接ID等信息组成。 源连接实例特定于租户和组织。

要创建源连接，请向 `/sourceConnections` 的端点 [!DNL Flow Service] API。

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
      "name": "Google PubSub source connection",
      "description": "A source connection for Google PubSub",
      "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "topicId": "acme-project",
          "subscriptionId": "{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 确保源连接的名称具有描述性，因为您可以使用该名称查找有关源连接的信息。 |
| `description` | 可提供的可选值，用于包含有关源连接的更多信息。 |
| `baseConnectionId` | 您的基本连接ID [!DNL PubSub] 上一步中生成的源。 |
| `connectionSpec.id` | 的固定连接规范ID [!DNL PubSub]. 此ID为： `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 的格式 [!DNL PubSub] 要摄取的数据。 目前，唯一支持的数据格式是 `json`. |
| `params.topicId` | 您的 [!DNL PubSub] 主题。 在 [!DNL PubSub]，主题是表示消息馈送的命名资源。 |
| `params.subscriptionId` | 与给定主题对应的订阅ID。 在 [!DNL PubSub]，则订阅允许您读取主题中的消息。 可以为单个主题分配一个或多个订阅。 |
| `params.dataType` | 此参数定义正在摄取的数据的类型。 支持的数据类型包括： `raw` 和 `xdm`. |

**响应**

成功的响应会返回唯一标识符(`id`)。 在下一个教程中，需要此ID才能创建数据流。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL PubSub] 源连接使用 [!DNL Flow Service] API。 在下一个教程中，您可以使用此源连接ID [使用创建流数据流 [!DNL Flow Service] API](../../collect/streaming.md).
