---
keywords: Experience Platform；主页；智能服务；热门主题；智能服务；智能服务
solution: Experience Platform
title: 准备数据以在智能服务中使用
topic-legacy: Intelligent Services
description: 为了使智能服务能够从营销事件数据中发现洞察，必须在语义上对数据进行扩充并以标准结构进行维护。 智能服务使用体验数据模型(XDM)架构来实现此目的。
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '2919'
ht-degree: 0%

---

# 准备数据以在中使用 [!DNL Intelligent Services]

为 [!DNL Intelligent Services] 要从营销事件数据中发现洞察，必须在语义上对数据进行扩充并在标准结构中进行维护。 [!DNL Intelligent Services] 利用 [!DNL Experience Data Model] (XDM)模式来实现此目的。 具体而言， [!DNL Intelligent Services] 必须符合Consumer ExperienceEvent(CEE)XDM架构或使用Adobe Analytics连接器。 此外， Customer AI还支持Adobe Audience Manager连接器。

本文档就将营销事件数据从多个渠道映射到CEE架构提供了一般指导，概述了架构内重要字段的信息，以帮助您确定如何将数据有效映射到其结构。 如果您计划使用Adobe Analytics数据，请查看 [Adobe Analytics数据准备](#analytics-data). 如果您计划使用Adobe Audience Manager数据（仅限Customer AI），请查看 [AdobeAudience Manger数据准备](#AAM-data).

## 数据要求

[!DNL Intelligent Services] 根据您创建的目标，需要不同数量的历史数据。 无论如何，您准备的数据 **全部** [!DNL Intelligent Services] 必须同时包含正面和负面的客户历程/事件。 同时具有负事件和正事件可提高模型精度和准确性。

例如，如果您使用Customer AI来预测购买产品的倾向，则Customer AI的模型需要成功购买路径的示例和失败路径的示例。 这是因为在模型培训期间， Customer AI会了解哪些事件和历程会导致购买。 此外，还包括未购买的客户执行的操作，例如在将项目添加到购物车时停止其历程的个人。 这些客户可能表现出类似的行为，但是， Customer AI可以提供洞察并深入分析导致倾向得分较高的主要差异和因素。 同样，Attribution AI需要同时使用事件类型和历程类型，才能按接触点位置显示接触点有效性、热门转化路径和划分等量度。

有关历史数据要求的更多示例和信息，请访问 [客户人工智能](./customer-ai/input-output.md#data-requirements) 或 [Attribution AI](./attribution-ai/input-output.md#data-requirements) 输入/输出文档中的历史数据要求部分。

### 拼合数据的准则

建议您尽可能将用户的事件拼合到通用ID中。 例如，您可能有10个事件中的“id1”用户数据。 之后，同一用户删除了Cookie ID，并在接下来的20个事件中记录为“id2”。 如果您知道id1和id2对应于同一用户，则最佳实践是将所有30个事件与一个通用id拼合在一起。

如果这不可能，则在创建模型输入数据时，应将每组事件视为不同的用户。 这可确保在模型培训和评分期间获得最佳结果。

## 工作流摘要

准备过程会因数据是存储在Adobe Experience Platform中还是存储在外部而异。 此部分概述了在两种情况下需要采取的必要步骤。

### 外部数据准备

如果您的数据存储在Experience Platform之外，则需要将数据映射到 [消费者体验事件架构](#cee-schema). 可以使用自定义字段组扩展此模式，以更好地捕获客户数据。 映射后，您可以使用消费者体验事件架构创建数据集，并 [将数据摄取到平台](../ingestion/home.md). 然后，在配置 [!DNL Intelligent Service].

根据 [!DNL Intelligent Service] 您希望使用，可能需要不同的字段。 请注意，如果您有可用的数据，则最好将数据添加到字段。 要了解有关必填字段的更多信息，请访问 [Attribution AI](./attribution-ai/input-output.md) 或 [客户人工智能](./customer-ai/input-output.md) 输入/输出指南。

### Adobe Analytics数据准备 {#analytics-data}

Customer AI和Attribution AI本地支持Adobe Analytics数据。 要使用Adobe Analytics数据，请按照文档中概述的步骤，设置 [Analytics源连接器](../sources/tutorials/ui/create/adobe-applications/analytics.md).

在源连接器将您的数据流式传输到Experience Platform后，您便能够在实例配置期间选择Adobe Analytics作为数据源，后跟一个数据集。 连接设置期间，将自动创建所有必需架构字段组和单个字段。 您无需对数据集进行ETL（提取、转换、加载）操作，即可将其转换为CEE格式。

如果比较通过Adobe Analytics源连接器传输到Adobe Experience Platform的数据与Adobe Analytics数据，您可能会注意到一些差异。 在转换到体验数据模型(XDM)架构期间，Analytics源连接器可能会丢弃行。 整行可能存在多个不适合进行转换的原因，包括缺少时间戳、缺少人员ID、无效或较大的人员ID、分析值无效等。

有关更多信息和示例，请访问 [比较Adobe Analytics和Customer Journey Analytics数据](https://www.adobe.com/go/compare-aa-data-to-cja-data). 本文旨在帮助您诊断和解决这些差异，以便您和您的团队能够不受数据完整性方面的顾虑的影响，将Adobe Experience Platform数据用于Intelligent Services。

在Adobe Experience Platform查询服务中，按channel.typeAtSource查询运行以下开始时间戳和结束时间戳之间的记录总数，以按营销渠道查找计数。

```SELECT channel.typeAtSource as typeAtSource,
       Count(_id) AS Records 
FROM  df_hotel
WHERE timestamp>=from_utc_timestamp('2021-05-15','UTC')
        AND timestamp<from_utc_timestamp('2022-01-10','UTC')
        AND timestamp IS NOT NULL
        AND enduserids._experience.aaid.id IS NOT NULL
GROUP BY channel.typeAtSource
```

>[!IMPORTANT]
>
>Adobe Analytics连接器最多需要四周时间才能回填数据。 如果您最近设置了连接，则应验证数据集是否具有客户或Attribution AI所需的最小数据长度。 请查看 [客户人工智能](./customer-ai/input-output.md#data-requirements) 或 [Attribution AI](./attribution-ai/input-output.md#data-requirements)，并验证是否有足够的数据来实现预测目标。

### Adobe Audience Manager数据准备（仅限Customer AI） {#AAM-data}

Customer AI本地支持Adobe Audience Manager数据。 要使用Audience Manager数据，请按照文档中概述的步骤，设置 [Audience Manager源连接器](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

在源连接器将您的数据流式传输到Experience Platform后，您便能够在Customer AI配置期间选择Adobe Audience Manager作为数据源，后跟一个数据集。 连接设置期间，将自动创建所有架构字段组和单个字段。 您无需对数据集进行ETL（提取、转换、加载）操作，即可将其转换为CEE格式。

>[!IMPORTANT]
>
>如果您最近设置了一个连接器，则应验证数据集是否具有所需的最小数据长度。 请查看 [输入/输出文档](./customer-ai/input-output.md) ，并验证您是否有足够的数据来实现预测目标。

### [!DNL Experience Platform] 数据准备

如果您的数据已存储在 [!DNL Platform] 且不会通过Adobe Analytics或Adobe Audience Manager（仅限Customer AI）源连接器进行流式传输，请执行以下步骤。 我们仍建议您了解CEE模式。

1. 查看 [消费者体验事件架构](#cee-schema) 并确定数据是否可以映射到其字段。
2. 联系Adobe咨询服务部门，以帮助将您的数据映射到架构并将其摄取到 [!DNL Intelligent Services]或 [按照本指南中的步骤操作](#mapping) 如果您想自己映射数据，请执行以下操作：

## 了解CEE架构 {#cee-schema}

消费者体验事件架构描述个人的行为，因为它与数字营销事件（Web或移动设备）以及在线或离线商务活动相关。 需要使用此架构， [!DNL Intelligent Services] 由于其语义上定义良好的字段（列），因此可以避免任何未知名称，否则这些名称会使数据变得不那么清晰。

与所有XDM ExperienceEvent架构一样，CEE架构可在发生事件（或事件集）时捕获系统基于时间序列的状态，包括所涉及主题的时间点和身份。 体验事件是所发生事件的事实记录，因此它们不可更改，不经聚合或解释即表示所发生事件。

[!DNL Intelligent Services] 利用此架构中的几个关键字段从营销事件数据生成分析，所有这些数据均可在根级别找到并展开以显示其必需子字段。

![](./images/data-preparation/schema-expansion.gif)

与所有XDM架构一样，CEE架构字段组也是可扩展的。 换言之，可以将其他字段添加到CEE字段组，并且如有必要，可以将不同的变体包含在多个架构中。

有关字段组的完整示例，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). 此外，您还可以查看和复制以下内容 [JSON文件](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) 例如，如何构建数据以符合CEE模式。 在了解下面章节中概述的关键字段时，请参阅这两个示例，以确定如何将您自己的数据映射到架构。

## 关键字段

CEE字段组中有几个关键字段，应用这些关键字段 [!DNL Intelligent Services] 以生成有用的分析。 此部分介绍这些字段的用例和预期数据，并提供指向参考文档的链接以获取更多示例。

### 必填字段

尽管强烈建议使用所有键字段，但有两个字段是 **必需** 为 [!DNL Intelligent Services] 工作：

* [主标识字段](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (仅对于Attribution AI必填)

#### 主标识 {#identity}

架构中的其中一个字段必须设置为主标识字段，该字段允许 [!DNL Intelligent Services] 将时间序列数据的每个实例关联到个人。

您必须根据数据的来源和性质确定要用作主标识的最佳字段。 标识字段必须包括 **标识命名空间** 表示字段期望作为值的身份数据类型。 一些有效的命名空间值包括：

* &quot;电子邮件&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(用于Adobe Audience Manager ID)
* &quot;aaid&quot;(用于Adobe Analytics ID)

如果不确定应将哪个字段用作主标识，请联系Adobe咨询服务部门以确定最佳解决方案。 如果未设置主标识，则Intelligent Service应用程序会使用以下默认行为：

| 默认 | Attribution AI | 客户人工智能 |
| --- | --- | --- |
| 标识列 | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| 命名空间 | AAID | ECID |

要设置主标识，请从 **[!UICONTROL 模式]** 选项卡，然后选择架构名称超链接以打开 **[!DNL Schema Editor]**.

![导航到架构](./images/data-preparation/navigate_schema.png)

接下来，导航到要作为主标识的字段，并将其选中。 的 **[!UICONTROL 字段属性]** 菜单。

![选择字段](./images/data-preparation/find_field.png)

在 **[!UICONTROL 字段属性]** 菜单，向下滚动直到您找到 **[!UICONTROL 身份]** 复选框。 选中该框后，用于将所选标识设置为 **[!UICONTROL 主标识]** 中。 也选中此框。

![选中复选框](./images/data-preparation/set_primary_identity.png)

接下来，您必须提供 **[!UICONTROL 身份命名空间]** 从下拉列表中的预定义命名空间列表。 在此示例中，选择ECID名称空间是因为Adobe Audience Manager ID `mcid.id` 中。 选择 **[!UICONTROL 应用]** 要确认更新，请选择 **[!UICONTROL 保存]** ，以保存对架构所做的更改。

![保存更改](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

此字段表示事件发生的日期时间。 此值必须作为字符串提供，符合ISO 8601标准。

#### xdm:channel {#channel}

>[!NOTE]
>
>只有在使用Attribution AI时，此字段才是必填字段。

此字段表示与ExperienceEvent相关的营销渠道。 该字段包含有关渠道类型、媒体类型和位置类型的信息。

![](./images/data-preparation/channel.png)

**示例架构**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

有关 `xdm:channel`，请参阅 [体验渠道架构](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) 规范。 有关某些示例映射，请参阅 [下表](#example-channels).

#### 渠道映射示例 {#example-channels}

下表提供了一些映射到 `xdm:channel` 架构：

| 渠道 | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 付费搜索 | https:/<span>/ns.adobe/com/xdm/channel-types/search | 已付 | 点击 |
| 社交 — 营销 | https:/<span>/ns.adobe/com/xdm/channel-types/social | 挣得 | 点击 |
| 显示 | https:/<span>/ns.adobe/com/xdm/channel-types/display | 已付 | 点击 |
| 电子邮件 | https:/<span>/ns.adobe/com/xdm/channel-types/email | 已付 | 点击 |
| 内部反向链接 | https:/<span>/ns.adobe/com/xdm/channel-types/direct | 自有 | 点击 |
| 显示显示显示到达 | https:/<span>/ns.adobe/com/xdm/channel-types/display | 已付 | 展示次数 |
| QR代码重定向 | https:/<span>/ns.adobe/com/xdm/channel-types/direct | 自有 | 点击 |
| 移动设备 | https:/<span>/ns.adobe/com/xdm/channel-types/mobile | 自有 | 点击 |

### 推荐字段

本节概述了其余的关键字段。 虽然这些字段不一定是 [!DNL Intelligent Services] 为了使用，强烈建议您尽可能多地使用这些函数来获取更丰富的洞察信息。

#### xdm:productListItems

此字段是表示客户选择的产品的项目数组，包括产品SKU、名称、价格和数量。

![](./images/data-preparation/productListItems.png)

**示例架构**

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

有关 `xdm:productListItems`，请参阅 [商务详细信息架构](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 规范。

#### xdm:commerce

此字段包含有关ExperienceEvent的特定于商务的信息，包括采购订单编号和付款信息。

![](./images/data-preparation/commerce.png)

**示例架构**

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

有关 `xdm:commerce`，请参阅 [商务详细信息架构](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 规范。

#### xdm:web

此字段表示与ExperienceEvent相关的Web详细信息，如交互、页面详细信息和反向链接。

![](./images/data-preparation/web.png)

**示例架构**

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

有关 `xdm:productListItems`，请参阅 [ExperienceEvent Web详细信息架构](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) 规范。

#### xdm:marketing

此字段包含与接触点处于活动状态的营销活动相关的信息。

![](./images/data-preparation/marketing.png)

**示例架构**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

有关 `xdm:productListItems`，请参阅 [营销部门](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) 规范。

## 映射和摄取数据 {#mapping}

确定营销事件数据是否可以映射到CEE架构后，下一步是确定要引入哪些数据 [!DNL Intelligent Services]. 中使用的所有历史数据 [!DNL Intelligent Services] 必须位于四个月数据的最小时间范围内，另外还应包含预期作为回顾期的天数。

在确定要发送的数据范围后，请联系Adobe咨询服务部门，以帮助将您的数据映射到架构并将其摄取到服务中。

如果您有 [!DNL Adobe Experience Platform] 订阅，并想要自行映射和摄取数据，请按照以下部分中所述的步骤操作。

### 使用Adobe Experience Platform

>[!NOTE]
>
>以下步骤需要订阅Experience Platform。 如果您无权访问Platform，请跳转至 [后续步骤](#next-steps) 中。

本节概述了将数据映射和摄取到Experience Platform中以供在中使用的工作流 [!DNL Intelligent Services]，包括指向教程的链接以了解详细步骤。

#### 创建CEE架构和数据集

当您准备好开始准备数据以进行摄取时，第一步是创建一个新的XDM架构，该架构将采用CEE字段组。 以下教程将指导在UI或API中创建新架构的过程：

* [在UI中创建架构](../xdm/tutorials/create-schema-ui.md)
* [在API中创建架构](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>上述教程遵循创建模式的通用工作流。 为架构选择类时，必须使用 **XDM ExperienceEvent类**. 选择此类后，您可以将CEE字段组添加到架构中。

将CEE字段组添加到架构后，您可以根据数据中其他字段的需要，添加其他字段组。

创建并保存架构后，您便可以基于该架构创建新数据集。 以下教程将演示在UI或API中创建新数据集的过程：

* [在UI中创建数据集](../catalog/datasets/user-guide.md#create) （按照使用现有架构的工作流操作）
* [在API中创建数据集](../catalog/datasets/create.md)

创建数据集后，您可以在的平台UI中找到该数据集 **[!UICONTROL 数据集]** 工作区。

![](images/data-preparation/dataset-location.png)

#### 向数据集添加标识字段

如果您从 [!DNL Adobe Audience Manager], [!DNL Adobe Analytics]或其他外部源，则可以选择将架构字段设置为标识字段。 要将架构字段设置为标识字段，请查看有关在 [UI教程](../xdm/tutorials/create-schema-ui.md#identity-field) 或 [API教程](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) 创建模式。

如果您要从本地CSV文件摄取数据，则可以跳到 [映射和摄取数据](#ingest).

#### 映射和摄取数据 {#ingest}

创建CEE架构和数据集后，您可以开始将数据表映射到架构，并将该数据摄取到平台。 请参阅 [将CSV文件映射到XDM模式](../ingestion/tutorials/map-a-csv-file.md) 以了解有关如何在UI中执行此操作的步骤。 您可以使用以下内容 [JSON文件示例](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) ，以在使用您自己的数据之前测试摄取流程。

填充数据集后，可以使用同一数据集摄取其他数据文件。

如果您的数据存储在支持的第三方应用程序中，则还可以选择创建 [源连接器](../sources/home.md) 将营销事件数据摄取到 [!DNL Platform] 实时。

## 后续步骤 {#next-steps}

本文档就准备数据以在中使用提供了一般指导 [!DNL Intelligent Services]. 如果您需要根据您的用例进行其他咨询，请联系Adobe咨询支持。

成功使用客户体验数据填充数据集后，您可以使用 [!DNL Intelligent Services] 以生成分析。 请参阅以下文档以开始操作：

* [归因人工智能概述](./attribution-ai/overview.md)
* [客户人工智能概述](./customer-ai/overview.md)
