---
solution: Experience Platform
title: 多实体分段概述
description: 多实体分段是一种使用基于产品、商店或其他非用户档案类的附加数据扩展用户档案数据的能力。 连接后，其他类中的数据将变得可用，就好像它们是配置文件架构的原生数据一样。
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# 多实体分段概述

多实体分段是Adobe Experience Platform中一项高级功能 [!DNL Segmentation Service]. 此功能允许您扩展 [!DNL Real-Time Customer Profile] 包含您的组织可能定义的其他“非人员”数据（也称为“维度实体”）的数据，例如与产品或商店相关的数据。 多实体分段在基于与您的独特业务需求相关的数据定义区段定义时提供了灵活性，并且无需具备查询数据库的专业知识即可执行。 通过多实体分段，您可以将关键数据添加到区段定义，而无需对数据流进行成本高昂的更改或等待后端数据合并。

## 快速入门

多实体分段需要深入了解分段中涉及的各种Adobe Experience Platform服务。 在继续阅读本指南之前，请查看以下文档：

* [[!DNL Real-Time Customer Profile]](../profile/home.md)：根据来自多个源的汇总数据，实时提供统一的用户配置文件。
   * [轮廓护栏](../profile/guardrails.md)：用于创建受支持的数据模型的最佳实践 [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md)：允许您从构建受众 [!DNL Real-Time Customer Profile] 数据。
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../xdm/schema/composition.md#union)：了解撰写要在Experience Platform中使用的架构的最佳实践。 为了更好地利用分段，请确保您的数据被摄取为用户档案和事件，并符合 [数据建模的最佳实践](../xdm/schema/best-practices.md).

## 用例

为了说明多实体分段的价值，请考虑三个标准营销用例，这些用例说明了大多数营销应用程序中存在的挑战：

### 整合在线和离线购买数据

构建电子邮件营销活动的营销人员可能试图通过在最近三个月内使用客户商店购买来构建受众。 理想情况下，此受众需要项目名称和进行购买的商店名称。 以前，难题是从购买事件中捕获商店标识符，并将其分配给单个客户配置文件。

### 因购物车放弃而重新定位电子邮件

针对购物车放弃创建用户并将其限定为区段定义非常复杂。 要了解在个性化重定位活动中包含哪些产品，需要有关每个用户放弃哪些产品的数据。 此数据绑定到商业事件，这些事件以前对监控和提取数据具有挑战性。

## 创建多实体区段定义

创建多实体区段定义首先需要定义架构之间的关系，然后再使用 [!DNL Segmentation] 用于生成区段定义的API或区段生成器UI。

### 定义关系

在体验数据模型(XDM)架构的结构中定义关系是多实体区段创建过程中不可或缺的一部分。 对于关系，需要将目标中的字段标记为该架构的主要标识。 只能在字符串上标记标识，不能在数组中标记标识。 此外，关系不一定需要一对一，因为您可以将配置文件和体验事件连接到多个目标。

可以使用架构注册表API或架构编辑器定义关系。 有关显示如何定义两个架构之间关系的详细步骤，请从以下教程中选择：

* [使用API定义两个架构之间的关系](../xdm/tutorials/relationship-api.md)
* [使用架构编辑器UI定义两个架构之间的关系](../xdm/tutorials/relationship-ui.md)

### 构建多实体区段定义

定义必要的XDM关系后，即可开始构建多实体区段定义。 可使用分段API或区段生成器UI执行此操作。 有关详细信息，请从以下指南中选择：

* [使用分段API创建区段定义](./tutorials/create-a-segment.md)
* [使用区段生成器UI创建区段定义](./ui/overview.md)

## 评估和访问多实体区段定义

创建区段定义后，您可以使用分段API评估和访问结果。 评估多实体区段定义与评估标准区段定义非常相似。 此流程只能使用分段API完成。 有关如何使用API来评估和访问区段定义的详细指南，请参阅 [评估和访问区段定义](./tutorials/evaluate-a-segment.md) 教程。
