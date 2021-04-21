---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；护栏；指导原则；限制；实体；主实体；尺寸实体；
title: 实时客户用户档案数据的保证
solution: Experience Platform
product: experience platform
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform提供了一系列护栏，帮助您避免创建实时客户用户档案无法支持的数据模型。 本文档概述了建模用户档案数据时需要注意的最佳做法和限制。
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 1%

---

# [!DNL Real-time Customer Profile]数据的护栏

[!DNL Real-time Customer Profile] 提供个人用户档案，使您能够根据行为洞察和客户属性提供个性化的跨渠道体验。为了实现此目标，Adobe Experience Platform内的[!DNL Profile]和分段引擎使用高度非规范的混合数据模型，该模型优惠了开发客户用户档案的新方法。 使用这种混合数据模型使得正确建模所收集的数据变得极为重要。 虽然维护用户档案数据的[!DNL Profile]数据存储不是关系存储，[!DNL Profile]允许与小维度实体集成，以便以简化和直观的方式创建段。 此集成称为多实体细分。

Adobe Experience Platform提供了一系列护栏，帮助您避免创建[!DNL Real-time Customer Profile]不支持的数据模型。 本文档概述了在使用用户档案数据进行细分时的这些护栏以及最佳做法和限制。

>[!NOTE]
>
>本文档中概述的护栏和限制正在不断改进。 请定期回访以获取更新。

## 入门指南

建议您在尝试构建数据模型以在[!DNL Real-time Customer Profile]中使用之前阅读以下Experience Platform服务文档。 使用文档模型和本Experience Platform中概述的护栏需要了解与管理[!DNL Real-time Customer Profile]实体相关的各种服务：

* [[!DNL Real-time Customer Profile]](home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [Adobe Experience Platform Identity Service](../identity-service/home.md):在客户被引入时，通过连接来自不同数据源的身份，支持创建“客户的单一视图”  [!DNL Platform]。
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):平台通过该标准化框架组织客户体验数据。
   * [模式合成的基础](../xdm/schema/composition.md):介绍模式和Experience Platform中的数据建模。
* [Adobe Experience Platform Segmentation Service](../segmentation/home.md):中的细分引擎， [!DNL Platform] 用于根据客户行为和属性从用户档案创建受众细分。
   * [多实体细分](../segmentation/multi-entity-segmentation.md):创建将维实体与用户档案数据集成的区段的指南。

## 实体类型

[!DNL Profile]存储数据模型由两个核心实体类型组成：

* **主实体：** 主实体或用户档案实体将数据合并在一起，为个人构成“单一真相源”。此统一数据使用称为“合并视图”的数据表示。 合并视图将实现相同类的所有模式的字段聚合为一个合并模式。 [!DNL Real-time Customer Profile]的合并模式是非规范的混合数据模型，充当所有用户档案属性和行为事件的容器。

   时间无关属性（也称为“记录数据”）使用[!DNL XDM Individual Profile]建模，而时间序列数据(也称为“事件数据”)使用[!DNL XDM ExperienceEvent]建模。 在Adobe Experience Platform中摄取记录和时间序列数据时，它会触发[!DNL Real-time Customer Profile]以开始摄取已启用以供使用的数据。 所摄取的交互和细节越多，单个用户档案就越健壮。

   ![](images/guardrails/profile-entity.png)

* **Dimension实** 体：您的组织还可以定义XDM类来描述个人以外的事物，如商店、产品或属性。这些非[!DNL XDM Individual Profile]模式称为“维实体”，不包含时间序列数据。 Dimension实体提供查找数据，这些数据有助于和简化多实体段定义，并且必须足够小，以便分段引擎能够将整个数据集加载到内存中以进行最佳处理（快速点查找）。

   ![](images/guardrails/profile-and-dimension-entities.png)

## 限制类型

在定义数据模型时，建议保留在提供的护栏内，以确保适当的性能并避免系统错误。 本文档提供的护栏包括两种限制类型：

* **软限制：软** 限制为最佳系统性能提供建议的最大值。在不中断系统或接收错误消息的情况下可以超越软限制，但超越软限制将导致性能降低。 建议保持在软限制内以避免总体性能下降。

* **硬限制：** 硬限制为系统提供绝对最大值。超出硬限制将导致故障和错误，使系统无法按预期运行。

## 数据模型护栏

在创建与[!DNL Real-time Customer Profile]一起使用的数据模型时，建议遵循以下护栏。

### 主要实体护栏

| 瓜德赖尔 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 建议贡献到[!DNL Profile]合并模式的数据集数 | 20 | 柔和 | **建议最多支持 [!DNL Profile]20个数据集。** 要为启用其他数 [!DNL Profile]据集，应首先删除或禁用现有数据集。 |
| 建议的多实体关系数 | 5 | 柔和 | **建议在主图元和维度图元之间定义最多5个多实体关系。** 在删除或禁用现有关系之前，不应创建其他关系映射。 |
| 在多实体关系中使用的ID字段的最大JSON深度 | 4 | 柔和 | **在多实体关系中使用的ID字段建议的最大JSON深度为4。** 这意味着在高度嵌套的模式中，嵌套超过4级的字段不应用作关系中的ID字段。 |
| 用户档案片段中的数组基数 | &lt;=500 | 柔和 | **用户档案片段（与时间无关的数据）中的最佳数组基数是  &lt;>** |
| ExperienceEvent中的数组基数 | &lt;=10 | 柔和 | **ExperienceEvent（时间系列数据）中的最佳数组基数是  &lt;>** |

### Dimension实体护栏

| 瓜德赖尔 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 不允许非[!DNL XDM Individual Profile]实体使用时间序列数据 | 0 | 硬 | **用户档案服务中的非实体不允许使用[!DNL XDM Individual Profile] 时间序列数据。** 如果时间序列数据集与非ID关[!DNL XDM Individual Profile] 联，则不应为启用该数据集 [!DNL Profile]。 |
| 无嵌套关系 | 0 | 柔和 | **您不应在两个非模式之间创建关[!DNL XDM Individual Profile] 系。** 对于不属于合并模式的任何模式，不建议能够创建关 [!DNL Profile] 系。 |
| 主ID字段的最大JSON深度 | 4 | 柔和 | **主ID字段的建议最大JSON深度为4。** 这意味着在高度嵌套的模式中，如果某个字段嵌套的深度超过4个级别，则不应选择该字段作为主ID。位于第4个嵌套级别的字段可用作主ID。 |

## 数据大小护栏

以下护栏引用数据大小，建议您确保可以按照预期摄取、存储和查询数据。

>[!NOTE]
>
>在摄取时，数据大小将作为JSON中的未压缩数据来度量。

### 主要实体护栏

| 瓜德赖尔 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每个用户档案片段的最大大小 | 10KB | 柔和 | **建议的最大用户档案片段大小为10KB。** 引入较大的用户档案片段将影响系统性能。例如，加载某些用户档案片段大小为50kB的重量CRM数据集将导致系统性能降低。 |
| 每个用户档案片段的绝对最大大小 | 1MB | 硬 | **用户档案片段的绝对最大大小为1MB。** 尝试上传大于1MB的用户档案片段时，摄取将失败。 |

### Dimension实体护栏

| 瓜德赖尔 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 所有维图元的最大总大小 | 5 GB | 柔和 | **所有维图元的建议最大总大小为5GB。** 引入大维度实体将导致系统性能降低。例如，不建议尝试将10GB产品目录作为维度实体加载。 |
| 每维实体模式 | 5 | 柔和 | **建议与每个维实体模式关联的最多5个数据集。** 例如，如果您为“产品”创建模式并添加五个贡献数据集，则不应创建与产品模式关联的第六个数据集。 |

## 分段护栏

本节中概述的护栏是指组织在Experience Platform中创建的区段的数量和性质，以及将区段映射和激活到目标。

| 瓜德赖尔 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每个沙箱的最大段数 | 10K | 柔和 | **组织可创建的最大区段数为每个沙箱10K。** 一个组织总共可以有10K以上的区段，只要每个沙箱中的区段少于10,000个。尝试创建其他区段将导致系统性能降低。 |
| 每个沙箱的最大流段数 | 500 | 柔和 | **组织可以创建的流区段最多为每个沙箱500个。** 只要每个沙箱中的流段少于500个，组织总共可以有500多个流段。尝试创建额外的流区段将导致系统性能降低。 |
| 每个沙箱的最大批处理段数 | 1万 | 柔和 | **单位可创建的批量段最多为每个沙箱10K。** 一个组织总共可以有10K以上的批区段，只要每个沙箱中的批区段少于10,000个。尝试创建额外的批处理段将导致系统性能降低。 |
