---
keywords: Experience Platform；主页；智能服务；热门话题；智能服务；智能服务
solution: Experience Platform, Intelligent Services
title: 准备要在智能服务中使用的数据
topic: Intelligent Services
description: 为了使智能服务能够从您的营销事件数据中发掘洞察，数据必须在语义上以标准结构进行丰富和维护。 智能服务使用体验数据模型(XDM)模式来实现这一点。
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
translation-type: tm+mt
source-git-commit: 867c97d58f3496cb9e9e437712f81bd8929ba99f
workflow-type: tm+mt
source-wordcount: '2387'
ht-degree: 0%

---

# 准备要在[!DNL Intelligent Services]中使用的数据

要[!DNL Intelligent Services]从营销事件数据中发掘洞察，数据必须从语义上进行丰富并以标准结构进行维护。 [!DNL Intelligent Services] 利 [!DNL Experience Data Model] 用(XDM)模式实现这一目标。具体而言，[!DNL Intelligent Services]中使用的所有数据集必须符合Consumer ExperienceEvent(CEE)XDM模式或使用Adobe Analytics连接器。 此外，客户AI支持Adobe Audience Manager连接器。

本文档提供有关将您的营销事件数据从多个渠道映射到CEE模式的一般指导，概述模式中重要字段的信息，以帮助您确定如何将数据有效映射到其结构。 如果您计划使用Adobe Analytics数据，请视图[Adobe Analytics数据准备](#analytics-data)部分。 如果您计划使用Adobe Audience Manager数据（仅限客户AI），请视图[Adobe受众管理器数据准备](#AAM-data)的部分。

## 工作流摘要

准备过程因数据是存储在Adobe Experience Platform还是外部而异。 本节总结了在两种情况下需要采取的必要步骤。

### 外部数据准备

如果数据存储在[!DNL Experience Platform]之外，请按照以下步骤操作：

1. 请与Adobe咨询服务联系，请求专用Azure Blob存储容器的访问凭据。
1. 使用访问凭据，将数据上传到Blob容器。
1. 使用Adobe咨询服务，将您的数据映射到[ Consumer ExperienceEvent模式](#cee-schema)并引入[!DNL Intelligent Services]。

### Adobe Analytics数据准备{#analytics-data}

客户人工智能和Attribution AI本身支持Adobe Analytics数据。 要使用Adobe Analytics数据，请按照文档中概述的步骤设置[Analytics源连接器](../sources/tutorials/ui/create/adobe-applications/analytics.md)。

在源连接器将数据流化到Experience Platform中后，您可以在实例配置期间选择Adobe Analytics作为数据源，然后选择数据集。 所有必需的模式字段和混音在连接设置期间自动创建。 您无需将数据集ETL（提取、转换、加载）转换为CEE格式。

>[!IMPORTANT]
>
>Adobe Analytics连接器回填数据最长需要4周。 如果您最近设置了连接，则应验证数据集是否具有客户或Attribution AI所需的最小数据长度。 请查看[客户AI](./customer-ai/input-output.md#data-requirements)或[Attribution AI](./attribution-ai/input-output.md#data-requirements)中的历史数据部分，并验证您是否有足够的数据用于预测目标。

### Adobe Audience Manager数据准备（仅限客户人工智能）{#AAM-data}

客户人工智能本身支持Adobe Audience Manager数据。 要使用Audience Manager数据，请按照文档中概述的步骤设置[Audience Manager源连接器](../sources/tutorials/ui/create/adobe-applications/audience-manager.md)。

在源连接器将您的数据流化到Experience Platform中后，您可以在客户AI配置期间选择Adobe Audience Manager作为数据源，然后选择数据集。 所有必需的模式字段和混音在连接设置期间自动创建。 您无需将数据集ETL（提取、转换、加载）转换为CEE格式。

>[!IMPORTANT]
>
>如果您最近设置了连接器，则应验证数据集是否具有所需的最小数据长度。 请查看客户AI的[输入/输出文档](./customer-ai/input-output.md)中的历史数据部分，并验证您有足够的数据用于预测目标。

### [!DNL Experience Platform] 数据准备

如果您的数据已存储在[!DNL Platform]中，且未通过Adobe Analytics或Adobe Audience Manager（仅限客户AI）源连接器进行流式传输，请遵循以下步骤。 如果您计划与客户人工智能合作，仍建议您了解CEE模式。

1. 查看[Consumer ExperienceEvent模式](#cee-schema)的结构，并确定是否可以将数据映射到其字段。
2. 请与Adobe咨询服务联系，帮助将数据映射到模式并将其收录到[!DNL Intelligent Services]中，或者，如果您想自己映射数据，请按照本指南](#mapping)中的步骤操作。[

## 了解CEE模式{#cee-schema}

“消费者体验事件”模式描述个人的行为，因为该行为与数字营销事件（Web或移动）以及在线或离线商务活动相关。 [!DNL Intelligent Services]需要使用此模式，因为其语义上定义良好的字段（列），避免了任何未知名称，否则会使数据变得不那么清晰。

与所有XDM ExperienceEvent模式一样，CEE模式在事件(或一组事件)发生时捕获系统基于时间序列的状态，包括时间点和相关主题的身份。 体验事件是已发生事实的记录，因此它们是不可改变的，代表未经汇总或解释而发生的事情。

[!DNL Intelligent Services] 利用此模式中的几个关键字段，从您的营销事件数据中生成洞察，所有这些数据都可以在根级别找到并展开，以显示其必需的子字段。

![](./images/data-preparation/schema-expansion.gif)

与所有XDM模式一样，CEE混音是可扩展的。 换句话说，CEE混音中可以添加其他字段，如有必要，可以在多个模式中包含不同的变量。

在[公共XDM存储库](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)中可以找到混合的完整示例。 此外，您还可以视图并复制以下[JSON文件](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)，以了解如何构建数据以符合CEE模式。 在了解以下部分中概述的关键字段时，请参阅这两个示例，以确定如何将您自己的数据映射到模式。

## 键字段

CEE混音中有几个关键字段应加以利用，以便[!DNL Intelligent Services]生成有用的洞察。 本节介绍这些字段的用例和预期数据，并提供指向参考文档的链接以获取更多示例。

### 必填字段

强烈建议使用所有键字段，但有两个字段是&#x200B;**required** ，以便[!DNL Intelligent Services]正常工作：

* [主标识字段](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:渠道](#channel) (仅对Attribution AI强制)

#### 主标识{#identity}

您模式中的其中一个字段必须设置为主标识字段，这允许[!DNL Intelligent Services]将时间序列数据的每个实例链接到个人。

您必须根据数据的来源和性质确定用作主要标识的最佳字段。 标识字段必须包含&#x200B;**标识命名空间**，该标识指示字段期望作为值的标识数据的类型。 某些有效的命名空间值包括：

* &quot;电子邮件&quot;
* &quot;phone&quot;
* “mcid”(对于Adobe Audience Manager ID)
* “aid”(对于Adobe Analytics ID)

如果您不确定应将哪个字段用作主要标识，请与Adobe咨询服务部门联系以确定最佳解决方案。 如果未设置主标识，则Intelligent Service应用程序将使用以下默认行为：

| 默认 | Attribution AI | 客户人工智能 |
| --- | --- | --- |
| 标识列 | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| 命名空间 | AAID | ECID |

要设置主标识，请从&#x200B;**[!UICONTROL Schemas]**&#x200B;选项卡导航到您的模式，然后选择模式名称超链接以打开&#x200B;**[!DNL Schema Editor]**。

![导航到模式](./images/data-preparation/navigate_schema.png)

接下来，导航到您希望作为主标识的字段并选择它。 将打开该字段的&#x200B;**[!UICONTROL Field properties]**&#x200B;菜单。

![选择字段](./images/data-preparation/find_field.png)

在&#x200B;**[!UICONTROL Field properties]**&#x200B;菜单中，向下滚动直到找到&#x200B;**[!UICONTROL Identity]**&#x200B;复选框。 选中该框后，将显示将选定标识设置为&#x200B;**[!UICONTROL Primary identity]**&#x200B;的选项。 也选择此框。

![选中复选框](./images/data-preparation/set_primary_identity.png)

接下来，您必须从下拉菜单中预定义命名空间的列表中提供&#x200B;**[!UICONTROL Identity namespace]**。 在此示例中，选择ECID命名空间，因为正在使用Adobe Audience Manager ID `mcid.id`。 选择&#x200B;**[!UICONTROL Apply]**&#x200B;以确认更新，然后选择右上角的&#x200B;**[!UICONTROL Save]**&#x200B;以将更改保存到模式。

![保存更改](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

此字段表示事件发生的日期时间。 必须按照ISO 8601标准将此值作为字符串提供。

#### xdm:渠道 {#channel}

>[!NOTE]
>
>此字段仅在使用Attribution AI时是必填字段。

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

有关`xdm:channel`的每个必需子字段的完整信息，请参阅[体验渠道模式](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md)规范。 有关某些示例映射，请参阅](#example-channels)下的[表。

#### 渠道映射示例{#example-channels}

下表提供了映射到`xdm:channel`渠道的营销模式的一些示例：

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 付费搜索 | https:/<span>/ns.adobe.com/xdm/渠道-types/search | 付 | 单击 |
| 社交 — 营销 | https:/<span>/ns.adobe/xdm/渠道-types/social | 挣 | 单击 |
| 显示 | https:/<span>/ns.adobe.com/xdm/渠道-types/display | 付 | 单击 |
| 电子邮件 | https:/<span>/ns.adobe.com/xdm/渠道-types/email | 付 | 单击 |
| 内部推荐人 | https:/<span>/ns.adobe.com/xdm/渠道-types/direct | 拥有 | 单击 |
| 显示浏览 | https:/<span>/ns.adobe.com/xdm/渠道-types/display | 付 | 印象 |
| QR码重定向 | https:/<span>/ns.adobe.com/xdm/渠道-types/direct | 拥有 | 单击 |
| 移动设备 | https:/<span>/ns.adobe.com/xdm/渠道-types/mobile | 拥有 | 单击 |

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

#### xdm:commerce

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

有关`xdm:productListItems`的每个必需子字段的完整信息，请参阅[营销部门](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md)规范。

## 映射和摄取数据{#mapping}

确定营销事件数据是否可映射到CEE模式后，下一步是确定要导入[!DNL Intelligent Services]的数据。 [!DNL Intelligent Services]中使用的所有历史数据必须位于四个月数据的最小时间窗口内，加上预期作为回顾期的天数。

在确定要发送的数据范围后，请与Adobe咨询服务联系，帮助将数据映射到模式并将其引入服务。

如果您有[!DNL Adobe Experience Platform]订阅，并且想自己映射和收录数据，请遵循以下部分中概述的步骤。

### 使用Adobe Experience Platform

>[!NOTE]
>
>以下步骤需要订阅Experience Platform。 如果您无权访问平台，请跳到[后续步骤](#next-steps)部分。

本节概述了将数据映射和引入Experience Platform以在[!DNL Intelligent Services]中使用的工作流，包括指向教程的链接，以了解详细步骤。

#### 创建CEE模式和数据集

当您准备好开始准备数据以用于摄取时，第一步是创建一个使用CEE混音的新XDM模式。 以下教程将演练在UI或API中创建新模式的过程：

* [在UI中创建模式](../xdm/tutorials/create-schema-ui.md)
* [在API中创建模式](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>以上教程遵循创建模式的通用工作流程。 为模式选择类时，必须使用&#x200B;**XDM ExperienceEvent类**。 选择此类后，您即可将CEE混音添加到模式。

在将CEE混音添加到模式后，您可以根据数据中其他字段的需要添加其他混音。

创建并保存模式后，即可基于该模式创建新数据集。 以下教程将指导您在UI或API中创建新数据集的过程：

* [在UI中创建数据集](../catalog/datasets/user-guide.md#create) (按照工作流使用现有模式)
* [在API中创建数据集](../catalog/datasets/create.md)

创建数据集后，您可以在&#x200B;**[!UICONTROL Datasets]**&#x200B;工作区的平台UI中找到它。

![](images/data-preparation/dataset-location.png)

#### 向数据集添加标识字段

如果要从[!DNL Adobe Audience Manager]、[!DNL Adobe Analytics]或其他外部源导入模式，则可以选择将数据字段设置为标识字段。 要将模式字段设置为标识字段，请视图有关在用于创建模式的[UI教程](../xdm/tutorials/create-schema-ui.md#identity-field)或[API教程](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor)中设置标识字段的部分。

如果从本地CSV文件中收录数据，则可以跳到[映射上的下一节，并收录数据](#ingest)。

#### 映射和摄取数据{#ingest}

创建CEE模式和数据集后，您可以开始将数据表映射到模式，并将数据收录到平台。 有关如何在UI中执行此操作的步骤，请参阅有关[将CSV文件映射到XDM模式](../ingestion/tutorials/map-a-csv-file.md)的教程。 在使用您自己的数据之前，可以使用以下[示例JSON文件](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)测试摄取过程。

填充数据集后，同一数据集即可用于收录其他数据文件。

如果您的事件存储在受支持的第三方应用程序中，您还可以选择创建[源连接器](../sources/home.md)以将您的营销数据实时收录到[!DNL Platform]中。

## 后续步骤 {#next-steps}

本文档提供了有关准备要在[!DNL Intelligent Services]中使用的数据的一般指导。 如果您需要根据您的用例进行其他咨询，请联系Adobe咨询支持。

成功使用客户体验数据填充数据集后，即可使用[!DNL Intelligent Services]生成洞察。 请参阅以下文档以开始：

* [Attribution AI 概述](./attribution-ai/overview.md)
* [Customer AI 概述](./customer-ai/overview.md)
