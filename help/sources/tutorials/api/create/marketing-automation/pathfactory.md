---
title: 使用流服务API创建PathFactory基本连接
description: 了解如何使用流服务API对Experience Platform验证您的PathFactory帐户。
badge: Beta 版
exl-id: 2bdfe38b-d3f7-480f-87c6-0b98b9521be2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API创建[!DNL PathFactory]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

阅读本文档以了解如何使用[[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)为[!DNL PathFactory]创建基本连接。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

以下部分提供了使用[!DNL Flow Service] API成功连接到[!DNL PathFactory]时需要了解的其他信息。

### 收集所需的凭据 {#gather-credentials}

要在Experience Platform上访问PathFactory帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 用户名 | 您的[!DNL PathFactory]帐户用户名。 这对于识别您在系统中的帐户至关重要。 |
| 密码 | 与您的[!DNL PathFactory]帐户关联的密码。 确保此安全设置以防止未经授权的访问。 |
| 域 | 与您的[!DNL PathFactory]帐户关联的域。 这通常指您的[!DNL PathFactory] URL中的唯一标识符。 |
| 访问令牌 | 用于API身份验证的唯一令牌以确保您的系统与[!DNL PathFactory]之间的安全通信。 |
| API端点 | 用于访问数据的特定API端点：访客、会话和页面查看。 每个端点对应于可检索的不同数据集。 **注意：**&#x200B;这些由[!DNL PathFactory]预定义，特定于您要访问的数据： <ul><li>**访客终结点**： `/api/public/v3/data_lake_apis/visitors.json`</li><li>**会话终结点**： `/api/public/v3/data_lake_apis/sessions.json`</li><li>**页面查看终结点**： `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

有关如何保护和使用凭据以及如何获取和刷新访问令牌的详细信息，请访问[[!DNL PathFactory] 支持中心](https://support.pathfactory.com/categories/adobe/)。 此资源提供有关管理凭据以及确保有效且安全的API集成的综合指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL PathFactory]身份验证凭据作为请求正文的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL PathFactory]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.clientId` | 与您的[!DNL PathFactory]应用程序关联的客户端ID。 |
| `auth.params.clientSecret` | 与您的[!DNL PathFactory]应用程序关联的客户端密钥。 |
| `connectionSpec.id` | [!DNL PathFactory]连接规范ID： `ea1c2a08-b722-11eb-8529-0242ac130003`。 |

**响应**

成功的响应返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL PathFactory]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将营销自动化数据引入Experience Platform](../../collect/marketing-automation.md)
