---
title: 使用流服务API创建Google BigQuery基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Google BigQuery。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API创建[!DNL Google BigQuery]基本连接

>[!IMPORTANT]
>
>[!DNL Google BigQuery]源在源目录中可供已购买Real-time Customer Data Platform Ultimate的用户使用。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Google BigQuery]创建基本连接。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时允许您使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了将单个Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Google BigQuery]所需了解的其他信息。

### 收集所需的凭据

有关收集所需凭据的详细步骤，请阅读[[!DNL Google BigQuery] 身份验证指南](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供[!DNL Google BigQuery]身份验证凭据作为POST参数的一部分时，向`/connections`端点请求请求。

**API格式**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 使用基本身份验证]

**请求**

以下请求使用基本身份验证为[!DNL Google BigQuery]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection with basic authentication",
        "description": "Google BigQuery connection with basic authentication",
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
| `auth.params.project` | 要查询的默认[!DNL Google BigQuery]项目的项目ID。 反对。 |
| `auth.params.clientId` | 用于生成刷新令牌的ID值。 |
| `auth.params.clientSecret` | 用于生成刷新令牌的客户端值。 |
| `auth.params.refreshToken` | 从[!DNL Google]获得的刷新令牌用于授权访问[!DNL Google BigQuery]。 |
| `connectionSpec.id` | [!DNL Google BigQuery]连接规范ID： `3c9b37f8-13a6-43d8-bad3-b863b941fedd`。 |

**响应**

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

>[!TAB 使用服务身份验证]


**请求**

以下请求使用服务身份验证为[!DNL Google BigQuery]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery base connection with service account",
        "description": "Google BigQuery connection with service account",
        "auth": {
            "specName": "Service Authentication",
            "params": {
                    "projectId": "{PROJECT_ID}",
                    "keyFileContent": "{KEY_FILE_CONTENT},
                    "largeResultsDataSetId": "{LARGE_RESULTS_DATASET_ID}"
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
| `auth.params.projectId` | 要查询的默认[!DNL Google BigQuery]项目的项目ID。 反对。 |
| `auth.params.keyFileContent` | 用于验证服务帐户的密钥文件。 您必须在[!DNL Base64]中编码密钥文件内容。 |
| `auth.params.largeResultsDataSetId` | （可选）启用大型结果集支持所需的预创建[!DNL Google BigQuery]数据集ID。 |

**响应**

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

>[!ENDTABS]


## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Google BigQuery]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API将数据库数据引入平台](../../collect/database-nosql.md)
