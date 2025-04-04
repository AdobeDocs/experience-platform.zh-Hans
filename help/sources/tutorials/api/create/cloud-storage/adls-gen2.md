---
keywords: Experience Platform；主页；热门主题；Azure Data Lake Storage Gen2；Azure Data Lake Storage；Azure
solution: Experience Platform
title: 使用流服务API创建Azure Data Lake Storage Gen2基本连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到Azure Data Lake Storage Gen2。
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL Azure Data Lake Storage Gen2]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Azure Data Lake Storage Gen2]（以下称为“ADLS Gen2”）创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功创建ADLS Gen2源连接所需的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]连接到ADLS Gen2，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | ADLS Gen2的端点。 终结点模式为： `https://<accountname>.dfs.core.windows.net`。 |
| `servicePrincipalId` | 应用程序的客户端ID。 |
| `servicePrincipalKey` | 应用程序的密钥。 |
| `tenant` | 包含您的应用程序的租户信息。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 ADLS Gen2的连接规范ID为： `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`。 |

有关这些值的详细信息，请参阅[此ADLS Gen2文档](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供ADLS Gen2身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为ADLS Gen2创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.url` | ADLS Gen2帐户的URL端点。 |
| `auth.params.servicePrincipalId` | ADLS Gen2帐户的服务主体ID。 |
| `auth.params.servicePrincipalKey` | ADLS Gen2帐户的服务主体密钥。 |
| `auth.params.tenant` | ADLS Gen2帐户的租户信息。 |
| `connectionSpec.id` | ADLS Gen2连接规范标识： `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## 后续步骤

通过学习本教程，您已使用API创建了ADLS Gen2连接，并获取了唯一ID作为响应正文的一部分。 您可以使用此连接ID以使用流服务API](../../explore/cloud-storage.md)来[浏览云存储。
