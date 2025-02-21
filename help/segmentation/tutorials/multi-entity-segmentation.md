---
solution: Experience Platform
title: 多实体分段概述
description: 多实体分段是使用基于产品、商店或其他非配置文件类的附加数据扩展配置文件数据的能力。 连接后，其他类中的数据将变得可用，就好像它们是配置文件架构的原生数据一样。
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 630041a7ef82993038ef4510dd08d3bc67bfce41
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# 多实体分段概述

多实体分段是Adobe Experience Platform [!DNL Segmentation Service]中提供的高级功能。 此功能允许您使用组织可能定义的其他“非人员”数据（也称为“维度实体”）扩展[!DNL Real-Time Customer Profile]数据，例如与产品或商店相关的数据。 多实体分段在基于与您的独特业务需求相关的数据定义区段定义时提供了灵活性，并且无需在查询数据库方面拥有专业知识即可执行。 借助多实体分段，您可以将关键数据添加到区段定义，而无需对数据流进行成本高昂的更改或等待后端数据合并。

## 快速入门

多实体分段需要深入了解分段中涉及的各种Adobe Experience Platform服务。 在继续本指南之前，请查看以下文档：

* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：基于来自多个源的聚合数据，实时提供统一的使用者配置文件。
   * [配置文件护栏](../../profile/guardrails.md)：用于创建[!DNL Profile]支持的数据模型的最佳实践。
* [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：允许您从[!DNL Real-Time Customer Profile]数据构建受众。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合基础](../../xdm/schema/composition.md#union)：了解在Experience Platform中组合架构的最佳实践。 为了更好地利用分段，请确保根据用于数据建模的[最佳实践](../../xdm/schema/best-practices.md)，将您的数据作为配置文件和事件摄取。

## 用例

为了说明多实体分段的价值，请考虑三个标准营销用例，这些用例说明了大多数营销应用程序中存在的挑战：

### 将在线和离线购买数据相结合

构建电子邮件营销活动的营销人员可能在过去三个月中尝试过使用最近客户商店购买次数来构建受众。 理想情况下，此受众需要项目名称和购买地商店的名称。 以前，难题是从购买事件中捕获商店标识符，并将其分配给单个客户配置文件。

### 针对购物车放弃的电子邮件重新定位

针对购物车放弃创建用户并将其限定为区段定义非常复杂。 要了解在个性化重定位促销活动中包含哪些产品，需要有关每个用户放弃哪些产品的数据。 此数据绑定到商业事件，以前这些事件在从监控和提取数据方面富有挑战性。

## 创建多实体区段定义

创建多实体区段定义首先需要定义架构之间的关系，然后再使用[!DNL Segmentation] API或区段生成器UI生成区段定义。

### 定义关系

在体验数据模型(XDM)架构的结构中定义关系是多实体区段创建过程中不可或缺的一部分。 对于关系，目标中的字段需要标记为该架构的主要标识。 只能在字符串上标记标识，不能在数组中标记标识。 此外，关系不一定是一对一的，因为您可以将配置文件和体验事件连接到多个目标。

可以使用架构注册表API或架构编辑器定义关系。 有关显示如何定义两个架构之间关系的详细步骤，请从以下教程中选择：

* [使用API定义两个架构之间的关系](../../xdm/tutorials/relationship-api.md)
* [使用架构编辑器UI定义两个架构之间的关系](../../xdm/tutorials/relationship-ui.md)

### 构建多实体区段定义

定义必要的XDM关系后，即可开始构建多实体区段定义。 可使用分段API或区段生成器UI执行此操作。 有关详细信息，请从以下指南中选择：

* [使用分段API创建区段定义](./create-a-segment.md)
* [使用区段生成器UI创建区段定义](../ui/overview.md)

## 评估和访问多实体区段定义

创建区段定义后，您可以使用分段API评估和访问结果。 评估多实体区段定义与评估标准区段定义非常相似。 此过程只能使用分段API完成。 有关如何使用API来评估和访问区段定义的详细指南，请参阅[评估和访问区段定义](./evaluate-a-segment.md)教程。
