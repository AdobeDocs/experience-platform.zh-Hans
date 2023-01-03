---
keywords: Experience Platform；主页；热门主题；分段；分段；区段服务；区段；区段；多实体；多实体分段；多实体区段；
solution: Experience Platform
title: 多实体分段概述
topic-legacy: overview
description: 多实体分段功能可以根据产品、商店或其他非用户档案类使用附加数据扩展用户档案数据。 连接后，来自其他类的数据将变得可用，就像它们是配置文件架构的本机数据一样。
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# 多实体分段概述

多实体分段是作为Adobe Experience Platform的一部分提供的一项高级功能 [!DNL Segmentation Service]. 此功能允许您扩展 [!DNL Real-Time Customer Profile] 您的组织可能定义的附加“非人员”数据（也称为“维度实体”）的数据，例如与产品或商店相关的数据。 在根据与您的独特业务需求相关的数据定义受众区段时，多实体分段提供了灵活性，并且可以在没有查询数据库专业知识的情况下执行。 通过多实体分段，您可以向区段添加关键数据，而无需对数据流进行成本高昂的更改或等待后端数据合并。

## 快速入门

多实体分段需要对分段中涉及的各种Adobe Experience Platform服务有一定的了解。 在继续阅读本指南之前，请查阅以下文档：

* [[!DNL Real-Time Customer Profile]](../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户资料。
   * [配置文件护栏](../profile/guardrails.md):创建受 [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):允许您从 [!DNL Real-Time Customer Profile] 数据。
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../xdm/schema/composition.md#union):了解合成架构以用于Experience Platform的最佳实践。 为了最好地利用分段，请确保根据 [数据建模最佳实践](../xdm/schema/best-practices.md).

## 用例

为了说明多实体分段的价值，请考虑三个标准营销用例，这些用例说明了大多数营销应用程序中存在的挑战：

### 整合在线和离线购买数据

构建电子邮件促销活动的营销人员可能已尝试通过使用最近客户商店在过去三个月内购买的内容为目标受众构建区段。 理想情况下，此区段既需要项目名称和进行购买的商店的名称。 以前，难题是从购买事件中捕获商店标识符并将其分配给单个客户资料。

### 针对放弃购买的电子邮件重定位

创建用户并确定其是否加入定向放弃购买的区段通常比较复杂。 要了解要包含在个性化重定向营销活动中的哪些产品，需要提供有关每个人放弃了哪些产品的数据。 此数据与商务事件相关，这些事件以前在监控和提取数据方面具有挑战性。

## 创建多实体区段

创建多实体区段首先需要先定义架构之间的关系，然后再使用 [!DNL Segmentation] 用于构建区段定义的API或区段生成器UI。

### 定义关系

在体验数据模型(XDM)架构的结构中定义关系是创建多实体区段的一个必不可少的部分。 对于关系，目标中的字段需要标记为该架构的主标识。 标识只能在字符串上标记，不能在数组上标记。 此外，由于您可以将用户档案和体验事件关联到多个目标，因此关系不一定需要一对一。

定义关系可以使用架构注册表API或架构编辑器完成。 有关如何定义两个架构之间关系的详细步骤，请从以下教程中进行选择：

* [使用API定义两个架构之间的关系](../xdm/tutorials/relationship-api.md)
* [使用架构编辑器UI定义两个架构之间的关系](../xdm/tutorials/relationship-ui.md)

### 构建多实体区段

定义必要的XDM关系后，您可以开始构建多实体区段。 可以使用分段API或区段生成器UI来完成此操作。 有关更多信息，请从以下指南中进行选择：

* [使用分段API创建区段](./tutorials/create-a-segment.md)
* [使用区段生成器UI创建区段](./ui/overview.md)

## 评估和访问多实体区段

创建区段后，您可以使用分段API评估和访问区段结果。 评估多实体区段与评估标准区段非常相似。 此过程只能使用分段API完成。 有关如何使用API评估和访问区段的详细指南，请阅读 [评估和访问区段](./tutorials/evaluate-a-segment.md) 教程。
