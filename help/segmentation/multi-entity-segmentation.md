---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 多实体分割
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 多实体分割

多实体细分是指能够根据产品、商店或其他非用户档案类扩展用户档案数据和附加数据。 连接后，来自其他类的数据将变为可用，就像它们是用户档案模式的本机数据一样。

有关多实体细分的更多信息，请阅读分 [段概述](./home.md)。

## 入门指南

本教程需要对使用细分时涉及的各种Adobe Experience Platform服务进行有效的了解。 在开始本教程之前，请查看以下服务的相关文档：

- [实时客户用户档案](../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
- [Adobe Experience Platform Segmentation Service](./home.md):允许您通过实时客户用户档案构建细分。
- [体验数据模型(XDM)](../xdm/home.md):平台通过标准化框架组织客户体验数据。

## 如何定义XDM关系

定义与体验数据模型(XDM)模式结构的关系是细分创建的重要组成部分。

此过程可以使用模式注册表API或模式编辑器完成。 有关使用API定义两个模式之间关系的详细指南，请阅读 [使用API定义两个模式之间关系的教程](../xdm/tutorials/relationship-api.md)。 有关使用模式编辑器定义两个模式之间关系的详细指南，请阅读 [使用模式编辑器定义两个模式之间关系的教程](../xdm/tutorials/relationship-ui.md)。

## 如何使用创建使用XDM关系的细分

定义XDM关系后，您可以使用实时客户用户档案API构建细分。

此过程可以使用实时客户用户档案API或区段生成器完成。 有关使用API构建区段的详细指南，请阅 [读使用实时客户用户档案API创建区段的教程](./tutorials/create-a-segment.md)。 有关使用区段生成器构建区段的详细指南，请阅 [读区段生成器用户指南](./ui/overview.md)。

## 如何评估和访问多实体细分的细分

创建区段后，您可以使用实时客户用户档案API评估和访问区段结果。 评估多实体细分与评估常规细分非常相似。

此过程只能使用实时客户用户档案API完成。 有关使用API评估和访问区段的详细指南，请阅读有关评估 [和访问区段的教程](./tutorials/evaluate-a-segment.md)。