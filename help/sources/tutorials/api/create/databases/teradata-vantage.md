---
keywords: Experience Platform；主页；热门主题；Teradata Vantage
title: 使用流服务API创建Teradata Vantage基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Teradata Vantage。
exl-id: 88707dca-3c7a-43c7-9d71-473ad9715fc6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL Teradata Vantage]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Teradata Vantage]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

以下部分提供了使用[!DNL Flow Service] API成功连接到[!DNL Teradata Vantage]时需要了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Teradata Vantage]连接，您必须提供以下连接属性：

| 凭据 | 描述 |
| --- | --- |
| `connectionString` | 连接字符串是一个字符串，它提供有关数据源以及如何连接到该数据源的信息。 [!DNL Teradata Vantage]的连接字符串模式为`DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Teradata Vantage]的连接规范ID为： `2fa8af9c-2d1a-43ea-a253-f00a00c74412` |

有关入门的详细信息，请参阅此[[!DNL Teradata Vantage] 文档](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options)。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Teradata Vantage]身份验证凭据作为请求正文的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Teradata Vantage]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Teradata Vantage base connection",
      "description": "Teradata Vantage base connection",
      "auth": {
          "specName": "ConnectionString,
          "params": {
              "connectionString": "DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.connectionString` | 用于连接到[!DNL Teradata Vantage]实例的连接字符串。 [!DNL Teradata Vantage]的连接字符串模式为`DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL Teradata Vantage]连接规范ID： `2fa8af9c-2d1a-43ea-a253-f00a00c74412`。 |

**响应**

成功的响应返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Teradata Vantage]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将数据库数据引入Experience Platform](../../collect/database-nosql.md)
