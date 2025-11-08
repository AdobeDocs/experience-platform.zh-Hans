---
keywords: Experience Platform；主页；智能服务；热门主题；智能服务；智能服务
solution: Experience Platform
title: 准备数据以用于智能服务
description: 为了使智能服务从营销事件数据中发掘洞察信息，必须在语义上丰富并维护标准结构中的数据。 智能服务使用Experience Data Model (XDM)架构来实现这一点。
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '2951'
ht-degree: 0%

---

# 准备数据以在[!DNL Intelligent Services]中使用

为了让[!DNL Intelligent Services]从营销事件数据中发掘见解，必须在标准结构中从语义上扩充和维护数据。 [!DNL Intelligent Services]利用[!DNL Experience Data Model] (XDM)架构来实现这一点。 具体而言，[!DNL Intelligent Services]中使用的所有数据集都必须符合Consumer ExperienceEvent (CEE) XDM架构或使用Adobe Analytics连接器。 此外，客户人工智能支持Adobe Audience Manager连接器。

本文档提供了有关将营销事件数据从多个渠道映射到CEE架构的一般指导，其中概述了架构内重要字段的信息，以帮助您确定如何有效地将数据映射到其结构。 如果您计划使用Adobe Analytics数据，请查看[Adobe Analytics数据准备](#analytics-data)部分。 如果您计划使用Adobe Audience Manager数据（仅限客户人工智能），请查看[Adobe Audience Manger数据准备](#AAM-data)部分。

## 数据要求

根据您创建的目标，[!DNL Intelligent Services]需要不同的历史数据量。 无论如何，您为&#x200B;**所有** [!DNL Intelligent Services]准备的数据都必须包括正面和负面客户历程/事件。 同时具有负事件和正事件可以提高模型的精度和准确性。

例如，如果您使用客户人工智能来预测购买产品的倾向，则客户人工智能模型需要购买路径成功示例和不成功路径示例。 这是因为在模型培训期间，客户人工智能着眼于了解哪些事件和历程促成了购买。 这还包括未购买的客户执行的操作，例如个人停止了将商品添加到购物车的历程。 这些客户可能会表现出相似的行为，但客户人工智能可以提供洞察并深入分析导致倾向分数较高的主要差异和因素。 同样，Attribution AI需要事件和历程这两种类型，才能显示接触点有效性、排名最前的转化路径和按接触点位置划分等量度。

有关历史数据要求的更多示例和信息，请访问输入/输出文档中的[客户人工智能](./customer-ai/data-requirements.md#data-requirements)或[归因人工智能](./attribution-ai/input-output.md#data-requirements)历史数据要求部分。

### 数据拼合准则

建议尽可能将用户事件拼合到一个通用ID中。 例如，您可能拥有10个事件中具有“id1”的用户数据。 稍后，同一用户删除了Cookie ID，并在接下来的20个事件中记录为“id2”。 如果您知道id1和id2对应于同一个用户，则最佳实践是将所有30个事件与同一id拼合在一起。

如果无法执行此操作，则在创建模型输入数据时，应将每组事件视为不同的用户。 这确保在模型训练和评分期间获得最佳结果。

## 工作流摘要

根据您的数据存储在Adobe Experience Platform中还是外部，准备过程会有所不同。 本节总结了您在任一情况下需要采取的必要步骤。

### 外部数据准备

如果您的数据存储在Experience Platform之外，则需要将数据映射到[消费者ExperienceEvent架构](#cee-schema)中的必填字段和相关字段。 此架构可通过自定义字段组进行增强，以更好地捕获客户数据。 映射后，您可以使用消费者ExperienceEvent架构创建数据集并[将数据摄取到Experience Platform](../ingestion/home.md)。 在配置[!DNL Intelligent Service]时，可以选择CEE数据集。

根据您希望使用的[!DNL Intelligent Service]，可能需要不同的字段。 请注意，如果数据可用，则最佳实践是向字段添加数据。 要了解有关必填字段的更多信息，请访问[归因人工智能](./attribution-ai/input-output.md)或[客户人工智能](./customer-ai/data-requirements.md)数据要求指南。

### Adobe Analytics数据准备 {#analytics-data}

客户人工智能和归因人工智能原生支持Adobe Analytics数据。 要使用Adobe Analytics数据，请按照文档中概述的步骤设置[Analytics源连接器](../sources/tutorials/ui/create/adobe-applications/analytics.md)。

一旦源连接器将您的数据流式传输到Experience Platform中，您就能够在实例配置期间选择Adobe Analytics作为数据源，然后选择一个数据集。 在连接设置过程中，将自动创建所有必需的架构字段组和单个字段。 您不需要将数据集ETL（提取、转换、加载）为CEE格式。

如果将通过Adobe Analytics源连接器流向Adobe Experience Platform的数据与Adobe Analytics数据进行比较，您可能会注意到一些差异。 Analytics Source连接器在将数据转换到Experience Data Model (XDM)架构的过程中可能会丢弃一些行。 整个行不适合转换的原因可能有多种，包括缺少时间戳、缺少人员ID、人员ID无效或过大、分析值无效等。

有关更多信息和示例，请访问[比较Adobe Analytics和Customer Journey Analytics数据](https://www.adobe.com/go/compare-aa-data-to-cja-data)的文档。 本文旨在帮助您诊断和解决这些差异，以使您和您的团队可以将Adobe Experience Platform数据用于智能服务，而不受数据完整性问题的影响。

在Adobe Experience Platform查询服务中，按channel.typeAtSource查询运行以下介于开始和结束时间戳之间的记录总数以按营销渠道查找计数。

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
>Adobe Analytics连接器最多需要四周时间来回填数据。 如果您最近设置了连接，则应验证数据集是否具有客户或归因人工智能所需的最小数据长度。 请查看[客户人工智能](./customer-ai/data-requirements.md#data-requirements)或[归因人工智能](./attribution-ai/input-output.md#data-requirements)中的历史数据部分，并验证您是否有足够的数据实现您的预测目标。

### Adobe Audience Manager数据准备（仅限客户人工智能） {#AAM-data}

客户人工智能原生支持Adobe Audience Manager数据。 要使用Audience Manager数据，请按照文档中概述的步骤设置[Audience Manager源连接器](../sources/tutorials/ui/create/adobe-applications/audience-manager.md)。

一旦源连接器将您的数据流式传输到Experience Platform中，您就能够在客户人工智能配置期间选择Adobe Audience Manager作为数据源，然后选择一个数据集。 在连接设置过程中，将自动创建所有架构字段组和单个字段。 您不需要将数据集ETL（提取、转换、加载）为CEE格式。

>[!IMPORTANT]
>
>如果您最近设置了连接器，则应验证数据集是否具有所需的最小数据长度。 请查看客户人工智能的[输入/输出文档](./customer-ai/data-requirements.md)中的历史数据部分，并验证您是否有足够的数据实现预测目标。

### [!DNL Experience Platform]数据准备

如果您的数据已存储在[!DNL Experience Platform]中，并且未通过Adobe Analytics或Adobe Audience Manager（仅限客户人工智能）源连接器流式传输，请按照以下步骤操作。 仍建议您了解CEE架构。

1. 查看[消费者ExperienceEvent架构](#cee-schema)的结构，并确定数据是否可以映射到其字段。
2. 请联系Adobe Consulting服务，帮助将数据映射到架构并将其摄取到[!DNL Intelligent Services]，或者，如果您希望自己映射数据，请[按照本指南中的步骤操作](#mapping)。

## 了解CEE模式 {#cee-schema}

消费者ExperienceEvent架构描述个人行为，因为它与数字营销事件（Web或移动设备）以及在线或离线商务活动相关。 [!DNL Intelligent Services]需要使用此架构，因为其语义上定义良好的字段（列），从而避免使用任何可能使数据变得不清晰的未知名称。

与所有XDM ExperienceEvent架构一样，CEE架构可在事件（或事件集）发生时捕获系统的基于时间系列的状态，包括时间点和所涉及主体的身份。 体验事件是所发生事件的事实记录，因此它们是不变的，表示在没有聚合或解释的情况下发生的事件。

[!DNL Intelligent Services]利用此架构中的几个关键字段从营销事件数据生成见解，所有这些可在根级别找到并展开以显示其必需的子字段。

![在Adobe Experience Platform UI中演示架构扩展，显示导航和子字段详细信息。](./images/data-preparation/schema-expansion.gif)

与所有XDM架构一样，CEE架构字段组是可扩展的。 换句话说，可以将其他字段添加到CEE字段组，并且如果需要，可以在多个架构中包含不同的变体。

可在[公共XDM存储库](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)中找到字段组的完整示例。 此外，您可以查看和复制以下[JSON文件](https://github.com/AdobeDocs/experience-platform.zh-Hans/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)，以示例说明如何构建数据以符合CEE架构。 在了解下节中概述的关键字段时，请参阅这两个示例，以确定如何将您自己的数据映射到架构。

## 关键字段

CEE字段组中有几个键字段应该被使用，以便[!DNL Intelligent Services]生成有用的见解。 此部分介绍了这些字段的用例和预期数据，并提供指向更多示例的参考文档的链接。

### 必填字段

虽然强烈建议使用所有键字段，但为了使[!DNL Intelligent Services]正常工作，有两个字段是&#x200B;**必需的**：

* [主要标识字段](#identity)
* [xdm：timestamp](#timestamp)
* [xdm：channel](#channel)（仅对于归因人工智能是必需的）

#### 主要身份标识 {#identity}

架构中的某个字段必须设置为主标识字段，这允许[!DNL Intelligent Services]将时间序列数据的每个实例链接到个人。

您必须根据数据的来源和性质确定要用作主标识的最佳字段。 标识字段必须包含&#x200B;**标识命名空间**，该命名空间指示该字段期望作为值的标识数据的类型。 一些有效的命名空间值包括：

>[!NOTE]
>
>Experience Cloud ID (ECID)也称为MCID，将继续在命名空间中使用。

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(适用于Adobe Audience Manager ID)
* &quot;aaid&quot;(适用于Adobe Analytics ID)

如果不确定应使用哪个字段作为主要身份，请联系Adobe Consulting服务以确定最佳解决方案。 如果未设置主标识，Intelligent Service应用程序将使用以下默认行为：

| 默认 | 归因人工智能 | 客户人工智能 |
| --- | --- | --- |
| 标识列 | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| 命名空间 | AAID | ECID |

要设置主标识，请从&#x200B;**[!UICONTROL 架构]**&#x200B;选项卡导航到您的架构，然后选择架构名称超链接以打开&#x200B;**[!DNL Schema Editor]**。

![导航到Adobe Experience Platform UI中的架构。](./images/data-preparation/navigate_schema.png)

接下来，导航到要作为主标识的字段并选择它。 将打开&#x200B;**[!UICONTROL 字段属性]**&#x200B;菜单。

![在Adobe Experience Platform UI中选择所需字段的过程。](./images/data-preparation/find_field.png)

在&#x200B;**[!UICONTROL 字段属性]**&#x200B;菜单中，向下滚动直到找到&#x200B;**[!UICONTROL 标识]**&#x200B;复选框。 选中该框后，将显示将所选身份设置为&#x200B;**[!UICONTROL 主身份]**&#x200B;的选项。 也选中此框。

![用于在Adobe Experience Platform UI中设置主要标识的复选框。](./images/data-preparation/set_primary_identity.png)

接下来，必须从下拉列表中的预定义命名空间列表中提供&#x200B;**[!UICONTROL 身份命名空间]**。 在此示例中，由于正在使用Adobe Audience Manager ID `mcid.id`，因此选择了ECID命名空间。 选择&#x200B;**[!UICONTROL 应用]**&#x200B;以确认更新，然后选择右上角的&#x200B;**[!UICONTROL 保存]**&#x200B;以将更改保存到架构。

![下拉菜单，其中显示Adobe Experience Platform UI中选定的ECID命名空间。](./images/data-preparation/select_namespace.png)

#### xdm：timestamp {#timestamp}

此字段表示事件发生时的日期时间。 必须按照ISO 8601标准以字符串形式提供此值。

#### xdm：channel {#channel}

>[!NOTE]
>
>仅当使用归因人工智能时，此字段才是必填字段。

此字段表示与ExperienceEvent相关的营销渠道。 字段包括有关渠道类型、媒体类型和位置类型的信息。

![显示xdm：channel字段结构的图表，包括子字段，如type、mediaType和mediaAction。](./images/data-preparation/channel.png)

**示例架构**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

有关`xdm:channel`的每个必需子字段的完整信息，请参阅[体验渠道架构](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md)规范。 有关某些映射示例，请参阅下面的[表](#example-channels)。

#### 示例渠道映射 {#example-channels}

下表提供了映射到`xdm:channel`架构的营销渠道的一些示例：

| 渠道 | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 付费搜索 | https:/<span>/ns.adobe.com/xdm/channel-types/search | 已付 | 点击次数 |
| 社交 — 营销 | https:/<span>/ns.adobe.com/xdm/channel-types/social | 已获取 | 点击次数 |
| 显示 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 已付 | 点击次数 |
| 电子邮件 | https:/<span>/ns.adobe.com/xdm/channel-types/email | 已付 | 点击次数 |
| 内部反向链接 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 拥有 | 点击次数 |
| 显示显示显示到达 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 已付 | 展示次数 |
| 二维码重定向 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 拥有 | 点击次数 |
| 移动设备 | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | 拥有 | 点击次数 |

### 推荐的字段

本节概述了其余关键字段。 虽然[!DNL Intelligent Services]不一定需要这些字段才能正常工作，但强烈建议您尽可能多地使用这些字段以获得更丰富的见解。

#### xdm：productListItems

此字段由一系列项目组成，表示客户选择的产品，包括产品SKU、名称、价格和数量。

![xdm：productListItems字段，包括SKU、name、currencyCode、quantity和priceTotal等子字段。](./images/data-preparation/productListItems.png)

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

有关`xdm:productListItems`的每个必需子字段的完整信息，请参阅[商业详细信息架构](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md)规范。

#### xdm：commerce

此字段包含有关ExperienceEvent的特定于商业的信息，包括采购订单号和付款信息。

![&#x200B; xdm：commerce字段的结构，包括子字段，如订单、购买和付款。](./images/data-preparation/commerce.png)

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

有关`xdm:commerce`的每个必需子字段的完整信息，请参阅[商业详细信息架构](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md)规范。

#### xdm：web

此字段表示与ExperienceEvent相关的Web详细信息，例如交互、页面详细信息和反向链接。

![xdm：web字段，包括webPageDetails和webReferrer等子字段。](./images/data-preparation/web.png)

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

有关`xdm:productListItems`的每个必需子字段的完整信息，请参阅[ExperienceEvent Web详细信息架构](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md)规范。

#### xdm：marketing

此字段包含与通过接触点激活的营销活动相关的信息。

![xdm：marketing字段的结构，包括子字段，如trackingCode、campaignGroup和campaignName。](./images/data-preparation/marketing.png)

**示例架构**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

有关`xdm:productListItems`的每个必需子字段的完整信息，请参阅[营销密码](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md)规范。

## 映射和摄取数据 {#mapping}

确定营销事件数据是否可以映射到CEE架构后，下一步是确定要将哪些数据引入[!DNL Intelligent Services]。 [!DNL Intelligent Services]中使用的所有历史数据必须在四个月数据的最小时间窗口内，外加用作回顾期间的天数。

在确定要发送的数据范围后，请联系Adobe Consulting服务，帮助将您的数据映射到架构并将其摄取到服务中。

如果您有[!DNL Adobe Experience Platform]订阅，并且希望自己映射和摄取数据，请按照以下部分中列出的步骤操作。

### 使用Adobe Experience Platform

>[!NOTE]
>
>以下步骤需要订阅Experience Platform。 如果您无权访问Experience Platform，请跳至[后续步骤](#next-steps)部分。

本节概述了将数据映射和摄取到Experience Platform以在[!DNL Intelligent Services]中使用的工作流，包括指向详细步骤的教程的链接。

#### 创建CEE架构和数据集

当您准备好开始准备数据以进行摄取时，第一步是创建一个采用CEE字段组的新XDM架构。 以下教程介绍了在UI或API中创建新架构的过程：

* [在UI中创建架构](../xdm/tutorials/create-schema-ui.md)
* [在API中创建架构](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>上述教程遵循创建架构的通用工作流。 为架构选择类时，必须使用&#x200B;**XDM ExperienceEvent类**。 选择此类后，您可以将CEE字段组添加到架构中。

将CEE字段组添加到架构后，您可以根据需要在数据中添加其他字段组。

创建并保存架构后，您可以根据该架构创建新数据集。 以下教程介绍了在UI或API中创建新数据集的过程：

* [在UI中创建数据集](../catalog/datasets/user-guide.md#create) （按照工作流使用现有架构）
* [在API中创建数据集](../catalog/datasets/create.md)

创建数据集后，您可以在&#x200B;**[!UICONTROL 数据集]**&#x200B;工作区的Experience Platform UI中找到该数据集。

![](images/data-preparation/dataset-location.png)

#### 将身份字段添加到数据集

如果您从[!DNL Adobe Audience Manager]、[!DNL Adobe Analytics]或其他外部源引入数据，则可以选择将架构字段设置为标识字段。 要将架构字段设置为标识字段，请查看[UI教程](../xdm/tutorials/create-schema-ui.md#identity-field)或[API教程](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor)中有关设置标识字段的部分以创建架构。

如果您从本地CSV文件摄取数据，则可以跳到有关[映射和摄取数据](#ingest)的下一节。

#### 映射和摄取数据 {#ingest}

创建CEE架构和数据集后，您可以开始将数据表映射到架构，并将这些数据摄取到Experience Platform中。 请参阅有关[将CSV文件映射到XDM架构](../ingestion/tutorials/map-csv/overview.md)的教程，以了解如何在UI中执行此操作的步骤。 您可以使用以下[示例JSON文件](https://github.com/AdobeDocs/experience-platform.zh-Hans/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)测试摄取过程，然后再使用您自己的数据。

填充某个数据集后，可使用相同的数据集来摄取其他数据文件。

如果您的数据存储在受支持的第三方应用程序中，您还可以选择创建[源连接器](../sources/home.md)，将营销事件数据实时摄取到[!DNL Experience Platform]。

## 后续步骤 {#next-steps}

本文档提供了有关准备数据以在[!DNL Intelligent Services]中使用的一般指导。 如果您需要根据用例进行其他咨询，请联系Adobe Consulting支持。

成功使用客户体验数据填充数据集后，您可以使用[!DNL Intelligent Services]生成见解。 请参阅以下文档以开始使用：

* [归因人工智能概述](./attribution-ai/overview.md)
* [客户人工智能概述](./customer-ai/overview.md)
