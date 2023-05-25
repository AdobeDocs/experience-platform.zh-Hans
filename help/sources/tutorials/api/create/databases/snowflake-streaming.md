---
title: 将您的Snowflake流帐户连接到Adobe Experience Platform
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到Snowflake流。
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: 825da75c8f98863b408477a4895cd9146d121d3d
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 2%

---

# 流 [!DNL Snowflake] 要使用进行Experience Platform的数据 [!DNL Flow Service] API

>[!IMPORTANT]
>
>* 此 [!DNL Snowflake] 流源为测试版。 请阅读 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记源的更多信息。
>* 此 [!DNL Snowflake] 源目录中提供了流源，以供已购买Real-Time CDP Ultimate的客户使用。


本教程提供了有关如何连接和流式传输数据的步骤。 [!DNL Snowflake] Adobe Experience Platform帐户，使用 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

有关先决条件设置的信息，请参阅 [!DNL Snowflake] 流源。 请阅读 [[!DNL Snowflake] 流源概述](../../../../connectors/databases/snowflake-streaming.md).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接 {#create-a-base-connection}

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL Snowflake] 作为请求正文一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL Snowflake]：

>[!TIP]
>
>此 `auth.specName` 输入的值必须与下面的示例完全相同，包括空格。

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
| `auth.params.account` | 您的名称 [!DNL Snowflake] 流帐户。 |
| `auth.params.database` | 您的名称 [!DNL Snowflake] 从中提取数据的数据库。 |
| `auth.params.warehouse` | 您的名称 [!DNL Snowflake] 仓库。 此 [!DNL Snowflake] warehouse管理应用程序的查询执行过程。 每个仓库彼此独立，在将数据传送到Platform时必须单独访问。 |
| `auth.params.username` | 您的用户名 [!DNL Snowflake] 流帐户。 |
| `auth.params.schema` | （可选）与以下对象关联的数据库架构： [!DNL Snowflake] 流帐户。 |
| `auth.params.password` | 您的密码 [!DNL Snowflake] 流帐户。 |
| `auth.params.role` | （可选）对此的用户角色 [!DNL Snowflake] 连接。 如果未提供，则此值默认为 `public`. |
| `connectionSpec.id` | 此 [!DNL Snowflake] 连接规范ID： `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**响应**

成功响应将返回新创建的基本连接及其对应的etag。

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 浏览您的数据表 {#explore-your-data-tables}

接下来，使用基本连接ID通过对以下对象发出GET请求，来浏览和浏览源的数据表： `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` 端点，同时将基本连接ID作为参数提供。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 您的的基本连接ID [!DNL Snowflake] 流源。 |


**请求**

以下请求检索的结构和内容 [!DNL Snowflake] 流帐户。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会在根级别返回源数据的结构和内容。

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

POST要创建源连接，请向 `/sourceConnections` 的端点 [!DNL Flow Service] API。

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
          "backfill": "true"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `baseConnectionId` | 贵机构的已验证基本连接ID [!DNL Snowflake] 流源。 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | 的连接规范ID [!DNL Snowflake] 流源。 |
| `params.tableName` | 中的表的名称 [!DNL Snowflake] 要带到Platform的数据库。 |
| `params.timestampColumn` | 用于获取增量值的时间戳列的名称。 |
| `params.backfill` | 一个布尔标志，用于确定是从开始（0纪元时间）还是从启动源时获取数据。 有关此值的详细信息，请阅读 [[!DNL Snowflake] 流源概述](../../../../connectors/databases/snowflake-streaming.md). |

**响应**

成功的响应将返回源连接ID及其对应的etag。 源连接ID将在后面的步骤中用于创建数据流。

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 创建数据流

创建数据流以流式传输导览中的数据 [!DNL Snowflake] POST帐户，则必须向 `/flows` 端点，同时提供以下值：

>[!TIP]
>
>有关如何检索以下ID的分步指南，请访问以下链接。

* [源连接ID](#create-a-source-connection)
* [目标连接ID](../../collect/database-nosql.md#create-a-target-connection)
* [流量规范ID](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [映射 ID](../../collect/database-nosql.md#create-a-mapping)

**API格式**

```http
POST /flows
```

**请求**

以下请求为您的创建一个流数据流 [!DNL Snowflake] 帐户。

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
| `sourceConnectionIds` | 的源连接ID [!DNL Snowflake] 流源。 |
| `targetConnectionIds` | 的目标连接ID [!DNL Snowflake] 流源。 |
| `flowSpec.id` | 用于为创建数据流的流规范ID [!DNL Snowflake] 流源。 此流规范ID允许您创建具有映射转换的流数据流。 此ID是固定的，它是： `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | 数据流的映射ID。 |

**响应**

成功的响应将返回您的流ID及其对应的etag。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## 后续步骤

按照本教程，您已为创建一个流数据流， [!DNL Snowflake] 数据使用 [!DNL Flow Service] API。 有关Adobe Experience Platform源的其他信息，请访问以下文档：

* [源概述](../../../../home.md)
* [使用API监控数据流](../../monitor.md)