---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments;multi-entity;multi-entity segmentation;multi-entity segments;
solution: Experience Platform
title: 多实体分割
topic: overview
description: 多实体细分是指能够根据产品、商店或其他非用户档案类扩展用户档案数据和附加数据。 连接后，来自其他类的数据将变得像用户档案模式的本机数据一样可用。
translation-type: tm+mt
source-git-commit: 5dd07bf9afe96be3a4c3f4a4d4e3b23aef4fde70
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---


# 多实体分割

多实体分割是Adobe Experience Platform的一个高级功能 [!DNL Segmentation Service]。 此功能允许您使用 [!DNL Real-time Customer Profile] 组织可定义的其他“非人员”数据（也称为“维实体”）扩展数据，如与产品或商店相关的数据。 多实体细分在根据与您独特的业务需求相关的数据定义受众细分时提供了灵活性，并且无需在查询数据库方面具有专业知识即可执行。 通过多实体细分，您可以向细分中添加关键数据，而无需对数据流进行代价高昂的更改或等待后端数据合并。

## 入门指南

多实体细分需要对细分中涉及的Adobe Experience Platform各种服务进行有效的了解。 在继续使用本指南之前，请查阅以下文档：

* [!DNL Real-time Customer Profile](../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
   * [用户档案护栏](../profile/guardrails.md):创建受支持的数据模型的最佳实 [!DNL Profile]践。
* [!DNL Adobe Experience Platform Segmentation Service](./home.md):允许您根据数据构建 [!DNL Real-time Customer Profile] 细分。
* [!DNL Experience Data Model (XDM)](../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../xdm/schema/composition.md#union):了解编写模式以用于Experience Platform的最佳实践。

## 用例

为了说明多实体细分的价值，请考虑三个标准营销用例，这些案例说明了大多数营销应用程序中存在的挑战：

### 组合线上和线下购买数据

构建电子邮件活动的营销人员可能已尝试在过去三个月内使用最近的目标商店购买来构建受众的细分。 理想情况下，此区段需要物品名称和进行购买的商店的名称。 以前，难题是从购买事件捕获商店标识符并将其分配给单个客户用户档案。

### 电子邮件重定位以放弃购物车

创建用户并将其限定为针对放弃购物车的细分通常很复杂。 了解要包含在个性化重新定位活动中的产品需要有关每个人已放弃哪些产品的数据。 此数据与商业事件相关，而商业以前很难监控和提取数据。

## 创建多实体区段

创建多实体区段首先需要定义模式之间的关系，然 [!DNL Segmentation] 后使用API或区段生成器UI构建区段定义。

### 定义关系

在体验数据模型(XDM)模式的结构中定义关系是创建多实体细分的一个组成部分。 此过程可以使用模式注册表API或模式编辑器完成。 有关说明如何定义两个模式之间关系的详细步骤，请从以下教程中进行选择：

* [使用API定义两个模式之间的关系](../xdm/tutorials/relationship-api.md)
* [使用模式编辑器UI定义两个模式之间的关系](../xdm/tutorials/relationship-ui.md)

### 构建多实体细分

定义必要的XDM关系后，您可以开始构建多实体细分。 此过程可使用分段API或段生成器UI完成。 有关详细信息，请从以下指南中进行选择：

* [使用分段API创建段](./tutorials/create-a-segment.md)
* [使用区段生成器UI创建区段](./ui/overview.md)

## 评估和访问多实体细分

创建区段后，您可以使用分段API评估和访问区段结果。 评估多实体区段与评估标准区段非常相似。 此过程只能使用分段API完成。 有关如何使用API评估和访问区段的详细指南，请阅读评估 [和访问区段教程](./tutorials/evaluate-a-segment.md) 。
