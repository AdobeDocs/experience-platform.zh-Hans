---
title: 实时客户个人资料数据和分段的默认护栏
solution: Experience Platform
product: experience platform
type: Documentation
description: 了解配置文件数据和分段的性能和系统强制护栏，以确保充分使用 Real-Time CDP 功能。
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: c7537959b1cc53998acafbccaa2f39686afd9f15
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 2%

---

# 默认护栏 [!DNL Real-Time Customer Profile] 数据和分段

Adobe Experience Platform允许您以实时客户配置文件的形式，根据行为见解和客户属性提供个性化的跨渠道体验。 为了支持这种新的配置文件方法，Experience Platform使用与传统关系数据模型不同的高度非规范化混合数据模型。

本文档提供了默认的使用和速率限制，帮助您为配置文件数据建模以获得最佳系统性能。 查看以下护栏时，假定您已正确建模数据。 如果您对如何建立数据模型有疑问，请联系您的客户服务代表。

>[!NOTE]
>
>大多数客户不会超过这些默认限制。 如果您想了解自定义限制，请联系您的客户关怀代表。

## 快速入门

实时客户档案数据建模涉及以下Experience Platform服务：

* [[!DNL Real-Time Customer Profile]](home.md)：使用来自多个源的数据创建统一的使用者配置文件。
* [身份](../identity-service/home.md)：在身份被摄取到Platform中时桥接来自不同数据源的身份。
* [架构](../xdm/home.md)：体验数据模型(XDM)架构是Platform用于组织客户体验数据的标准化框架。
* [受众](../segmentation/home.md)：Platform中的分段引擎用于根据客户行为和属性，从客户配置文件中创建受众。

## 限制类型

此文档有两种类型的默认限制：

| 护栏类型 | 描述 |
|----------|---------|
| **性能护栏（软限制）** | 性能护栏是与用例范围相关的使用限制。 当超出性能护栏时，您可能会遇到性能下降和延迟问题。 Adobe不对此类性能下降负责。 始终超过性能护栏的客户可以选择许可额外的容量，以避免性能下降。 |
| **系统强制的护栏（硬限制）** | Real-Time CDP UI或API强制实施系统强制的护栏。 这些限制不得超过，因为UI和API将阻止您这样做或您会返回错误。 |

{style="table-layout:auto"}

>[!NOTE]
>
>本文档中概述的限制不断得到改进。 请定期查看以获取最新信息。 如果您有兴趣了解自定义限制，请联系您的客户关怀代表。

## 数据模型限制

在为实时客户个人资料数据建模时，以下护栏提供了建议的限制。 要了解有关主要实体和维度实体的更多信息，请参阅 [实体类型](#entity-types) 在附录中。

![一个图表，显示了Adobe Experience Platform中配置文件数据的各种护栏。](./images/guardrails/profile-guardrails.png)

### 主实体护栏

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| XDM个人资料类数据集 | 20 | 性能护栏 | 建议最多使用20个利用XDM个人资料类的数据集。 |
| XDM ExperienceEvent类数据集 | 20 | 性能护栏 | 建议最多使用20个利用XDM ExperienceEvent类的数据集。 |
| 为配置文件启用的Adobe Analytics报表包数据集 | 1 | 性能护栏 | 应为配置文件启用最多一(1)个Analytics报表包数据集。 尝试为配置文件启用多个Analytics报表包数据集可能会对数据质量产生意想不到的后果。 有关更多信息，请参阅以下部分： [Adobe Analytics数据集](#aa-datasets) 在附录中。 |
| 多实体关系 | 5 | 性能护栏 | 建议在主要实体和维度实体之间最多定义5个多实体关系。 在删除或禁用现有关系之前，不应进行其他关系映射。 |
| 多实体关系中使用的ID字段的JSON深度 | 4 | 性能护栏 | 对于在多实体关系中使用的ID字段，建议的最大JSON深度为4。 这意味着在高度嵌套的架构中，超过4级嵌套的字段不应用作关系中的ID字段。 |
| 配置文件片段中的数组基数 | &lt;=500 | 性能护栏 | 配置文件片段（与时间无关的数据）中的最佳数组基数&lt;=500。 |
| ExperienceEvent中的数组基数 | &lt;=10 | 性能护栏 | ExperienceEvent（时间序列数据）中的最佳数组基数&lt;=10。 |
| 个人配置文件身份图的身份计数 | 50 | 系统强制的护栏 | **单个配置文件的身份图中的最大身份数为50。** 任何标识超过50的用户档案都将从分段、导出和查找中排除。 |

{style="table-layout:auto"}

### Dimension实体护栏

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 不允许对以下对象使用时间序列数据：[!DNL XDM Individual Profile] 实体 | 0 | 系统强制的护栏 | **时序数据不允许用于非[!DNL XDM Individual Profile] 配置文件服务中的实体。** 如果时间序列数据集与非[!DNL XDM Individual Profile] ID，不应为以下项启用数据集 [!DNL Profile]. |
| 无嵌套关系 | 0 | 性能护栏 | 您不应在两个非[!DNL XDM Individual Profile] 模式。 不建议将创建关系的功能用于任何不属于的架构 [!DNL Profile] 合并架构。 |
| 主ID字段的JSON深度 | 4 | 性能护栏 | 主ID字段建议的最大JSON深度为4。 这意味着，在高度嵌套的架构中，如果某个字段嵌套的深度超过4级，则不应选择该字段作为主ID。 第4个嵌套级别的字段可用作主ID。 |

{style="table-layout:auto"}

## 数据大小限制

以下护栏参考数据大小，并根据需要为可以摄取、存储和查询的数据提供建议的限制。 要了解有关主要实体和维度实体的更多信息，请参阅 [实体类型](#entity-types) 在附录中。

>[!NOTE]
>
>数据大小在摄取时以JSON的未压缩数据来测量。

### 主实体护栏

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 最大ExperienceEvent大小 | 10KB | 系统强制的护栏 | **事件的最大大小为10KB。** 将继续引入，但任何大于10 KB的事件将被丢弃。 |
| 最大配置文件记录大小 | 100KB | 系统强制的护栏 | **配置文件记录的最大大小为100KB。** 将继续引入，但大于100 KB的配置文件记录将被丢弃。 |
| 最大配置文件片段大小 | 50MB | 系统强制的护栏 | **单个配置文件片段的最大大小为50MB。** 对于任何报表，分段、导出和查找操作都可能会失败 [配置文件片段](#profile-fragments) 大于50MB。 |
| 最大配置文件存储大小 | 50MB | 性能护栏 | **存储配置文件的最大大小为50MB。** 正在添加 [配置文件片段](#profile-fragments) 到大于50MB的配置文件中将影响系统性能。 例如，配置文件可以包含一个50MB的片段，也可以包含多个数据集的多个片段，组合总大小为50MB。 尝试存储单个片段大于50MB的配置文件，或多个片段的组合大小超过50MB的配置文件将影响系统性能。 |
| 每天摄取的配置文件或ExperienceEvent批次数 | 90 | 性能护栏 | **每天摄取的Profile或ExperienceEvent批次的最大数量为90。** 这意味着每天摄取的Profile和ExperienceEvent批次总数不能超过90。 摄取其他批次将影响系统性能。 |
| 每个配置文件记录的ExperienceEvents数 | 5000 | 性能护栏 | **每个配置文件记录的ExperienceEvents最大数量为5000。** 超过5000个ExperienceEvents的用户档案将 **非** 应考虑进行分段。 |

{style="table-layout:auto"}

### Dimension实体护栏

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 所有维实体的总大小 | 5GB | 性能护栏 | 建议所有维度实体的总大小为5GB。 摄取大尺寸实体可能会影响系统性能。 例如，不建议尝试将10GB的产品目录加载为维度实体。 |
| 每个维度实体架构的数据集 | 5 | 性能护栏 | 建议最多5个与每个维度实体架构关联的数据集。 例如，如果您为“产品”创建架构，并添加五个参与数据集，则不应创建与产品架构绑定的第六个数据集。 |
| 每日摄取的Dimension实体批次 | 每个实体4个 | 性能护栏 | 建议每天摄取的维度实体批次的最大数量为每个实体4个。 例如，您每天最多可以摄取4次产品目录的更新。 为同一实体摄取其他维度实体批次可能会影响系统性能。 |

{style="table-layout:auto"}

## 分段护栏 {#segmentation-guardrails}

此部分中概述的护栏是指组织可以在Experience Platform中创建的受众的数量和性质，以及映射和激活受众到目标。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每个沙盒的受众 | 4000 | 性能护栏 | 一个组织总共可以有4000多个受众，前提是每个沙盒中的受众少于4000个。 尝试创建其他受众可能会影响系统性能。 详细了解 [创建受众](/help/segmentation/ui/segment-builder.md) 通过区段生成器。 |
| 每个沙盒的Edge受众 | 150 | 性能护栏 | 只要每个沙盒中的边缘受众少于150个，组织就可以总共拥有150个以上的边缘受众。 尝试创建其他Edge受众可能会影响系统性能。 详细了解 [Edge受众](/help/segmentation/ui/edge-segmentation.md). |
| 每个沙盒的流受众 | 500 | 性能护栏 | 一个组织总共可以有500多个流受众，前提是每个沙盒中的流受众少于500个。 尝试创建其他流受众可能会影响系统性能。 详细了解 [流受众](/help/segmentation/ui/streaming-segmentation.md). |
| 每个沙盒的批量受众 | 4000 | 性能护栏 | 一个组织总共可以有4000多个批次受众，前提是每个沙盒中的批次受众少于4000个。 尝试创建其他批处理受众可能会影响系统性能。 |
| 每个沙盒的帐户受众 | 50 | 系统强制的护栏 | 在一个沙盒中最多可创建50个帐户受众。 在一个沙盒中达到50个受众之后， **[!UICONTROL 创建受众]** 在尝试创建新帐户受众时，将禁用控件。 详细了解 [帐户受众](/help/segmentation/ui/account-audiences.md). |
| 每个沙盒已发布的合成 | 10 | 性能护栏 | 一个沙盒中最多可以有10个已发布的合成。 详细了解 [UI指南中的受众构成](/help/segmentation/ui/audience-composition.md). |
| 最大受众规模 | 30% | 性能护栏 | 建议的最大受众成员数为系统中配置文件总数的30%。 将超过30%的用户档案创建为成员或多个大型受众是可行的，但将影响系统性能。 |

{style="table-layout:auto"}

## 附录

本节提供了有关本文档中限制的其他详细信息。

### 实体类型

此 [!DNL Profile] 存储数据模型包含两种核心实体类型： [主要实体](#primary-entity) 和 [维度实体](#dimension-entity).

#### 主要实体

主要实体或个人资料实体将数据合并在一起，形成个人的“单一真实来源”。 此统一数据使用所谓的“联合视图”来表示。 联合视图将实施相同类的所有架构的字段聚合到单个联合架构中。 的合并架构 [!DNL Real-Time Customer Profile] 是一个非规范化的混合数据模型，充当所有配置文件属性和行为事件的容器。

独立于时间的属性（也称为“记录数据”）使用进行建模 [!DNL XDM Individual Profile]，而时序数据（也称为“事件数据”）则使用进行建模 [!DNL XDM ExperienceEvent]. 当在Adobe Experience Platform中摄取记录和时间序列数据时，将触发 [!DNL Real-Time Customer Profile] 开始摄取已启用的数据。 引入的交互和详细信息越多，个人资料就越可靠。

![概述记录数据与时间序列数据之间差异的信息图表。](images/guardrails/profile-entity.png)

#### Dimension实体

虽然维护用户档案数据的用户档案数据存储不是关系存储，但用户档案允许与小型维度实体集成，以便以简化且直观的方式创建受众。 此集成称为 [多实体分割](../segmentation/multi-entity-segmentation.md).

您的组织还可以定义XDM类来描述个人以外的其他内容，如商店、产品或资产。 此等非[!DNL XDM Individual Profile] 架构称为“维度实体”（也称为“查找实体”），不包含时间序列数据。 表示维度实体的架构通过使用 [架构关系](../xdm/tutorials/relationship-ui.md).

Dimension实体提供查找数据，这有助于并简化多实体区段定义，并且必须足够小，以便分段引擎可以将整个数据集加载到内存中以进行最佳处理（快速点查找）。

![显示配置文件图元由尺寸图元组成的信息图。](images/guardrails/profile-and-dimension-entities.png)

### 配置文件片段

在本文档中，有多个护栏称为“配置文件片段”。 在Experience Platform中，多个配置文件片段合并在一起，形成Real-time Customer Profile。 每个片段表示给定数据集中该ID的唯一主标识以及相应的记录或完整的事件数据集。 要了解有关配置文件片段的更多信息，请参阅 [配置文件概述](home.md#profile-fragments-vs-merged-profiles).

### 合并策略 {#merge-policies}

将来自多个来源的数据集合在一起时，合并策略是Platform用来确定数据优先顺序的规则以及将合并哪些数据以创建该统一视图。 例如，如果客户跨多个渠道与您的品牌互动，则您的组织将在多个数据集中显示多个与该单个客户相关的配置文件片段。 将这些片段摄取到Platform后，会合并在一起，以便为该客户创建一个配置文件。 当来自多个源的数据发生冲突时，合并策略会确定个人配置文件中要包含哪些信息。 每个组织最多允许五(5)个合并策略。 要了解有关合并策略的更多信息，请阅读 [合并策略概述](merge-policies/overview.md).

### Platform中的Adobe Analytics报表包数据集 {#aa-datasets}

只需解决所有数据冲突，即可为配置文件启用多个报表包。 您可以使用数据准备功能解决eVar、列表和Prop之间的数据冲突。 要了解有关如何使用数据准备功能的更多信息，请参阅 [Adobe Analytics连接器用户界面指南](../sources/tutorials/ui/create/adobe-applications/analytics.md).

## 后续步骤

请参阅Real-Time CDP产品描述文档中的以下文档，了解有关其他Experience Platform服务护栏、端到端延迟信息和许可信息的更多信息：

* [Real-Time CDP护栏](/help/rtcdp/guardrails/overview.md)
* [端到端延迟图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 用于各种Experience Platform服务。
* [Real-time Customer Data Platform （B2C版本 — Prime和Ultimate包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2P — 主要和最终包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B - Prime和Ultimate包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
