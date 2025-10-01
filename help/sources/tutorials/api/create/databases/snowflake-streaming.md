---
title: 将您的Snowflake流帐户连接到Adobe Experience Platform
description: 了解如何使用流服务API将Adobe Experience Platform连接到Snowflake Streaming。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: a4a464f1f3b61311754a39f2a6e6a4ef21af3ab0
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 4%

---

# 使用[!DNL Snowflake] API将[!DNL Flow Service]数据流式传输到Experience Platform

>[!IMPORTANT]
>
>
> [!DNL Snowflake]流源在API中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

本教程提供了有关如何使用[!DNL Snowflake]API[[!DNL Flow Service] 将数据从](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)帐户连接并流式传输到Adobe Experience Platform的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Snowflake] 概述](../../../../connectors/databases/snowflake-streaming.md#prerequisites)。

## 创建基本连接 {#create-a-base-connection}

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的`/connections`身份验证凭据作为请求正文的一部分时，向[!DNL Snowflake]端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Snowflake]创建基本连接：

>[!TIP]
>
>必须完全按照以下示例输入`auth.specName`值，包括空格。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "Basic Authentication for Snowflake",
          "params": {
              "account": "wixnnnd-ui60793.snowflakecomputing.com",
              "database": "ACME_DB",
              "warehouse": "ACME_WH",
              "username": "nikola15",
              "schema": "PUBLIC",
              "password": "xxxx",
              "role": "ACCOUNTADMIN"
          }
      },
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.account` | 您的[!DNL Snowflake]流帐户的名称。 |
| `auth.params.database` | 将从其中提取数据的[!DNL Snowflake]数据库的名称。 |
| `auth.params.warehouse` | [!DNL Snowflake]仓库的名称。 [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个仓库彼此独立，在将数据传送到Experience Platform时必须单独访问。 |
| `auth.params.username` | 您的[!DNL Snowflake]流帐户的用户名。 |
| `auth.params.schema` | （可选）与您的[!DNL Snowflake]流帐户关联的数据库架构。 |
| `auth.params.password` | 您的[!DNL Snowflake]流帐户的密码。 |
| `auth.params.role` | （可选）此[!DNL Snowflake]连接的用户角色。 如果未提供，此值默认为`public`。 |
| `connectionSpec.id` | [!DNL Snowflake]连接规范ID： `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`。 |

**响应**

成功的响应将返回新创建的基本连接及其对应的电子标记。

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 浏览您的数据表 {#explore-your-data-tables}

接下来，使用基本连接ID来浏览和导航源的数据表，方法是在提供基本连接ID作为参数的同时，向`/connections/{BASE_CONNECTION_ID}/explore?objectType=root`端点发出GET请求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | [!DNL Snowflake]流源的基本连接ID。 |


**请求**

以下请求检索您的[!DNL Snowflake]流帐户的结构和内容。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将在根级别返回源数据的结构和内容。

```json
{
    "items": [
        {
            "type": "table",
            "name": "ACME"
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `items.type` | 表的类型。 |
| `items.names` | 表的名称。 |

## 创建源连接 {#create-a-source-connection}

源连接创建和管理与摄取数据的外部源的连接。

要创建源连接，请向`/sourceConnections` API的[!DNL Flow Service]端点发出POST请求。

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Snowflake Streaming Source Connection",
      "description": "A source connection for Snowflake Streaming data",
      "baseConnectionId": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      },
      "params": {
          "tableName": "ACME",
          "timestampColumn": "dOb",
          "backfill": "true",
          "timezoneValue": "PST"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `baseConnectionId` | [!DNL Snowflake]流源的已验证基本连接ID。 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | [!DNL Snowflake]流源的连接规范ID。 |
| `params.tableName` | [!DNL Snowflake]数据库中要带到Experience Platform的表的名称。 |
| `params.timestampColumn` | 用于获取增量值的时间戳列的名称。 |
| `params.backfill` | 一个布尔标志，用于确定是从开始（0纪元时间）还是从启动源时获取数据。 有关此值的详细信息，请阅读[[!DNL Snowflake] 流源概述](../../../../connectors/databases/snowflake-streaming.md)。 |
| `params.timezoneValue` | 时区值指示在查询[!DNL Snowflake]数据库时应获取哪个时区的当前时间。 如果配置中的时间戳列设置为`TIMESTAMP_NTZ`，则应提供此参数。 如果未提供，`timezoneValue`将默认为UTC。 |

**响应**

成功的响应将返回您的源连接ID及其对应的电子标记。 源连接ID将在后面的步骤中用于创建数据流。

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 创建数据流

>[!NOTE]
>
>创建或更新流数据流后，需要短暂暂停数据摄取5分钟，以防出现任何潜在的数据丢失或数据丢失情况。

要创建数据流以将数据从导览[!DNL Snowflake]帐户流式传输到Experience Platform，您必须在提供以下值时向`/flows`端点发出POST请求：

>[!TIP]
>
>有关如何检索以下ID的分步指南，请访问下面的链接。

* [Source连接Id](#create-a-source-connection)
* [目标连接ID](../../collect/database-nosql.md#create-a-target-connection)
* [流量规范ID](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [映射 ID](../../collect/database-nosql.md#create-a-mapping)

**API格式**

```http
POST /flows
```

**请求**

以下请求为您的[!DNL Snowflake]帐户创建流式数据流。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake Streaming Dataflow",
      "description": "A dataflow for Snowflake streaming data",
      "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
      ],
      "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
      ],
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

| 属性 | 描述 |
| --- | --- |
| `sourceConnectionIds` | 您的[!DNL Snowflake]流源的源连接ID。 |
| `targetConnectionIds` | [!DNL Snowflake]流源的目标连接ID。 |
| `flowSpec.id` | 用于为[!DNL Snowflake]流源创建数据流的流规范ID。 此流规范ID允许您通过映射转换创建流数据流。 此ID是固定的，为： `c1a19761-d2c7-4702-b9fa-fe91f0613e81`。 |
| `transformations.params.mappingId` | 数据流的映射ID。 |

**响应**

成功的响应将返回您的流ID及其对应的电子标记。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Snowflake] API为[!DNL Flow Service]数据创建流式数据流。 有关Adobe Experience Platform源的其他信息，请访问以下文档：

* [源概述](../../../../home.md)
* [使用API监控数据流](../../monitor.md)
