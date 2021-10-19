---
keywords: Experience Platform；主页；热门主题；Snowflake;snowflake
solution: Experience Platform
title: 使用流服务API创建Snowflake库连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Snowflake。
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 76b3e3e9bcb27eb2bd6981ae6eb109410ae16336
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# 创建 [!DNL Snowflake] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Snowflake] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

以下部分提供了成功连接到所需了解的其他信息 [!DNL Snowflake] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Snowflake]，则必须提供以下连接属性：

| 凭据 | 描述 |
| --- | --- |
| `account` | 与您的 [!DNL Snowflake] 帐户。 完全合格 [!DNL Snowflake] 帐户名称包括您的帐户名称、地区和云平台。 例如：`cj12345.east-us-2.azure`。有关帐户名称的更多信息，请参阅此 [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | 的 [!DNL Snowflake] 仓库管理应用程序的查询执行过程。 每个 [!DNL Snowflake] 仓库彼此独立，在将数据移至Platform时必须单独进行访问。 |
| `database` | 的 [!DNL Snowflake] 数据库包含要引入平台的数据。 |
| `username` | 的用户名 [!DNL Snowflake] 帐户。 |
| `password` | 的密码 [!DNL Snowflake] 用户帐户。 |
| `connectionString` | 用于连接到的连接字符串 [!DNL Snowflake] 实例。 的连接字符串模式 [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Snowflake] is `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

有关入门的更多信息，请参阅此 [[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Snowflake] 身份验证凭据作为请求正文的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Snowflake]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Snowflake base connection",
        "description": "Snowflake base connection",
        "auth": {
            "specName": "Basic Authentication for Snowflake,
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.connectionString` | 用于连接到的连接字符串 [!DNL Snowflake] 实例。 的连接字符串模式 [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | 的 [!DNL Snowflake] 连接规范ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

通过阅读本教程，您已创建 [!DNL Snowflake] 使用 [!DNL Flow Service] API，并且已获取连接的唯一ID值。 在您了解如何 [使用流服务API浏览数据库](../../explore/database-nosql.md).
