---
keywords: Experience Platform；快速入门；客户人工智能；热门主题；客户人工智能输入；客户人工智能输出
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 客户人工智能中的输入与输出
topic-legacy: Getting started
description: 进一步了解Customer AI使用的必需事件、输入和输出。
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 0f408f217dd168b9c94b8dbbd7dc3c6edb06488c
workflow-type: tm+mt
source-wordcount: '3096'
ht-degree: 1%

---

# Customer AI中的输入和输出

以下文档概述了客户人工智能中使用的不同必需事件、输入和输出。

## 快速入门

Customer AI通过分析以下数据集之一来预测客户流失率或转化倾向得分：

- Adobe Analytics数据(使用 [Analytics源连接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager数据(使用 [Audience Manager源连接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- 体验事件(EE)数据集
- 消费者体验事件(CEE)数据集

如果每个数据集共享相同的身份类型（命名空间）（如ECID），则可以从不同的源添加多个数据集。 有关添加多个数据集的更多信息，请访问 [Customer AI用户指南](./user-guide/configure.md#select-data)

>[!IMPORTANT]
>
>源连接器最多需要四周时间才能回填数据。 如果您最近设置了一个连接器，则应验证数据集是否具有Customer AI所需的最小数据长度。 请查看 [历史数据](#data-requirements) 部分，以验证是否有足够的数据来实现预测目标。

本文档要求对CEE架构有基本的了解。 请查看 [智能服务数据准备](../data-preparation.md) 文档，然后再继续。

下表概述了本文档中使用的一些常用术语：

| 搜索词 | 定义 |
| --- | --- |
| [体验数据模型(XDM)](../../xdm/home.md) | XDM是基础框架，它允许由Adobe Experience Platform提供支持的Adobe Experience Cloud在适当的时间，通过适当的渠道向适当的人员提供适当的信息。 构建Experience Platform的方法 — XDM系统，可操作Experience Data Model模式以供Platform服务使用。 |
| XDM 架构 | Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。在将数据摄取到平台中之前，必须构建一个架构来描述数据的结构，并对每个字段中可包含的数据类型提供约束。 架构由基本XDM类和零个或多个架构字段组组成。 |
| XDM类 | 所有XDM架构都描述了可以分类为记录或时间序列的数据。 架构的数据行为由架构的类定义，该类在首次创建架构时分配给架构。 XDM类描述架构必须包含的最小属性数，以表示特定数据行为。 |
| [字段组](../../xdm/schema/composition.md) | 在架构中定义一个或多个字段的组件。 字段组强制执行其字段在架构层次结构中的显示方式，因此在每个架构中显示的结构都与其中包含的结构相同。 字段组仅与特定类兼容，这些类由其标识 `meta:intendedToExtend` 属性。 |
| [数据类型](../../xdm/schema/composition.md) | 还可以为架构提供一个或多个字段的组件。 但是，与字段组不同，数据类型不受特定类的限制。 这使数据类型成为一种更灵活的选项，用于描述在具有潜在不同类的多个架构中可重复使用的常用数据结构。 CEE架构和Adobe Analytics架构均支持本文档中概述的数据类型。 |
| 流失率 | 取消或选择不续订其订阅的帐户百分比的度量。 较高的流失率可能会对每月经常性收入(MRR)产生负面影响，也可能表示对产品或服务的不满。 |
| [实时客户资料](../../profile/home.md) | Real-time Customer Profile提供了集中式消费者用户档案，以进行有针对性的个性化体验管理。 每个用户档案都包含在所有系统中汇总的数据，以及涉及您与Experience Platform一起使用的任何系统中发生的个人事件的带有时间戳的可操作帐户。 |

## 客户人工智能输入数据

>[!TIP]
>
> Customer AI会自动确定哪些事件对预测有用，如果可用数据不足以生成质量预测，则会发出警告。

Customer AI支持Adobe Analytics、Adobe Audience Manager、Experience Event(EE)和Cunsomer Experience Event(CEE)数据集。 CEE架构要求您在架构创建过程中添加字段组。 如果您使用Adobe Analytics或Adobe Audience Manager数据集，则源连接器会直接映射连接过程中列出的标准事件（商务、网页详细信息、应用程序和搜索）。 如果每个数据集共享相同的身份类型（命名空间）（如ECID），则可以从不同的源添加多个数据集。

有关映射Adobe Analytics数据或Audience Manager数据的更多信息，请访问 [Analytics字段映射](../../sources/connectors/adobe-applications/analytics.md) 或 [Audience Manager字段映射](../../sources/connectors/adobe-applications/mapping/audience-manager.md) 的双曲余切值。

### Customer AI使用的标准事件 {#standard-events}

XDM体验事件用于确定各种客户行为。 根据数据的结构方式，下面列出的事件类型可能并不包含客户的所有行为。 由您决定哪些字段具有明确、明确地识别Web用户活动所需的必要数据。 根据您的预测目标，所需的必填字段可能会发生更改。

Customer AI依靠不同的事件类型来构建模型功能。 这些事件类型会使用多个XDM字段组自动添加到您的架构中。

>[!NOTE]
>
>如果您使用的是Adobe Analytics或Adobe Audience Manager数据，则会自动创建架构，并包含捕获数据所需的标准事件。 如果您要创建自己的自定义CEE架构来捕获数据，则需要考虑捕获数据所需的字段组。

无需包含下面列出的每个标准事件的数据，但某些情况需要某些事件。 如果您有任何可用的标准事件数据，建议您将其包含在架构中。 例如，如果您想要创建用于预测购买事件的Customer AI应用程序，则从 `Commerce` 和 `Web page details` 数据类型。

要在平台UI中查看字段组，请选择 **[!UICONTROL 模式]** 选项卡，然后选择 **[!UICONTROL 字段组]** 选项卡。

| 字段组 | 事件类型 | XDM字段路径 |
| --- | --- | --- |
| [!UICONTROL 商务详细信息] | 订购 | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | 结账 | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | 购买 | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemuves | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Web详细信息] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL 应用程序详细信息] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashss | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL 搜索详细信息] | 搜索 | search.keywords |

此外， Customer AI可以使用订阅数据构建更好的流失模型。 每个使用 [[!UICONTROL 订阅]](../../xdm/data-types/subscription.md) 数据类型格式。 大多数字段是可选的，但是，为了获得最佳的流失模型，强烈建议您为尽可能多的字段提供数据，例如 `startDate`, `endDate`，以及任何其他相关详细信息。

### 添加自定义事件和配置文件属性

如果您除了 [标准事件字段](#standard-events) Customer AI使用的自定义事件和自定义配置文件属性选项在 [实例配置](./user-guide/configure.md#custom-events).

如果您选择的数据集包含架构中定义的自定义事件或配置文件属性（如“酒店预订”或“X公司员工”），则可以将其添加到实例中。 Customer AI使用这些其他自定义事件和配置文件属性来改进模型质量并提供更准确的结果。

### 历史数据 {#data-requirements}

Customer AI要求提供模型培训的历史数据，但所需数据量基于两个关键元素：结果窗口和合格人口。

默认情况下，如果在应用程序配置期间未提供符合条件的群体定义，则Customer AI会查找用户在过去120天内具有活动的情况。 此外，客户人工智能要求根据预测的目标定义至少500个符合条件的事件和500个不符合条件的事件（共1000个）历史数据。

以下示例使用一个简单的公式来帮助您确定所需的最小数据量。 如果超出了最低要求，则模型可能会提供更准确的结果。 如果您的数量小于所需的最小数量，则模型将失败，因为没有足够的数据量进行模型培训。

**公式**:

所需数据的最小长度=符合条件的群体+结果窗口

>[!NOTE]
>
> 30是合格人口所需的最低天数。 如果未提供，则默认值为120天。

示例：

- 您希望预测客户是否可能在未来30天内购买手表。 您还希望对过去60天内有某些Web活动的用户进行评分。 在这种情况下，所需数据的最小长度为60天+30天。 合格人口为60天，结果期为30天，总共90天。

- 您想要预测用户是否可能在接下来7天内购买手表。 在这种情况下，所需数据的最小长度为120天+ 7天。 合格人口默认为120天，结果窗口为7天，总共为127天。

- 您希望预测客户是否可能在未来7天内购买手表。 您还希望对过去7天内有某些Web活动的用户进行评分。 在这种情况下，所需数据的最小长度为30天+ 7天。 合格人口至少需要30天，结果窗口为7天，总共37天。

除了所需的最低数据之外， Customer AI还可以最好地处理最新数据。 在此用例中， Customer AI正在根据用户最近的行为数据对未来进行预测。 换句话说，更新的数据可能会产生更准确的预测。

### 示例方案

在此部分中，描述了Customer AI实例的不同情景以及必需和推荐的事件类型。 请参阅 [标准事件表](#standard-events) 以了解有关字段组及其字段路径的详细信息。

>[!NOTE]
>
> 必需事件类型用于清晰、明确地识别Web用户活动。 所需事件类型的数量将根据您的架构的预测目标和结构而发生更改。 如果您不确定是否需要特定事件类型，建议在构建CEE架构时包含该事件类型。 如果您使用的是Adobe Analytics或Adobe Audience Manager数据，则必需的标准事件应根据您正在流式传输的数据而可用。

### 场景1:电子商务零售网站上的购买转化

**预测目标：** 预测符合条件的用户档案在网站上购买特定服装文章的转化倾向。

**必需的标准事件类型：**

要获得具有此特定预测目标的最佳Customer AI输出，需要使用以下列出的事件类型。 根据您的预测目标可以排除所需事件，但是，排除多个事件可能会导致结果不佳。

- 订购
- 结账
- 购买
- webVisit
- 搜索

**其他推荐的标准事件类型：**

其余任何 [事件类型](#standard-events) 配置Customer AI实例时，可能需要满足以下条件：目标和符合条件群体的复杂性。 如果数据可用于特定数据类型，则建议将此数据包含在您的架构中。

### 场景2:媒体流服务网站上的订阅转换

**预测目标：** 预测符合条件的用户档案提交特定级别的订阅转化倾向，如标准或高级计划。

**必需的标准事件类型：**

要获得具有此特定预测目标的最佳Customer AI输出，需要使用以下列出的事件类型。 根据您的预测目标可以排除所需事件，但是，排除多个事件可能会导致结果不佳。

- 订购
- 结账
- 购买
- webVisit
- 搜索

在本例中， `order`, `checkouts`和 `purchases` 用于指示已购买订阅及其类型。

此外，为了获得准确的模型，建议您使用 [订阅数据类型](../../xdm/data-types/subscription.md).

**其他推荐的标准事件类型：**

其余任何 [事件类型](#standard-events) 配置Customer AI实例时，可能需要满足以下条件：目标和符合条件群体的复杂性。 如果数据可用于特定数据类型，则建议将此数据包含在您的架构中。

### 情景3:电子商务零售网站的流失率

**预测目标：** 预测不发生购买事件的可能性。

**必需的标准事件类型：**

要获得具有此特定预测目标的最佳Customer AI输出，需要使用以下列出的事件类型。 根据您的预测目标可以排除所需事件，但是，排除多个事件可能会导致结果不佳。

- 订购
- 结账
- 购买
- webVisit
- 搜索

**其他推荐的标准事件类型：**

其余任何 [事件类型](#standard-events) 配置Customer AI实例时，可能需要满足以下条件：目标和符合条件群体的复杂性。 如果数据可用于特定数据类型，则建议将此数据包含在您的架构中。

### 场景4:电子商务零售网站上的追加销售转化

**预测目标：** 预测已购买特定产品的群体购买新相关产品的倾向。

**必需的标准事件类型：**

要获得具有此特定预测目标的最佳Customer AI输出，需要使用以下列出的事件类型。 根据您的预测目标可以排除所需事件，但是，排除多个事件可能会导致结果不佳。

- 订购
- 结账
- 购买
- webVisit
- 搜索

**其他推荐的标准事件类型：**

其余任何 [事件类型](#standard-events) 配置Customer AI实例时，可能需要满足以下条件：目标和符合条件群体的复杂性。 如果数据可用于特定数据类型，则建议将此数据包含在您的架构中。

### 场景5:在线新闻发布网站取消订阅（流失率）

**预测目标：** 预测符合条件的群体下月退订服务的倾向。

**必需的标准事件类型：**

要获得具有此特定预测目标的最佳Customer AI输出，需要使用以下列出的事件类型。 根据您的预测目标可以排除所需事件，但是，排除多个事件可能会导致结果不佳。

- webVisit
- 搜索

此外，为了获得准确的模型，建议您使用 [订阅数据类型](../../xdm/data-types/subscription.md).

**其他推荐的标准事件类型：**

其余任何 [事件类型](#standard-events) 配置Customer AI实例时，可能需要满足以下条件：目标和符合条件群体的复杂性。 如果数据可用于特定数据类型，则建议将此数据包含在您的架构中。

### 场景6:启动移动应用程序

**预测目标：** 预测符合条件的用户档案在未来X天内启动付费移动应用程序的倾向。 这类似于预测“每月活动用户”的关键绩效指标(KPI)。

**必需的标准事件类型：**

要获得具有此特定预测目标的最佳Customer AI输出，需要使用以下列出的事件类型。 根据您的预测目标可以排除所需事件，但是，排除多个事件可能会导致结果不佳。

- 订购
- 结账
- 购买
- webVisit
- applicationCloses
- applicationCrashss
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

在本例中， `order`, `checkouts`和 `purchases` 在需要购买移动应用程序时使用。

**其他推荐的标准事件类型：**

其余任何 [事件类型](#standard-events) 配置Customer AI实例时，可能需要满足以下条件：目标和符合条件群体的复杂性。 如果数据可用于特定数据类型，则建议将此数据包含在您的架构中。

### 情景7:已实现的特征(Adobe Audience Manager)

**预测目标：** 预测某些特征的实现倾向。

**必需的标准事件类型：**

要使用Adobe Audience Manager中的特征，您需要使用 [Audience Manager源连接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). 源连接器会自动使用正确的字段组创建架构。 您无需手动添加其他事件类型，架构便可与Customer AI配合使用。

配置新客户AI实例时， `audienceName` 和 `audienceID` 可用于在定义目标时为评分选择特定特征。

## 客户AI输出数据

Customer AI会为被认为符合条件的个人用户档案生成多个属性。 根据您配置的内容，可使用两种方式来使用得分（输出）。 如果您有一个启用了“实时客户资料”的数据集，则可以在 [区段生成器](../../segmentation/ui/segment-builder.md). 如果您没有启用了配置文件的数据集，则可以 [下载Customer AI输出](./user-guide/download-scores.md) 数据湖上可用的数据集。

您可以在 **数据集** 中。 所有Customer AI输出数据集均以名称开头 **Customer AI得分 — Name_of_app** 而所有Customer AI输出架构均以名称开头 **Customer AI架构 — Name_of_app**.

![cai-schema-name-of-app](./images/user-guide/cai-schema-name-of-app.png)

>[!NOTE]
>
> 输出值由实时客户配置文件使用，该配置文件可用于创建和定义区段。

下表描述了Customer AI输出中的各种属性：

| 属性 | 描述 |
| ----- | ----------- |
| 得分 | 客户在定义的时间范围内实现预测目标的相对可能性。 此值不应视为概率百分比，而应视为个人与整体群体的比较可能性。 此分数的范围为0到100。 |
| 概率 | 此属性是配置文件在定义的时间范围内实现预测目标的真实概率。 在比较不同目标的输出时，建议您考虑概率大于百分位数或分数。 在确定符合条件的群体的平均概率时，应始终使用概率，因为对于不经常发生的事件，概率往往位于较低的一方。 概率范围在0到1之间的值。 |
| 百分位数 | 此值提供有关用户档案相对于其他类似评分用户档案的性能的信息。 例如，对于流失率，百分位等级为99的用户档案表示，与之相比，其他所有得分用户档案的99%存在更高的流量风险。 百分位数介于1到100之间。 |
| 倾向类型 | 所选的倾向类型。 |
| 得分日期 | 打分的日期。 |
| 影响因素 | 预测了用户档案可能转化或流失的原因。 因素包括以下属性：<ul><li>代码：积极影响用户档案预测分数的用户档案或行为属性。 </li><li>值：配置文件或行为属性的值。</li><li>重要性：指示用户档案或行为属性对预测得分（低、中、高）的权重</li></ul> |

## 后续步骤 {#next-steps}

准备数据并部署所有凭据和模式后，请首先按照 [配置Customer AI实例](./user-guide/configure.md) 的双曲余切值。 本指南将指导您为Customer AI创建一个实例。
