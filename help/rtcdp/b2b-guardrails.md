---
keywords: 配置文件；实时客户配置文件；故障诊断；护栏；准则；限制；实体；主实体；维度实体；RTCDP;CDP;B2B Edition;Real-time Customer Data Platform；实时客户数据平台；实时CDP;b2b;CDP;
title: Real-time Customer Data Platform B2B版的默认护栏
type: Documentation
description: Adobe Experience Platform 使用与传统关系数据模型不同的高度非规范化混合数据模型。本文档提供了默认使用和速率限制，以帮助您使用Real-time Customer Data Platform B2B Edition为数据建模以获得最佳系统性能。
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 2%

---

# Real-time Customer Data Platform B2B版的默认护栏

>[!NOTE]
>
>本文档中概述的限制表示Real-time Customer Data Platform B2B Edition启用的更改。 有关Real-time CDP B2B Edition默认限制的完整列表，请将这些限制与 [实时客户资料数据文档的防护](../profile/guardrails.md).

Real-time Customer Data Platform B2B Edition使您能够以实时客户配置文件和帐户配置文件的形式，根据行为分析和客户属性提供个性化的跨渠道体验。 为了支持这种新的用户档案方法，Experience Platform使用了与传统关系数据模型不同的高度异常化混合数据模型。

本文档提供默认使用和费率限制，以帮助您为数据建模以获得最佳系统性能。 在查看以下护栏时，我们假定您已正确建模数据。 如果您对如何建立数据模型有任何疑问，请联系您的客户服务代表。

>[!INFO]
>
>大多数客户未超出这些默认限制。 如果您想了解自定义限制，请联系您的客户关怀代表。

## 限制类型

本文档中有两种类型的默认限制：

* **软限制：** 可以超出软限制，但软限制为系统性能提供了建议的准则。

* **硬限制：** 硬限制提供绝对最大值。

>[!INFO]
>
>本文档中概述的限制正在不断改进。 请定期查看以获取最新信息。 如果您有兴趣了解自定义限制，请联系您的客户关怀代表。

## 数据模型限制

以下护栏在对实时客户资料数据进行建模时提供了建议的限制。 要了解有关主要实体和维度实体的更多信息，请参阅 [实体类型](#entity-types) 中。

### 主实体护栏

>[!NOTE]
>
>本节中概述的数据模型限制表示Real-time Customer Data Platform B2B Edition启用的更改。 有关Real-time CDP B2B Edition默认限制的完整列表，请将这些限制与 [实时客户资料数据文档的防护](../profile/guardrails.md).

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| Real-time CDP B2B Edition标准XDM类数据集 | 60 | 柔和 | 建议最多60个数据集利用由Real-time CDP B2B Edition提供的标准Experience Data Model(XDM)类。 有关B2B用例的标准XDM类的完整列表，请参阅 [实时CDP B2B Edition文档中的模式](schemas/b2b.md). <br/><br/>*注意：由于Experience Platform异常混合数据模型的性质，大多数客户并未超过此限制。 如果您对如何建立数据模型存有疑问，或者希望了解有关自定义限制的更多信息，请联系您的客户关怀代表。* |
| 旧版多实体关系 | 20 | 柔和 | 建议在主要实体和维度实体之间最多定义20个多实体关系。 在删除或禁用现有关系之前，不应进行其他关系映射。 |
| 每个XDM类的多对一关系 | 2 | 柔和 | 建议每个XDM类最多定义2个多对一关系。 在删除或禁用现有关系之前，不应建立其他关系。 有关如何创建两个模式之间关系的步骤，请参阅 [定义B2B模式关系](../xdm/tutorials/relationship-b2b.md). |

### Dimension实体护栏

>[!NOTE]
>
>本节中概述的数据模型限制表示Real-time Customer Data Platform B2B Edition启用的更改。 有关Real-time CDP B2B Edition默认限制的完整列表，请将这些限制与 [实时客户资料数据文档的防护](../profile/guardrails.md).

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 无嵌套的旧关系 | 0 | 柔和 | 您不应在两个非[!DNL XDM Individual Profile] 模式。 对于不属于 [!DNL Profile] 并集模式。 |
| 只有B2B对象可以参与多对一关系 | 0 | 硬 | 该系统仅支持B2B对象之间的多对一关系。 有关多对一关系的更多信息，请参阅 [定义B2B模式关系](../xdm/tutorials/relationship-b2b.md). |
| B2B对象之间嵌套关系的最大深度 | 3 | 硬 | B2B对象之间嵌套关系的最大深度为3。 这意味着在高度嵌套的架构中，B2B对象之间不应存在深度超过3级的关系。 |

## 数据大小限制

以下护栏引用了数据大小，并对可以按预期摄取、存储和查询的数据提供了建议的限制。 要了解有关主要实体和维度实体的更多信息，请参阅 [实体类型](#entity-types) 中。

>[!INFO]
>
>摄取时，数据大小以JSON中的未压缩数据衡量。

### 主实体护栏

>[!NOTE]
>
>本节中概述的数据大小限制表示Real-time Customer Data Platform B2B Edition启用的更改。 有关Real-time CDP B2B Edition默认限制的完整列表，请将这些限制与 [实时客户资料数据文档的防护](../profile/guardrails.md).

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每天按XDM类摄取的批次数 | 45 | 柔和 | 每个XDM类每天摄取的批次总数不得超过45个。 摄取其他批次可能会阻止最佳性能。 |

### Dimension实体护栏

>[!NOTE]
>
>本节中概述的数据大小限制表示Real-time Customer Data Platform B2B Edition启用的更改。 有关Real-time CDP B2B Edition默认限制的完整列表，请将这些限制与 [实时客户资料数据文档的防护](../profile/guardrails.md).

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 所有维实体的总大小 | 5 GB | 柔和 | 所有维度实体的建议总大小为5GB。 摄取大维度实体可能会影响系统性能。 例如，不建议尝试将10GB产品目录作为维度实体进行加载。 |
| 每维实体架构的数据集 | 5 | 柔和 | 建议最多5个与每个维度实体架构关联的数据集。 例如，如果为“产品”创建架构并添加五个贡献数据集，则不应创建与产品架构绑定的第六个数据集。 |
| Dimension实体每天摄取的批次 | 每个实体4个 | 柔和 | 建议每天摄取的维度实体批次数上限为每个实体4个。 例如，您每天最多可以摄取4次产品目录更新。 为同一实体摄取其他维度实体批可能会影响系统性能。 |

## 分段护栏

本节中概述的防护是指组织在Experience Platform内可创建的区段的数量和性质，以及将区段映射和激活到目标的过程。

>[!NOTE]
>
>本节中概述的分段限制表示Real-time Customer Data Platform B2B Edition启用的更改。 有关Real-time CDP B2B Edition默认限制的完整列表，请将这些限制与 [实时客户资料数据文档的防护](../profile/guardrails.md).

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每个B2B沙盒的区段 | 400 | 柔和 | 一个组织总共可以有400个以上的区段，但前提是每个B2B沙盒中的区段少于400个。 尝试创建其他区段可能会影响系统性能。 |

## 后续步骤

本文档中概述的限制表示Real-time Customer Data Platform B2B Edition启用的更改。 有关Real-time CDP B2B Edition默认限制的完整列表，请将这些限制与 [实时客户资料数据文档的防护](../profile/guardrails.md).

## 附录

本节提供了本文档中限制的其他详细信息。

### 实体类型

的 [!DNL Profile] 存储数据模型由两种核心实体类型组成：

* **主要实体：** 主实体或用户档案实体可将数据合并在一起，为个人形成“单一真相来源”。 此统一数据使用称为“并集视图”的表示。 并集视图将实现同一类的所有架构的字段聚合到单个并集架构中。 的并集架构 [!DNL Real-time Customer Profile] 是一个非规范的混合数据模型，充当所有配置文件属性和行为事件的容器。

   与时间无关的属性（也称为“记录数据”）使用 [!DNL XDM Individual Profile]，而时间系列数据（也称为“事件数据”）则使用 [!DNL XDM ExperienceEvent]. 在Adobe Experience Platform中摄取记录和时间系列数据时，会触发 [!DNL Real-time Customer Profile] 开始摄取已启用供其使用的数据。 摄取的交互和详细信息越多，个人用户档案就越可靠。

   ![](../profile/images/guardrails/profile-entity.png)

* **Dimension实体：** 虽然配置文件数据存储维护配置文件数据不是关系存储，但配置文件允许与小维度实体集成，以便以简单直观的方式创建区段。 此集成称为 [多实体分段](../segmentation/multi-entity-segmentation.md). 贵组织还可以定义XDM类来描述个人以外的其他内容，如商店、产品或资产。 这些非[!DNL XDM Individual Profile] 架构称为“维实体”，不包含时间系列数据。 Dimension实体提供查找数据，这有助于并简化多实体区段定义，并且必须足够小，以便分段引擎能够将整个数据集加载到内存中，以实现最佳处理（快速点查找）。

   ![](../profile/images/guardrails/profile-and-dimension-entities.png)
