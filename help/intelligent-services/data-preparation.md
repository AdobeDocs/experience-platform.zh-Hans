---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: 准备要在Intelligent Services中使用的数据
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 8e24c7c50d700bc3644ce710f77073e537207a6f
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 0%

---


# 准备要在Intelligent Services中使用的数据

为了使智能服务能够从您的营销事件数据中发掘洞察，必须以标准结构从语义上丰富和维护数据。 智能服务利用体验数据模型(XDM)模式来实现此目标。 具体而言，智能服务中使用的所有数据集必须符 **合消费者体验事件** (CEE)XDM模式。

此文档提供有关将营销事件数据从多个渠道映射到此模式的一般指南，概述模式中重要字段的信息，以帮助您确定如何有效地将数据映射到其结构。

## 了解CEE模式

消费者体验事件模式描述个人的行为，因为它与数字营销事件（Web或移动）以及在线或离线商务活动相关。 智能服务需要使用此模式，因为其语义上定义良好的字段（列），从而避免了任何未知名称，否则这些名称会使数据变得不那么清晰。

智能服务利用此模式中的几个关键字段从您的营销事件数据中生成洞察，所有这些数据都可以在根级别找到并展开以显示其必需的子字段。

![](./images/data-preparation/schema-expansion.gif)

与所有XDM模式一样， CEE混合是可扩展的。 换言之，CEE混音中可添加其他字段，如果需要，可在多个模式中包含不同的变体。

在公共XDM存储库中可以找到混 [合的完整示例](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)，并应用作以下部分概述的关键字段的引用。

## 键字段

以下各节重点介绍了CEE混音中的关键字段，这些字段应用于智能服务以生成有用的洞察，包括说明和指向参考文档的链接，以供进一步示例使用。

>[!IMPORTANT] 为 `xdm:channel` 了使归因AI能够处理您的数 **据** ，字段（如下面第一节所述）是必需的，而客户AI没有任何必填字段。 强烈建议使用所有其他键字段，但不是强制使用。

### xdm:渠道

此字段表示与ExperienceEvent相关的营销渠道。 该字段包括有关渠道类型、媒体类型和位置类型的信息。 **必须提&#x200B;_供此字_段，Attribution AI才能处理您的数据**。

![](./images/data-preparation/channel.png)

**示例模式**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

有关每个必需子字段的完整信息，请 `xdm:channel`参阅体验渠道 [模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) 。 有关某些示例映射，请参 [阅下表](#example-channels)。

#### 渠道映射示例 {#example-channels}

下表提供映射到该渠道的营销模式的一些示 `xdm:channel` 例：

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 付费搜索 | https:/<span>/ns.adobe.com/xdm/渠道类型／搜索 | 付款 | 点击 |
| 社交——营销 | https:/<span>/ns.adobe.com/xdm/渠道类型／社交 | 挣 | 点击 |
| 显示 | https:/<span>/ns.adobe.com/xdm/渠道类型／显示 | 付款 | 点击 |
| 电子邮件 | https:/<span>/ns.adobe.com/xdm/渠道类型／电子邮件 | 付款 | 点击 |
| 内部推荐人 | https:/<span>/ns.adobe.com/xdm/渠道类型／直接 | 自 | 点击 |
| 显示浏览 | https:/<span>/ns.adobe.com/xdm/渠道类型／显示 | 付款 | 印象 |
| QR码重定向 | https:/<span>/ns.adobe.com/xdm/渠道类型／直接 | 自 | 点击 |
| 移动设备 | https:/<span>/ns.adobe.com/xdm/渠道类型／移动 | 自 | 点击 |

### xdm:productListItems

此字段是表示客户选择的产品的一组项目，包括产品SKU、名称、价格和数量。

![](./images/data-preparation/productListItems.png)

**示例模式**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

有关每个必需子字段的完整信息， `xdm:productListItems`请参阅商务详细 [信息模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 。

### xdm：商务

此字段包含有关ExperienceEvent的商务特定信息，包括采购订单编号和付款信息。

![](./images/data-preparation/commerce.png)

**示例模式**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

有关每个必需子字段的完整信息， `xdm:commerce`请参阅商务详细 [信息模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 。

### xdm:web

此字段表示与ExperienceEvent相关的Web详细信息，如交互、页面详细信息和推荐人。

![](./images/data-preparation/web.png)

**示例模式**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

有关每个必需子字段的完整信息，请 `xdm:productListItems`参阅ExperienceEvent Web详 [细信息模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) 。

### xdm：营销

此字段包含与与触点处于活动状态的营销活动相关的信息。

![](./images/data-preparation/marketing.png)

**示例模式**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

有关每个必需子字段的完整信息，请 `xdm:productListItems`参阅市场营销 [规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) 。

## 映射和摄取数据

确定营销事件数据是否可映射到CEE模式后，下一步是确定要将哪些数据引入智能服务。 智能服务中使用的所有历史数据必须在四个月数据的最短时间窗口中，加上计划作为回顾期的天数。

在确定要发送的数据范围后，请与Adobe咨询服务部门联系，帮助将数据映射到模式并将其引入服务。

如果您拥有Adobe Experience Platform订阅并希望自己映射和摄取数据，请按照以下部分中概述的步骤操作。

### 使用Adobe Experience Platform

>[!NOTE] 以下步骤需要订阅Experience Platform。 如果您无权访问平台，请跳到下一 [步部分](#next-steps) 。

本节概述了将数据映射到Experience Platform以用于智能服务的工作流程，包括指向教程的链接以了解详细步骤。

#### 创建CEE模式和数据集

当您准备好开始准备数据以进行摄取时，第一步是创建一个使用CEE混音的新XDM模式。 以下教程将演练在UI或API中创建新模式的过程：

* [在UI中创建模式](../xdm/tutorials/create-schema-ui.md)
* [在API中创建模式](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] 以上教程遵循创建模式的通用工作流程。 为模式选择类时，必须使用 **XDM ExperienceEvent类**。 选择此类后，您可以将CEE混音添加到模式。

在将CEE混音添加到模式后，您可以根据数据中其他字段的需要添加其他混音。

创建并保存模式后，您可以基于该模式创建新数据集。 以下教程将演练在UI或API中创建新数据集的过程：

* [在UI中创建数据集](../catalog/datasets/user-guide.md#create) (按照工作流使用现有模式)
* [在API中创建数据集](../catalog/datasets/create.md)

#### 向数据集添加主标识命名空间标记

如果您从Adobe受众管理器、Adobe Analytics或其他外部源导入数据，则必须向数据集 `primaryIdentityNameSpace` 添加一个标记。 这可以通过向Catalog Service API发出PATCH请求来完成。

如果从本地CSV文件中摄取数据，可跳到有关映射和摄取数据的下 [一节](#ingest)。

在与下面的示例API调用一起进行之前，请参 [阅目录开发人员指南](../catalog/api/getting-started.md) 中的“入门”部分，以了解有关所需标头的重要信息。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 您之前创建的数据集的ID。 |

**请求**

根据您从哪个源接收数据，您必须在请求有效负荷 `primaryIdentityNamespace` 中提 `sourceConnectorId` 供适当的和标记值。

以下请求为受众管理器添加适当的标记值：

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["mcid"],
          "sourceConnectorId": ["audiencemanager"],
        }
      }'
```

以下请求为Analytics添加适当的标记值：

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["aaid"],
          "sourceConnectorId": ["analytics"],
        }
      }'
```

>[!NOTE] 有关在平台中使用身份命名空间的更多信息，请参阅 [身份命名空间概述](../identity-service/namespaces.md)。

**响应**

成功的响应会返回包含更新数据集ID的数组。 此ID应与在PATCH请求中发送的ID匹配。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

#### 映射和摄取数据 {#ingest}

创建CEE模式和数据集后，您可以开始将数据表映射到模式，并将数据引入平台。 有关如何在 [UI中执行此操作的步骤](../ingestion/tutorials/map-a-csv-file.md) ，请参阅将CSV文件映射到XDM模式的教程。 填充数据集后，可以使用同一数据集来摄取其他数据文件。

如果您的数据存储在支持的第三方应用程序中，您还可以选择创建源 [连接器](../sources/home.md) ，以实时将营销事件数据引入平台。

## 后续步骤 {#next-steps}

本文档提供了有关准备数据以用于智能服务的一般指导。 如果您需要根据您的用例进行其他咨询，请与Adobe咨询支持联系。

成功填充包含客户体验数据的数据集后，即可使用Intelligent Services生成洞察。 请参阅以下文档以开始：

* [归因人工智能概述](./attribution-ai/overview.md)
* [客户人工智能概述](./customer-ai/overview.md)
