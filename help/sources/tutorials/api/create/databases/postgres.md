---
keywords: Experience Platform；主页；热门主题；PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: 使用流服务API创建PostgreSQL Base连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流程服务API将Adobe Experience Platform连接到PostgreSQL。
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API创建[!DNL PostgreSQL]基本连接

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL PostgreSQL]创建基本连接的步骤。


## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL PostgreSQL]。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL PostgreSQL]连接，必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的[!DNL PostgreSQL]帐户关联的连接字符串。 [!DNL PostgreSQL]连接字符串模式为：`Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL PostgreSQL]的连接规范ID为`74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

有关获取连接字符串的详细信息，请参阅此[[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/9.2/app-psql.html)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL PostgreSQL]身份验证凭据时，向`/connections`端点发出POST请求。

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
| `auth.params.connectionString` | 与您的[!DNL PostgreSQL]帐户关联的连接字符串。 [!DNL PostgreSQL]连接字符串模式为：`Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL PostgreSQL]连接规范ID:`74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

**响应**

成功的响应返回新创建的基本连接的唯一标识符(`id`)。 在下一个教程中浏览[!DNL PostgreSQL]数据库时需要此ID。

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL PostgreSQL]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您正在学习如何使用流服务API](../../explore/database-nosql.md)来浏览数据库或NoSQL系统。[
