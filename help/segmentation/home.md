---
keywords: Experience Platform；主页；热门主题；分段；区段；区段服务；区段；区段；区段；区段
solution: Experience Platform
title: Segmentation Service概述
topic-legacy: overview
description: 了解Adobe Experience Platform Segmentation Service及其在平台生态系统中的作用。
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 52197a6c009fb5b0b6037a4fef3c98ad7c327e2e
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 0%

---

# [!DNL Segmentation Service]概述

Adobe Experience Platform [!DNL Segmentation Service] 提供了用户界面和RESTful API，允许您从中构建区段并生成受众 [!DNL Real-time Customer Profile] 数据。 这些区段在上集中配置和维护 [!DNL Platform]，并且任何Adobe解决方案都可随时访问。

本文档提供了 [!DNL Segmentation Service] 以及它在Adobe Experience Platform的作用。

## 入门 [!DNL Segmentation Service]

请务必了解本文档中使用的以下关键术语：

- **分段**:将大量个人（如客户、潜在客户、用户或组织）划分为具有相似特征且将对营销策略做出类似响应的较小组。
- **区段定义**:用于描述目标受众的关键特征或行为的规则集。 概念化后，区段定义中概述的规则将用于确定某个区段的合格受众成员。
- **受众**:生成的一组符合区段定义标准的用户档案。

## 分段的工作原理

分段是定义用户档案库中用户档案子集共享的特定属性或行为的过程，用于将可销售的人群与客户群区分开来。 例如，在名为“您忘记购买运动鞋吗？”的电子邮件促销活动中，您可能希望看到过去30天内搜索跑鞋但未完成购买的所有用户的受众。

在概念上定义区段后，即内置该区段 [!DNL Experience Platform]. 通常，区段由营销人员或受众专家构建，尽管某些组织希望区段由其营销部门与其数据分析人员协作创建。 审核发送到的数据时 [!DNL Platform]，数据分析师通过选择用于构建区段规则或条件的字段和值来组合区段定义。 可使用UI或API完成此操作。

## 创建区段

是使用API创建，还是使用 [!DNL Segment Builder]，区段最终使用 [!DNL Profile Query Language] (PQL)。 在这里，将使用构建的语言描述概念区段定义，以检索符合标准的用户档案。 有关更多信息，请参阅 [PQL概述](./pql/overview.md).

了解如何在 [!DNL Segment Builder] (的UI实施 [!DNL Segmentation Service])，请参阅 [区段生成器指南](./ui/overview.md).

有关使用API构建区段定义的信息，请参阅 [使用API创建受众区段](./tutorials/create-a-segment.md).

>[!NOTE]
>
>如果架构扩展，则所有将来的上载都必须相应地更新新添加的字段。 有关自定义的更多信息 [!DNL Experience Data Model] (XDM)，请访问 [模式编辑器教程](../xdm/tutorials/create-schema-ui.md).
>
>此外，如果数据集上已启用生存时间(TTL)，则这可能会影响已创建区段的成员资格。 有关TTL以及它如何影响分段的更多信息，请阅读 [配置文件服务TTL指南](../profile/apply-ttl.md).

## 评估区段 {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="评价方法"
>abstract="平台当前支持三种评估区段的方法：流分段、批量分段和边缘分段。"

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="流评估"
>abstract="流式客户细分是一种持续的数据选择流程，可根据用户活动更新您的区段。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="使用流分段近乎实时地评估事件"

平台当前支持三种评估区段的方法：流分段、批量分段和边缘分段。

### 流分段 {#streaming}

流式客户细分是一种持续的数据选择流程，可根据用户活动更新您的区段。 生成并保存区段后，会将区段定义应用于 [!DNL Real-time Customer Profile]. 会定期处理区段添加和移除，以确保您的目标受众仍然相关。

要了解有关流式分段的更多信息，请阅读 [流分段文档](./api/streaming-segmentation.md).

### 批量分段 {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="批量评估"
>abstract="作为持续数据选择流程的替代方法，批量分段会通过区段定义一次移动所有配置文件数据以生成相应的受众。 创建区段后，会保存并存储该区段，以便您导出该区段以供使用。"

作为持续数据选择流程的替代方法，批量分段会通过区段定义一次移动所有配置文件数据以生成相应的受众。 创建后，将保存并存储此区段，以便您导出该区段以供使用。

每24小时自动评估一次批量区段。 如果要按需评估批区段，您可以使用区段任务。 要了解有关区段作业的更多信息，请阅读 [区段作业文档](./api/segment-jobs.md).

### 边缘分割 {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="边缘评估"
>abstract="边缘分段功能可以在Experience Edge上即时评估Platform中的区段，从而实现同页和下一页的个性化用例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="边缘分段UI指南"

边缘分割功能可以即时评估Platform中的区段 [在Experience Edge上](../edge/home.md)，启用同页和下一页个性化用例。

要了解有关边缘分割的更多信息，请阅读 [API文档](./api/edge-segmentation.md) 或 [用户界面文档](./ui/edge-segmentation.md).

## 访问分段结果

要了解如何访问导出的区段，请参阅 [区段评估教程](./tutorials/evaluate-a-segment.md).

## 区段元数据

区段元数据有助于在任何区段被重用和/或组合时进行索引。

通过API或 [!DNL Segment Builder])要求您定义区段名称和合并策略。

### 区段名称

创建新区段时，需要提供区段名称。 区段名称用于标识由构建的集合中的特定区段 [!DNL Segmentation Service]. 因此，区段名称应当具有描述性、简洁性和唯一性。

>[!NOTE]
>
>在规划区段时，请记住，可以从任何其他区段中引用区段并将其与之组合。 选择名称时，请考虑区段可能包含可重复使用的部分。

### 合并策略

合并策略是 [!DNL Profile] 确定数据在特定条件下的优先级，并将其合并到统一视图中。
如果未定义合并策略，则默认 [!DNL Platform] 使用合并策略。 如果您希望使用特定于贵组织的合并策略，则可以创建自己的合并策略并将其标记为贵组织的默认策略。

有关合并策略的更多信息，请参阅 [合并策略指南](../profile/api/merge-policies.md).

>[!NOTE]
>
>受众大小的估算基于组织的默认用户档案合并策略。

### 其他区段元数据

除了区段名称和合并策略之外， [!DNL Segment Builder] 提供了一个额外的“区段描述”元数据字段，您可以在该字段中概述区段定义的用途。

## 高级分段功能

可以通过将 [流式数据引入](../ingestion/streaming-ingestion/overview.md) 具有以下任何高级分段功能：
- [顺序分段](#sequential)
- [动态分段](#dynamic)
- [多实体分段](#multi-entity)

以下各节将更详细地讨论这些高级功能。

## 顺序分段 {#sequential}

标准用户历程在性质上是连续的。 Adobe Experience Platform允许您定义一系列有序的区段来反映此历程，从而在事件序列发生时捕获事件序列。 您可以使用 [!DNL Segment Builder].

需要按顺序分段的客户历程示例包括产品查看>产品添加>结账>无购买。

## 动态分段 {#dynamic}

动态分段可解决营销人员在为营销活动构建区段时传统上遇到的可扩展性问题。

与静态分段不同，动态分段要求您明确并重复地捕获每个可能的用例，而动态分段则使用变量来构建规则逻辑并动态表达关系。

### 用例：寻找在本国以外购买产品的客户

为了说明此高级分段功能的价值，请考虑由数据架构师与营销人员协作，以识别在其本地状态以外购买过产品的客户。

**问题**

静态分段要求您先定义具有唯一家庭状态属性的单个区段，然后再筛选不等于家庭状态的购买事件。 此类型的明确部分将显示为“我在犹他州寻找购买地不在犹他州的人”。 使用此方法创建受众时，需要为每个美国州定义一个区段，总共50个区段。

由于缩放时不可避免地会出现不同的区段组合，因此静态分段所需的手动过程会变得更耗时，从而降低整体效率。

**解决方案**

通过将变量分配给购买状态属性，您的动态区段可简化为“查找购买状态不等于客户家庭状态的购买”。 这样，您就可以将50个静态区段合并到单个动态区段中。

## 多实体分段 {#multi-entity}

借助高级多实体分段功能，您可以 [!DNL Real-time Customer Profile] 基于产品、商店或其他非人员（也称为“维度”实体）的附加数据。 因此， [!DNL Segmentation Service] 可以在区段定义期间访问其他字段，就像它们是 [!DNL Profile] 数据存储。 在根据与您的独特业务需求相关的数据确定受众时，多实体分段可提供了更大的灵活性。 有关更多信息（包括用例和工作流），请参阅 [多实体分段指南](multi-entity-segmentation.md).

## [!DNL Segmentation Service] 数据类型

[!DNL Segmentation Service] 支持各种原始和复杂的数据类型。 有关详细信息（包括支持的数据类型列表），请参阅 [支持的数据类型指南](./data-types.md).

## 后续步骤

[!DNL Segmentation Service] 提供了从构建区段的统一工作流 [!DNL Real-time Customer Profile] 数据。 总之：

- [!DNL Segmentation] 是从用户档案库定义用户档案子集的过程，用于表示所需可销售群组的行为或属性。 [!DNL Segmentation Service] 使这个过程成为可能。
- 在规划区段时，请记住，可以从任何其他区段中引用区段并将其与其组合。
- 区段可以基于用户档案数据、相关时间系列数据或两者的规则构建。
- 区段可以按需评估，也可以连续评估。 在按需评估时，所有用户档案数据都会同时通过区段定义进行传递。 连续评估时，数据流在进入时通过区段定义 [!DNL Platform].

要了解如何在UI中定义区段，请参阅 [区段生成器指南](./ui/overview.md). 有关使用API构建区段定义的信息，请参阅 [使用API创建区段](./tutorials/create-a-segment.md).
