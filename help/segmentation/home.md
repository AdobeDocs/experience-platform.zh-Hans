---
keywords: Experience Platform；主页；热门主题；分段；分段；分段；段服务；段；段；段；段
solution: Experience Platform
title: 分段服务概述
topic: overview
description: 了解Adobe Experience Platform分段服务及其在平台生态系统中的作用。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---


# [!DNL Segmentation Service]概述

Adobe Experience Platform[!DNL Segmentation Service]提供用户界面和RESTful API，使您能够根据[!DNL Real-time Customer Profile]数据构建细分和生成受众。 这些细分在[!DNL Platform]上集中配置和维护，任何Adobe解决方案都可轻松访问。

此文档概述了[!DNL Segmentation Service]及其在Adobe Experience Platform的作用。

## [!DNL Segmentation Service]入门

了解本文档中使用的以下主要术语非常重要：

- **细分**:将大量个人(如客户、潜在客户、用户或组织)划分为具有相似特征并将对营销策略做出类似反应的较小群体。
- **细分定义**:用于描述目标受众的关键特性或行为的规则集。概念化后，使用细分定义中概述的规则确定某个细分的合格受众成员。
- **受众**:生成的一组符合区段定义条件的用户档案。

## 细分的工作原理

分段是定义用户档案子集从用户档案商店共享的特定属性或行为的过程，以区分有价人群和客户群。 例如，在名为“您忘记购买运动鞋吗？”的电子邮件活动中，您可能希望受众过去30天内搜索跑步鞋但未完成购买的所有用户。

在概念上定义区段后，会在[!DNL Experience Platform]中构建它。 通常，细分由营销人员或受众专家构建，但某些组织希望由其营销部门与数据分析师协作创建。 在审核发送到[!DNL Platform]的数据时，数据分析师通过选择将用于构建区段规则或条件的字段和值来组成区段定义。 这是使用UI或API完成的。

## 创建区段

无论是使用API创建还是使用[!DNL Segment Builder]创建，区段最终都是使用[!DNL Profile Query Language](PQL)定义的。 在这里，将在构建用来检索符合标准的用户档案的语言中描述概念段定义。 有关详细信息，请参阅[ PQL概述](./pql/overview.md)。

要了解如何在[!DNL Segment Builder]（[!DNL Segmentation Service]的UI实现）中创建和使用区段，请参阅[区段生成器指南](./ui/overview.md)。

有关使用API构建受众段定义的信息，请参阅教程[使用API](./tutorials/create-a-segment.md)创建数据段。

>[!NOTE]
>
>在扩展事件中，所有将来的上传必须相应更新新添加的字段。 有关自定义[!DNL Experience Data Model](XDM)的详细信息，请访问[模式编辑器教程](../xdm/tutorials/create-schema-ui.md)。

## 评估区段

### 流细分

流细分是一个持续不断的数据选择过程，它会根据用户活动更新细分。 在构建并保存区段后，会将区段定义应用于传入数据至[!DNL Real-time Customer Profile]。 会定期处理细分添加和删除，确保您的目标受众保持相关性。

要进一步了解流分段，请阅读[流分段文档](./api/streaming-segmentation.md)。

### 批分段

作为当前数据选择流程的替代方法，批处理分段通过段定义一次移动所有用户档案数据以生成相应的受众。 创建后，会保存并存储此区段，以便您将其导出以供使用。

要了解如何评估区段，请参阅[区段评估教程](./tutorials/evaluate-a-segment.md)。

## 访问分段结果

要了解如何访问导出的区段，请参阅[区段评估教程](./tutorials/evaluate-a-segment.md)。

## 细分元数据

区段元数据可方便您在事件中重新使用和／或组合任何区段进行索引。

合成区段（通过API或[!DNL Segment Builder]）需要您定义区段名称并合并策略。

### 区段名称

创建新区段时，您需要提供区段名称。 段名称用于标识由[!DNL Segmentation Service]构建的集合中的特定段。 因此，区段名称应具有描述性、简洁性和唯一性。

>[!NOTE]
>
>在规划区段时，请记住，区段可以从任何其他区段进行引用，并与之组合。 在选择名称时，请考虑您的区段是否可能包含可重用部分。

### 合并策略

合并策略是[!DNL Profile]使用的规则，用于确定在某些条件下如何对数据进行优先级排序并合并为一个统一视图。
如果未定义合并策略，则使用默认的[!DNL Platform]合并策略。 如果您希望使用特定于您的组织的合并策略，您可以创建自己的策略并将其标记为您的组织的默认策略。

有关合并策略的详细信息，请参阅[合并策略指南](../profile/api/merge-policies.md)。

>[!NOTE]
>
>受众大小的估计基于组织的默认用户档案合并策略。

### 其他细分元数据

除了区段名称和合并策略之外，[!DNL Segment Builder]还为您优惠了一个额外的“区段描述”元数据字段，您可以在该字段中总结区段定义的用途。

## 高级细分功能

通过将[流数据摄取](../ingestion/streaming-ingestion/overview.md)与以下任何高级细分功能相结合，可将细分配置为持续生成受众:
- [顺序分段](#sequential)
- [动态细分](#dynamic)
- [多实体分割](#multi-entity)

以下各节将更详细地讨论这些高级功能。

## 顺序分段{#sequential}

标准用户旅程本质上是连续的。 Adobe Experience Platform允许您定义一系列有序的细分来反映此旅程，从而在事件发生时捕获序列。 您可以使用[!DNL Segment Builder]中的可视事件时间轴，将事件排列到其所需的顺序。

需要顺序细分的客户旅程的示例包括产品视图>产品添加>结帐>无购买。

## 动态分段{#dynamic}

动态细分解决了营销人员在为营销活动构建细分时通常面临的可伸缩性问题。

与静态分段不同，静态分段要求您显式地重复捕获每个可能的用例，动态分段使用变量来构建规则逻辑并动态地表示关系。

### 用例：寻找在家以外购买产品的客户

要说明此高级细分功能的价值，请考虑一位与营销人员协作的数据架构师，以确定在家以外购买产品的客户。

**问题**

静态分段要求您定义具有唯一家庭状态属性的单独区段，然后筛选不等于家庭状态的购买事件。 此类型的明确部分将写成“我正在寻找犹他州的人，他们的购买状态不是犹他州”。 使用此方法创建受众需要您为每个美国州定义一个区段，总共50个区段。

由于缩放时不可避免地会出现不同的细分组合，因此静态细分所需的手动过程变得更加耗时，从而降低整体效率。

**解决方案**

通过为购买状态属性分配一个变量，您的动态细分可以简化为“在购买状态不等于客户家庭状态的情况下查找购买”。 这样，您就可以将50个静态细分合并到单个动态细分中。

## 多实体分段{#multi-entity}

借助高级的多实体细分功能，您能够根据产品、商店或其他非人（也称为“维”实体）扩展具有附加数据的[!DNL Real-time Customer Profile]数据。 因此，[!DNL Segmentation Service]在段定义期间可以访问其他字段，就像它们是[!DNL Profile]数据存储的本机字段一样。 多实体细分在根据与您独特的业务需求相关的数据识别受众时提供了灵活性。 有关更多信息(包括用例和工作流)，请参阅[多实体分段指南](multi-entity-segmentation.md)。

## [!DNL Segmentation Service] 数据类型

[!DNL Segmentation Service] 支持各种简单和复杂的数据类型。在[支持的数据类型指南](./data-types.md)中可以找到包括受支持数据类型列表在内的详细信息。

## 后续步骤

[!DNL Segmentation Service] 提供了一个整合的工作流，以便根据数据构建 [!DNL Real-time Customer Profile] 区段。总结：

- [!DNL Segmentation] 是从用户档案商店定义用户档案子集的过程，它允许您描述所需可销售组的行为或属性。[!DNL Segmentation Service] 使这一过程成为可能。
- 在规划区段时，请牢记，区段可以从任何其他区段中引用，并与之组合。
- 区段可以基于用户档案数据、相关时间序列数据或两者的规则构建。
- 区段可按需评估或持续评估。 在按需评估时，所有用户档案数据都会一次通过区段定义。 连续评估时，数据流在进入[!DNL Platform]时通过段定义。

要了解如何在UI中定义区段，请参阅[区段生成器指南](./ui/overview.md)。 有关使用API构建段定义的信息，请参阅教程中的[使用API](./tutorials/create-a-segment.md)创建段。