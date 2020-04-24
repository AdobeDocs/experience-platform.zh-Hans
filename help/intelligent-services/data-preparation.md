---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: 准备要在智能服务中使用的数据
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 1b367eb65d1e592412d601d089725671e42b7bbd

---


# 准备要在智能服务中使用的数据

为了让智能服务从您的营销事件数据中发掘洞察，数据必须在语义上得到丰富并以标准结构进行维护。 智能服务利用体验数据模型(XDM)模式来实现这一点。 具体而言，智能服务中使用的所有数据集都必须符合 **Consumer ExperienceEvent(CEE)** XDM模式。

本文档提供有关将营销事件数据从多个渠道映射到本模式的一般指导，概述有关该模式中重要字段的信息，以帮助您确定如何将数据有效地映射到其结构。

## 了解CEE模式

消费者体验事件模式描述个人的行为，因为它与数字营销事件（Web或移动）以及在线或离线商务活动相关。 智能服务需要使用此模式，因为其语义上定义良好的字段（列），从而避免了任何未知名称，否则这些名称会使数据变得不那么清晰。

智能服务利用此模式中的几个关键字段，根据您的营销事件数据生成洞察，所有这些洞察均可在根级别找到并展开，以显示其必需的子字段。

![](./images/data-preparation/schema-expansion.gif)

与所有XDM模式一样，CEE mixin是可扩展的。 换句话说，可以向CEE mixin添加其他字段，如果需要，可以在多个模式中包含不同的变体。

可以在公共XDM存储库中找到混音的完整示例 [](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)，并应用作以下部分概述的关键字段的引用。

## 关键字段

以下各节重点介绍了CEE Mix中的关键字段，这些字段应用于智能服务以生成有用的洞察，包括说明和指向参考文档的链接，以获取更多示例。

### xdm:渠道

此字段表示与ExperienceEvent相关的营销渠道。 该字段包含有关渠道类型、媒体类型和位置类型的信息。 **必须提&#x200B;_供此字段_，才能让归因AI处理您的数据**。

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

有关每个必需子字段的完整信息，请 `xdm:channel`参阅体验渠道 [模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) 。 有关某些映射的示例，请参 [阅下表](#example-channels)。

#### 示例渠道映射 {#example-channels}

下表提供映射到该渠道的营销模式的一些示 `xdm:channel` 例：

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 付费搜索 | https:/<span>/ns.adobe.com/xdm/渠道类型／搜索 | 已付 | 单击 |
| 社交——营销 | https:/<span>/ns.adobe.com/xdm/渠道类型／社交 | 挣 | 单击 |
| 显示 | https:/<span>/ns.adobe.com/xdm/渠道类型／显示 | 已付 | 单击 |
| 电子邮件 | https:/<span>/ns.adobe.com/xdm/渠道类型／电子邮件 | 已付 | 单击 |
| 内部推荐人 | https:/<span>/ns.adobe.com/xdm/渠道类型／直接 | 自有 | 单击 |
| 显示浏览 | https:/<span>/ns.adobe.com/xdm/渠道类型／显示 | 已付 | 印象 |
| QR码重定向 | https:/<span>/ns.adobe.com/xdm/渠道类型／直接 | 自有 | 单击 |
| 移动设备 | https:/<span>/ns.adobe.com/xdm/渠道类型／移动 | 自有 | 单击 |

### xdm:productListItems

此字段是代表客户选择的产品的一组项目，包括产品SKU、名称、价格和数量。

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

有关每个必填字段的完整信息，请参 `xdm:productListItems`阅商务详细信 [息模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 。

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

有关每个必填字段的完整信息，请参 `xdm:commerce`阅商务详细信 [息模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 。

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

有关每个必需子字段的完整信息，请参 `xdm:productListItems`阅ExperienceEvent Web详细信 [息模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) 。

### xdm：营销

此字段包含与与接触点处于活动状态的营销活动相关的信息。

![](./images/data-preparation/marketing.png)

**示例模式**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

有关每个必需子字段的完整信息，请 `xdm:productListItems`参阅市场营销部 [门规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) 。

## 映射和摄取数据

确定营销事件数据是否可映射到CEE模式后，您可以开始将数据导入智能服务的过程。 联系Adobe咨询服务，帮助将数据映射到模式并将其引入服务。

如果您拥有Adobe Experience Platform订阅并希望自己映射和摄取数据，请按照以下部分中所述的步骤操作。

### 使用Adobe Experience Platform

>[!NOTE] 以下步骤需要订阅到Experience Platform。 如果您无权访问平台，请跳到下一步 [部分](#next-steps) 。

本节概述了将数据映射到Experience Platform以用于智能服务的工作流程，包括指向教程的详细步骤链接。

#### 创建CEE模式和数据集

当您准备好开始准备数据以进行摄取时，第一步是创建一个使用CEE混音的新XDM模式。 以下教程将逐步介绍在UI或API中创建新模式的过程：

* [在UI中创建模式](../xdm/tutorials/create-schema-ui.md)
* [在API中创建模式](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] 以上教程遵循了创建模式的通用工作流程。 为模式选择类时，必须使用 **XDM ExperienceEvent类**。 选择此类后，您可以将CEE混音添加到模式。

在将CEE混音添加到模式后，您可以根据数据中其他字段的需要添加其他混音。

创建并保存模式后，您可以基于该模式创建新数据集。 以下教程将逐步介绍在UI或API中创建新数据集的过程：

* [在UI中创建数据集](../catalog/datasets/user-guide.md#create) (按照工作流使用现有模式)
* [在API中创建数据集](../catalog/datasets/create.md)

#### 映射和摄取数据

创建CEE模式和数据集后，您可以开始将数据表映射到模式，并将该数据引入平台。 有关如何在UI [中执行此操作的步骤](../ingestion/tutorials/map-a-csv-file.md) ，请参阅有关将CSV文件映射到XDM模式的教程。 在填充数据集后，可以使用同一数据集摄取其他数据文件。

## 后续步骤 {#next-steps}

本文档为准备要在智能服务中使用的数据提供了一般指导。 如果您需要根据您的用例进行其他咨询，请联系Adobe咨询支持。

成功填充包含客户体验数据的数据集后，您便可以使用Intelligent Services生成洞察。 请参阅以下文档以开始：

* [归因人工智能概述](./attribution-ai/overview.md)
* [客户人工智能概述](./customer-ai/overview.md)
