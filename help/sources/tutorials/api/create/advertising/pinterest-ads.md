---
title: 使用流服务API为Pinterest Ads创建源连接和数据流
description: 了解如何使用流服务API将Adobe Experience Platform连接到Pinterest Ads。
badge: Beta 版
hide: true
hidefromtoc: true
exl-id: 293a3ec9-38ea-4b71-a923-1f4e28a41236
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2278'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API为[!DNL Pinterest Ads]创建源连接和数据流

>[!NOTE]
>
>[!DNL Pinterest Ads]源为测试版。 阅读[源概述](../../../../home.md#terms-and-conditions)，了解有关使用测试版标记源的更多信息。

以下教程将指导您完成创建[!DNL Pinterest Ads]源连接和数据流的步骤，以便使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将[[!DNL Pinterest Ads]](https://ads.pinterest.com/)数据引入Adobe Experience Platform。

## 快速入门 {#getting-started}

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Pinterest Ads]所需了解的其他信息。

### 先决条件 {#prerequisites}

为了将[!DNL Pinterest Ads]连接到Experience Platform，您必须提供以下连接属性的值：

* [!DNL Pinterest] `accessToken`。
* [!DNL Pinterest] `adAccountId`。
* [!DNL Pinterest] `campaign`、`adGroup`或`ad` ID中的一个。

有关这些连接属性的详细信息，请阅读[[!DNL Pinterest Ads] 概述](../../../../connectors/advertising/pinterest-ads.md#prerequisites)。

## 使用[!DNL Flow Service] API将[!DNL Pinterest Ads]连接到Experience Platform {#connect-platform-to-flow-api}

下面概述了将[!DNL Pinterest Ads]连接到Experience Platform所需执行的步骤。

### 创建基本连接 {#base-connection}

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Pinterest Ads]身份验证凭据作为请求正文的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Pinterest Ads]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Pinterest Ads",
      "description": "Create a live inbound connection to your Pinterest Ads instance, to ingest both historic and scheduled data into Experience Platform",
      "connectionSpec": {
          "id": "f82aae23-91e7-4884-b25f-2d2159d841fd",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {  
              "accessToken": "{PINTEREST_ACCESS_TOKEN}"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基础连接的名称。 确保基本连接的名称是描述性的，因为您可以使用此名称查找有关基本连接的信息。 |
| `description` | 可包含的可选值，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 源的连接规范ID。 在您的源通过[!DNL Flow Service] API注册和批准后，可以检索此ID。 |
| `auth.specName` | 您用于向Experience Platform验证源的身份验证类型。 |
| `auth.params.accessToken` | 包含对源进行身份验证所需的[!DNL Pinterest]访问令牌值。 |

**响应**

成功的响应返回新创建的基本连接，包括其唯一连接标识符(`id`)。 在下一步中浏览源的文件结构和内容时，需要此ID。

```json
{
    "id": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
    "etag": "\"4d08164f-0000-0200-0000-6368b7bf0000\""
}
```

### 浏览您的源 {#explore}

使用您在上一步中生成的基本连接ID，您可以通过执行GET请求来浏览文件和目录。
使用以下调用查找要带入Experience Platform的文件的路径：

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

执行GET请求以浏览源的文件结构和内容时，必须包括下表列出的查询参数：


| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 上一步中生成的基本连接ID。 |
| `objectType=rest` | 您希望探索的对象类型。 目前，此值始终设置为`rest`。 |
| `{OBJECT}` | 只有在查看特定目录时才需要此参数。 其值表示您希望浏览的目录的路径。 |
| `fileType=json` | 要带到Experience Platform的文件类型。 当前，`json`是唯一支持的文件类型。 |
| `{PREVIEW}` | 一个布尔值，定义连接的内容是否支持预览。 |
| `{SOURCE_PARAMS}` | 为要带到Experience Platform的源文件定义参数。 要检索`{SOURCE_PARAMS}`的已接受格式类型，必须在base64中编码整个`{"ad_account_id":"{PINTEREST_AD_ACCOUNT_ID}","object_ids":"{COMMA_SEPERATED_OBJECT_IDS}","object_type":"{OBJECT_TYPE}}"}`字符串。 |

[!DNL Pinterest Ads]支持多个[!DNL Pinterest] Analytics API端点。 根据您利用请求发送的对象类型，如下所示：

**请求**

>[!BEGINTABS]

>[!TAB 营销活动]

对于[!DNL Pinterest Ads]，当利用营销活动分析API时，`{SOURCE_PARAMS}`的值作为`{"ad_account_id":"123456789000","object_ids":"000123456789","object_type":"campaigns"}`传递。 在base64中进行编码时，它等于`YHsiYWRfYWNjb3VudF9pZCI6IjEyMzQ1Njc4OTAwMCIsIm9iamVjdF9pZHMiOiIwMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImNhbXBhaWducyJ9`，如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=YHsiYWRfYWNjb3VudF9pZCI6IjEyMzQ1Njc4OTAwMCIsIm9iamVjdF9pZHMiOiIwMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImNhbXBhaWducyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB 广告组]

对于[!DNL Pinterest Ads]，在使用广告组分析API时，`{SOURCE_PARAMS}`的值将作为`{"ad_account_id":"123456789000","object_ids":"000123456789,100123456789","object_type":"ad_groups"}`传递。 在base64中进行编码时，它等于`eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjAwMDEyMzQ1Njc4OSwxMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImFkX2dyb3VwcyJ9`，如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjAwMDEyMzQ1Njc4OSwxMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImFkX2dyb3VwcyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB 广告]

对于[!DNL Pinterest Ads]，当利用广告分析API时，`{SOURCE_PARAMS}`的值作为`{"ad_account_id":"123456789000","object_ids":"687247811001,687247811002,687247815005,687247834765","object_type":"ads"}`传递。 在base64中进行编码时，它等于`eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjY4NzI0NzgxMTAwMSw2ODcyNDc4MTEwMDIsNjg3MjQ3ODE1MDA1LDY4NzI0NzgzNDc2NSIsIm9iamVjdF90eXBlIjoiYWRzIn0=`，如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjY4NzI0NzgxMTAwMSw2ODcyNDc4MTEwMDIsNjg3MjQ3ODE1MDA1LDY4NzI0NzgzNDc2NSIsIm9iamVjdF90eXBlIjoiYWRzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!ENDTABS]

**响应**

>[!NOTE]
>
>一些记录已被截断，以便更好地呈现。

>[!BEGINTABS]

>[!TAB 营销活动]

成功响应将返回您调用的相应[!DNL Pinterest Ads] API的数据结构。

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "IMPRESSION_1_GROSS": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "DATE": {
                "type": "string"
            },
            "TOTAL_CLICKTHROUGH": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "CAMPAIGN_ID": {
                "type": "string"
            },
            "TOTAL_IMPRESSION_USER": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "REPIN_1": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_ENGAGEMENT": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ENGAGEMENT_RATE": {
                "type": "number"
            },
            "CAMPAIGN_NAME": {
                "type": "string"
            },
            "ECTR": {
                "type": "number"
            }
        }
    },
    "data": [
        {
            "IMPRESSION_1_GROSS": 355,
            "DATE": "2023-02-10",
            "TOTAL_CLICKTHROUGH": 7,
            "CAMPAIGN_ID": "000123456789",
            "TOTAL_IMPRESSION_USER": 324,
            "REPIN_1": 2,
            "TOTAL_ENGAGEMENT": 10,
            "ENGAGEMENT_RATE": 0.029940119760479042,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "ECTR": 0.020833333333333332
        }
    ]
}
```

>[!TAB 广告组]

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "IMPRESSION_1_GROSS": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "DATE": {
                "type": "string"
            },
            "TOTAL_CLICKTHROUGH": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "CAMPAIGN_ID": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_IMPRESSION_USER": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_ENGAGEMENT": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ENGAGEMENT_RATE": {
                "type": "number"
            },
            "CAMPAIGN_NAME": {
                "type": "string"
            },
            "AD_GROUP_ID": {
                "type": "string"
            },
            "ECTR": {
                "type": "number"
            }
        }
    },
    "data": [
        {
            "IMPRESSION_1_GROSS": 164,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 2,
            "CAMPAIGN_ID": 626747962992,
            "TOTAL_IMPRESSION_USER": 149,
            "TOTAL_ENGAGEMENT": 3,
            "ENGAGEMENT_RATE": 0.01910828025477707,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": "000123456789",
            "ECTR": 0.012658227848101266
        },
        {
            "IMPRESSION_1_GROSS": 177,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 5,
            "CAMPAIGN_ID": 626747962992,
            "TOTAL_IMPRESSION_USER": 167,
            "TOTAL_ENGAGEMENT": 5,
            "ENGAGEMENT_RATE": 0.028901734104046242,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": "100123456789",
            "ECTR": 0.028901734104046242
        }
    ]
}
```

>[!TAB 广告]

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "IMPRESSION_1_GROSS": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "DATE": {
                "type": "string"
            },
            "TOTAL_CLICKTHROUGH": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "CAMPAIGN_ID": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_IMPRESSION_USER": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "AD_ID": {
                "type": "string"
            },
            "TOTAL_ENGAGEMENT": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ENGAGEMENT_RATE": {
                "type": "number"
            },
            "CAMPAIGN_NAME": {
                "type": "string"
            },
            "AD_GROUP_ID": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ECTR": {
                "type": "number"
            }
        }
    },
    "data": [
        {
            "IMPRESSION_1_GROSS": 146,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 2,
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 132,
            "AD_ID": "687247811001",
            "TOTAL_ENGAGEMENT": 3,
            "ENGAGEMENT_RATE": 0.02158273381294964,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 000123456789,
            "ECTR": 0.014285714285714285
        },
        {
            "IMPRESSION_1_GROSS": 19,
            "DATE": "2023-02-13",
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 18,
            "AD_ID": "687247811002",
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 000123456789
        },
        {
            "IMPRESSION_1_GROSS": 63,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 1,
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 57,
            "AD_ID": "687247815005",
            "TOTAL_ENGAGEMENT": 1,
            "ENGAGEMENT_RATE": 0.016129032258064516,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 100123456789,
            "ECTR": 0.016129032258064516
        },
        {
            "IMPRESSION_1_GROSS": 116,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 4,
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 115,
            "AD_ID": "687247834765",
            "TOTAL_ENGAGEMENT": 4,
            "ENGAGEMENT_RATE": 0.035398230088495575,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 100123456789,
            "ECTR": 0.035398230088495575
        }
    ]
}
```

>[!ENDTABS]

### 创建源连接 {#source-connection}

您可以通过向[!DNL Flow Service] API发出POST请求来创建源连接。 源连接由基本连接ID、源数据文件的路径以及连接规范ID组成。

**API格式**

```https
POST /sourceConnections
```

**请求**

[!DNL Pinterest Ads]源支持多个[!DNL Pinterest] Analytics API端点。 根据您利用以下请求所使用的对象类型，会创建源连接：

>[!BEGINTABS]

>[!TAB 营销活动]

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Source Connection",
        "description": "Pinterest Ads Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "ad_account_id": "123456789000",
            "object_type": "campaigns",
            "object_ids": "2680074532641"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可包含的可选值，用于提供有关源连接的更多信息。 |
| `baseConnectionId` | [!DNL Pinterest Ads]的基本连接ID。 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 要摄取的[!DNL Pinterest Ads]数据的格式。 当前，唯一支持的数据格式为`json`。 |
| `params.ad_account_id` | [!DNL Pinterest] `Ad account ID`。 |
| `params.object_type` | 由于需要[!DNL Pinterest] Campaign Analytics API端点，因此值为`campaigns`。 |
| `params.object_ids` | [!DNL Pinterest]促销活动ID的逗号分隔列表。 |

>[!TAB 广告组]

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Source Connection",
        "description": "Pinterest Ads Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "ad_account_id": "123456789000",
            "object_type": "ad_groups",
            "object_ids": "2680074532641,2680074533547"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可包含的可选值，用于提供有关源连接的更多信息。 |
| `baseConnectionId` | [!DNL Pinterest Ads]的基本连接ID。 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 要摄取的[!DNL Pinterest Ads]数据的格式。 当前，唯一支持的数据格式为`json`。 |
| `params.ad_account_id` | [!DNL Pinterest] `Ad account ID`。 |
| `params.object_type` | 由于需要[!DNL Pinterest]广告组分析API终结点，因此值为`ad_groups`。 |
| `params.object_ids` | [!DNL Pinterest]个广告组ID的逗号分隔列表。 |

>[!TAB 广告]

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Source Connection",
        "description": "Pinterest Ads Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "ad_account_id": "123456789000",
            "object_type": "ads",
            "object_ids": "687247811001,687247811002,687247815005,687247834765"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可包含的可选值，用于提供有关源连接的更多信息。 |
| `baseConnectionId` | [!DNL Pinterest Ads]的基本连接ID。 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 要摄取的[!DNL Pinterest Ads]数据的格式。 当前，唯一支持的数据格式为`json`。 |
| `params.ad_account_id` | [!DNL Pinterest] `Ad account ID`。 |
| `params.object_type` | 由于需要[!DNL Pinterest] Ad Analytics API终结点，因此值为`ads`。 |
| `params.object_ids` | [!DNL Pinterest]个广告ID的逗号分隔列表。 |

>[!ENDTABS]

**响应**

成功的响应返回新创建的源连接的唯一标识符(`id`)。 此ID是稍后步骤创建数据流所必需的。

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### 创建目标XDM架构 {#target-schema}

为了在Experience Platform中使用源数据，必须创建目标架构，以根据您的需求构建源数据。 然后，使用目标架构创建包含源数据的Experience Platform数据集。

通过对[架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)执行POST请求，可以创建目标XDM架构。

有关如何创建目标XDM架构的详细步骤，请参阅有关使用API [创建架构的教程](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create)。

### 创建目标数据集 {#target-dataset}

通过向[目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/)执行POST请求，在有效负载中提供目标架构的ID，可以创建目标数据集。

有关如何创建目标数据集的详细步骤，请参阅有关[使用API创建数据集的教程](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html)。

### 创建目标连接 {#target-connection}

目标连接表示与要存储所摄取数据的目标的连接。 要创建目标连接，您必须提供对应于数据湖的固定连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

现在，您拥有目标架构、目标数据集以及到数据湖的连接规范ID。 使用这些标识符，您可以使用[!DNL Flow Service] API创建目标连接，以指定将包含入站源数据的数据集。

**API格式**

```https
POST /targetConnections
```

**请求**

以下请求为[!DNL Pinterest Ads]创建目标连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Target Connection",
        "description": "Pinterest Ads Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "5ef4551c52e054191a61a99f"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 目标连接的名称。 确保目标连接的名称是描述性的，因为您可以使用此名称查找有关目标连接的信息。 |
| `description` | 可包含的可选值，用于提供有关目标连接的更多信息。 |
| `connectionSpec.id` | 对应于[!DNL Data Lake]的连接规范ID。 此固定ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |
| `data.format` | 要带到Experience Platform的[!DNL Pinterest Ads]数据的格式。 |
| `params.dataSetId` | 在上一步中检索到的目标数据集ID。 |

**响应**

成功的响应返回新目标连接的唯一标识符(`id`)。 此ID在后续步骤中是必需的。

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### 创建映射 {#mapping}

要将源数据摄取到目标数据集中，必须首先将其映射到目标数据集所遵循的目标架构。 这是通过在请求有效负载中定义数据映射的情况下对[[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)执行POST请求来实现的。

**API格式**

```http
POST /conversion/mappingSets
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
            "sourceType": "ATTRIBUTE",
            "source": "CAMPAIGN_ID",
            "destination": "_extconndev.ID_CAMPAIGN"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "CAMPAIGN_NAME",
            "destination": "_extconndev.NAME_CAMPAIGN"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "AD_GROUP_ID",
            "destination": "_extconndev.AD_GROUP_ID"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "AD_ID",
            "destination": "_extconndev.AD_ID"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "DATE",
            "destination": "_extconndev.DATE"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "ECTR",
            "destination": "_extconndev.ECTR"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "ENGAGEMENT_RATE",
            "destination": "_extconndev. ENGAGEMENT_RATE"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "IMPRESSION_1_GROSS",
            "destination": "_extconndev. IMPRESSION_1_GROSS"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "REPIN_1",
            "destination": "_extconndev. REPIN_1"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "TOTAL_CLICKTHROUGH",
            "destination": "_extconndev. TOTAL_CLICKTHROUGH"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "TOTAL_ENGAGEMENT",
            "destination": "_extconndev. TOTAL_ENGAGEMENT"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "TOTAL_IMPRESSION_USER",
            "destination": "_extconndev. TOTAL_IMPRESSION_USER"
            }
        ],
        "outputSchema": {
            "schemaRef": {
            "id": "{{schemaId}}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `outputSchema.schemaRef.id` | 在之前的步骤中生成的[目标XDM架构](#target-schema)的ID。 |
| `mappings.sourceType` | 正在映射的源属性类型。 |
| `mappings.source` | 需要映射到目标XDM路径的源属性。 |
| `mappings.destination` | 源属性将映射到的目标XDM路径。 |

**响应**

成功的响应返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要使用此值来创建数据流。

```json
{
    "id": "059c69f7207b4d7e9b48c47e2fd966a6",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 创建流 {#flow}

将数据从[!DNL Pinterest Ads]引入Experience Platform的最后一步是创建数据流。 现在，您已准备以下必需值：

* [Source连接Id](#source-connection)
* [目标连接ID](#target-connection)
* [映射 ID](#mapping)

数据流负责从源中计划和收集数据。 您可以通过在有效负载中提供前面提到的值时执行POST请求来创建数据流。

要计划摄取，您必须先将开始时间值设置为纪元时间（以秒为单位）。 然后，必须将频率值设置为五个选项之一： `once`、`minute`、`hour`、`day`或`week`。 间隔值用于指定两次连续摄取之间的时间段，但是，创建一次性摄取不需要设置间隔。 对于所有其他频率，间隔值必须设置为等于或大于`15`。

**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads dataflow",
        "description": "Pinterest Ads dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3"
        ],
        "targetConnectionIds": [
            "6b137bf6-d2a0-48c8-914b-d50f4942eb85"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "059c69f7207b4d7e9b48c47e2fd966a6",
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

| 属性 | 描述 |
| --- | --- |
| `name` | 您的数据流的名称。 确保数据流的名称是描述性的，因为您可以使用此名称查找数据流上的信息。 |
| `description` | 可包含的可选值，用于提供有关数据流的更多信息。 |
| `flowSpec.id` | 创建数据流所需的流规范ID。 此固定ID为： `6499120c-0b15-42dc-936e-847ea3c24d72`。 |
| `flowSpec.version` | 流规范ID的相应版本。 此值默认为`1.0`。 |
| `sourceConnectionIds` | 在之前的步骤中生成的[源连接ID](#source-connection)。 |
| `targetConnectionIds` | 在之前的步骤中生成的[目标连接ID](#target-connection)。 |
| `transformations` | 此属性包含需要应用于数据的各种转换。 将不符合XDM的数据引入Experience Platform时，需要此属性。 |
| `transformations.name` | 分配给转换的名称。 |
| `transformations.params.mappingId` | 在之前的步骤中生成的[映射ID](#mapping)。 |
| `transformations.params.mappingVersion` | 映射ID的相应版本。 此值默认为`0`。 |
| `scheduleParams.startTime` | 此属性包含有关数据流的摄取计划的信息。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括： `once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 间隔指定两次连续流运行之间的周期。 间隔的值应为非零整数。 当频率设置为`once`时不需要间隔，其他频率值应大于或等于`15`。 |

**响应**

成功的响应返回新创建的数据流的ID (`id`)。 您可以使用此ID监视、更新或删除数据流。

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## 附录 {#appendix}

以下部分提供了有关监视、更新和删除数据流的步骤的信息。

### 监测数据流 {#monitor-dataflow}

创建数据流后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 有关完整的API示例，请阅读有关[使用API监视源数据流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html)的指南。

### 更新您的数据流 {#update-dataflow}

通过提供数据流的ID，向[!DNL Flow Service] API的`/flows`端点发出PATCH请求来更新数据流的详细信息，例如其名称和描述，以及其运行计划和关联的映射集。 发出PATCH请求时，必须在`If-Match`标头中提供数据流唯一的`etag`。 有关完整的API示例，请阅读有关使用API [更新源数据流的指南](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新您的帐户 {#update-account}

在提供基本连接ID作为查询参数的同时，通过向[!DNL Flow Service] API执行PATCH请求来更新源帐户的名称、描述和凭据。 发出PATCH请求时，必须在`If-Match`标头中提供源帐户的唯一`etag`。 有关完整的API示例，请阅读有关[使用API更新源帐户](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html)的指南。

### 删除您的数据流 {#delete-dataflow}

在查询参数中提供要删除的数据流的ID时，通过向[!DNL Flow Service] API执行DELETE请求来删除数据流。 有关完整的API示例，请阅读有关[使用API删除数据流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html)的指南。

### 删除您的帐户 {#delete-account}

在提供要删除的帐户的基本连接ID时，通过向[!DNL Flow Service] API执行DELETE请求来删除您的帐户。 有关完整的API示例，请阅读有关使用API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html)删除源帐户[的指南。
