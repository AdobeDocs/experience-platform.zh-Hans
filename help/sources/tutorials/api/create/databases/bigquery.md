---
title: 使用流服务API创建Google BigQuery基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Google BigQuery。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 4%

---

# 创建 [!DNL Google BigQuery] 基本连接使用 [!DNL Flow Service] API

>[!IMPORTANT]
>
>此 [!DNL Google BigQuery] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Google BigQuery] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL Google BigQuery] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 连接 [!DNL Google BigQuery] 到Platform时，必须提供以下OAuth 2.0身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `project` | 默认的项目ID [!DNL Google BigQuery] 要查询的项目。 |
| `clientID` | 用于生成刷新令牌的ID值。 |
| `clientSecret` | 用于生成刷新令牌的机密值。 |
| `refreshToken` | 刷新令牌获取自 [!DNL Google] 用于授权访问 [!DNL Google BigQuery]. |
| `largeResultsDataSetId` | 预先创建的  [!DNL Google BigQuery] 启用对大型结果集的支持所需的数据集ID。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Google BigQuery] 为： `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

有关这些值的更多信息，请参阅此 [[!DNL Google BigQuery] 文档](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Google BigQuery] 作为请求参数一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL Google BigQuery]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.project` | 默认的项目ID [!DNL Google BigQuery] 要查询的项目。 反对。 |
| `auth.params.clientId` | 用于生成刷新令牌的ID值。 |
| `auth.params.clientSecret` | 用于生成刷新令牌的客户端值。 |
| `auth.params.refreshToken` | 刷新令牌获取自 [!DNL Google] 用于授权访问 [!DNL Google BigQuery]. |
| `connectionSpec.id` | 此 [!DNL Google BigQuery] 连接规范ID： `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL Google BigQuery] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流以使用将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
