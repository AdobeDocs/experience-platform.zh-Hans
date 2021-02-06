---
keywords: Experience Platform；主页；智能服务；热门话题；智能服务；智能服务
solution: Experience Platform, Intelligent Services
title: 准备要在智能服务中使用的数据
topic: Intelligent Services
description: '为了使智能服务能够从您的营销事件数据中发掘洞察，必须以标准结构从语义上丰富和维护数据。 智能服务利用体验数据模型(XDM)模式来实现此目标。 具体而言，在智能服务中使用的所有数据集]必须符合Consumer ExperienceEvent(CEE)XDM模式。 '
translation-type: tm+mt
source-git-commit: eb163949f91b0d1e9cc23180bb372b6f94fc951f
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 0%

---


# 准备要在[!DNL Intelligent Services]中使用的数据

要[!DNL Intelligent Services]从营销事件数据中发掘洞察，必须在语义上对数据进行丰富和维护，使其达到标准结构。 [!DNL Intelligent Services] 利 [!DNL Experience Data Model] 用(XDM)模式来实现此目标。具体而言，[!DNL Intelligent Services]中使用的所有数据集都必须符合Consumer ExperienceEvent(CEE)XDM模式。

此文档提供有关将营销事件数据从多个渠道映射到此模式的一般指南，概述模式中重要字段的信息，以帮助您确定如何有效地将数据映射到其结构。

## 工作流摘要

准备过程因数据是存储在Adobe Experience Platform还是外部而异。 本节总结了在任一情况下需要采取的必要步骤。

### 外部数据准备

如果数据存储在[!DNL Experience Platform]之外，请按照以下步骤操作：

1. 联系Adobe咨询服务以请求专用Azure Blob存储容器的访问凭据。
1. 使用访问凭据，将数据上传到Blob容器。
1. 使用Adobe咨询服务，获取映射到[消费者体验事件模式](#cee-schema)并引入到[!DNL Intelligent Services]的数据。

### [!DNL Experience Platform] 数据准备

如果数据已存储在[!DNL Platform]中，请按照以下步骤操作：

1. 查看[Consumer ExperienceEvent模式](#cee-schema)的结构，并确定是否可以将数据映射到其字段。
1. 联系Adobe咨询服务，帮助将数据映射到模式并将其引入[!DNL Intelligent Services]，或者，如果您想自己映射数据，请按照本指南](#mapping)中的步骤操作。[

## 了解CEE模式{#cee-schema}

消费者体验事件模式描述个人的行为，因为它与数字营销事件（Web或移动）以及在线或离线商务活动相关。 由于[!DNL Intelligent Services]的字段（列）在语义上定义良好，因此需要使用此模式，以避免任何未知名称，否则会使数据变得不那么清晰。

与所有XDM ExperienceEvent模式一样， CEE模式在发生事件(或一组事件)时捕获基于时间序列的系统状态，包括时间点和相关主题的身份。 体验事件是事实记录，因此它们是不可改变的，代表所发生的事情，而不经过聚合或解释。

[!DNL Intelligent Services] 利用此模式中的几个关键字段从营销事件数据中生成洞察，所有这些数据都可以在根级别找到并展开以显示其必需的子字段。

![](./images/data-preparation/schema-expansion.gif)

与所有XDM模式一样， CEE混合是可扩展的。 换言之，CEE混音中可添加其他字段，如果需要，可在多个模式中包含不同的变体。

在[公共XDM存储库](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)中可以找到该混合的完整示例。 此外，您还可以视图并复制以下[JSON文件](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)，以了解如何构建数据以符合CEE模式。 当您了解下面部分中概述的关键字段时，请参阅这两个示例，以确定如何将您自己的数据映射到模式。

## 键字段

CEE mix中有几个关键字段应用于[!DNL Intelligent Services]以生成有用的洞察。 本节介绍这些字段的用例和预期数据，并提供参考文档的链接以获取更多示例。

### 必填字段

强烈建议使用所有键字段，但有两个字段是&#x200B;**required**，以便[!DNL Intelligent Services]工作：

* [主标识字段](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:渠道](#channel) (仅对Attribution AI强制)

#### 主标识{#identity}

模式中的其中一个字段必须设置为主标识字段，这允许[!DNL Intelligent Services]将时间序列数据的每个实例链接到单个人。

您必须根据数据的来源和性质确定用作主要标识的最佳字段。 标识字段必须包含&#x200B;**标识命名空间**，该标识指示字段期望作为值的标识数据的类型。 一些有效的命名空间值包括：

* &quot;电子邮件&quot;
* &quot;phone&quot;
* “mcid”(针对Adobe Audience ManagerID)
* “aaid”(针对Adobe AnalyticsID)

如果您不确定应将哪个字段用作主要标识，请与Adobe咨询服务部门联系以确定最佳解决方案。

#### xdm:timestamp {#timestamp}

此字段表示发生事件的日期时间。 必须按照ISO 8601标准将此值作为字符串提供。

#### xdm:渠道{#channel}

>[!NOTE]
>
>仅当使用Attribution AI时，此字段才是必填字段。

此字段表示与ExperienceEvent相关的营销渠道。 该字段包括有关渠道类型、媒体类型和位置类型的信息。

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

有关`xdm:channel`的每个必需子字段的完整信息，请参阅[体验渠道模式](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md)规范。 有关某些映射的示例，请参阅下面的[表](#example-channels)。

##### 渠道映射示例{#example-channels}

下表提供映射到`xdm:channel`渠道的营销模式的一些示例：

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

### 推荐字段

本节概述了其余的关键字段。 虽然[!DNL Intelligent Services]工作不一定需要这些字段，但强烈建议您尽可能多地使用这些字段以获得更丰富的洞察。

#### xdm:productListItems

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

有关`xdm:productListItems`的每个必需子字段的完整信息，请参阅[商务详细信息模式](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md)规范。

#### xdm：商务

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

有关`xdm:commerce`的每个必需子字段的完整信息，请参阅[商务详细信息模式](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md)规范。

#### xdm:web

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

有关`xdm:productListItems`的每个必需子字段的完整信息，请参阅[ExperienceEvent Web详细信息模式](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md)规范。

#### xdm：营销

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

有关`xdm:productListItems`的每个必需子字段的完整信息，请参阅[营销部门](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md)规范。

## 映射和摄取数据{#mapping}

一旦您确定营销事件数据是否可以映射到CEE模式，下一步就是确定要引入[!DNL Intelligent Services]的数据。 [!DNL Intelligent Services]中使用的所有历史数据必须在四个月数据的最小时间窗口内，加上预期作为回顾期的天数。

在确定要发送的Adobe范围后，请与模式咨询服务部门联系，帮助将数据映射到并将其引入服务。

如果您具有[!DNL Adobe Experience Platform]订阅，并且希望自己映射和摄取数据，请按照以下部分中概述的步骤操作。

### 使用Adobe Experience Platform

>[!NOTE]
>
>以下步骤需要订阅Experience Platform。 如果您无权访问平台，请跳到后续步骤](#next-steps)部分。[

本节概述了将数据映射到Experience Platform以用于[!DNL Intelligent Services]的工作流，包括指向教程的链接，以了解详细步骤。

#### 创建CEE模式和数据集

当您准备好开始准备数据以进行摄取时，第一步是创建一个使用CEE混音的新XDM模式。 以下教程将演练在UI或API中创建新模式的过程：

* [在UI中创建模式](../xdm/tutorials/create-schema-ui.md)
* [在API中创建模式](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>以上教程遵循创建模式的通用工作流程。 为模式选择类时，必须使用&#x200B;**XDM ExperienceEvent类**。 选择此类后，您可以将CEE混音添加到模式。

在将CEE混音添加到模式后，您可以根据数据中其他字段的需要添加其他混音。

创建并保存模式后，您可以基于该模式创建新数据集。 以下教程将演练在UI或API中创建新数据集的过程：

* [在UI中创建数据集](../catalog/datasets/user-guide.md#create) (按照工作流使用现有模式)
* [在API中创建数据集](../catalog/datasets/create.md)

创建数据集后，您可以在&#x200B;**[!UICONTROL 数据集]**&#x200B;工作区的平台UI中找到它。

![](images/data-preparation/dataset-location.png)

#### 向数据集添加标识字段

如果导入来自[!DNL Adobe Audience Manager]、[!DNL Adobe Analytics]或其他外部源的数据，则可以选择将模式字段设置为标识字段。 要将模式字段设置为标识字段，请视图有关在[UI教程](../xdm/tutorials/create-schema-ui.md#identity-field)或[API教程](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor)中设置标识字段的部分，以创建模式。

如果从本地CSV文件中摄取数据，可跳到[映射的下一节，并摄取数据](#ingest)。

#### 映射和摄取数据{#ingest}

创建CEE模式和数据集后，您可以开始将数据表映射到模式，并将数据引入平台。 有关如何在UI中执行此操作的步骤，请参阅有关将CSV文件映射到XDM模式](../ingestion/tutorials/map-a-csv-file.md)的教程。 [在使用您自己的数据之前，可以使用以下[示例JSON文件](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)测试摄取过程。

填充数据集后，可以使用同一数据集来摄取其他数据文件。

如果您的事件存储在支持的第三方应用程序中，您还可以选择创建[源连接器](../sources/home.md)，以实时将您的营销数据收录到[!DNL Platform]中。

## 后续步骤 {#next-steps}

本文档提供了有关准备要在[!DNL Intelligent Services]中使用的数据的一般指导。 如果您需要根据您的用例进行其他咨询，请与Adobe咨询支持联系。

成功用客户体验数据填充数据集后，可使用[!DNL Intelligent Services]生成洞察。 请参阅以下文档以开始：

* [Attribution AI 概述](./attribution-ai/overview.md)
* [Customer AI 概述](./customer-ai/overview.md)
