---
keywords: Experience Platform；主页；热门主题；PostgreSQL；postgresql；PSQL；psql
solution: Experience Platform
title: 使用流服务API创建PostgreSQL基本连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到PostgreSQL。
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API创建[!DNL PostgreSQL]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL PostgreSQL]创建基本连接的步骤。


## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL PostgreSQL]所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL PostgreSQL]连接，您必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的[!DNL PostgreSQL]帐户关联的连接字符串。 [!DNL PostgreSQL]连接字符串模式为： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL PostgreSQL]的连接规范ID为`74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

有关获取连接字符串的详细信息，请参阅此[[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/9.2/app-psql.html)。

#### 为连接字符串启用SSL加密

您可以为[!DNL PostgreSQL]连接字符串启用SSL加密，方法是使用以下属性附加连接字符串：

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `EncryptionMethod` | 允许您对[!DNL PostgreSQL]数据启用SSL加密。 | <uL><li>`EncryptionMethod=0`（已禁用）</li><li>`EncryptionMethod=1`（已启用）</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 在应用`EncryptionMethod`时验证[!DNL PostgreSQL]数据库发送的证书。 | <uL><li>`ValidationServerCertificate=0`（已禁用）</li><li>`ValidationServerCertificate=1`（已启用）</li></ul> |

以下是附加了SSL加密的[!DNL PostgreSQL]连接字符串的示例： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL PostgreSQL]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL PostgreSQL]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| ------------- | --------------- |
| `auth.params.connectionString` | 与您的[!DNL PostgreSQL]帐户关联的连接字符串。 [!DNL PostgreSQL]连接字符串模式为： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL PostgreSQL]连接规范ID： `74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

**响应**

成功的响应返回新创建的基本连接的唯一标识符(`id`)。 在下一个教程中，需要此ID才能浏览您的[!DNL PostgreSQL]数据库。

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## 后续步骤

通过学习本教程，您已使用[!DNL Flow Service] API创建了[!DNL PostgreSQL]连接基连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将数据库数据引入Experience Platform](../../collect/database-nosql.md)
