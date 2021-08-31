---
keywords: Experience Platform；主页；热门主题；Google PubSub;Google Pubsub
solution: Experience Platform
title: 使用流程服务API创建Google PubSub源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Google PubSub帐户。
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---

# 使用流服务API创建[!DNL Google PubSub]源连接

>[!NOTE]
>
>[!DNL Google PubSub]连接器处于测试阶段。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

本教程将指导您完成使用[[!DNL Flow Service]  API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将[!DNL Google PubSub]（以下称“[!DNL PubSub]”）连接到Experience Platform的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功将[!DNL PubSub]连接到平台。

### 收集所需的凭据

要使[!DNL Flow Service]连接到[!DNL PubSub]，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `projectId` | 验证[!DNL PubSub]所需的项目ID。 |
| `credentials` | 验证[!DNL PubSub]所需的凭据或密钥。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基目标连接和源目标连接相关的验证规范。 [!DNL PubSub]连接规范ID为：`70116022-a743-464a-bbfe-e226a7f8210c`。 |

有关这些值的更多信息，请参阅此[[!DNL PubSub] authentication](https://cloud.google.com/pubsub/docs/authentication)文档。 要使用基于服务帐户的身份验证，请参阅本[[!DNL PubSub] 创建服务帐户指南](https://cloud.google.com/docs/authentication/production#create_service_account) ，以了解如何生成凭据的步骤。

>[!TIP]
>
>如果您使用基于服务帐户的身份验证，请确保您已向您的服务帐户授予足够的用户访问权限，并且在复制和粘贴凭据时，JSON中没有额外的空格。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

创建源连接的第一步是验证[!DNL PubSub]源并生成基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL PubSub]身份验证凭据时，向`/connections`端点发出POST请求。

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
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "auth": {
            "specName": "Google PubSub authentication credentials",
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
| `auth.params.projectId` | 验证[!DNL PubSub]所需的项目ID。 |
| `auth.params.credentials` | 验证[!DNL PubSub]所需的凭据或密钥。 |
| `connectionSpec.id` | [!DNL PubSub]连接规范ID:`70116022-a743-464a-bbfe-e226a7f8210c`。 |

**响应**

成功的响应返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此基本连接ID才能创建源连接。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 创建源连接 {#source}

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
            "topicId": "{TOPIC_ID}",
            "subscriptionId": "{SUBSCRIPTION_ID}",
            "dataType": "raw"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 确保源连接的名称具有描述性，因为您可以使用该名称查找有关源连接的信息。 |
| `description` | 可提供的可选值，用于包含有关源连接的更多信息。 |
| `baseConnectionId` | 在上一步中生成的[!DNL PubSub]源的基本连接ID。 |
| `connectionSpec.id` | [!DNL PubSub]的固定连接规范ID。 此ID为：`70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 要摄取的[!DNL PubSub]数据的格式。 目前，唯一支持的数据格式是`json`。 |
| `params.topicId` | 主题ID定义了由发布者发送消息的特定命名资源 |
| `params.subscriptionId` | 订阅ID定义特定的命名资源，该资源表示来自单个特定主题的消息流，该消息流将被传送到订阅应用程序。 |
| `params.dataType` | 此参数定义正在摄取的数据的类型。 支持的数据类型包括：`raw`和`xdm`。 |

**响应**

成功的响应会返回新创建源连接的唯一标识符(`id`)。 在下一个教程中，需要此ID才能创建数据流。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL PubSub]源连接。 在下一个教程中，您可以使用此源连接ID来使用 [!DNL Flow Service] API](../../collect/streaming.md)创建流数据流。[
