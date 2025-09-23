---
title: 使用流量服务API将毛细管连接到Experience Platform
description: 了解如何使用API将Capillary连接到Experience Platform。
badge: Beta 版
exl-id: 763792d0-d5dc-40ac-b86a-6a0d26463b71
source-git-commit: 91d6206c6ce387fde365fa72dc79ca79fc0e46fa
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 2%

---

# 使用[!DNL Capillary Streaming Events] API将[!DNL Flow Service]连接到Experience Platform

>[!AVAILABILITY]
>
>[!DNL Capillary Streaming Events]源为测试版。 有关使用测试版标记源的更多信息，请阅读源概述中的[条款和条件](../../../../home.md#terms-and-conditions)。

阅读本指南，了解如何使用[!DNL Capillary Streaming Events]和[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将数据从[!DNL Capillary]帐户流式传输到Adobe Experience Platform。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Capillary Streaming Events] 概述](../../../../connectors/loyalty/capillary.md)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请阅读[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

>[!BEGINSHADEBOX]

## 开发人员流程核对清单

1. 使用架构注册表创建或选择目标&#x200B;**体验数据模型(XDM)架构**。 使用此XDM架构在目录服务中&#x200B;**创建数据集**。
2. 创建&#x200B;**基本连接**&#x200B;以存储[!DNL Capillary]凭据。
3. 创建一个&#x200B;**源连接**&#x200B;以绑定到您的`baseConnectionId`。
4. 创建&#x200B;**目标连接**&#x200B;以确保您的数据登陆到数据湖。
5. 使用数据准备创建将[!DNL Capillary]源字段映射到正确XDM字段的映射。
6. 使用您的`sourceConnectionId`、`targetConnectionId`和`mappingID`创建数据流
7. 使用单个示例用户档案/交易事件进行测试，以验证您的数据流。

>[!ENDSHADEBOX]

## 创建基本连接 {#base-connection}

基本连接会保留凭据和连接详细信息。 要为[!DNL Capillary]创建基础连接，请向`/connections` API的[!DNL Flow Service]端点发出POST请求，并在请求正文中提供您的[!DNL Capillary]凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Capillary]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary base connection",
    "description": "Base connection to authenticate the [!DNL Capillary] source.",
    "connectionSpec": {
      "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
      "version": "1.0"
    },
    "auth": {
      "specName": "OAuth generic-rest-connector",
      "params": {
        "clientId": "{CLIENT_ID}",
        "clientSecret": "{CLIENT_SECRET}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    }
  }'
```

**响应**

```
A successful response returns the newly created base connection, including its unique connection identifier (id). This ID is required to explore your source's file structure and contents in the next step.

{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### 创建源连接

要创建源连接，请在提供基本连接ID的同时向`/sourceConnections`端点发出POST请求。

**API格式**

```http
POST /flowservice/sourceConnections
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Capillary Streaming",
      "description": "Capillary Streaming",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
          "version": "1.0"
      }
    }'
```

**响应**

成功的响应返回HTTP状态201，其中包含新创建的源连接的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

### 架构配置

>[!BEGINTABS]

>[!TAB 配置文件摄取]

配置文件包含身份和忠诚度属性。 查看以下有效负载，了解基于[!DNL Capillary]配置文件架构的示例。 您可以配置此架构并将其映射到XDM个人资料。

**请求**

```json
{
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john.doe@capillarytech.com",
        "primary": true
      }
    ]
  },
  "loyalty": {
    "tier": "gold",
    "points": 1250,
    "lifetimePoints": 122,
    "expiredPoints": 12,
    "pointsRedeemed": 500,
    "program": "loyalty program name",
    "status": "active"
  }
}
```

**响应**

```json
{
  "id": "8c19f1c3-4b91-47cd-8cb5-b152a93f7349",
  "status": "success",
  "message": "Profile record ingested successfully"
}
```

>[!TAB 事务引入]

交易捕获商业活动。 查看基于[!DNL Capillary]事件架构的示例的以下有效负载。 您可以配置此架构并将其映射到XDM体验事件。

**请求**

```json
{
  "_id": "T0001",
  "timestamp": "2025-07-14T12:00:00-06:00",
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john@capillarytech.com",
        "primary": true
      }
    ]
  },
  "commerce": {
    "commerceScope": {
      "storeCode": "HSR"
    },
    "order": {
      "priceTotal": 90
    }
  },
  "productLineItems": [
    {
      "SKU": "sku_01",
      "quantity": 1,
      "priceTotal": 100,
      "name": "Kitkat",
      "discountAmount": 10
    }
  ]
}
```

**响应**

```json
{
  "id": "T0001",
  "status": "success",
  "message": "Transaction event ingested successfully"
}
```

>[!ENDTABS]

<!--### Supported Events

The [!DNL Capillary] source supports the following events:

* `pointsIssued`
* `tierDowngraded`
* `tierUpgraded`
* `pointsExpiryChange`
* `pointsExpired`
* `transactionUpdated`
* `customerAdded`
* `tierDowngradeReminder`
* `promotionEarned`
* `pointsExpiryReminder`
* `pointsRedeemed`
* `transactionAdded`
* `tierRenewed`
* `customerUpdated`-->

### 历史数据迁移

您可以将历史忠诚度和交易数据导入Experience Platform。 只需从[!DNL Capillary]中将您的数据导出为结构化CSV文件，使用[!DNL SFTP]安全地传输它们，并将它们摄取到Experience Platform数据集中。 初始迁移后，您的数据将通过事件驱动连接器实时保持最新。

### 创建目标XDM架构 {#target-schema}

Experience Data Model (XDM)架构提供了一种标准化的方式，用于在Experience Platform中组织和描述客户体验数据。 要将源数据摄取到Experience Platform，您必须首先创建目标XDM架构，该架构定义要摄取的数据结构和类型。 此架构将用作您摄取的数据将驻留的Experience Platform数据集的蓝图。

通过对[架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)执行POST请求，可以创建目标XDM架构。 有关如何创建目标XDM架构的详细步骤，请阅读以下指南：

* [使用API创建架构](../../../../../xdm/api/schemas.md)。
* [使用用户界面创建架构](../../../../../xdm/tutorials/create-schema-ui.md)。

创建后，稍后需要目标XDM架构`$id`才能进行目标数据集和映射。

## 创建目标数据集 {#target-dataset}

数据集是用于数据集合的存储和管理结构，其结构通常类似于具有列（架构）和行（字段）的表。 成功引入Experience Platform的数据将作为数据集存储在数据湖中。 在此步骤中，您可以创建新数据集或使用现有数据集。

您可以创建目标数据集，方法是：向[目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/)发出POST请求，同时在有效负载中提供目标架构的ID。 有关如何创建目标数据集的详细步骤，请阅读有关[使用API创建数据集](../../../../../catalog/api/create-dataset.md)的指南。


## 创建目标连接 {#target}

目标连接表示与所摄取数据所登陆的目标之间的连接。 要创建目标连接，必须提供与该数据湖关联的固定连接规范ID。 此连接规范ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

**API格式**

```http
POST /targetConnections
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Capillary Target Connection",
      "description": "Capillary Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

### 创建映射 {#mapping}

接下来，将源数据映射到目标数据集所遵循的目标架构。 要创建映射，请向`mappingSets`API[[!DNL Data Prep] 的](https://developer.adobe.com/experience-platform-apis/references/data-prep/)端点发出POST请求。 包含您的目标XDM架构ID以及要创建的映射集的详细信息。

将毛细管字段映射到相应的XDM架构字段，如下所示：

| 源架构 | 目标架构 |
|------------------------------|-------------------------------|
| `identityMap.email.id` | `xdm:identityMap.email[0].id` |
| `loyalty.points` | `xdm:loyalty.points` |
| `loyalty.tier` | `xdm:loyalty.tier` |
| `commerce.order.priceTotal` | `xdm:commerce.order.priceTotal` |
| `productLineItems.SKU` | `xdm:productListItems.SKU` |

>[!TIP]
>
>您可以在准备映射数据时，为[和](../../../../images/tutorials/create/capillary/mappings.zip)下载[!DNL Capillary]事件和配置文件映射[将文件导入数据准备](../../../../../data-prep/ui/mapping.md#import-mapping)。

### 创建数据流 {#flow}

创建源连接、映射和目标连接后，可以配置数据流以将数据从[!DNL Capillary]移到Experience Platform中。

典型的数据流包括：

* **配置文件数据流**：将[!DNL Capillary]配置文件数据摄取到XDM个人配置文件数据集。
* **交易数据流**：将[!DNL Capillary]交易数据摄取到XDM ExperienceEvent数据集。

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary dataflow",
    "description": "Capillary → Experience Platform dataflow",
    "flowSpec": {
      "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "version": "1.0"
    },
    "sourceConnectionIds": "{SOURCE_CONNECTION_ID}",
    "targetConnectionIds": "{TARGET_CONNECTION_ID}",
    "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "{MAPPING_ID}",
          "mappingVersion": "0"
        }
      }
    ],
    "scheduleParams": {
      "startTime": "1625040887",
      "frequency": "minute",
      "interval": 15
    }
  }'
```

>[!NOTE]
>
>`startTime`处于UNIX纪元秒内。

**响应**

成功响应会返回您的数据流及其对应的数据流ID。

```json
{
  "id": "92f11b8c-0a9f-45a9-8239-60b4e8430a88",
  "status": "enabled",
  "message": "Dataflow created successfully"
}
```

## 错误处理

对于以下情况，连接器包含可靠的错误处理：

* **身份验证错误**：身份验证失败时自动刷新Adobe凭据。
* **速率限制错误**：在达到API速率限制时，通过指数回退实现重试。
* **网络错误**：记录并重试失败的网络请求。
* **数据验证错误**：记录无效的负载，以进行手动审查和解决。

所有错误均与错误类型、时间戳、请求有效负载和Adobe API响应等详细信息一起记录，以促进故障排除和调试。

## 测试您的连接

请按照以下步骤了解测试连接时可以采取的步骤：

* 向`/connections/{BASE_CONNECTION_ID}`发出GET请求并提供您的基本连接ID以验证您的基本连接是否存在。 在此步骤中，您还可以验证基础连接的状态是否设置为`active`。
* 向`/flowservice/sourceConnections/{SOURCE_CONNECTION_ID}`发出GET请求并提供源连接ID以验证您的源连接。
* 使用您的流端点URL发送示例配置文件有效负载（使用配置文件摄取JSON）。
* 导航到Experience Platform UI中的数据集，并对该数据集运行查询以确认您的记录。
* 使用数据准备日志检查错误。
* 如果必须打开支持工单，请确保您具备以下条件：
   * 请求有效负载
   * 响应正文
   * Request-id
   * 时间戳
   * 资源ID

## 附录

有关其他操作的指南，请访问以下文档

* [监视数据流](../../../../../dataflows/ui/monitor-sources.md)
* [更新数据流](../../../ui/update-dataflows.md)
* [删除数据流](../../../ui/delete.md)
* [更新源帐户](../../../ui/update.md)
