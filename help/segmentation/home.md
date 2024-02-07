---
solution: Experience Platform
title: 分段服务概述
description: 了解Adobe Experience Platform分段服务及其在Platform生态系统中发挥的作用。
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 14%

---

# [!DNL Segmentation Service] 概述

Adobe Experience Platform [!DNL Segmentation Service] 提供了一个用户界面和RESTful API，允许您通过区段定义或其他来源创建受众。 [!DNL Real-Time Customer Profile] 数据。 这些受众在 [!DNL Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

本文档概述了 [!DNL Segmentation Service] 以及它在Adobe Experience Platform中发挥的作用。

## [!DNL Segmentation Service] 入门

您应该了解本文档中使用的以下关键术语：

- **分段**：将大量个人（例如客户、潜在客户、用户或组织）划分为具有相似特征且对营销策略的响应也相似的较小组。
- **受众**：一组具有相似行为和/或特征的人。 此人员集合既可以通过Adobe Experience Platform使用区段定义生成（Platform生成的受众），也可以从外部源（外部生成的受众）生成。
- **区段定义**：Adobe Experience Platform用于描述目标受众的关键特征或行为的规则集。

## 分段的工作方式

分段是定义由配置文件存储中的配置文件子集共享的特定属性或行为的过程，以区分可营销的人员组和您的客户群。 例如，在名为“您是否忘记购买运动鞋？”的电子邮件促销活动中，您可能希望受众包含在最近30天内搜索跑鞋但未完成购买的所有用户。

从概念上定义受众后，该受众即内置于 [!DNL Experience Platform]. 通常，受众由营销人员或受众专家构建，但有些组织希望由营销部门与数据分析师合作创建。 在查看要发送到的数据时 [!DNL Platform]，数据分析师可以通过两种方式创建受众 — 通过选择将用于构建受众规则或条件的字段和值来创建区段定义，或通过使用受众构成构成构成受众。

## 创建受众

在 Adob&#x200B;&#x200B;e Experience Platform 上可以通过两种不同的方式创建受众 - 直接组成受众或通过平台派生的区段定义进行创建。

### 受众组合

在Platform上直接合成受众时，可以使用受众合成。 要了解如何使用受众组合创建受众，请参阅 [受众构成指南](./ui/audience-composition.md) 以了解更多信息。

### 区段定义

无论是使用API还是使用 [!DNL Segment Builder]，区段定义最终使用以下方式定义 [!DNL Profile Query Language] (PQL)。 在这里，概念区段定义将以构建用于检索符合条件的用户档案的语言进行描述。 欲了解更多信息，请参见 [PQL概述](./pql/overview.md).

要了解如何在中创建和使用区段，请执行以下操作 [!DNL Segment Builder] (的UI实现 [!DNL Segmentation Service])，请参见 [区段生成器指南](./ui/overview.md).

有关使用API构建区段定义的信息，请参阅关于的教程 [使用API创建区段定义](./tutorials/create-a-segment.md).

>[!NOTE]
>
>在扩展架构时，所有未来上传必须相应地更新新添加的字段。 有关自定义的详细信息 [!DNL Experience Data Model] (XDM)，访问 [架构编辑器教程](../xdm/tutorials/create-schema-ui.md).
>
>此外，如果对数据集启用了体验事件过期值，这可能会影响所创建区段定义的成员资格。 请阅读指南： [体验事件过期时间](../profile/event-expirations.md) 以了解有关此功能如何影响区段的更多信息。

## 评估受众 {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="评估方法"
>abstract="Platform 目前支持三种受众评估方法：流式分段、批量分段和边缘分段。"

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="流式评估"
>abstract="流式分段是一个持续的数据选择过程，会更新受众以响应用户活动。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=zh-Hans" text="通过流式分段近乎实时地评估事件"

Platform 目前支持三种受众评估方法：流式分段、批量分段和边缘分段。

### 流式客户细分 {#streaming}

流式分段是一个持续的数据选择过程，会更新区段以响应用户活动。构建并保存受众后，区段定义将应用于的传入数据 [!DNL Real-Time Customer Profile]. 会定期处理受众的添加和移除操作，确保您的目标受众仍然相关。

要了解有关流式客户细分的更多信息，请阅读 [流式分段文档](./api/streaming-segmentation.md).

### 批次分段 {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="批量评估"
>abstract="作为持续数据选择过程的替代方案，批量分段通过区段定义一次性移动所有配置文件数据以产生相应的受众。创建后，受众将会保存，以便您能够将其导出以供使用。"

作为持续数据选择过程的替代方案，批量分段通过区段定义一次性移动所有配置文件数据以产生相应的受众。创建受众后，将保存并存储生成的受众，以便将其导出以供使用。

每24小时自动评估批次受众。 如果要根据需要评估批受众，则可以使用区段作业。 要了解有关区段作业的更多信息，请阅读 [区段作业文档](./api/segment-jobs.md).

### 边缘分段 {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="边缘评估"
>abstract="边缘分段能够在 Edge Network 上即时评估 Platform 中的区段，从而实现同一页和下一页个性化用例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=zh-Hans" text="边缘分段 UI 指南"

边缘分段是一种在Platform中即时评估区段的能力 [在Edge Network](../edge/home.md)，启用同一页面和下一页面个性化用例。

要了解有关边缘分段的更多信息，请阅读 [API文档](./api/edge-segmentation.md) 或 [UI文档](./ui/edge-segmentation.md).

## 访问分段结果

要了解如何访问导出的受众，请参阅 [区段定义评估教程](./tutorials/evaluate-a-segment.md).

## 区段定义元数据

区段定义元数据有助于在重用和/或合并任何受众时进行索引。

构成区段定义(通过API或 [!DNL Segment Builder])要求您定义名称和合并策略。

### 区段定义名称

创建新区段定义时，需要提供名称。 区段定义名称用于在构建的集合中标识特定区段定义 [!DNL Segmentation Service]. 因此，区段定义名称应具有描述性、简洁性和唯一性。

>[!NOTE]
>
>规划区段定义时，请记住，区段定义可引用并与任何其他区段定义结合使用。 选择名称时，请考虑区段定义可能包含可重用部分的可能性。

### 合并策略

合并策略是使用的规则 [!DNL Profile] 以确定在特定条件下如何区分数据的优先级并将其组合到统一视图中。

如果未定义合并策略，则默认为 [!DNL Platform] 使用了合并策略。 如果您希望使用特定于贵组织的合并策略，则可以创建自己的合并策略并将其标记为贵组织的默认值。

有关合并策略的更多信息，请参阅 [合并策略指南](../profile/api/merge-policies.md).

>[!NOTE]
>
>受众规模的估计基于组织的默认配置文件合并策略。

### 其他区段定义元数据

除了名称和合并策略之外， [!DNL Segment Builder] 为您提供额外的描述元数据字段，您可以在其中概述区段定义的用途。

## 高级分段功能

区段定义可以配置为通过合并来持续生成受众 [流式数据摄取](../ingestion/streaming-ingestion/overview.md) 的任意高级分段功能：
- [顺序分段](#sequential)
- [动态分段](#dynamic)
- [多实体分段](#multi-entity)

以下各节将更详细地讨论这些高级功能。

### 顺序分段 {#sequential}

标准用户历程本质上属于连续过程。 Adobe Experience Platform允许您定义一系列有序的受众来反映此历程，从而捕获事件发生的顺序。 您可以使用中的可视化事件时间轴，按照所需的顺序排列事件。 [!DNL Segment Builder].

例如，需要顺序分段的客户历程包括：产品查看>产品添加>结账>无购买。

### 动态分段 {#dynamic}

动态分段解决了营销人员在为营销活动构建受众时传统上面临的可扩展性问题。

静态分段要求您明确而重复地捕获每个可能的使用案例，而动态分段使用变量来构建规则逻辑并动态表达关系。

要说明此高级分段功能的价值，请考虑由数据架构师与营销人员合作来识别在家庭状态之外进行购买的客户。

静态分段要求您先使用唯一的home状态属性定义各个分段，然后再筛选不等于home状态的购买事件。 这种类型的明确区段定义将为：“我在犹他州寻找购买地不是犹他州的人。” 使用此方法创建受众时，需要您为每个美国州定义一个区段定义，共有50个区段。

随着规模的扩大，会不可避免地出现不同的区段定义组合，因此，静态分段所需的手动过程会变得更加耗时，从而降低您的整体效率。

通过将变量分配给purchase state属性，您的动态区段定义简化为“在购买状态不等于客户住宅状态的情况下查找购买”。 这样，您就可以将50个静态区段合并到一个动态区段定义中。

### 多实体分段 {#multi-entity}

借助高级多实体分段功能，您可以扩展 [!DNL Real-Time Customer Profile] 包含基于产品、商店或其他非人员（也称为“维度”实体）的附加数据的数据。 因此， [!DNL Segmentation Service] 可在区段定义期间访问其他字段，就像它们是本地字段一样 [!DNL Profile] 数据存储。 在根据与您的独特业务需求相关的数据确定受众时，多实体分段可提供灵活性。 有关更多信息（包括用例和工作流），请参阅 [多实体分段指南](multi-entity-segmentation.md).

## [!DNL Segmentation Service] 数据类型

[!DNL Segmentation Service] 支持各种原始和复杂的数据类型。 有关详细信息（包括支持的数据类型列表），请参见 [支持的数据类型指南](./data-types.md).

## 后续步骤

[!DNL Segmentation Service] 提供了一个整合的工作流，用于从中构建受众 [!DNL Real-Time Customer Profile] 数据。

有关使用分段服务UI的更多信息，请阅读 [分段服务UI概述](./ui/overview.md).

要了解如何在UI中组合受众，请参阅 [受众构成指南](./ui/audience-composition.md). 要了解如何在UI中定义区段定义，请参阅 [区段生成器指南](./ui/overview.md). 有关使用API构建区段定义的信息，请参阅关于的教程 [使用API创建区段定义](./tutorials/create-a-segment.md).
