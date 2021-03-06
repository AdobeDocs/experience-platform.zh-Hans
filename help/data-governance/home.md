---
keywords: Experience Platform；主页；热门主题；DULE;DULE
solution: Experience Platform
title: 数据管理概述
topic-legacy: overview
description: Adobe Experience Platform数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和政策。 它在Experience Platform的各个级别中发挥着关键作用，包括编目、数据谱系、数据使用标签、数据使用策略，以及控制数据在营销操作中的使用
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 0c78b5dc420a1346c92bf9ed7864fa1733422a83
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# 数据管理概述

Adobe Experience Platform的核心功能之一是将多个企业系统中的数据整合在一起，以便营销人员更好地识别、了解和吸引客户。 此数据可能受贵组织或法律法规定义的使用限制的约束。 因此，务必确保在 [!DNL Platform] 符合数据使用策略。

Adobe Experience Platform数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和政策。 它在 [!DNL Experience Platform] 在不同级别，包括编目、数据谱系、数据使用标签、数据使用策略，以及控制营销操作数据的使用。

## 数据管理角色

作为一个概念，数据治理既不是自动的，也不是在真空中发生。 随着数据治理生态系统的扩大，最初作为个人角色的角色 — 通常被公认为是数据管理者 — 已大幅增长。 如今，数据管理需要持续的管理和监控才能取得成功，并且依赖于数据管理员，他们拥有能够正确标记数据的工具，可以创建使用策略，并且可以强制执行对这些策略的合规性。

虽然数据管理应由组织中的每个人负责，但以下是数据管理周期中的一些基本角色：

![数据管理角色](./images/overview/roles.png)

### 数据管理

数据管理员是数据管理的核心。 此角色负责解释法规、合同限制和政策，并将其直接应用于数据。 根据对这些法规、限制和政策的了解，数据管理员的作用包括：

* 查看数据、数据集和数据示例，以应用和管理元数据使用标签设置。
* 创建数据策略并将其应用到数据集和字段。
* 将数据策略传达到组织。

### 营销人员

营销人员是数据管理的终点。 他们从由数据管理员、科学家和工程师创建的数据管理基础架构中请求数据。 营销人员在营销伞下涵盖了许多不同的专业，包括以下内容：

* 营销分析人员请求数据，以便了解客户(无论是个人还是群组（也称为区段）中的客户)。
* 营销专家和体验设计人员使用数据来设计新的客户体验。


## 数据管理框架

数据管理框架简化了对数据进行分类和创建数据使用策略的过程并简化了这些过程。 应用数据标签并制定数据使用策略后，可以评估营销操作以确保正确使用数据。

数据管理框架有三个关键元素：标签、策略和执行。

1. **标签：** 对反映隐私相关注意事项和合同条件的数据进行分类，以符合法规和组织政策。
1. **策略：** 描述允许或不允许对特定数据执行哪种类型的营销操作。
1. **执行：** 使用策略框架在不同数据访问模式中建议并实施策略。

## 数据使用标签

“数据管理”允许数据管理人员在数据集和字段级别应用使用标签，以根据应用的策略类型对数据进行分类。

“数据管理”框架包括预定义的数据使用标签，可用于通过三种方式对数据进行分类：

![数据使用标签类别](./images/overview/label-categories.png)

* **合同“C”数据标签：** 对具有合同义务或与客户数据管理策略相关的数据进行标签和分类。
* **身份“I”数据标签：** 为可识别或联系特定人员的数据设置标签和分类。
* **敏感“S”数据标签：** 对与敏感数据（如地理数据）相关的数据进行标签和分类。

>[!NOTE]
>
>请参阅 [支持的数据使用标签](labels/reference.md) 以获取可用标签的完整列表以及每个标签类型的定义。

标签可随时应用，从而在您选择如何管理数据方面提供了灵活性。 最佳实践是鼓励在将数据摄取到 [!DNL Experience Platform]，或者当数据在 [!DNL Platform].

请参阅 [数据使用标签](./labels/overview.md) 以了解更多信息。

## 数据使用策略

为了有效支持数据合规性的数据使用标签，必须实施数据使用策略。 数据使用策略是描述您允许或限制对内数据执行的营销操作类型的规则 [!DNL Experience Platform].

营销操作的示例可能是希望将数据集导出到第三方服务。 如果有策略指示无法导出个人身份信息(PII)，并且“I”标签（身份数据）已应用于数据集， [!DNL Policy Service] 阻止将此数据集导出到第三方目标的任何操作。 如果尝试了其中一项操作，策略服务会发送一条消息，告知您数据使用策略已被违反。

可用的策略有两种类型：

* **[!UICONTROL 数据管理政策]**:根据正在执行的营销操作以及相关数据携带的数据使用标签限制数据激活。
* **[!UICONTROL 同意策略]**:筛选可激活的用户档案 [目标](../destinations/home.md) 基于客户的同意或偏好。

应用数据使用标签后，数据管理人员可以使用 [!DNL Policy Service] API或 [!DNL Experience Platform] 用户界面。 有关数据使用策略和营销操作的更多信息，请参阅 [策略概述](./policies/overview.md).

>[!IMPORTANT]
>
>默认情况下，所有数据使用策略(包括由Adobe提供的核心策略)都处于禁用状态。 要考虑实施单个策略，必须手动启用该策略。

## 后续步骤

本文件对《数据管理》和《数据管理框架》作了简要介绍。 您现在可以继续 [数据使用标签用户指南](labels/user-guide.md) 并开始向体验数据添加使用情况标签。

## 附录

以下部分提供了有关“数据管理”的其他信息。

### 数据管理术语

下表概述了与“数据管理”和“数据管理”框架相关的关键术语。

| 搜索词 | 定义 |
|---|---|
| **合同标签** | 合同“C”标签用于对具有合同义务或与贵组织的数据管理策略相关的数据进行分类。 |
| **跨站点数据** | 跨站点数据是来自多个站点的数据的组合，包括站点数据和站点外数据的组合，或来自多个站点外源的数据的组合。 |
| **数据管理** | 数据管理包括用于确保数据在数据使用方面符合法规和公司政策的战略和技术。 |
| **数据管理** | 数据管理员负责管理、监督和执行组织的数据资产。 数据管理人员还确保数据管理政策得到维护和维护，以符合政府法规和组织政策。 |
| **数据使用标签** | 数据使用标签为用户提供了对反映隐私相关考虑因素和合同条件的数据进行分类的功能，以符合法规和公司政策。 |
| **数据集标签** | 可以向数据集添加标签。 数据集中的所有字段都会继承数据集的标签。 |
| **字段标签** | 字段标签是从数据集继承或直接应用于字段的数据管理标签。  应用到字段的数据管理标签不会继承到数据集。 |
| **地理围栏** | 地理围栏是由GPS或RFID技术定义的虚拟地理边界，它使软件能够在移动设备进入或离开特定区域时触发响应。 |
| **身份标签** | 身份“I”标签用于对可识别或联系特定人员的数据进行分类。 |
| **基于兴趣的定位** | 如果满足以下三个条件，则会进行基于兴趣的定位（也称为个性化）：网站上收集的数据用于对用户兴趣做出推论，用于其他上下文，例如在其他网站或应用程序（站外）上，并用于根据这些推论选择提供哪些内容或广告。 |
| **营销操作** | 在数据管理框架中，营销行动是指 [!DNL Experience Platform] 数据使用者所采用的数据，需要检查其是否违反了数据使用策略 |
| **策略** | 在数据管理框架中，策略是一条规则，用于描述允许或不允许对特定数据采取何种营销操作。 |
| **敏感标签** | 敏感的“S”标签用于对您和您的组织认为敏感的数据进行分类。 |

## 其他资源

以下视频旨在支持您对“数据管理”框架的了解。

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

以下视频介绍了Experience Platform中的各种数据管理功能。

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)
