---
keywords: Experience Platform；主页；热门主题；分段；分段；分段；段服务；段；段；段；段；段
solution: Experience Platform
title: 分段服务概述
topic: 概述
description: 了解Adobe Experience Platform Segmentation Service及其在平台生态系统中的作用。
translation-type: tm+mt
source-git-commit: 738256021fb583e7dc14fd33f5df193813a6e0bb
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---


# [!DNL Segmentation Service]概述

Adobe Experience Platform [!DNL Segmentation Service]提供了用户界面和RESTful API，使您能够根据[!DNL Real-time Customer Profile]数据构建区段和生成受众。 这些区段在[!DNL Platform]上集中配置和维护，任何Adobe解决方案都可随时访问。

本文档概述了[!DNL Segmentation Service]及其在Adobe Experience Platform中所起的作用。

## [!DNL Segmentation Service]入门

了解本文档中使用的以下主要术语非常重要：

- **细分**:将一大群人(如客户、潜在客户、用户或组织)划分为具有相似特征且响应类似营销策略的较小群组。
- **细分定义**:用于描述目标受众的关键特性或行为的规则集。概念化后，区段定义中概述的规则用于确定某个区段的合格受众成员。
- **受众**:最终的一组符合区段定义条件的用户档案。

## 细分的工作原理

分段是定义由用户档案子集从用户档案库共享的特定属性或行为的过程，以区分有价人群和客户群。 例如，在名为“您忘记购买运动鞋了吗？”的电子邮件活动中，您可能希望受众过去30天内搜索跑鞋但未完成购买的所有用户。

在概念上定义区段后，会在[!DNL Experience Platform]中构建该区段。 通常，细分由营销人员或受众专家构建，但某些组织希望由其营销部门与数据分析师协作创建。 在查看发送到[!DNL Platform]的数据时，数据分析师通过选择将用于构建区段规则或条件的字段和值来组合区段定义。 这是使用UI或API完成的。

## 创建区段

无论是使用API创建还是使用[!DNL Segment Builder]创建，区段最终都是使用[!DNL Profile Query Language](PQL)定义的。 在这里，概念区段定义将用构建的语言进行描述，以检索满足标准的用户档案。 有关详细信息，请参阅[ PQL概述](./pql/overview.md)。

要了解如何在[!DNL Segment Builder]（[!DNL Segmentation Service]的UI实现）中创建和使用区段，请参阅[区段生成器指南](./ui/overview.md)。

有关使用API构建区段定义的信息，请参阅有关使用API](./tutorials/create-a-segment.md)创建受众区段的教程。[

>[!NOTE]
>
>在扩展模式的事件中，所有将来的上载必须相应地更新新添加的字段。 有关自定义[!DNL Experience Data Model](XDM)的详细信息，请访问[模式编辑器教程](../xdm/tutorials/create-schema-ui.md)。

## 评估区段

平台目前支持两种评估细分的方法：流分段和批分段。

### 流细分

流细分是一个持续不断的数据选择过程，可根据用户活动更新细分。 在构建并保存区段后，会将区段定义应用于传入数据至[!DNL Real-time Customer Profile]。 我们会定期处理细分增加和删除，以确保您的目标受众保持相关。

要了解有关流分段的更多信息，请阅读[流分段文档](./api/streaming-segmentation.md)。

### 批分段

作为当前用户档案选择流程的替代方法，批处理分段通过段定义一次移动所有受众数据以生成相应的数据。 创建后，会保存并存储此区段，以便您导出该区段以供使用。

使用批细分评估的区段每24小时进行评估。 但是，对于现有区段，增量细分使用最新的批细分功能使区段评估保持长达一小时。 任何新的或最近修改的区段都需要等到运行下一个完全批量分段作业才能利用增量分段。

要了解如何评估区段，请参阅[区段评估教程](./tutorials/evaluate-a-segment.md)。

### 边缘分割

边缘细分是指在Platform中即时评估边缘区段的能力，支持相同页面和下一页个性化使用案例。

要了解有关边缘分割的更多信息，请阅读[API文档](./api/edge-segmentation.md)或[UI文档](./ui/edge-segmentation.md)。

## 访问分段结果

要了解如何访问导出的区段，请参阅[区段评估教程](./tutorials/evaluate-a-segment.md)。

## 区段元数据

区段元数据有助于在事件中建立索引，您的任何区段都会被重复使用和/或组合。

通过API或[!DNL Segment Builder]合成区段需要定义区段名称并合并策略。

### 区段名称

创建新区段时，您需要提供区段名称。 段名称用于标识由[!DNL Segmentation Service]构建的集合中的特定段。 因此，区段名称应具有描述性、简洁性和唯一性。

>[!NOTE]
>
>在规划区段时，请记住，区段可以从任何其他区段引用，并与之组合。 在选择名称时，请考虑您的区段可能包含可重用部分。

### 合并策略

合并策略是[!DNL Profile]使用的规则，用于确定在某些条件下如何对数据进行优先排序并合并为统一视图。
如果未定义合并策略，则使用默认的[!DNL Platform]合并策略。 如果您希望使用特定于您的组织的合并策略，您可以创建自己的策略并将其标记为您的组织的默认策略。

有关合并策略的详细信息，请参阅[合并策略指南](../profile/api/merge-policies.md)。

>[!NOTE]
>
>受众大小的估计基于组织的默认用户档案合并策略。

### 其他区段元数据

除了区段名称和合并策略之外，[!DNL Segment Builder]还为您优惠了一个额外的“区段描述”元数据字段，您可以从中总结区段定义的用途。

## 高级细分功能

通过将[流数据摄取](../ingestion/streaming-ingestion/overview.md)与以下任何高级细分功能组合，可将细分配置为持续不断地生成受众:
- [顺序分段](#sequential)
- [动态细分](#dynamic)
- [多实体细分](#multi-entity)

以下部分将更详细地讨论这些高级功能。

## 顺序分段{#sequential}

标准的用户旅程本质上是连续的。 Adobe Experience Platform允许您定义一系列有序的细分，以反映此旅程，从而在发生事件序列时捕获这些序列。 可以使用[!DNL Segment Builder]中的可视事件时间轴将事件排列到所需顺序。

需要按顺序细分的客户旅程示例包括产品视图>产品添加>结帐>无购买。

## 动态分段{#dynamic}

动态细分解决了营销人员在为营销活动构建细分时传统上面临的可扩展性问题。

与静态分段不同，动态分段要求您显式并重复捕获每个可能的用例，动态分段使用变量来构建规则逻辑并动态表达关系。

### 用例：寻找在本国以外购买产品的客户

为了说明此高级细分功能的价值，请考虑一位与营销人员协作的数据架构师，以确定在本国以外购买产品的客户。

**问题**

静态分段要求您定义具有唯一家庭状态属性的单个细分，然后筛选不等于家庭状态的购买事件。 此类别的明确部分将写成“我正在寻找来自犹他州的人，他们的购买状态不是犹他州”。 使用此方法创建受众需要为每个美国州定义一个区段，总共为50个区段。

由于缩放时不可避免地会出现不同的细分组合，因此静态细分所需的手动过程变得更加耗时，从而降低了整体效率。

**解决方案**

通过为购买状态属性分配变量，您的动态细分可以简化，以便“在购买状态不等于客户家庭状态的情况下查找购买”。 这样，您就可以将50个静态细分合并到单个动态细分中。

## 多实体分段{#multi-entity}

利用高级多实体细分功能，您可以根据产品、商店或其他非人（也称为“维”实体）使用额外数据扩展[!DNL Real-time Customer Profile]数据。 因此，[!DNL Segmentation Service]在区段定义期间可以访问其他字段，就像它们是[!DNL Profile]数据存储的本机字段一样。 多实体细分在根据与您的独特业务需求相关的数据识别受众时提供了灵活性。 有关包括用例和工作流在内的详细信息，请参阅[多实体分段指南](multi-entity-segmentation.md)。

## [!DNL Segmentation Service] 数据类型

[!DNL Segmentation Service] 支持各种简单而复杂的数据类型。在[支持的数据类型指南](./data-types.md)中可以找到包括支持的数据类型列表在内的详细信息。

## 后续步骤

[!DNL Segmentation Service] 提供了一个整合的工作流，用于根据数据构建 [!DNL Real-time Customer Profile] 区段。总而言之：

- [!DNL Segmentation] 是从用户档案库定义用户档案子集的过程，允许您描述所需可销售组的行为或属性。[!DNL Segmentation Service] 使这一过程成为可能。
- 在规划区段时，请记住，区段可以从任何其他区段中引用，并与之组合。
- 区段可以基于用户档案数据、相关时间序列数据或两者的规则构建。
- 区段可以按需评估，也可以连续评估。 在按需评估时，所有用户档案数据都会一次通过区段定义。 连续计算时，数据流在进入[!DNL Platform]时通过段定义。

要了解如何在UI中定义区段，请参阅[区段生成器指南](./ui/overview.md)。 有关使用API构建区段定义的信息，请参阅有关使用API](./tutorials/create-a-segment.md)创建区段的教程。[