---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 分段教程
topic: tutorial
type: Tutorial
description: Adobe Experience Platform分段服务提供用户界面和RESTful API，使您能够根据实时客户用户档案数据构建细分和生成受众。 这些细分在平台上集中配置和维护，任何Adobe解决方案均可轻松访问。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# 分段教程

Adobe Experience Platform [!DNL Segmentation Service] 提供用户界面和RESTful API，使您能够根据数据构建细分和生成 [!DNL Real-time Customer Profile] 受众。 这些细分集中配置和维护， [!DNL Platform]并且任何Adobe解决方案都可轻松访问。 要了解有关分段的更多信息，请首先阅读分段 [服务概述](../segmentation/home.md)。

## 创建区段定义

段定义是用于描述目标受众的关键特性或行为的规则集。 概念化后，使用细分定义中概述的规则确定某个细分的合格受众成员。 可使用用户界面或API完成区段定义的开发、测 [!DNL Platform] 试、预览和保存。 要创建区段定义，请按照创 [建区段API教程](../segmentation/tutorials/create-a-segment.md) 或区 [段生成器UI用户指南进行操作](../segmentation/ui/overview.md)。

## 评估区段和访问结果

开发、测试和保存区段定义后，您便可以通过计划评估或按需评估来评估区段。 计划评估（也称为“计划分段”）允许您创建在特定时间运行导出作业的循环计划，而点播评估涉及创建区段作业以立即构建受众。 要了解更多信息，请访问教程，以评 [估和访问区段结果](../segmentation/tutorials/evaluate-a-segment.md)。

## 导出区段数据

导出包含数 [!DNL Profile] 据的段 [需要先创建要将数据导出到的数据集](../segmentation/tutorials/create-dataset-export-segment.md)，然后启动新的导出作业。 有关生成导出作业的步骤，请参阅评估区段 [的教程](../segmentation/tutorials/evaluate-a-segment.md)。

## 配置合并策略

Adobe Experience Platform使您能够将来自多个来源的数据整合在一起，以便全面视图每位客户。 将数据整合在一起时，合并策略是确定 [!DNL Platform] 数据的优先级以及合并哪些数据以创建统一视图的规则。 使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 要在UI中使用合并策 [!DNL Platform] 略，请访问合 [并策略用户指南](../profile/ui/merge-policies.md)。 要使用API处理合并策略，请 [!DNL Real-time Customer Profile] 参阅合并策 [略开发人员指南](../profile/api/merge-policies.md)。

## 为细分强制实施数据使用合规性

允许在中使用的区段 [!DNL Real-time Customer Profile] 在其区段定义中包含合并策略ID。 此合并策略包含有关区段中要包含哪些数据集的信息，这些数据集又包含任何适用的数据使用标签。 有关强制受众区段遵守数据使用规范的具体步骤，请遵循区 [段的数据使用规范实施教程](../segmentation/tutorials/governance.md)。

## 流细分

流细分是一种在事件进入特定细分组后立即对客户进行评估的能力。 借助此功能，现在可以在数据传入Adobe Experience Platform时评估大多数细分规则，这意味着，在不运行计划的细分作业的情况下，细分成员资格将保持最新。 要了解更多信息，请访 [问流细分概述](../segmentation/api/streaming-segmentation.md)。

## 多实体分割

多实体细分是指能够根据产 [!DNL Profile] 品、商店或其他非用户档案类使用额外数据扩展数据。 连接后，来自其他类的数据将变得像模式本身一样可 [!DNL Profile] 用。 要了解移动，请参 [阅多实体细分文档](../segmentation/multi-entity-segmentation.md)。