---
keywords: Experience Platform；快速入门；客户人工智能；热门主题；客户人工智能输入；客户人工智能输出；数据要求
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI中的数据要求
topic-legacy: Getting started
description: 进一步了解Customer AI使用的必需事件、输入和输出。
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 2%

---


# Customer AI中的输入和输出

以下文档概述了客户人工智能中使用的不同必需事件、输入和输出。

## 快速入门 {#getting-started}

以下是在Customer AI中构建倾向模型并确定用于个性化营销的目标受众的步骤：

1. 概要用例：倾向模型如何帮助识别个性化营销的目标受众？ 实现目标的业务目标和相应策略是什么？ 倾向建模在此过程中可以适合哪些情况？

2. 优先处理用例：哪些是业务的最优先事项？

3. 在Customer AI中构建模型：看这个 [快速教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html) 请参阅 [UI指南](../customer-ai/user-guide/configure.md) 以逐步构建模型。

4. [生成区段](../customer-ai/user-guide/create-segment.md) 使用模型结果。

5. 根据这些区段采取有针对性的业务操作。 监控结果并迭代操作以改进。

以下是第一个模型的配置示例。  在本文档中构建的示例模型使用Customer AI模型来预测未来30天内哪些人可能会转化为零售企业。 输入数据集是Adobe Analytics数据集。

| 步骤 | 定义 | 示例 |
| ---- | ------ | ------- |
| 设置 | 指定有关模型的基本信息。 | **名称**:铅笔购买倾向模型 <br> **模型类型**:转化 |
| 选择数据 | 指定用于构建模型的数据集。 | **数据集**:Adobe Analytics数据集 <br> **身份**:确保将每个数据集的标识列设置为通用标识。 |
| 定义目标 | 定义目标、符合条件的群体、自定义事件和用户档案属性。 | **预测目标**:选择 `commerce.purchases.value` 等于铅笔 <br> **结果窗口**:30天。 |
| 设置选项 | 设置模型刷新计划并启用用户档案的得分 | **计划**:每周 <br> **为配置文件启用**:必须为要用于分段的模型输出启用此功能。 |

## 数据概述 {#data-overview}

以下各节概述了客户人工智能中使用的不同必需事件、输入和输出。

Customer AI通过分析以下数据集来预测流失率（客户可能停止使用产品）或转化（客户可能进行购买）倾向得分：

- Adobe Analytics数据(使用 [Analytics源连接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager数据(使用 [Audience Manager源连接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [体验事件数据集](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [消费者体验事件数据集](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

如果每个数据集共享相同的身份类型（命名空间）（如ECID），则可以从不同的源添加多个数据集。 有关添加多个数据集的更多信息，请访问 [Customer AI用户指南](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>源连接器最多需要四周时间才能回填数据。 如果您最近设置了一个连接器，则应验证数据集是否具有Customer AI所需的最小数据长度。 请查看 [历史数据](#data-requirements) 部分，以验证是否有足够的数据来实现预测目标。

下表概述了本文档中使用的一些常用术语：

| 搜索词 | 定义 |
| --- | --- |
| [体验数据模型(XDM)](../../xdm/home.md) | XDM是基础框架，它允许由Adobe Experience Platform提供支持的Adobe Experience Cloud在适当的时间，通过适当的渠道向适当的人员提供适当的信息。 Platform使用XDM系统以特定方式组织数据，从而更便于用于Platform服务。 |
| [XDM 架构](../../xdm/schema/composition.md) | Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。在将数据摄取到平台中之前，必须构建一个架构来描述数据的结构，并对每个字段中可包含的数据类型提供约束。 架构由基本XDM类和零个或多个架构字段组组成。 |
| [XDM类](../../xdm/schema/field-constraints.md) | 所有XDM架构都描述了可分类为 `Experience Event`. 架构的数据行为由架构的类定义，该类在首次创建架构时分配给架构。 XDM类描述架构必须包含的最小属性数，以表示特定数据行为。 |
| [字段组](../../xdm/schema/composition.md) | 定义架构中一个或多个字段的组件。 字段组强制执行其字段在架构层次结构中的显示方式，因此在每个架构中显示的结构都与其中包含的结构相同。 字段组仅与特定类兼容，这些类由其标识 `meta:intendedToExtend` 属性。 |
| [数据类型](../../xdm/schema/composition.md) | 还可以为架构提供一个或多个字段的组件。 但是，与字段组不同，数据类型不受特定类的限制。 这使数据类型成为一种更灵活的选项，用于描述在具有潜在不同类的多个架构中可重复使用的常用数据结构。 CEE架构和Adobe Analytics架构均支持本文档中概述的数据类型。 |
| [实时客户资料](../../profile/home.md) | Real-time Customer Profile提供了集中式消费者用户档案，以进行有针对性的个性化体验管理。 每个用户档案都包含在所有系统中汇总的数据，以及涉及您与Experience Platform一起使用的任何系统中发生的个人事件的带有时间戳的可操作帐户。 |

## 客户人工智能输入数据 {#customer-ai-input-data}

对于输入数据集(如Adobe Analytics和Adobe Audience Manager)，在连接过程中，默认情况下，相应的源连接器会直接映射这些标准字段组（商务、Web、应用程序和搜索）中的事件。 下表显示了Customer AI的默认标准字段组中的事件字段。

有关映射Adobe Analytics数据或Audience Manager数据的更多信息，请访问Analytics字段映射或Audience Manager [字段映射指南](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

您可以将体验事件或消费者体验事件XDM架构用于未通过上述任一连接器填充的输入数据集。 在架构创建过程中，可以添加其他XDM字段组。 字段组可由标准字段组或自定义字段组等Adobe提供，这些字段组与平台中的数据表示形式相匹配。

>[!IMPORTANT]
>
>您必须确保数据被填充到这些输入数据集中。 如果在输入数据集中未找到标准字段组中的事件，则必须在配置工作流中添加自定义事件。 请参阅有关自定义事件的详细信息。

### Customer AI使用的标准字段组 {#standard-events}

体验事件用于确定各种客户行为。 根据数据的结构方式，下面列出的事件类型可能并不包含客户的所有行为。 需要您自行确定哪些字段具有明确和明确地识别Web或其他特定于渠道的用户活动所需的必要数据。 根据您的预测目标，所需的必填字段可能会发生更改。

>[!NOTE]
>
>如果您使用的是Adobe Analytics或Adobe Audience Manager数据，则会自动创建架构，并包含捕获数据所需的标准事件。 如果您要创建自己的自定义EE模式来捕获数据，则需要考虑捕获数据所需的字段组。

默认情况下， Customer AI使用这四个标准字段组中的事件：商务、Web、应用程序和搜索。 在下面列出的标准字段组中，不必包含每个事件的数据，但某些情况需要某些事件。 如果您在标准字段组中有任何可用事件，建议将其包含在架构中。 例如，如果要创建用于预测购买事件的Customer AI模型，则有关商务和网页详细信息字段组的数据将非常有用。

要在平台UI中查看字段组，请选择 **[!UICONTROL 模式]** 选项卡，然后选择 **[!UICONTROL 字段组]** 选项卡。

| 字段组 | 事件类型 | XDM字段路径 |
| --- | --- | --- |
| [!UICONTROL 商务详细信息] | 订单 | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | 结账 | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | 购买 | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemuves | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Web详细信息] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL 应用程序详细信息] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashss | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL 搜索详细信息] | 搜索 | `search.keywords` |

此外， Customer AI可以使用订阅数据构建更好的流失模型。 每个使用 [[!UICONTROL 订阅]](../../xdm/data-types/subscription.md) 数据类型格式。 大多数字段是可选的，但是，为了获得最佳的流失模型，强烈建议您为尽可能多的字段提供数据，例如 `startDate`, `endDate`，以及任何其他相关详细信息。 请联系您的客户团队，以获取有关此功能的其他支持。

### 添加自定义事件和配置文件属性 {#add-custom-events}

如果除了默认信息之外，您还希望包含其他信息 [标准事件字段](#standard-events) 由Customer AI使用，您可以使用 [自定义事件配置](./user-guide/configure.md#custom-events) 以扩充模型使用的数据。

#### 何时使用自定义事件

在数据集选择步骤中选择的数据集包含时，需要自定义事件 *无* Customer AI使用的默认事件字段的。 Customer AI需要有关结果以外的至少一个用户行为事件的信息。

自定义事件有助于：

- 将领域知识或先前的专业知识纳入模型。

- 提高预测模型质量。

- 获取更多见解和解释。

自定义事件的最佳候选者是包含可能预测结果的域知识的数据。 自定义事件的一些常规示例包括：

- 注册帐户

- 订阅新闻稿

- 致电客户服务

以下是一系列特定于行业的自定义事件示例：

| 行业 | 自定义事件 |
| --- | --- |
| 零售 | 店内交易<br>注册俱乐部卡<br>剪贴移动优惠券。 |
| 娱乐 | 购买季会员资格 <br> 流视频。 |
| 酒店 | 预订餐厅 <br> 购买会员积分。 |
| 旅行 | 添加已知的旅行者信息购买里程。 |
| 通信 | 升级/降级/取消计划。 |

自定义事件必须表示用户启动的操作，才能进行选择。 例如，“电子邮件发送”是营销人员而不是用户发起的一项操作，因此不应将其用作自定义事件。

### 历史数据

Customer AI要求提供模型培训的历史数据。 数据在系统中存在的所需持续时间由两个关键元素决定：结果窗口和合格人口。

默认情况下，如果在应用程序配置期间未提供符合条件的群体定义，则Customer AI会查找用户在过去45天内具有活动。 此外，客户人工智能需要根据预测目标定义从历史数据中至少500个符合条件事件和500个不符合条件事件（总数为1000个）。

以下示例演示了如何使用一个简单的公式，该公式可帮助您确定所需的最小数据量。 如果您的数据多于最低要求，则模型可能会提供更准确的结果。 如果您的数量小于所需的最小数量，则模型将失败，因为模型培训没有足够的数据。

**公式**:

要确定系统内现有数据所需的最短持续时间，请执行以下操作：

- 创建功能所需的最少数据为30天。 比较资格回顾窗口与30天：

   - 如果资格回顾窗口大于30天，则数据要求=资格回顾窗口+结果窗口。

   - 否则，数据要求= 30天+结果窗口。

**如果定义符合条件的群体有多个条件，则资格回顾窗口是最长的一个。

>[!NOTE]
>
>30是合格人口所需的最低天数。 如果未提供，则默认值为45天。

**示例**:

- 您希望预测客户是否可能在未来30天内为那些在过去60天内进行某些Web活动的用户购买手表。

   - 资格回顾时间范围= 60天

   - 结果窗口= 30天

   - 所需数据= 60天+ 30天= 90天

- 您想要预测用户是否可能在接下来7天内购买手表 **无** 提供明确的合格人口。 在这种情况下，符合条件的群体默认为“过去45天内有活动的人”，结果窗口为7天。

   - 资格回顾时间范围= 45天

   - 结果窗口= 7天

   - 所需数据= 45天+ 7天= 52天

- 您希望预测客户是否可能在未来7天内为那些在过去7天内有一些Web活动的用户购买手表。

   - 资格回顾窗口= 7天

   - 创建功能所需的最少数据= 30天

   - 结果窗口= 7天

   - 所需数据= 30天+ 7天= 37天

尽管Customer AI要求将数据在系统内存在的最短时间，但它也最适合于最近的数据。 通过使用更新的行为数据， Customer AI可能会生成更准确的用户未来行为预测。

## 客户AI输出数据 {#customer-ai-output-data}

Customer AI会为被认为符合条件的个人用户档案生成多个属性。 根据您配置的内容，可使用两种方式来使用得分（输出）。 如果您有一个启用了“实时客户资料”的数据集，则可以在 [区段生成器](../../segmentation/ui/segment-builder.md). 如果您没有启用了配置文件的数据集，则可以 [下载Customer AI输出](./user-guide/download-scores.md) 数据湖上可用的数据集。

您可以在平台中找到输出数据集 **数据集** 工作区。 所有Customer AI输出数据集均以名称开头 **Customer AI得分 — NAME_OF_APP**. 同样，所有Customer AI输出架构都以名称开头 **Customer AI架构 — Name_of_app**.

![Customer AI中输出数据集的名称](./images/user-guide/cai-schema-name-of-app.png)

下表描述了Customer AI输出中的各种属性：

| 属性 | 描述 |
| ----- | ----------- |
| [!UICONTROL 得分] | 客户在定义的时间范围内实现预测目标的相对可能性。 此值不应视为概率百分比，而应视为个人与整体群体的比较可能性。 此分数的范围为0到100。 |
| 概率 | 此属性是配置文件在定义的时间范围内实现预测目标的真实概率。 在比较不同目标的输出时，建议考虑概率大于百分位数或得分。 在确定符合条件的群体的平均概率时，应始终使用概率，因为对于不经常发生的事件，概率往往位于较低的一方。 概率范围在0到1之间的值。 |
| 百分位数 | 此值提供有关用户档案相对于其他类似评分用户档案的性能的信息。 例如，对于流失率，百分位等级为99的用户档案表示，与之相比，其他所有得分用户档案的99%存在更高的流量风险。 百分位数介于1到100之间。 |
| 倾向类型 | 所选的倾向类型。 |
| 得分日期 | 打分的日期。 |
| 影响因素 | 预测了用户档案可能转化或流失的原因。 这些因素包括以下属性：<ul><li>代码：积极影响用户档案预测分数的用户档案或行为属性。 </li><li>值：配置文件或行为属性的值。</li><li>重要性：指示用户档案或行为属性对预测得分（低、中、高）的权重</li></ul> |

## 后续步骤 {#next-steps}

准备数据并确保所有凭据和架构都到位后，请参阅 [配置Customer AI实例](./user-guide/configure.md) 指南，该指南将指导您完成创建Customer AI实例的分步教程。