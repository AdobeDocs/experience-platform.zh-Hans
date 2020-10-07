---
keywords: Experience Platform;home;popular topics;offer management;Offer Management;Journey;customer journey;journey;decision events;decision event;Decision events
solution: Experience Platform
title: 决策服务
topic: overview
description: 决策服务提供在Adobe Experience Platform运行的应用程序中创建个性化、优化和精心编排的体验的功能。 使用决策服务，您可以从一组可用选项中确定最佳选项。 这些选项也称为替代选项，可以是优惠、产品推荐、Web体验的内容组件、对话脚本和要执行的操作。
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 0%

---


# 决策服务概述

[!DNL Decisioning Service] 提供在运行于Adobe Experience Platform的应用程序中创建个性化、优化和精心编排的体验的功能。 使 [!DNL Decisioning Service]用，您可以从一 *组可用* 选项中确定最佳选项。 这些选项也称为替代选项，可以是优惠、产品推荐、Web体验的内容组件、对话脚本和要执行的操作。 目前支持Offer Decisioning的用 *例和领域* ，其中决策选项被特别建模为优惠，支持未来更多的用例。

借 [!DNL Decisioning Service]助，客户可以重复使用业务逻辑，并跨渠道和应用程序共享一系列选项。 现在，无论客户的最终用户与业务或组织进行交互的渠道是何时、如何以及在何种，都可以利用决策选项，而不是在应用程序的深度管理决策选项和选择策略。

决策策略可以考虑客户在许多渠道和应用程序中进行的许多交互。 例如，呼叫中心应用程序活动可能在投诉后启用或禁止一段时间的营销消息，该消息本身可能基于客户进行的购买和发布的评论。

[!DNL Decisioning Service] 促进改进的体验个性化。

| 体验决策之前 | 体验决策之后 |
| --- | --- |
| 在一个渠道或少量的体验接触点内个性化和优化其用户体验。 | 体验是精心编排的跨交互响应。 |
| 优化集中在最终用户旅程的单一阶段，通常是短暂的 | 决策基于整个交互历史，从过去检测到的行为到最新的情境环境。 |
| 在客户体验中，选项和选择展示策略通常深入应用程序中。 | 选择最佳选项的策略是在特定渠道的应用程序之外定义的，并且可以重复使用。 |
| 客户体验是根据一个简单化的目标进行个性化和优化的，例如，增加网页上成功结帐的次数或接受与代表的交互中呈现的优惠。 | 根据对客户当前需求的全面了解来优化客户体验，并调整以适应用户拥有的所有体验，无论是好是坏。 例如，营销活动可能不适合最近投诉过产品或服务的客户。 |

[!DNL Decisioning Service] 将您的体验个性化功能从单一渠道定位到确定客户与独立于渠道的品牌互动生命周期的整个阶段。 生命周期阶段比细分会员要复杂得多，并且几乎始终基于复杂的事件流、业务规则和预测属性。

产品和服务为提供类似用例而使用的其他术语：

- 实时交互管理(RTIM)
- 旅程管理
- 全渠道营销和个性化
- 实时决策

## 如何工 [!DNL Decisioning Service] 作？

当客户通过入站渠道( [!DNL Decisioning Service] 例如您的网站或移动App)与您的品牌互动时，可以使用实时自定义体验。 决策还可用于通过出站渠道（如电子邮件或推送通知）自定义消息。

决策可以通过多种方式做出。 一种方法是连续地消除选项，直到只保留一个选项或将选项缩减，并且剩余一些子集或从缩减集中随机选取一个入选方。 此方法的变体，用于根据计算公式选择入选方案。 对合格选项进行排序是使用函数完成的。 对于优惠决策，该函数可以计算优惠对业务的成本、价值，并使用预先确定的优惠被最终用户接受的可能性。 结果得分可用于对优惠进行排序。

或者，或者另外，战略可以基于先前与建议相似选项的相似客户进行交互时收集的结果。 在该策略中，学习计算优先级值的函数。 最优结果值与活动目标相关，预测的绩效指标是在提出期权后取得结果的频率。

### 决策策略

决策策略通过称为活动的对象进行配置。 每个决策策略本质上是以N个选项{o1,o2,...oN}为输入并产生选项的有序列表(o1,o2,...oK)的算法或函数，由此列表中的第一个选项根据优化标准被视为最佳选项，结果列表中的第二个选项被视为第二最佳选项，等等。

在客户旅程中的任何给定时间，都会根据最新的上下文变量、规则和约束重新评估给定活动的最佳选项。 上下文变量包括存储在中的记录 [!DNL Real Time Customer Profile]。 中央记录实体是客户的用户档案，但诸如运营业务数据等其他实体对活动同样可用。

产生顶K选项列表的算法或函数会因用例而异。 对于不同的用例，该算法的内部组件是不同的。 这些组件在设计时在存储库中进行定义，并“编译”为用例特定决策策略的说明。

![决策优化](./images/decisioning-optimization.png)

## 使用 [!DNL Decisioning Service]

与 [!DNL Decisioning Service]其他服务 [!DNL Platform] 一样，该服务采用API优先理念。 这意味着API是通过API提供所有功能（包括管理功能）的主要接口。 它还意味着其 [!DNL Platform] 他服务、Adobe解决方案和第三方集成使用相同的API。

您可以在 [!DNL Decisioning Service] 由简单的HTTP REST API提供的同步请求——响应交互模式下使用。 API调用为单个用户档案返回当前最佳选项。 “当前最佳选项”选择将根据应用于给定活动所考虑的所有选项的规则和约束而改变。 REST API允许同时为多个活动获得下一个最佳选项。 这允许在渠道之间仲裁选项。 当同时获得多个活动的响应时，可应用附加规则。

![决策API](./images/decisioning-API.png)

### 与其他工作流 [!DNL Platform] 集成

使用是 [!DNL Decisioning Service] 可选的，除了创建和管理实体所需的典型步骤外，只需执行 [!DNL Profile] 几个步骤。

>[!NOTE]
>
>为了充分利用，该 [!DNL Real-time Customer Profile]服务器 [!DNL Decisioning Service] 直接与用户档案商店集成。 API调用只需为给定用户档案指示一个标识。

构建开始的典型步骤顺序：

- 验证 [!DNL Experience Platform]。
- 根据模式类定义用户档案，并根据体验事件类（可选）定义模式。
- 将数据集配置为将记录和时间序列数据上传到 [!DNL Customer Profile]。
- 通过上一步中配置的数据集添加数据，或通过Pipeline流式实例数据。
- 将体验事件流化 [!DNL Platform] 到用户档案中，用行为数据丰富。

此外，要使 [!DNL Decisioning Service]用，请执行以下步骤：

- 使用存储库API定义决策组件。 这些是构成决策策略的业务逻辑实体。 决策组件将自动编译为由使用的格式 [!DNL Decision Service Runtime]。 存储库API在下图左侧进行说明。
- 调用运行时API以根据上一步中定义的业务逻辑获得最佳选项。 API [!DNL Decision Service Runtime] 在下图的右侧进行说明。

![decisioning-API1](./images/decisioning-API1.png)

业务逻辑实体的激活自动、连续地发生。 一旦新选项保存在存储库中并标记为“已批准”，它将成为要包含在可用选项集中的候选选项。 一旦更新了决策规则，将重新组合规则集并准备执行运行时。 在此自动激活步骤中，将评估由业务逻辑定义的任何不依赖于运行时上下文的约束。 此激活步骤的结果将发送到运行时可用的缓存 [!DNL Decisioning Service] 中。 如下图所示。

![decisioning-API2](./images/decisioning-API2.png)

在激活选项集、规则集和约束并将其推送到节 [!DNL Decisioning Service] 点后，使用一个简单的API发布决策请求。 API通常由投放服务调用，该服务随后会采用建议的选项(例如，下一个最佳操作或下一个最佳优惠)并组合体验或执行操作。 如果提议是优惠，则查找表示该优惠的内容并将其插入到提供给最终用户的体验中。 如下图所示。

![decisioning-API3](./images/decisioning-API3.png)

[!DNL Delivery Service] 为决策请求收集数据。 它确定决定最佳选项的用户档案实体的ID。 它还组装任何未存储在决策逻辑中但 [!DNL Customer Profile] 可能被决策逻辑使用的上下文数据。

决策逻辑由活动组织，每个活动指定应为此考虑的选项子集的过滤器，以及单个回退选项。

通过首先应用约束来减少选项的数量，然后对剩余的选项进行排序来做出每个决策。 尽管大部分逻辑都在内部 [!DNL Decisioning Service]进行评估，但是各种附属服务都用于帮助这两个方面。 例如，限制服务管理选项在任何决策中使用的频率的上界，而另一服务可承载用于计算用户档案和选项得分的机器学习模型。

要进一步了解如何使用存储库API，请参阅有关使用API [管理决策实体和规则的教程](./tutorials/entities.md)

要进一步了解如何使 [!DNL Decisioning Service] 用运行时，请参 [阅关于使用API使用决策服务运行时的教程](./tutorials/runtime.md)