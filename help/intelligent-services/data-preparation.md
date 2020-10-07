---
keywords: Experience Platform;home;Intelligent Services;popular topics;intelligent service;Intelligent service
solution: Experience Platform
title: 准备要在Intelligent Services中使用的数据
topic: Intelligent Services
description: '为了使智能服务能够从您的营销事件数据中发掘洞察，必须以标准结构从语义上丰富和维护数据。 智能服务利用体验数据模型(XDM)模式来实现此目标。 具体而言，在智能服务中使用的所有数据集]必须符合Consumer ExperienceEvent(CEE)XDM模式。 '
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1979'
ht-degree: 0%

---


# 准备要在 [!DNL Intelligent Services]

要从营销 [!DNL Intelligent Services] 事件数据中发掘洞察，必须以标准结构从语义上丰富和维护数据。 [!DNL Intelligent Services] 利 [!DNL Experience Data Model] 用(XDM)模式实现这一目标。 具体而言，中使用的所 [!DNL Intelligent Services] 有数据集都必须符合Consumer ExperienceEvent(CEE)XDM模式。

此文档提供有关将营销事件数据从多个渠道映射到此模式的一般指南，概述模式中重要字段的信息，以帮助您确定如何有效地将数据映射到其结构。

## 工作流摘要

准备过程因数据是存储在Adobe Experience Platform还是外部而异。 本节总结了在任一情况下需要采取的必要步骤。

### 外部数据准备

如果数据存储在外部， [!DNL Experience Platform]请按照以下步骤操作：

1. 联系Adobe咨询服务以请求专用Azure Blob存储容器的访问凭据。
1. 使用访问凭据，将数据上传到Blob容器。
1. 使用Adobe咨询服务，将您的数据映射到消 [费者体验事件模式](#cee-schema) ，并引入 [!DNL Intelligent Services]中。

### [!DNL Experience Platform] 数据准备

如果数据已存储在中， [!DNL Platform]请按照以下步骤操作：

1. 查看“消费者体验 [事件”模式的结构](#cee-schema) ，并确定数据是否可以映射到其字段。
1. 联系Adobe咨询服务以帮助将您的数据映射到并将其 [!DNL Intelligent Services]引入 [模式，如果您想亲自映射数据，请遵循本指南中的步骤](#mapping) 。

## 了解CEE模式 {#cee-schema}

消费者体验事件模式描述个人的行为，因为它与数字营销事件（Web或移动）以及在线或离线商务活动相关。 由于此模式的语义定义良好 [!DNL Intelligent Services] 的字段（列），因此需要使用此，避免使用任何未知名称，否则会使数据变得不那么清晰。

与所有XDM ExperienceEvent模式一样， CEE模式在发生事件(或一组事件)时捕获基于时间序列的系统状态，包括时间点和相关主题的身份。 体验事件是事实记录，因此它们是不可改变的，代表所发生的事情，而不经过聚合或解释。

[!DNL Intelligent Services] 利用此模式中的几个关键字段从营销事件数据中生成洞察，所有这些数据都可以在根级别找到并展开以显示其必需的子字段。

![](./images/data-preparation/schema-expansion.gif)

与所有XDM模式一样， CEE混合是可扩展的。 换言之，CEE混音中可添加其他字段，如果需要，可在多个模式中包含不同的变体。

在公共XDM存储库中可以找到混合 [的完整示例](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)。 此外，您还可以视图并复制以 [下JSON文件](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) ，以了解如何构建数据以符合CEE模式。 当您了解下面部分中概述的关键字段时，请参阅这两个示例，以确定如何将您自己的数据映射到模式。

## 键字段

CEE混音中有几个关键字段应用于生成有用 [!DNL Intelligent Services] 的洞察。 本节介绍这些字段的用例和预期数据，并提供参考文档的链接以获取更多示例。

### 必填字段

强烈建议使用所有关键字段，但有两个字段是必 **填** ，才能 [!DNL Intelligent Services] 工作：

* [主标识字段](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:渠道](#channel) (仅对Attribution AI强制)

#### 主要身份 {#identity}

模式中的其中一个字段必须设置为主标识字段，该字段允许 [!DNL Intelligent Services] 将时间序列数据的每个实例关联到个人。

您必须根据数据的来源和性质确定用作主要标识的最佳字段。 标识字段必须包含标 **识命名空间** ，该标识指示字段期望作为值的标识数据类型。 一些有效的命名空间值包括：

* &quot;电子邮件&quot;
* &quot;phone&quot;
* “mcid”(针对Adobe Audience ManagerID)
* “aaid”(针对Adobe AnalyticsID)

如果您不确定应将哪个字段用作主要标识，请与Adobe咨询服务部门联系以确定最佳解决方案。

#### xdm:timestamp {#timestamp}

此字段表示发生事件的日期时间。 必须按照ISO 8601标准将此值作为字符串提供。

#### xdm:渠道 {#channel}

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

有关每个必需子字段的完整信息，请 `xdm:channel`参阅体验渠道 [模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) 。 有关某些示例映射，请参 [阅下表](#example-channels)。

##### 渠道映射示例 {#example-channels}

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

### 推荐字段

本节概述了其余的关键字段。 虽然这些字段不一定需要 [!DNL Intelligent Services] 才能使用，但强烈建议您尽可能多地使用它们以获得更丰富的洞察。

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

有关每个必需子字段的完整信息， `xdm:productListItems`请参阅商务详细 [信息模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 。

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

有关每个必需子字段的完整信息， `xdm:commerce`请参阅商务详细 [信息模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 。

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

有关每个必需子字段的完整信息，请 `xdm:productListItems`参阅ExperienceEvent Web详 [细信息模式规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) 。

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

有关每个必需子字段的完整信息，请 `xdm:productListItems`参阅市场营销 [规范](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) 。

## 映射和摄取数据 {#mapping}

确定营销事件数据是否可映射到CEE模式后，下一步是确定要引入哪些数据 [!DNL Intelligent Services]。 使用的所有历史数 [!DNL Intelligent Services] 据都必须在4个月数据的最短时间窗口内，加上计划作为回顾期的天数。

在确定要发送的Adobe范围后，请与模式咨询服务部门联系，帮助将数据映射到并将其引入服务。

如果您有 [!DNL Adobe Experience Platform] 订阅并希望自己映射和摄取数据，请按照以下部分中概述的步骤操作。

### 使用Adobe Experience Platform

>[!NOTE]
>
>以下步骤需要订阅Experience Platform。 如果您无权访问平台，请跳到下一 [步部分](#next-steps) 。

本节概述了将数据映射到Experience Platform并将其引入以供使用的工作流程， [!DNL Intelligent Services]包括指向教程的链接，以了解详细步骤。

#### 创建CEE模式和数据集

当您准备好开始准备数据以进行摄取时，第一步是创建一个使用CEE混音的新XDM模式。 以下教程将演练在UI或API中创建新模式的过程：

* [在UI中创建模式](../xdm/tutorials/create-schema-ui.md)
* [在API中创建模式](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>以上教程遵循创建模式的通用工作流程。 为模式选择类时，必须使用 **XDM ExperienceEvent类**。 选择此类后，您可以将CEE混音添加到模式。

在将CEE混音添加到模式后，您可以根据数据中其他字段的需要添加其他混音。

创建并保存模式后，您可以基于该模式创建新数据集。 以下教程将演练在UI或API中创建新数据集的过程：

* [在UI中创建数据集](../catalog/datasets/user-guide.md#create) (按照工作流使用现有模式)
* [在API中创建数据集](../catalog/datasets/create.md)

创建数据集后，您可以在数据集工作区的平台UI中找 **[!UICONTROL 到它]** 。

![](images/data-preparation/dataset-location.png)

#### 向数据集添加主标识命名空间标记

>[!NOTE]
>
>未来版本 [!DNL Intelligent Services] 将整合Adobe Experience Platform [身份服务](../identity-service/home.md) ，使其客户识别能力。 因此，以下概述的步骤可能会发生变化。

如果导入来自、或 [!DNL Adobe Audience Manager]其 [!DNL Adobe Analytics]他外部源的数据，则必须向数据集 `primaryIdentityNameSpace` 添加标记。 这可以通过向Catalog Service API发出PATCH请求来完成。

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

以下请求为Audience Manager添加适当的标记值：

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

>[!NOTE]
>
>有关在平台中使用身份命名空间的更多信息，请参阅 [身份命名空间概述](../identity-service/namespaces.md)。

**响应**

成功的响应会返回包含更新数据集ID的数组。 此ID应与在PATCH请求中发送的ID匹配。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

#### 映射和摄取数据 {#ingest}

创建CEE模式和数据集后，您可以开始将数据表映射到模式，并将数据引入平台。 有关如何在 [UI中执行此操作的步骤](../ingestion/tutorials/map-a-csv-file.md) ，请参阅将CSV文件映射到XDM模式的教程。 在使用您自己的数 [据之前](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) ，可以使用以下示例JSON文件测试摄取过程。

填充数据集后，可以使用同一数据集来摄取其他数据文件。

如果您的数据存储在支持的第三方应用程序中，您还可以选择创建源 [连接器](../sources/home.md) ，将营销事件数据实 [!DNL Platform] 时收集到中。

## 后续步骤 {#next-steps}

本文档提供了有关准备数据以供使用的一般指导 [!DNL Intelligent Services]。 如果您需要根据您的用例进行其他咨询，请与Adobe咨询支持联系。

成功填充包含客户体验数据的数据集后，即可用 [!DNL Intelligent Services] 于生成洞察。 请参阅以下文档以开始：

* [Attribution AI概述](./attribution-ai/overview.md)
* [客户人工智能概述](./customer-ai/overview.md)
