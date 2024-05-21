---
title: 使用流服务API创建Google PubSub源连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Google PubSub帐户。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: fcac805e151d6142886eb8e05da0eb1babad2f69
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 2%

---

# 创建 [!DNL Google PubSub] 使用流服务API的源连接

>[!IMPORTANT]
>
>此 [!DNL Google PubSub] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

本教程将指导您完成连接的步骤 [!DNL Google PubSub] (以下简称“[!DNL PubSub]“)Experience Platform，使用 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL PubSub] 到平台，使用 [!DNL Flow Service] API。

### 收集所需的凭据

您必须提供下面列出的连接属性的值才能连接 [!DNL PubSub] 帐户至 [!DNL Flow Service]. 有关身份验证和先决条件设置的详细信息，请参阅 [[!DNL PubSub source] 概述](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).

>[!BEGINTABS]

>[!TAB 基于项目的身份验证]

| 凭据 | 描述 |
| --- | --- |
| `projectId` | 验证时需要项目ID [!DNL PubSub]. |
| `credentials` | 身份验证所需的凭据 [!DNL PubSub]. 您必须确保从凭据中删除空格后放入完整的JSON文件。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础和源目标连接相关的身份验证规范。 此 [!DNL PubSub] 连接规范ID为： `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB 主题和基于订阅的身份验证]

| 凭据 | 描述 |
| --- | --- |
| `credentials` | 身份验证所需的凭据 [!DNL PubSub]. 您必须确保从凭据中删除空格后放入完整的JSON文件。 |
| `topicName` | 表示消息馈送的资源名称。 如果要提供对特定数据流的访问权限，您必须指定主题名称。 [!DNL PubSub] 源。 主题名称格式为： `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | 您的名称 [!DNL PubSub] 订阅。 在 [!DNL PubSub]，订阅允许您通过订阅消息已发布到的主题来接收消息。 **注意**：单个 [!DNL PubSub] 订阅只能用于一个数据流。 要创建多个数据流，您必须有多个订阅。 订阅名称格式为： `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础和源目标连接相关的身份验证规范。 此 [!DNL PubSub] 连接规范ID为： `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

有关这些值的详细信息，请阅读此 [[!DNL PubSub] 身份验证](https://cloud.google.com/pubsub/docs/authentication) 文档。 要使用基于服务帐户的身份验证，请阅读此 [[!DNL PubSub] 创建服务帐户指南](https://cloud.google.com/docs/authentication/production#create_service_account) 以了解有关如何生成凭据的步骤。

>[!TIP]
>
>如果您使用的是基于服务帐户的身份验证，请确保在复制和粘贴凭据时，您已经向服务帐户授予了足够的用户访问权限，并且JSON中没有额外的空格。

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

>[!TIP]
>
>创建后，便无法更改的身份验证类型 [!DNL Google PubSub] 基本连接。 要更改身份验证类型，必须创建新的基本连接。

创建源连接的第一步是验证您的 [!DNL PubSub] 并生成基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并识别要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL PubSub] 作为请求参数一部分的身份验证凭据。

此 [!DNL PubSub] 源允许您指定在身份验证期间允许的访问类型。 您可以将帐户设置为具有超级用户访问权限或限制对特定用户的访问权限 [!DNL PubSub] 主题和订阅。

>[!NOTE]
>
>分配给的主体（角色） [!DNL PubSub] 项目继承于内创建的所有主题和订阅中 [!DNL PubSub] 项目。 如果希望主体（角色）可以访问特定主题，则还必须将该主体（角色）添加到主题的相应订阅中。 欲知更多信息，请参阅 [[!DNL PubSub] 关于访问控制的文档](<https://cloud.google.com/pubsub/docs/access-control>).

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基于项目的身份验证]

POST要创建基于项目的身份验证的基本连接，请向 `/connections` 端点并提供您的 `projectId` 和 `credentials` 请求正文中。

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
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Project Based Authentication",
          "params": {
              "projectId": "{PROJECT_ID}",
              "credentials": "{CREDENTIALS}"
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
| `auth.params.projectId` | 验证时需要项目ID [!DNL PubSub]. |
| `auth.params.credentials` | 身份验证所需的凭据或密钥 [!DNL PubSub]. |
| `connectionSpec.id` | 此 [!DNL PubSub] 连接规范ID： `70116022-a743-464a-bbfe-e226a7f8210c`. |

++++

+++响应

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此基本连接ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!TAB 主题和基于订阅的身份验证]

POST要创建与主题和基于订阅的身份验证的基本连接，请向 `/connections` 端点并提供您的 `credentials`， `topicName`、和 `subscriptionName` 请求正文中。

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
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
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
| `auth.params.credentials` | 身份验证所需的凭据或密钥 [!DNL PubSub]. |
| `auth.params.topicName` | 的项目ID和主题ID对 [!DNL PubSub] 要提供访问权限的源。 |
| `auth.params.subscriptionName` | 的项目ID和订阅ID对 [!DNL PubSub] 要提供访问权限的源。 |
| `connectionSpec.id` | 此 [!DNL PubSub] 连接规范ID： `70116022-a743-464a-bbfe-e226a7f8210c`. |

+++

+++响应

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此基本连接ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!ENDTABS]


## 创建源连接 {#source}

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
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可提供的可选值，用于包含有关源连接的更多信息。 |
| `baseConnectionId` | 您的的基本连接ID [!DNL PubSub] 上一步中生成的源。 |
| `connectionSpec.id` | 的固定连接规范ID [!DNL PubSub]. 此ID为： `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 的格式 [!DNL PubSub] 要摄取的数据。 目前，唯一支持的数据格式为 `json`. |
| `params.topicName` | 您的名称 [!DNL PubSub] 主题。 在 [!DNL PubSub]，主题是一个命名资源，表示消息馈送。 |
| `params.subscriptionName` | 与给定主题对应的订阅名称。 在 [!DNL PubSub]，订阅允许您从主题中读取消息。 可以将一个或多个订阅分配给单个主题。 |
| `params.dataType` | 此参数定义正在摄取的数据的类型。 支持的数据类型包括： `raw` 和 `xdm`. |

**响应**

成功的响应将返回唯一标识符(`id`)。 在下一个教程中，创建数据流时需要此ID。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL PubSub] 源连接使用 [!DNL Flow Service] API。 您可以在下一教程中使用此源连接ID [使用创建流数据流 [!DNL Flow Service] API](../../collect/streaming.md).
