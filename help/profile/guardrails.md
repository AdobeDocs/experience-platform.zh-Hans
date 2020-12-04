---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: Experience Platform准则
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 1%

---


# [!DNL Platform] 护栏 [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] 提供个人用户档案，使您能够根据行为洞察和客户属性提供个性化的跨渠道体验。 为了实现这一目标，Adobe Experience Platform [!DNL Profile] 的分段引擎采用高度非规范的混合数据模型，该模型优惠了开发客户用户档案的新途径。 这种混合数据模型的使用使得正确建模所收集的数据变得尤为重要。 虽然维 [!DNL Profile] 护用户档案数据的存储不是关系存储， [!DNL Profile] 但允许与小维实体集成，以便以简化和直观的方式创建段。 此集成称为多实体细分。

Adobe Experience Platform提供了一系列护栏，帮助您避免创建无法支持的 [!DNL Real-time Customer Profile] 数据模型。 本文档概述了使用维实体（特别是在批分段中）时的最佳做法和限制。

>[!NOTE]
>
>本文档中概述的护栏和限制正在不断改进。 请定期回访以获取更新。

## 入门指南

建议您在尝试构建Experience Platform模型以在中使用之前阅读以下数据服务文档 [!DNL Real-time Customer Profile]。 使用文档模型和本Experience Platform中概述的保障，需要了解与管理实体相关的各种服务 [!DNL Real-time Customer Profile] :

* [[!DNL Real-time Customer Profile]](home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [Adobe Experience Platform身份服务](../identity-service/home.md):在客户被收录时，通过连接来自不同数据源的身份，支持创建“单一视图” [!DNL Platform]。
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):平台组织客户体验数据的标准化框架。
   * [模式合成基础](../xdm/schema/composition.md):介绍模式和Experience Platform内数据建模。
* [Adobe Experience Platform细分服务](../segmentation/home.md):中的细分引擎 [!DNL Platform] 用于根据客户行为和属性从客户用户档案创建受众细分。
   * [多实体细分](../segmentation/multi-entity-segmentation.md):创建将维实体与用户档案数据集成的区段的指南。

## 实体类型

存储 [!DNL Profile] 数据模型由两个核心实体类型组成：

* **主要实体：** 主实体或用户档案实体将数据合并在一起，为个人构成“单一真相来源”。 此统一数据使用称为“合并视图”的数据表示。 合并视图将实现同一类的所有模式的字段聚合为单个合并模式。 合并模式是一 [!DNL Real-time Customer Profile] 个非规范的混合数据模型，它充当所有用户档案属性和行为事件的容器。

   时间无关属性（也称为“记录数据”）使用建模 [!DNL XDM Individual Profile]，而时间序列数据(也称为“事件数据”)使用建模 [!DNL XDM ExperienceEvent]。 随着记录和时间序列数据在Adobe Experience Platform被摄入，它会触发 [!DNL Real-time Customer Profile] 数据开始被摄入已启用的数据。 所摄取的交互和细节越多，个体用户档案就越健壮。

   ![](images/guardrails/profile-entity.png)

* **Dimension实体：** 您的组织还可以定义XDM类来描述个人以外的事物，如商店、产品或属性。 这些非模式[!DNL XDM Individual Profile] 称为“维实体”，不包含时间序列数据。 Dimension实体提供查找数据，这有助于和简化多实体段定义，并且必须足够小，分段引擎才能将整个数据集加载到内存中以实现最佳处理（快速点查找）。

   ![](images/guardrails/profile-and-dimension-entities.png)

## 限制类型

在定义数据模型时，建议保留在提供的护栏内，以确保正确的性能并避免系统错误。 本文档提供的护栏包括两种限制类型：

* **软限制：** 软限制可提供建议的最大值以获得最佳系统性能。 可以在不中断系统或接收错误消息的情况下超出软限制，但超出软限制将导致性能降低。 建议保持在软限制内，以避免总体性能下降。

* **硬限制：** 硬限制为系统提供绝对最大值。 超出硬限制将导致故障和错误，从而阻止系统按预期运行。

## 数据模型护栏

在创建要与一起使用的数据模型时，建议遵循以下护栏 [!DNL Real-time Customer Profile]。

### 主实体护栏

| 瓜德赖尔 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 建议贡献给合并模式的数据集 [!DNL Profile] 数 | 20 | 柔和 | **建议最多支持 [!DNL Profile]20个数据集。** 要为其他数据集启 [!DNL Profile]用，应首先删除或禁用现有数据集。 |
| 建议的多实体关系数 | 5 | 柔和 | **建议在主图元和尺寸图元之间定义最多5个多实体关系。** 在删除或禁用现有关系之前，不应进行其他关系映射。 |
| 在多实体关系中使用的ID字段的最大JSON深度 | 4 | 柔和 | **在多实体关系中使用的ID字段，建议的最大JSON深度为4。** 这意味着在高度嵌套的模式中，嵌套超过4级的字段不应用作关系中的ID字段。 |
| 用户档案片段中的数组基数 | &lt;=500 | 柔和 | **用户档案片段（与时间无关的数据）中的最佳阵列基数为&lt;=500。** |
| ExperienceEvent中的数组基数 | &lt;=10 | 柔和 | **ExperienceEvent（时间序列数据）中的最佳阵列基数为&lt;=10。** |

### Dimension实体护栏

| 瓜德赖尔 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 不允许非实体使用时间序列数据[!DNL XDM Individual Profile] | 0 | 硬 | **用户档案服务中的非实体不允许使用[!DNL XDM Individual Profile] 时间序列数据。** 如果时间序列数据集与非ID关联[!DNL XDM Individual Profile] ，则不应启用该数据集 [!DNL Profile]。 |
| 无嵌套关系 | 0 | 柔和 | **您不应在两个非模式之间创建关系[!DNL XDM Individual Profile] 。** 对于不属于模式模式的任何合并，不建议创建关系 [!DNL Profile] 。 |
| 主ID字段的最大JSON深度 | 4 | 柔和 | **主ID字段的建议最大JSON深度为4。** 这意味着在高度嵌套的模式中，如果字段嵌套深度超过4个级别，则不应选择该字段作为主ID。 位于第4个嵌套级别的字段可用作主ID。 |

## 数据大小护栏

以下护栏引用数据大小，建议您确保数据可以按照预期进行摄取、存储和查询。

>[!NOTE]
>
>在摄取时，数据大小将在JSON中测量为未压缩数据。

### 主实体护栏

| 瓜德赖尔 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每个用户档案片段的最大大小 | 10KB | 柔和 | **建议的用户档案片段最大大小为10KB。** 引入较大的用户档案片段将影响系统性能。 例如，加载某些用户档案片段大小为50kB的重量CRM数据集将导致系统性能降低。 |
| 每个用户档案片段的绝对最大大小 | 1MB | 硬 | **用户档案片段的绝对最大大小为1MB。** 尝试上传大于1MB的用户档案片段时，摄取将失败。 |

### Dimension实体护栏

| 瓜德赖尔 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 所有维图元的最大总大小 | 5GB | 柔和 | **建议所有维实体的最大总大小为5GB。** 引入大维度实体将导致系统性能降低。 例如，不建议将10GB产品目录作为维实体加载。 |
| 每维实体模式 | 5 | 柔和 | **建议与每个维实体模式关联的数据集最多为5个。** 例如，如果您为“产品”创建模式并添加五个贡献数据集，则不应创建与产品模式关联的第六个数据集。 |