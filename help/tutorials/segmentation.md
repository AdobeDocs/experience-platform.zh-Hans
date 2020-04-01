---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 细分教程
topic: tutorial
translation-type: tm+mt
source-git-commit: 6705cb699b0785e317a6e437fc8a01ca77266f84

---


# 细分教程

Adobe Experience Platform Segmentation Service提供用户界面和RESTful API，使您能够构建细分并根据实时客户用户档案数据生成受众。 这些细分在平台上集中配置和维护，任何Adobe解决方案都可轻松访问。 要了解有关分段的更多信息，请首先阅读分段 [服务概述](../segmentation/home.md)。

## 创建区段定义

段定义是用于描述目标受众的关键特性或行为的规则集。 概念化后，区段定义中概述的规则用于确定区段的合格受众成员。 开发、测试、预览和保存区段定义可以使用平台用户界面或API完成。 要创建区段定义，请按照创建 [区段API教程](../segmentation/tutorials/create-a-segment.md) 或区段生成 [器UI用户指南操作](../segmentation/ui/overview.md)。

## 评估区段和访问结果

开发、测试和保存区段定义后，您便可以通过计划评估或点播评估来评估区段。 计划评估（也称为“计划细分”）允许您创建循环计划以在特定时间运行导出作业，而点播评估涉及创建区段作业以立即构建受众。 要了解更多信息，请访问教程，以评 [估和访问区段结果](../segmentation/tutorials/evaluate-a-segment.md)。

## 导出区段数据

导出包含用户档案数据的区段需 [要先创建要将数据导出到的数据集](../segmentation/tutorials/create-dataset-export-segment.md)，然后启动新的导出作业。 有关生成导出作业的步骤，请参阅导出API [教程](../segmentation/tutorials/export-data.md)。

## 配置合并策略

Adobe Experience Platform使您能够将来自多个来源的数据整合在一起，并将其合并，以便了解每位客户的完整视图。 整合这些数据时，合并策略是平台用来确定数据的优先级以及将哪些数据合并以创建统一视图的规则。 使用RESTful API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 要在平台UI中使用合并策略，请访问合 [并策略用户指南](../profile/ui/merge-policies.md)。 要使用实时客户用户档案API处理合并策略，请参阅合并策略开 [发人员指南](../profile/api/merge-policies.md)。

## 为细分强制实施数据使用合规性

在实时客户用户档案中启用的区段在其区段定义中包含合并策略ID。 此合并策略包含有关区段中要包含哪些数据集的信息，这些数据集又包含任何适用的数据使用标签。 有关强制受众区段遵守数据使用规范的具体步骤，请遵循区 [段的数据使用规范实施教程](../segmentation/tutorials/governance.md)。

## （测试版）流细分

>[!NOTE]
>流分段采用测试版，并可应要求提供。 功能和文档可能会发生更改。

流细分(也称为连续查询评估)是指在事件进入特定细分组后立即对客户进行评估的能力。 借助此功能，当数据传递到Adobe Experience Platform时，大多数细分规则现在都可以评估，这意味着，细分会员资格将保持最新状态，而无需运行计划的细分作业。 要了解更多信息，请访问流 [细分概述](../segmentation/api/streaming-segmentation.md)。

## 多实体分割

多实体细分是指能够根据产品、商店或其他非用户档案类扩展用户档案数据和附加数据。 连接后，来自其他类的数据将变为可用，就像它们是用户档案模式的本机数据一样。 要了解移动，请参阅 [多实体细分文档](../segmentation/multi-entity-segmentation.md)。