---
keywords: Experience Platform；主题；热门主题；分段；分段；分段；分段；分段服务；分段；多实体；多实体分段；
solution: Experience Platform
title: 多实体细分概述
topic: 概述
description: 多实体细分是指能够根据产品、商店或其他非用户档案类使用附加数据扩展用户档案数据。 连接后，来自其他类的数据就变得像它们是用户档案模式的本机数据一样可用。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# 多实体细分概述

多实体分段是Adobe Experience Platform [!DNL Segmentation Service]的一个高级功能。 此功能允许您使用您的组织可定义的其他“非人员”数据（也称为“维度实体”）扩展[!DNL Real-time Customer Profile]数据，例如与产品或商店相关的数据。 多实体细分在根据与您独特业务需求相关的数据定义受众细分时提供了灵活性，并且无需具备查询数据库的专业知识即可执行。 通过多实体细分，您无需对数据流进行代价高昂的更改或等待后端数据合并，即可将关键数据添加到细分。

## 入门指南

多实体分段需要对分段中涉及的各种Adobe Experience Platform服务进行有效的了解。 在继续使用本指南之前，请查阅以下文档：

* [[!DNL Real-time Customer Profile]](../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
   * [用户档案护栏](../profile/guardrails.md):创建受支持的数据模型的最佳实践 [!DNL Profile]。
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):允许您根据数据构建 [!DNL Real-time Customer Profile] 细分。
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础](../xdm/schema/composition.md#union):了解编写模式以用于Experience Platform的最佳实践。

## 用例

为了说明多实体细分的价值，请考虑三个标准营销用例，它们说明了大多数营销应用程序中存在的挑战：

### 整合线上和线下购买数据

构建电子邮件活动的营销人员可能已尝试通过使用最近三个月内购买的目标受众来构建细分。 理想情况下，此区段需要物品名称和进行购买的商店的名称。 以前，难题是从购买事件中捕获商店标识符并将其分配给单个用户档案。

### 电子邮件重定位以放弃购物车

创建和确定用户进入定位放弃购物车的细分通常很复杂。 了解要将哪些产品纳入个性化重定向活动，需要有关每位客户已放弃哪些产品的数据。 此数据与商业事件有关，这些商业以前很难监控和提取数据。

## 创建多实体区段

创建多实体区段首先需要先定义模式之间的关系，然后使用[!DNL Segmentation] API或区段生成器UI构建区段定义。

### 定义关系

在体验数据模型(XDM)模式的结构中定义关系是创建多实体细分的一个组成部分。 对于关系，目标中的字段需要标记为该模式的主要标识。 只能在字符串上标记标识，不能在数组上标记标识。 此外，关系不一定需要一对一，因为您可以将用户档案和体验事件连接到多个目标。

可以使用模式注册表API或模式编辑器来定义关系。 有关显示如何定义两个模式之间关系的详细步骤，请从以下教程中进行选择：

* [使用API定义两个模式之间的关系](../xdm/tutorials/relationship-api.md)
* [使用模式编辑器UI定义两个模式之间的关系](../xdm/tutorials/relationship-ui.md)

### 构建多实体细分

定义必要的XDM关系后，您可以开始构建多实体区段。 这可以使用分段API或区段生成器UI来完成。 有关详细信息，请从以下指南中进行选择：

* [使用分段API创建区段](./tutorials/create-a-segment.md)
* [使用区段生成器用户界面创建区段](./ui/overview.md)

## 评估和访问多实体细分

创建区段后，您可以使用分段API评估和访问区段结果。 评估多实体区段与评估标准区段非常相似。 此过程只能使用分段API完成。 有关如何使用API评估和访问区段的详细指南，请阅读[评估和访问区段](./tutorials/evaluate-a-segment.md)教程。
