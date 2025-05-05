---
keywords: Experience Platform；快速入门；客户人工智能；热门主题；客户人工智能输入；客户人工智能输出；数据要求
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: 客户人工智能中的数据要求
topic-legacy: Getting started
description: 进一步了解客户人工智能使用的所需事件、输入和输出。
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2551'
ht-degree: 1%

---


# Customer AI中的输入和输出

以下文档概述了Customer AI中使用的不同必需事件、输入和输出。

## 快速入门 {#getting-started}

以下是构建倾向模型和识别目标受众以在Customer AI中进行个性化营销的步骤：

1. 概述用例：倾向模型如何帮助确定个性化营销的目标受众？ 我的业务目标和实现该目标的相应策略是什么？ 倾向建模在此过程中处于什么地位？

2. 排定用例优先级：哪一项是业务的最高优先级？

3. 在Customer AI中构建模型：观看此[快速教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=zh-Hans)并参阅我们的[UI指南](../customer-ai/user-guide/configure.md)，了解构建模型的分步流程。

4. [使用模型结果生成区段](../customer-ai/user-guide/create-segment.md)。

5. 根据这些区段采取有针对性的业务行动。 监控结果并反复执行要改进的操作。

以下是第一个模型的配置示例。  本文档中构建的示例模型使用客户人工智能模型来预测谁可能在未来30天内转投零售业务。 输入数据集是Adobe Analytics数据集。

| 步骤 | 定义 | 示例 |
| ---- | ------ | ------- |
| 设置 | 指定有关模型的基本信息。 | **名称**：铅笔购买倾向模型<br> **模型类型**：转换 |
| 选择数据 | 指定用于构建模型的数据集。 | **数据集**： Adobe Analytics数据集<br> **标识**：确保将每个数据集的标识列设置为公共标识。 |
| 定义目标 | 定义目标、符合条件的群体、自定义事件和用户档案属性。 | **预测目标**：选择`commerce.purchases.value`等于铅笔<br> **结果窗口**： 30天。 |
| 设置选项 | 设置模型刷新计划并为配置文件启用得分 | **计划**：每周<br> **为配置文件**&#x200B;启用：必须为要用于分段中的模型输出启用此项。 |

## 数据概述 {#data-overview}

以下部分概述了客户人工智能中使用的各种所需事件、输入和输出。

客户人工智能通过分析以下数据集来预测客户流失（客户何时可能停止使用产品）或转化（客户何时可能购买）倾向分数：

- 使用[Analytics源连接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)的Adobe Analytics数据
- 使用[Adobe Audience Manager源连接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)的Audience Manager数据
- [体验事件数据集](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=zh-Hans)
- [使用者体验事件数据集](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html?lang=zh-Hans#cee-schema)

如果每个数据集共享相同的身份类型（命名空间）（如ECID），则可以添加来自不同来源的多个数据集。 有关添加多个数据集的更多信息，请访问[客户人工智能用户指南](../customer-ai/user-guide/configure.md)。

>[!IMPORTANT]
>
>Source连接器最多需要四周时间来回填数据。 如果您最近设置了连接器，则应验证数据集是否具有客户人工智能所需的最小数据长度。 请查看[历史数据](#data-requirements)部分，以验证您的预测目标是否有足够的数据。

下表概述了本文档中使用的一些常用术语：

| 搜索词 | 定义 |
| --- | --- |
| [体验数据模型(XDM)](../../xdm/home.md) | XDM是一个基础框架，它允许由Adobe Experience Platform提供支持的Adobe Experience Cloud在正确的时间通过正确的渠道向正确的人员传递正确的信息。 Experience Platform使用XDM系统以特定方式整理数据，以便更轻松地用于Experience Platform服务。 |
| [XDM架构](../../xdm/schema/composition.md) | Experience Platform使用架构，以一致且可重用的方式描述数据结构。 通过在系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。 将数据引入Experience Platform之前，必须构建架构以描述数据的结构并对每个字段中可以包含的数据类型提供约束。 架构由一个基本XDM类以及零个或多个架构字段组组成。 |
| [XDM类](../../xdm/schema/field-constraints.md) | 所有XDM架构都描述了可分类为`Experience Event`的数据。 架构的数据行为由架构的类定义，该类在首次创建架构时分配给架构。 XDM类描述架构必须包含的最小属性数，以便表示特定数据行为。 |
| [字段组](../../xdm/schema/composition.md) | 定义架构中一个或多个字段的组件。 字段组强制实施其字段在架构层次结构中的显示方式，因此它们包含的每个架构都具有相同的结构。 字段组仅与由其`meta:intendedToExtend`属性标识的特定类兼容。 |
| [数据类型](../../xdm/schema/composition.md) | 还可以为架构提供一个或多个字段的组件。 但是，与字段组不同，数据类型不受特定类的约束。 这使得数据类型成为描述通用数据结构的更灵活的选项，这些结构可以在具有不同类的多个架构中重用。 CEE和Adobe Analytics架构均支持本文档中概述的数据类型。 |
| [实时客户轮廓](../../profile/home.md) | Real-time Customer Profile为有针对性的个性化体验管理提供了一个集中式客户配置文件。 每个用户档案都包含跨所有系统汇总的数据，以及在您用于Experience Platform的任意系统中发生的涉及个人事件的可操作时间戳帐户。 |

## 客户人工智能输入数据 {#customer-ai-input-data}

对于输入数据集(如Adobe Analytics和Adobe Audience Manager)，默认情况下，源连接器在连接过程中直接映射这些标准字段组(Commerce、Web、应用程序和搜索)中的事件。 下表显示了Customer AI的默认标准字段组中的事件字段。

有关映射Adobe Analytics数据或Audience Manager数据的详细信息，请访问Analytics字段映射或Audience Manager [字段映射指南](../../sources/connectors/adobe-applications/mapping/audience-manager.md)。

您可以将体验事件或使用者体验事件XDM架构用于未通过以上连接器之一填充的输入数据集。 可在架构创建过程中添加其他XDM字段组。 字段组可由Adobe提供，例如标准字段组或自定义字段组，它们与Experience Platform中的数据表示形式匹配。

>[!IMPORTANT]
>
>您必须确保将数据填充到这些输入数据集中。 如果在输入数据集中未找到标准字段组中的事件，则必须在配置工作流期间添加自定义事件。 请参阅有关自定义事件的详细信息。

### 客户人工智能使用的标准字段组 {#standard-events}

体验事件用于确定各种客户行为。 根据数据的结构方式，下面列出的事件类型可能不会包含客户的所有行为。 由您来决定哪些字段具有必要的数据，该数据是清晰明确地识别Web或其他特定于渠道的用户活动所必需的。 根据您的预测目标，所需的必填字段可能会发生更改。

>[!NOTE]
>
>如果您使用的是Adobe Analytics或Adobe Audience Manager数据，则架构会使用捕获数据所需的标准事件自动创建。 如果您创建自己的自定义EE架构来捕获数据，则需要考虑捕获数据所需的字段组。

默认情况下，客户人工智能使用四个标准字段组中的事件：Commerce、Web、Application和Search。 无需在下面列出的标准字段组中为每个事件提供数据，但在某些情况下需要某些事件。 如果标准字段组中有任何可用事件，建议将其包含在架构中。 例如，如果要创建用于预测购买事件的客户人工智能模型，则从Commerce和网页详细信息字段组获得数据会很有用。

要在Experience Platform UI中查看字段组，请选择左边栏上的&#x200B;**[!UICONTROL 架构]**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 字段组]**&#x200B;选项卡。

| 字段组 | 事件类型 | XDM字段路径 |
| --- | --- | --- |
| [!UICONTROL Commerce详细信息] | 订单 | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListView | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | 结账 | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | 购买 | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | 产品视图 | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Web详细信息] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL 应用程序详细信息] | applicationClose | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunch | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationinstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunch | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrade | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL 搜索详细信息] | 搜索 | `search.keywords` |

此外，Customer AI可以使用订阅数据构建更好的流失模型。 使用[[!UICONTROL 订阅]](../../xdm/data-types/subscription.md)数据类型格式的每个配置文件都需要订阅数据。 大多数字段是可选的，但是，对于最佳流失模型，强烈建议您为尽可能多的字段（如`startDate`、`endDate`）提供数据，以及任何其他相关详细信息。 请联系您的帐户团队以获取有关此功能的更多支持。

### 添加自定义事件和配置文件属性 {#add-custom-events}

如果除了客户人工智能使用的默认[标准事件字段](#standard-events)之外，您还希望包含其他信息，则可以使用[自定义事件配置](./user-guide/configure.md#custom-events)来增加模型使用的数据。

#### 何时使用自定义事件

当在数据集选择步骤中选择的数据集包含&#x200B;*none*&#x200B;客户人工智能使用的默认事件字段时，需要自定义事件。 客户人工智能需要有关结果以外的至少一个用户行为事件的信息。

自定义事件有助于：

- 将领域知识或先前的专业知识纳入模型。

- 提高预测模型质量。

- 获得更多见解和解释。

自定义事件的最佳候选者是包含可以预测结果的域知识的数据。 自定义事件的一些常规示例包括：

- 注册帐户

- 订阅新闻稿

- 致电客户服务

以下是一些特定于行业的自定义事件示例：

| 行业 | 自定义事件 |
| --- | --- |
| 零售 | 店内交易<br>注册会员卡<br>剪辑移动优惠券。 |
| 娱乐 | 购买季成员资格<br>流视频。 |
| 招待 | 进行餐厅预订<br>购买会员积分。 |
| 旅行 | 添加已知的旅行者信息购买英里数。 |
| 通信 | 升级/降级/取消计划。 |

要选择自定义事件，必须表示用户启动的操作。 例如，“电子邮件发送”是由营销人员而不是用户启动的操作，因此不应将其用作自定义事件。

### 历史数据

客户人工智能需要历史数据来进行模型训练。 数据在系统中存在的所需持续时间由两个关键因素决定：结果窗口和合格群体。

默认情况下，如果在应用程序配置期间未提供符合条件的群体定义，客户人工智能会查找最近45天内有活动的用户。 此外，根据预测的目标定义，客户人工智能要求来自历史数据的至少500个符合条件事件和500个非符合条件事件（总共1000个）。

以下示例演示了如何使用一个简单的公式，该公式可帮助您确定所需的最小数据量。 如果您拥有的数据多于最低要求，则您的模型可能会提供更准确的结果。 如果少于所需的最小值，则模型将失败，因为没有足够的数据进行模型训练。

客户人工智能使用生存模型来估计在给定时间发生事件的概率，并识别影响因素，同时使用定义正和负群体的监督学习和`lightgbm`之类的决策树来生成概率分数。

**公式**：

要确定系统中现有数据所需的最短持续时间，请执行以下操作：

- 创建功能所需的最少数据为30天。 将资格回顾时间范围与30天进行比较：

   - 如果资格回顾窗口大于30天，则数据要求=资格回顾窗口+结果窗口。

   - 否则，数据要求= 30天+结果窗口。

**如果定义合格群体的条件不止一个，则合格回顾时间范围为最长。

>[!NOTE]
>
>30是符合条件的群体所需的最小天数。 如果未提供，则默认为45天。

**示例**：

- 您想要预测客户是否可能在接下来的30天内为过去60天内有某个Web活动的客户购买手表。

   - 资格回顾时间范围= 60天

   - 结果窗口= 30天

   - 所需数据= 60天+ 30天= 90天

- 您想要预测用户是否可能在&#x200B;**后7天内购买手表而不提供明确的合格群体**。 在这种情况下，符合条件的群体将默认为“过去45天内有活动的人”，并且结果窗口为7天。

   - 资格回顾时间范围= 45天

   - 结果窗口= 7天

   - 所需数据= 45天+ 7天= 52天

- 您想要预测客户是否可能在未来7天内为过去7天内进行某些Web活动的客户购买手表。

   - 资格回顾时间范围= 7天

   - 创建功能所需的最小数据= 30天

   - 结果窗口= 7天

   - 所需数据= 30天+ 7天= 37天

尽管客户人工智能要求数据在系统中存在最短时间，但它也最适用于最近的数据。 通过使用最新的行为数据，客户人工智能有可能对用户未来的行为产生更准确的预测。

## Customer AI输出数据 {#customer-ai-output-data}

客户人工智能为被认为符合条件的个人资料生成多个属性。 根据您配置的内容，可通过两种方式使用得分（输出）。 如果您拥有启用实时客户配置文件的数据集，则可以在[区段生成器](../../segmentation/ui/segment-builder.md)中使用来自实时客户配置文件的见解。 如果您没有启用配置文件的数据集，您可以[下载可在数据湖中使用的客户人工智能输出](./user-guide/download-scores.md)数据集。

您可以在Experience Platform **数据集**&#x200B;工作区中找到输出数据集。 所有客户人工智能输出数据集都以名称&#x200B;**客户人工智能分数 — NAME_OF_APP**&#x200B;开头。 同样，所有客户人工智能输出架构都以名称&#x200B;**客户人工智能架构 — Name_of_app**&#x200B;开头。

![客户人工智能中输出数据集的名称](./images/user-guide/cai-schema-name-of-app.png)

下表描述了在Customer AI输出中找到的各种属性：

| 属性 | 描述 |
| ----- | ----------- |
| [!UICONTROL 得分] | 客户在定义的时间范围内实现预测目标的相对可能性。 这个值不应被视为概率百分比，而应被视为个体相对于群体总数的可能性。 此得分从0到100不等。 |
| 概率 | 此属性是用户档案在定义的时间范围内实现预测目标的真实概率。 在比较不同目标的输出时，建议您考虑百分比或得分上的概率。 在确定合格群体的平均概率时，应始终使用概率，因为对于不频繁发生的事件，概率往往位于较低侧。 概率范围在0和1之间的值。 |
| 百分位数 | 此值提供有关用户档案相对于其他类似评分的用户档案的性能信息。 例如，百分位数等级为99的客户档案流失率表明，其流失风险高于所有其他已评分客户档案的99%。 百分位数的范围是1到100。 |
| 倾向性类型 | 选定的倾向性类型。 |
| 得分日期 | 评分发生的日期。 |
| 影响因素 | 这些是个人资料可能会发生转化或流失的预测原因。 这些因素由以下属性组成：<ul><li>代码：对个人资料的预测得分产生积极影响的个人资料或行为属性。 </li><li>值：配置文件或行为属性的值。</li><li>重要性：表示配置文件或行为属性对预测分数（低、中、高）的权重</li></ul> |

## 后续步骤 {#next-steps}

准备数据并确保所有凭据和架构均已就绪后，请参阅[配置客户人工智能实例](./user-guide/configure.md)指南，该指南将指导您完成创建客户人工智能实例的分步教程。