---
keywords: Experience Platform；主页；热门主题；Google PubSub;google pubsub
solution: Experience Platform
title: 使用流服务API创建Google PubSub源连接
topic: 概述
type: 教程
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到Google PubSub帐户。
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 2%

---


# 使用流服务API创建[!DNL Google PubSub]源连接

>[!NOTE]
>
>[!DNL Google PubSub]连接器处于测试状态。 有关使用测试版标记的连接器的详细信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

本教程使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)指导您完成将[!DNL Google PubSub]（以下称为“[!DNL PubSub]”）连接到Adobe Experience Platform的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用[!DNL Flow Service] API成功创建[!DNL PubSub]源连接。

### 收集所需凭据

要使[!DNL Flow Service]连接到[!DNL PubSub]，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `projectId` | 验证[!DNL PubSub]所需的项目ID。 |
| `credentials` | 验证[!DNL PubSub]所需的凭据或密钥。 |

有关这些值的详细信息，请参阅以下[PubSub身份验证](https://cloud.google.com/pubsub/docs/authentication)文档。 如果您使用基于服务帐户的身份验证，请参阅以下[PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account)，了解有关如何生成凭据的步骤。

>[!TIP]
>
>如果您使用基于服务帐户的身份验证，请确保您已授予对您的服务帐户的足够用户访问权限，并且在复制和粘贴凭据时，JSON中没有额外的空白。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关文档中用于示例API调用的约定的信息，请参阅Experience Platform疑难解答指南中关于如何读取示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

要调用平台API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个头，它指定操作将在中进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个[!DNL PubSub]帐户只需要一个连接，因为它可用于创建多个数据流以引入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建[!DNL PubSub]连接，必须在POST请求中提供提供程序ID和连接规范ID。 提供程序ID为`521eee4d-8cbe-4906-bb48-fb6bd4450033`，连接规范ID为`70116022-a743-464a-bbfe-e226a7f8210c`。

**API格式**

```http
POST /connections
```

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
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
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

成功的响应会返回新创建的[!DNL PubSub]连接的连接ID。 在下一个教程中浏览您的云存储数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

通过本教程，您已使用[!DNL Flow Service] API创建了[!DNL PubSub]连接，并获得了其唯一连接ID。 您可以使用此连接ID来使用流服务API](../../collect/streaming.md)收集流数据。[
