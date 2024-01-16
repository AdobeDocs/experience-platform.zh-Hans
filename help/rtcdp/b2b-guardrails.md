---
keywords: 配置文件；Real-time Customer Profile；故障排除；护栏；准则；限制；实体；主要实体；维度实体；RTCDP；CDP；B2B版本；Real-time Customer Data Platform；real time customer data platform；real time cdp；b2b；cdp；
title: Real-time Customer Data Platform B2B版本的默认护栏
type: Documentation
description: Adobe Experience Platform 使用与传统关系数据模型不同的高度非规范化混合数据模型。本文档提供了默认的使用和速率限制，以帮助您使用Adobe Real-time Customer Data Platform B2B版本为数据建模，以获得最佳系统性能。
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Guardrails, B2B
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 7c455b546b6a98936d60e6cd481cae8610c8be17
workflow-type: tm+mt
source-wordcount: '1675'
ht-degree: 2%

---

# Real-time Customer Data Platform B2B版本的默认护栏

>[!NOTE]
>
>本文档中概述的限制表示由Real-time Customer Data Platform B2B版本启用的更改。 要获取Real-Time CDP Adobe Experience Platform B2B版本的默认限制的完整列表，请将这些限制与 [Real-time Customer Profile数据文档的护栏](../profile/guardrails.md).

Real-time Customer Data Platform B2B Edition允许您以实时客户配置文件和帐户配置文件的形式，根据行为见解和客户属性提供个性化的跨渠道体验。 为了支持这种新的配置文件方法，Experience Platform使用与传统关系数据模型不同的高度非规范化混合数据模型。

本文档提供了默认的使用和速率限制，帮助您建模数据以获得最佳系统性能。 查看以下护栏时，假定您已正确建模数据。 如果您对如何建立数据模型有疑问，请联系您的客户服务代表。

>[!INFO]
>
>大多数客户不会超过这些默认限制。 如果您想了解自定义限制，请联系您的客户关怀代表。

## 限制类型

此文档有两种类型的默认限制：

* **软限制：** 可以超出软限制，但软限制提供了系统性能的推荐准则。

* **硬限制：** 硬限制提供绝对最大值。

>[!INFO]
>
>本文档中概述的限制不断得到改进。 请定期查看以获取最新信息。 如果您有兴趣了解自定义限制，请联系您的客户关怀代表。

## 数据模型限制

在为实时客户个人资料数据建模时，以下护栏提供了建议的限制。 要了解有关主要实体和维度实体的更多信息，请参阅 [实体类型](#entity-types) 在附录中。

### 主实体护栏

>[!NOTE]
>
>本节中概述的数据模型限制表示由Real-time Customer Data Platform B2B版本启用的更改。 要获取Real-Time CDP Adobe Experience Platform B2B版本的默认限制的完整列表，请将这些限制与 [Real-time Customer Profile数据文档的护栏](../profile/guardrails.md).

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| Real-Time CDP B2B版本标准XDM类数据集 | 60 | 柔光 | 建议最大使用Real-Time CDP B2B版本提供的标准Experience Data Model (XDM)类的数据集60个。 有关B2B用例的标准XDM类的完整列表，请参阅 [Real-Time CDP B2B版本文档中的架构](schemas/b2b.md). <br/><br/>*注意：由于Experience Platform的非标准化混合数据模型的性质，大多数客户不会超过此限制。 有关如何为数据建模的问题，或者如果您想了解有关自定义限制的更多信息，请联系您的客户关怀代表。* |
| 旧版多实体关系 | 20 | 柔光 | 建议在主要实体和维度实体之间最多定义20个多实体关系。 在删除或禁用现有关系之前，不应进行其他关系映射。 |
| 每个XDM类的多对一关系 | 2 | 柔光 | 建议每个XDM类最多定义2个多对一关系。 在删除或禁用现有关系之前，不应建立其他关系。 有关如何创建两个架构之间关系的步骤，请参阅关于的教程 [定义B2B架构关系](../xdm/tutorials/relationship-b2b.md). |

### Dimension实体护栏

>[!NOTE]
>
>本节中概述的数据模型限制表示由Real-time Customer Data Platform B2B版本启用的更改。 要获取Real-Time CDP Adobe Experience Platform B2B版本的默认限制的完整列表，请将这些限制与 [Real-time Customer Profile数据文档的护栏](../profile/guardrails.md).

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 无嵌套旧版关系 | 0 | 柔光 | 您不应在两个非[!DNL XDM Individual Profile] 模式。 不建议将创建关系的功能用于任何不属于的架构 [!DNL Profile] 合并架构。 |
| 只有B2B对象可以参与多对一关系 | 0 | 硬 | 系统仅支持B2B对象之间的多对一关系。 有关多对一关系的详细信息，请参阅关于的教程 [定义B2B架构关系](../xdm/tutorials/relationship-b2b.md). |
| B2B对象之间嵌套关系的最大深度 | 3 | 硬 | B2B对象之间嵌套关系的最大深度为3。 这意味着，在高度嵌套的架构中，嵌套超过3级的B2B对象之间不应存在关系。 |
| 每个维度实体有一个架构 | 1 | 硬 | 每个维度实体必须有一个架构。 尝试使用从多个架构创建的维度实体可能会影响分段结果。 不同的维度实体应具有单独的架构。 |

## 数据大小限制

以下护栏参考数据大小，并根据需要为可以摄取、存储和查询的数据提供建议的限制。 要了解有关主要实体和维度实体的更多信息，请参阅 [实体类型](#entity-types) 在附录中。

>[!INFO]
>
>数据大小在摄取时以JSON的未压缩数据来测量。

### 主实体护栏

>[!NOTE]
>
>本节中概述的数据大小限制表示由Real-time Customer Data Platform B2B版本启用的更改。 要获取Real-Time CDP Adobe Experience Platform B2B版本的默认限制的完整列表，请将这些限制与 [Real-time Customer Profile数据文档的护栏](../profile/guardrails.md).

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每天按XDM类摄取的批次 | 45 | 柔光 | 每个XDM类每天摄取的批次总数不应超过45。 摄取额外的批次可能会妨碍最佳性能。 |

### Dimension实体护栏

>[!NOTE]
>
>本节中概述的数据大小限制表示由Real-time Customer Data Platform B2B版本启用的更改。 要获取Real-Time CDP Adobe Experience Platform B2B版本的默认限制的完整列表，请将这些限制与 [Real-time Customer Profile数据文档的护栏](../profile/guardrails.md).

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 所有维实体的总大小 | 5GB | 柔光 | 建议所有维度实体的总大小为5GB。 摄取大尺寸实体可能会影响系统性能。 例如，不建议尝试将10GB的产品目录加载为维度实体。 |
| 每个维度实体架构的数据集 | 5 | 柔光 | 建议最多5个与每个维度实体架构关联的数据集。 例如，如果您为“产品”创建架构，并添加五个参与数据集，则不应创建与产品架构绑定的第六个数据集。 |
| 每日摄取的Dimension实体批次 | 每个实体4个 | 柔光 | 建议每天摄取的维度实体批次的最大数量为每个实体4个。 例如，您每天最多可以摄取4次产品目录的更新。 为同一实体摄取其他维度实体批次可能会影响系统性能。 |

## 分段护栏

本节中概述的护栏是指组织可以在Experience Platform中创建的区段的数量和性质，以及映射和激活区段到目标。

>[!NOTE]
>
>本节中概述的分段限制表示由Real-time Customer Data Platform B2B版本启用的更改。 要获取Real-Time CDP Adobe Experience Platform B2B版本的默认限制的完整列表，请将这些限制与 [Real-time Customer Profile数据文档的护栏](../profile/guardrails.md).

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每个B2B沙盒的区段 | 400 | 柔光 | 只要每个B2B沙盒中的区段少于400个，组织就可以总共拥有超过400个区段。 尝试创建其他区段可能会影响系统性能。 |

## 后续步骤

本文档中概述的限制表示由Real-time Customer Data Platform B2B版本启用的更改。 要获取Real-Time CDP Adobe Experience Platform B2B版本的默认限制的完整列表，请将这些限制与 [Real-time Customer Profile数据文档的护栏](../profile/guardrails.md).

## 附录

本节提供了有关本文档中限制的其他详细信息。

### 实体类型

此 [!DNL Profile] 存储数据模型包含两种核心实体类型： [主要实体](#primary-entity) 和 [维度实体](#dimension-entity).

#### 主要实体

主要实体或个人资料实体将数据合并在一起，形成个人的“单一真实来源”。 此统一数据使用所谓的“联合视图”来表示。 联合视图将实施相同类的所有架构的字段聚合到单个联合架构中。 的合并架构 [!DNL Real-Time Customer Profile] 是一个非规范化的混合数据模型，充当所有配置文件属性和行为事件的容器。

独立于时间的属性（也称为“记录数据”）使用进行建模 [!DNL XDM Individual Profile]，而时序数据（也称为“事件数据”）则使用进行建模 [!DNL XDM ExperienceEvent]. 当在Adobe Experience Platform中摄取记录和时间序列数据时，将触发 [!DNL Real-Time Customer Profile] 开始摄取已启用的数据。 引入的交互和详细信息越多，个人资料就越可靠。

![概述记录数据与时间序列数据之间差异的信息图表。](../profile/images/guardrails/profile-entity.png)

#### Dimension实体

虽然维护用户档案数据的用户档案数据存储不是关系存储，但用户档案允许与小型维度实体集成，以便以简化且直观的方式创建区段。 此集成称为 [多实体分割](../segmentation/multi-entity-segmentation.md).

您的组织还可以定义XDM类来描述个人以外的其他内容，如商店、产品或资产。 此等非[!DNL XDM Individual Profile] 架构称为“维度实体”（也称为“查找实体”），不包含时间序列数据。 表示维度实体的架构通过使用 [架构关系](../xdm/tutorials/relationship-ui.md).

Dimension实体提供查找数据，这有助于并简化多实体区段定义，并且必须足够小，以便分段引擎可以将整个数据集加载到内存中以进行最佳处理（快速点查找）。

![显示配置文件图元由尺寸图元组成的信息图。](../profile/images/guardrails/profile-and-dimension-entities.png)