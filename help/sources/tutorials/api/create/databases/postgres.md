---
keywords: Experience Platform；主页；热门主题；PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: 使用流服务API创建PostgreSQL Base连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流程服务API将Adobe Experience Platform连接到PostgreSQL。
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 0ca900b77275851076a13dcc4b8b4a9995ddd0be
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---

# 创建 [!DNL PostgreSQL] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL PostgreSQL] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL PostgreSQL] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL PostgreSQL]，则必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与 [!DNL PostgreSQL] 帐户。 的 [!DNL PostgreSQL] 连接字符串模式为： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL PostgreSQL] is `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

有关获取连接字符串的详细信息，请参阅此 [[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/9.2/app-psql.html).

#### 为连接字符串启用SSL加密

您可以为 [!DNL PostgreSQL] 连接字符串，方法是将连接字符串附加到以下属性：

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `EncryptionMethod` | 允许您在 [!DNL PostgreSQL] 数据。 | <uL><li>`EncryptionMethod=0`(已禁用)</li><li>`EncryptionMethod=1`(已启用)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 验证由您的 [!DNL PostgreSQL] 数据库 `EncryptionMethod` 的次数。 | <uL><li>`ValidationServerCertificate=0`(已禁用)</li><li>`ValidationServerCertificate=1`(已启用)</li></ul> |

以下是 [!DNL PostgreSQL] 附加了SSL加密的连接字符串： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL PostgreSQL] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL PostgreSQL]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.connectionString` | 与 [!DNL PostgreSQL] 帐户。 的 [!DNL PostgreSQL] 连接字符串模式为： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | 的 [!DNL PostgreSQL] 连接规范ID: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**响应**

成功的响应会返回唯一标识符(`id`)。 需要此ID才能浏览您的 [!DNL PostgreSQL] 数据库。

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL PostgreSQL] 连接基连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
