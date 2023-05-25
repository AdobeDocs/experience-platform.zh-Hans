---
keywords: Experience Platform；主页；热门主题；分段；分段；区段服务；区段；区段；区段；区段
solution: Experience Platform
title: 分段服务概述
description: 了解Adobe Experience Platform Segmentation Service及其在Platform生态系统中的作用。
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 11%

---

# [!DNL Segmentation Service] 概述

Adobe Experience Platform [!DNL Segmentation Service] 提供了一个用户界面和RESTful API，可让您生成区段并生成受众。 [!DNL Real-Time Customer Profile] 数据。 这些区段集中配置并维护于 [!DNL Platform]和可供任何Adobe解决方案轻松访问。

本文档提供了以下内容的概述 [!DNL Segmentation Service] 以及它在Adobe Experience Platform中扮演的角色。

## 快速入门 [!DNL Segmentation Service]

请务必了解本文档中使用的以下关键术语：

- **分段**：将大量个人（例如客户、潜在客户、用户或组织）划分为具有相似特征且对营销策略的响应也相似的较小组。
- **区段定义**：用于描述目标受众的关键特征或行为的规则集。 在概念化后，区段定义中概述的规则将用于确定区段的合格受众成员。
- **Audience**：符合区段定义标准的生成配置文件集。

## 分段的工作方式

分段是定义配置文件存储中由一部分配置文件共享的特定属性或行为的过程，以区分来自您的客户群的可销售人群组。 例如，在名为“您是否忘记购买运动鞋？”的电子邮件营销活动中，您可能希望了解过去30天内搜索跑鞋但未完成购买的所有用户。

在概念上定义区段后，即会内置该区段 [!DNL Experience Platform]. 通常，区段由营销人员或受众专家构建，但有些组织希望区段由其营销部门与其数据分析师协作创建。 在查看要发送到的数据时 [!DNL Platform]，数据分析师通过选择将用于构建区段规则或条件的字段和值来构建区段定义。 可使用UI或API完成此操作。

## 创建区段

无论是使用API还是使用 [!DNL Segment Builder]，最终通过以下方式定义区段： [!DNL Profile Query Language] (PQL)。 这是为检索符合标准的配置文件而构建的语言中描述概念区段定义的地方。 欲了解更多信息，请参见 [PQL概述](./pql/overview.md).

要了解如何在中创建和使用区段 [!DNL Segment Builder] (的UI实现 [!DNL Segmentation Service])，请参见 [Segment Builder指南](./ui/overview.md).

有关使用API构建区段定义的信息，请参阅关于的教程 [使用API创建受众区段](./tutorials/create-a-segment.md).

>[!NOTE]
>
>在扩展架构时，所有未来上传都必须相应地更新新添加的字段。 有关自定义的更多信息 [!DNL Experience Data Model] (XDM)，访问 [架构编辑器教程](../xdm/tutorials/create-schema-ui.md).
>
>此外，如果已在数据集中启用体验事件过期值，这可能会影响所创建区段的成员资格。 请阅读指南： [体验事件过期时间](../profile/event-expirations.md) 有关此功能如何影响分段的更多信息。

## 评估区段 {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="评估方法"
>abstract="Platform 目前支持三种区段评估方法：流式分段、批量分段和边缘分段。"

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="流式评估"
>abstract="流式分段是一个持续的数据选择过程，它会更新区段以响应用户活动。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=zh-Hans" text="通过流式分段近乎实时地评估事件"

Platform 目前支持三种区段评估方法：流式分段、批量分段和边缘分段。

### 流式客户细分 {#streaming}

流式分段是一个持续的数据选择过程，它会更新区段以响应用户活动。构建并保存区段后，区段定义将应用于传入数据 [!DNL Real-Time Customer Profile]. 定期处理区段添加和移除，确保您的目标受众仍然相关。

要了解有关流式客户细分的更多信息，请阅读 [流式分段文档](./api/streaming-segmentation.md).

### 批量分段 {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="批量评估"
>abstract="作为持续数据选择过程的替代方案，批量分段通过区段定义一次性移动所有配置文件数据以产生相应的受众。创建后，区段将保存，以便您能够将其导出以供使用。"

作为持续数据选择过程的替代方案，批量分段通过区段定义一次性移动所有配置文件数据以产生相应的受众。创建后，将保存并存储此区段，以便您可以将其导出以供使用。

每24小时自动评估批处理客户细分。 如果要根据需要评估批段，则可以使用段任务。 要了解有关区段作业的更多信息，请阅读 [区段作业文档](./api/segment-jobs.md).

### 边缘分段 {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="边缘评估"
>abstract="边缘分段能够在 Experience Edge 上即时评估 Platform 中的区段，从而实现同一页和下一页个性化用例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=zh-Hans" text="边缘分段 UI 指南"

边缘分段是在Platform中即时评估区段的能力 [在Experience Edge上](../edge/home.md)，启用同一页面和下一页面个性化用例。

要了解有关边缘分段的更多信息，请阅读 [API文档](./api/edge-segmentation.md) 或 [UI文档](./ui/edge-segmentation.md).

## 访问分段结果

要了解如何访问导出的区段，请参阅 [区段评估教程](./tutorials/evaluate-a-segment.md).

## 区段元数据

区段元数据有助于在重用和/或组合任何区段时进行索引。

构成区段(通过API或 [!DNL Segment Builder])要求您定义区段名称和合并策略。

### 区段名称

创建新区段时，需要提供区段名称。 区段名称用于在生成的集合中标识特定区段 [!DNL Segmentation Service]. 因此，区段名称应具有描述性、简洁且唯一。

>[!NOTE]
>
>在规划区段时，请记住，区段可以从任何其他区段引用并与之结合。 选择名称时，请考虑区段可能包含可重用部分的可能性。

### 合并策略

合并策略是使用的规则 [!DNL Profile] 以确定在特定条件下，如何区分数据的优先级并将其组合到统一视图中。
如果未定义合并策略，则默认为 [!DNL Platform] 使用了合并策略。 如果您希望使用特定于贵组织的合并策略，则可以创建自己的合并策略并将其标记为贵组织的默认值。

有关合并策略的更多信息，请参阅 [合并策略指南](../profile/api/merge-policies.md).

>[!NOTE]
>
>受众规模的估计基于组织的默认配置文件合并策略。

### 其他区段元数据

除了区段名称和合并策略之外， [!DNL Segment Builder] 为您提供额外的“区段描述”元数据字段，您可以在其中概述区段定义的用途。

## 高级分段功能

区段可以配置为通过组合来持续生成受众 [流式数据摄取](../ingestion/streaming-ingestion/overview.md) 具有以下任何高级分段功能：
- [顺序分段](#sequential)
- [动态分段](#dynamic)
- [多实体分段](#multi-entity)

以下各节将更详细地讨论这些高级功能。

## 顺序分段 {#sequential}

标准用户历程本质上是一个连续的过程。 Adobe Experience Platform允许您定义一系列有序的区段来反映此历程，从而在事件发生时捕获事件序列。 您可以使用中的可视化事件时间轴，按所需的顺序排列事件。 [!DNL Segment Builder].

需要顺序分段的客户历程的一个示例是产品查看>产品添加>结账>无购买。

## 动态分段 {#dynamic}

动态分段解决了营销人员在构建营销活动区段时传统上面临的可扩展性问题。

静态分段要求您明确而重复地捕获每个可能的使用案例，而动态分段使用变量来构建规则逻辑并动态表达关系。

### 用例：寻找在其家庭状态之外进行购买的客户

要说明此高级分段功能的价值，请考虑由数据架构师与营销人员协作来识别在家庭状态以外进行购买的客户。

**问题**

静态分段要求您先使用唯一的home状态属性定义各个区段，然后再筛选不等于home状态的购买事件。 此类的明确区段写着：“我正在从犹他州寻找用户，他们的购买状态不是犹他州”。 使用此方法创建受众时，您需要为每个美国州定义一个区段，总共50个区段。

随着规模的扩大，会不可避免地出现不同的区段组合，因此，静态分段所需的手动过程会变得更加耗时，从而降低您的整体效率。

**解决方案**

通过将变量分配给purchase state属性，您的动态区段简化为“在购买状态不等于客户主页状态的情况下查找购买”。 这样，您就可以将50个静态区段合并到一个动态区段中。

## 多实体分段 {#multi-entity}

利用高级多实体分段功能，您可以扩展 [!DNL Real-Time Customer Profile] 包含基于产品、商店或其他非人员（也称为“维度”实体）的附加数据的数据。 因此， [!DNL Segmentation Service] 可在区段定义期间访问其他字段，就好像它们是本地字段一样， [!DNL Profile] 数据存储。 在根据与您的独特业务需求相关的数据确定受众时，多实体分段可提供灵活性。 有关更多信息（包括用例和工作流），请参阅 [多实体分段指南](multi-entity-segmentation.md).

## [!DNL Segmentation Service] 数据类型

[!DNL Segmentation Service] 支持各种原始和复杂的数据类型。 有关详细信息（包括支持的数据类型列表），请参阅 [支持的数据类型指南](./data-types.md).

## 后续步骤

[!DNL Segmentation Service] 提供了一个整合的工作流，用于从中构建区段 [!DNL Real-Time Customer Profile] 数据。 总而言之：

- [!DNL Segmentation] 是从用户档案存储中定义用户档案子集的过程，允许您表征所需可营销组的行为或属性。 [!DNL Segmentation Service] 使这个过程成为可能。
- 在规划区段时，请记住，区段可以从任何其他区段引用并与之结合。
- 区段可以从基于用户档案数据、相关时间序列数据的规则构建，也可以从这两者构建。
- 区段可以按需评估，也可以连续评估。 在按需评估时，所有配置文件数据都会一次通过区段定义传递。 连续评估时，数据流在进入时通过区段定义 [!DNL Platform].

要了解如何在UI中定义区段，请参阅 [Segment Builder指南](./ui/overview.md). 有关使用API构建区段定义的信息，请参阅关于的教程 [使用API创建区段](./tutorials/create-a-segment.md).
