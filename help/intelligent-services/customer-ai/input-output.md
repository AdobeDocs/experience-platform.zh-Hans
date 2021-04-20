---
keywords: Experience Platform；入门；客户ai；热门主题；客户ai输入；客户ai输出
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 客户人工智能中的输入与输出
topic: Getting started
description: 进一步了解客户人工智能所使用的所需事件、输入和输出。
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
translation-type: tm+mt
source-git-commit: 2ef2a6431865e8ffdc2abd6cf527249e8b5ca4d0
workflow-type: tm+mt
source-wordcount: '2867'
ht-degree: 1%

---

# 客户人工智能中的输入和输出

以下文档概述了客户人工智能中使用的不同所需事件、输入和输出。

## 入门指南

客户人工智能通过分析以下数据集之一来预测客户流失或转化倾向得分：

- 消费者体验事件(CEE)数据集
- Adobe Analytics数据（使用[Analytics源连接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)）
- Adobe Audience ManagerAudience Manager使用[源连接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)

>[!IMPORTANT]
>
>源连接器回填数据最长需要4周。 如果您最近设置了连接器，则应验证数据集是否具有客户AI所需的最小数据长度。 请查看[历史数据](#data-requirements)部分，以验证您是否有足够的数据用于预测目标。

此文档要求对中东欧模式有基本的了解。 请在继续之前查阅[智能服务数据准备](../data-preparation.md)文档。

下表概述了本文档中使用的一些常见术语：

| 搜索词 | 定义 |
| --- | --- |
| [体验数据模型(XDM)](../../xdm/home.md) | XDM是基本框架，它允许以Adobe Experience Platform为后盾的Adobe Experience Cloud在恰当的时刻，在适当的渠道向适当的人员提供适当的信息。 构建Experience Platform的方法，即XDM系统，可操作由平台服务使用的体验数据模型模式。 |
| XDM 架构 | Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。在将数据引入平台之前，必须构建一个模式来描述数据的结构，并对每个字段中可以包含的数据类型提供约束。 模式由基XDM类和零个或多个混音组成。 |
| XDM类 | 所有XDM模式都描述了可以分类为记录或时间序列的数据。 模式的模式行为由的类定义，该类在首次创建模式时分配给。 XDM类描述模式必须包含的最小属性数，以表示特定数据行为。 |
| [Mixins](../../xdm/schema/composition.md) | 定义模式中一个或多个字段的组件。 Mixins强制实现其字段在模式层次结构中的显示方式，因此在每个模式中都显示其包含在中的相同结构。 Mixins仅与特定类兼容，由其`meta:intendedToExtend`属性标识。 |
| [数据类型](../../xdm/schema/composition.md) | 还可为模式提供一个或多个字段的组件。 但是，与混音不同，数据类型不限于特定类。 这使数据类型成为描述可跨具有潜在不同类的多个模式重用的常见数据结构的更灵活的选项。 CEE和Adobe Analytics模式均支持本文档中概述的数据类型。 |
| 客户流失 | 取消或选择不续订其订阅的帐户百分比度量。 较高的客户流失率可能会对月度经常性收入(MRR)产生负面影响，也可能表明对产品或服务的不满。 |
| [实时客户资料](../../profile/home.md) | 实时客户用户档案为有针对性的个性化体验管理提供了集中化的消费者用户档案。 每个用户档案都包含跨所有系统聚合的事件，以及涉及您与Experience Platform一起使用的任何系统中发生的个人的可操作时间戳帐户。 |

## 客户人工智能输入数据

>[!TIP]
>
> 客户人工智能自动确定哪些事件对预测有用，并在可用数据不足以生成质量预测时发出警告。

客户人工智能支持CEE、Adobe Analytics和Adobe Audience Manager数据集。 CEE模式要求您在创建模式的过程中添加混音。 如果您使用Adobe Analytics或Adobe Audience Manager数据集，源连接器会在连接过程中直接映射下面列出的标准事件（商务、网页详细信息、应用程序和搜索）。

有关映射Adobe Analytics数据或Audience Manager数据的详细信息，请访问[分析字段映射](../../sources/connectors/adobe-applications/analytics.md)或[Audience Manager字段映射](../../sources/connectors/adobe-applications/mapping/audience-manager.md)指南。

### 客户AI {#standard-events}使用的标准事件

XDM体验事件用于确定各种客户行为。 根据您的事件类型的结构，以下列出的数据可能不包括您的所有客户行为。 由您决定哪些字段具有明确、明确地识别Web用户活动所需的必要数据。 根据您的预测目标，需要的必填字段可能会更改。

客户人工智能依赖不同的事件类型来构建模型功能。 这些事件类型会使用多个XDM混音自动添加到您的模式。

>[!NOTE]
>
>如果您使用Adobe Analytics或Adobe Audience Manager数据，则会自动创建模式，并使用捕获数据所需的标准事件。 如果您要创建自己的自定义CEE模式来捕获数据，您需要考虑捕获数据所需的混音。

不必为下面列出的每个标准事件提供数据，但某些情况需要某些事件。 如果您有任何标准事件数据可用，建议您将其包含在模式中。 例如，如果要创建用于预测购买事件的客户人工智能应用程序，则使用`Commerce`和`Web page details`数据类型中的数据会很有用。

要在平台UI中视图混音，请选择左边栏上的&#x200B;**[!UICONTROL Schemas]**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL Mixins]**&#x200B;选项卡。


| Mixin | 事件类型 | XDM字段路径 |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | or | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | 结帐 | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | 购买 | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemults | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Web Details] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Application Details] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrasses | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Search Details] | 搜索 | search.keywords |

此外，订阅人工智能可以使用客户数据构建更好的客户流失模型。 使用[[!UICONTROL Subscription]](../../xdm/data-types/subscription.md)订阅类型格式的每个用户档案都需要数据。 但是，大多数字段都是可选的，对于最佳客户流失模型，强烈建议您为尽可能多的字段提供数据，如`startDate`、`endDate`和任何其他相关详细信息。

### 历史数据 {#data-requirements}

客户人工智能要求模型培训有历史数据，但所需数据量基于两个关键要素：结果窗口和合格人口。

默认情况下，如果在应用程序配置期间未提供符合条件的人口定义，客户AI会查找在过去120天内具有活动的用户。 此外，客户人工智能需要根据预测目标定义至少500个符合条件的事件和500个不符合条件的数据（总计1000个）。

提供的以下示例使用一个简单的公式帮助您确定所需的最少数据量。 如果您的要求超过最低要求，则您的模型可能会提供更准确的结果。 如果您的数据量小于所需的最小数量，则模型将失败，因为没有足够的数据用于模型培训。

**公式**:

所需数据的最小长度=合格人口+结果窗口

>[!NOTE]
>
> 30是合格人口所需的最少天数。 如果未提供，则默认值为120天。

示例：

- 您希望预测客户是否可能在未来30天内购买手表。 您还希望对过去60天中具有某些Web活动的用户进行评分。 在这种情况下，所需数据的最小长度= 60天+ 30天。 合格人口为60天，结果窗口为30天，共90天。

- 您希望预测用户是否可能在接下来7天内购买手表。 在这种情况下，所需数据的最小长度= 120天+ 7天。 合格人口默认为120天，结果窗口为7天，总共127天。

- 您希望预测客户是否可能在接下来7天内购买手表。 您还希望对过去7天中具有某些Web活动的用户进行评分。 在这种情况下，所需数据的最小长度= 30天+ 7天。 合格人口至少需要30天，结果窗口为7天，总共37天。

除了所需的最低数据外，客户人工智能还可以最佳地处理最新数据。 在此用例中，客户人工智能根据用户最近的行为数据对未来做出预测。 换句话说，更新的数据可能会产生更准确的预测。

### 示例方案

在本节中，描述了客户人工智能实例的不同方案以及所需的和推荐的事件类型。 有关mixin及其字段路径的详细信息，请参阅上面的[标准事件表](#standard-events)。

>[!NOTE]
>
> 必需的事件类型用于清晰、明确地识别Web用户活动。 所需事件类型的数量将根据您的模式的预测目标和结构而改变。 如果您不确定需要某个特定事件类型，建议在构建CEE模式时包含该事件类型。 如果您使用Adobe Analytics或Adobe Audience Manager数据，则根据您正在流化的数据，应提供所需的标准事件。

### 方案1:电子商务零售网站上的购买转换

**预测目标：** 预测合格用户档案在网站上购买某篇服装的转化倾向。

**所需的标准事件类型:**

以下列出的事件类型对于具有此特定预测目标的最佳客户人工智能输出是必需的。 根据预测目标，可以排除所需的事件，但是，排除多个事件可能会导致结果不佳。

- or
- 结帐
- 购买
- webVisit
- 搜索

**其他建议的标准事件类型:**

配置客户人工智能实例时，可能需要根据目标和合格人群的复杂性，使其余的[事件类型](#standard-events)中的任何一个。 如果数据可用于特定数据类型，则建议将此数据包含在您的模式中。

### 方案2:订阅在媒体流服务网站上的转换

**预测目标：** 预测合格用户档案承诺到特定订阅级别（如标准或高级计划）的订阅转化倾向。

**所需的标准事件类型:**

以下列出的事件类型对于具有此特定预测目标的最佳客户人工智能输出是必需的。 根据预测目标，可以排除所需的事件，但是，排除多个事件可能会导致结果不佳。

- or
- 结帐
- 购买
- webVisit
- 搜索

在此示例中，`order`、`checkouts`和`purchases`用于指示已购买订阅及其类型。

此外，对于准确的模型，建议使用[订阅数据类型](../../xdm/data-types/subscription.md)中的一些可用属性。

**其他建议的标准事件类型:**

配置客户人工智能实例时，可能需要根据目标和合格人群的复杂性，使其余的[事件类型](#standard-events)中的任何一个。 如果数据可用于特定数据类型，则建议将此数据包含在您的模式中。

### 方案3:电子商务零售网站的参与

**预测目标：** 预测不发生购买事件的可能性。

**所需的标准事件类型:**

以下列出的事件类型对于具有此特定预测目标的最佳客户人工智能输出是必需的。 根据预测目标，可以排除所需的事件，但是，排除多个事件可能会导致结果不佳。

- or
- 结帐
- 购买
- webVisit
- 搜索

**其他建议的标准事件类型:**

配置客户人工智能实例时，可能需要根据目标和合格人群的复杂性，使其余的[事件类型](#standard-events)中的任何一个。 如果数据可用于特定数据类型，则建议将此数据包含在您的模式中。

### 方案4:电子商务零售网站上的向上销售转化

**预测目标：** 预测已购买特定产品的人口购买新相关产品的购买倾向。

**所需的标准事件类型:**

以下列出的事件类型对于具有此特定预测目标的最佳客户人工智能输出是必需的。 根据预测目标，可以排除所需的事件，但是，排除多个事件可能会导致结果不佳。

- or
- 结帐
- 购买
- webVisit
- 搜索

**其他建议的标准事件类型:**

配置客户人工智能实例时，可能需要根据目标和合格人群的复杂性，使其余的[事件类型](#standard-events)中的任何一个。 如果数据可用于特定数据类型，则建议将此数据包含在您的模式中。

### 方案5:取消订阅（参与）在线新闻

**预测目** 标：预测合格人口下月取消订阅服务的倾向。

**所需的标准事件类型:**

以下列出的事件类型对于具有此特定预测目标的最佳客户人工智能输出是必需的。 根据预测目标，可以排除所需的事件，但是，排除多个事件可能会导致结果不佳。

- webVisit
- 搜索

此外，对于准确的模型，建议使用[订阅数据类型](../../xdm/data-types/subscription.md)中的一些可用属性。

**其他建议的标准事件类型:**

配置客户人工智能实例时，可能需要根据目标和合格人群的复杂性，使其余的[事件类型](#standard-events)中的任何一个。 如果数据可用于特定数据类型，则建议将此数据包含在您的模式中。

### 方案6:启动移动应用程序

**预测目标：** 预测合格用户档案在未来X天内启动付费移动应用程序的倾向。这类似于预测“每月活动用户”的关键绩效指标(KPI)。

**所需的标准事件类型:**

以下列出的事件类型对于具有此特定预测目标的最佳客户人工智能输出是必需的。 根据预测目标，可以排除所需的事件，但是，排除多个事件可能会导致结果不佳。

- or
- 结帐
- 购买
- webVisit
- applicationCloses
- applicationCrasses
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

在此示例中，需要购买移动应用程序时使用`order`、`checkouts`和`purchases`。

**其他建议的标准事件类型:**

配置客户人工智能实例时，可能需要根据目标和合格人群的复杂性，使其余的[事件类型](#standard-events)中的任何一个。 如果数据可用于特定数据类型，则建议将此数据包含在您的模式中。

### 方案7:已实现特征(Adobe Audience Manager)

**预测目标：** 预测要实现的某些特征的倾向。

**所需的标准事件类型:**

要使用Adobe Audience Manager的特征，您需要使用[Audience Manager源连接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)创建源连接。 源连接器自动创建具有适当混音的模式。 您无需手动添加其他事件类型,模式便可与客户人工智能结合使用。

在配置新客户AI实例时，`audienceName`和`audienceID`可用于在定义目标时为得分选择特定特征。

## 客户人工智能输出数据

客户人工智能为被认为符合条件的个别用户档案生成多个属性。 有两种方法可根据您已设置的内容使用得分（输出）。 如果您有启用实时客户用户档案的数据集，则可以在[区段生成器](../../segmentation/ui/segment-builder.md)的“实时客户用户档案”中使用洞察。 如果您没有启用用户档案的数据集，则可以[下载可在数据湖上使用的客户AI输出](./user-guide/download-scores.md)数据集。

>[!NOTE]
>
> 输出值由实时客户用户档案消耗，可用于创建和定义区段。

下表描述了在客户人工智能的输出中找到的各种属性：

| 属性 | 描述 |
| ----- | ----------- |
| 得分 | 客户在定义的时间范围内达到预测目标的相对可能性。 此值不应视为概率百分比，而应视为个人相对于总体人口的可能性。 此得分范围从0到100。 |
| 概率 | 此属性是用户档案在定义的时间范围内实现预测目标的真实概率。 在比较不同目标的输出时，建议您考虑百分比或分数的概率。 在确定合格人群的平均概率时，应始终使用概率，因为对于不频繁发生的事件，概率往往处于较低水平。 概率范围在0和1之间的值。 |
| 百分点 | 此值提供有关用户档案相对于其他类似计分用户档案的性能的信息。 例如，一个百分位排名为99的用户档案表示，与所有其他得分用户档案的99%相比，它更有可能出现剧烈波动。 百分比范围从1到100。 |
| 倾向类型 | 所选倾向类型。 |
| 得分日期 | 得分发生的日期。 |
| 影响因素 | 预测用户档案可能转化或参与的原因。 因素包括以下属性：<ul><li>代码：对用户档案的预测得分产生积极影响的用户档案或行为属性。 </li><li>值：用户档案或行为属性的值。</li><li>重要性：指示用户档案或行为属性对预测得分（低、中、高）的权重</li></ul> |

## 后续步骤 {#next-steps}

准备数据并准备好所有凭据和模式后，请按照[配置客户AI实例](./user-guide/configure.md)指南进行开始。 本指南将指导您为客户人工智能创建一个实例。
