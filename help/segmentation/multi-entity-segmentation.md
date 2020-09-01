---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments;multi-entity;multi-entity segmentation;multi-entity segments;
solution: Experience Platform
title: 多实体分割
topic: overview
description: 多实体细分是指能够根据产品、商店或其他非用户档案类扩展用户档案数据和附加数据。 连接后，来自其他类的数据将变得像用户档案模式的本机数据一样可用。
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# 多实体分割

多实体细分是指能够根据产 [!DNL Profile] 品、商店或其他非用户档案类使用额外数据扩展数据。 连接后，来自其他类的数据就变得像它们是模式的本机一样 [!DNL Profile] 可用。

要进一步了解多实体细分，请继续阅读文档并通过观看以下视频或浏览细分概述来补充 [您的学习](./home.md)。

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## 入门指南

本教程需要对使用分段时涉及的Adobe Experience Platform各项服务进行有效的了解。 在开始本教程之前，请查看以下服务的相关文档：

- [[!DNL实时客户用户档案]](../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
- [Adobe Experience Platform细分服务](./home.md):允许您从实时客户用户档案构建细分。
- [[!DNL体验数据模型(XDM)]](../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

## 如何定义XDM关系

定义与(XDM)模式结 [!DNL Experience Data Model] 构的关系是段创建的重要和不可或缺的一部分。

此过程可以使用API [!DNL Schema Registry] 或API完 [!DNL Schema Editor]成。 有关使用API定义两个模式之间关系的详细指南，请阅 [读有关使用API定义两个模式之间关系的教程](../xdm/tutorials/relationship-api.md)。 有关使用定义两个模式之 [!DNL Schema Editor] 间关系的详细指南，请阅 [读使用模式编辑器定义两个模式之间关系的教程](../xdm/tutorials/relationship-ui.md)。

## 如何创建使用XDM关系的细分

定义XDM关系后，您可以使用 [!DNL Segmentation Service] API构建细分。

此过程可以使用API [!DNL Segmentation] 或用户界面 [!DNL Segment Builder] 完成。 有关使用API构建区段的详细指南，请阅 [读有关使用分段API创建区段的教程](./tutorials/create-a-segment.md)。 有关使用区段生成器构建区段的详细指南，请阅 [读区段生成器用户指南](./ui/overview.md)。

## 如何评估和访问多实体细分的细分

创建区段后，您可以使用API评估和访问区段 [!DNL Segmentation Service] 结果。 评估多实体细分与评估常规细分非常相似。

此过程只能使用API完 [!DNL Segmentation Service] 成。 有关使用API评估和访问区段的详细指南，请阅读有关评估和访 [问区段的教程](./tutorials/evaluate-a-segment.md)。