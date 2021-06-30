---
keywords: Experience Platform；主页；热门主题；bigquery;Google;Google;Google BigQuery
solution: Experience Platform
title: 使用流服务API创建Google BigQuery基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Google BigQuery。
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: e8c6620a6d2447a577bd56192030ff4353c62c62
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Google BigQuery]基本连接

>[!NOTE]
>
>[!DNL Google BigQuery]连接器处于测试阶段。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service]  API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)为[!DNL Google BigQuery]（以下称“[!DNL BigQuery]”）创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL BigQuery]。

### 收集所需的凭据

要使[!DNL Flow Service]连接[!DNL BigQuery]到平台，您必须提供以下OAuth 2.0身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `project` | 要查询的默认[!DNL BigQuery]项目的项目ID。 |
| `clientID` | 用于生成刷新令牌的ID值。 |
| `clientSecret` | 用于生成刷新令牌的密钥值。 |
| `refreshToken` | 从[!DNL Google]获取的刷新令牌，用于授权对[!DNL BigQuery]的访问。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL BigQuery]的连接规范ID是：`3c9b37f8-13a6-43d8-bad3-b863b941fedd`。 |

有关这些值的详细信息，请参阅此[[!DNL BigQuery] 文档](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL BigQuery]身份验证凭据时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL BigQuery]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.project` | 要查询的默认[!DNL BigQuery]项目的项目ID。 反对。 |
| `auth.params.clientId` | 用于生成刷新令牌的ID值。 |
| `auth.params.clientSecret` | 用于生成刷新令牌的客户端值。 |
| `auth.params.refreshToken` | 从[!DNL Google]获取的刷新令牌，用于授权对[!DNL BigQuery]的访问。 |
| `connectionSpec.id` | [!DNL Google BigQuery]连接规范ID:`3c9b37f8-13a6-43d8-bad3-b863b941fedd`。 |

**响应**

成功的响应返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL BigQuery]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您正在学习如何使用流服务API](../../explore/database-nosql.md)来浏览数据库或NoSQL系统。[
