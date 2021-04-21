---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 分段教程
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Segmentation Service提供用户界面和RESTful API，使您能够构建细分并根据实时客户用户档案数据生成受众。 这些细分在平台上集中配置和维护，任何Adobe解决方案都可轻松访问。
exl-id: e45de6b5-ff71-4908-ad79-898084763704
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# 分段教程

Adobe Experience Platform [!DNL Segmentation Service]提供了用户界面和RESTful API，使您能够根据[!DNL Real-time Customer Profile]数据构建区段和生成受众。 这些区段在[!DNL Platform]上集中配置和维护，任何Adobe解决方案都可随时访问。 要了解有关分段的更多信息，请首先阅读[分段服务概述](../segmentation/home.md)。

## 创建区段定义

区段定义是用于描述目标受众的关键特性或行为的规则集。 概念化后，区段定义中概述的规则用于确定某个区段的合格受众成员。 使用[!DNL Platform]用户界面或API可以完成区段定义的开发、测试、预览和保存。 要创建区段定义，请按照[创建区段API教程](../segmentation/tutorials/create-a-segment.md)或[区段生成器UI用户指南](../segmentation/ui/overview.md)进行操作。

## 评估区段和访问结果

开发、测试和保存区段定义后，您便可以通过计划评估或按需评估来评估区段。 计划评估（也称为“计划分段”）允许您创建在特定时间运行导出作业的循环计划，而按需评估则涉及创建区段作业以立即构建受众。 要了解详细信息，请访问教程[评估和访问区段结果](../segmentation/tutorials/evaluate-a-segment.md)。

## 导出区段数据

要导出包含[!DNL Profile]数据的区段，首先需要[创建要将数据导出到的数据集](../segmentation/tutorials/create-dataset-export-segment.md)，然后启动新的导出作业。 有关生成导出作业的步骤，请参阅[评估区段](../segmentation/tutorials/evaluate-a-segment.md)的教程。

## 配置合并策略

Adobe Experience Platform使您能够将来自多个来源的数据整合在一起，并将其合并，以全面视图每位客户。 合并策略是[!DNL Platform]用来确定如何对数据进行优先级排序以及将哪些数据合并以创建统一视图的规则。 使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 要在[!DNL Platform] UI中使用合并策略，请访问[合并策略用户指南](../profile/ui/merge-policies.md)。 要使用[!DNL Real-time Customer Profile] API处理合并策略，请参阅[合并策略开发人员指南](../profile/api/merge-policies.md)。

## 强制区段遵守数据使用规范

允许在[!DNL Real-time Customer Profile]中使用的区段在其区段定义中包含合并策略ID。 此合并策略包含有关区段中要包含哪些数据集的信息，这些数据集又包含任何适用的数据使用标签。 有关强制受众区段符合数据使用规范的具体步骤，请遵循区段](../segmentation/tutorials/governance.md)[数据使用符合性实施教程。

## 流细分

流细分是指在事件进入特定细分组后立即评估客户的能力。 借助此功能，现在可以在数据传入Adobe Experience Platform时评估大多数细分规则，这意味着区段成员资格将保持最新，而不运行计划的细分作业。 要了解更多信息，请访问[流分段概述](../segmentation/api/streaming-segmentation.md)。

## 多实体细分

多实体分段是使用附加数据扩展[!DNL Profile]数据的能力，这些数据基于产品、存储或其他非用户档案类。 连接后，来自其他类的数据将变得可用，就像它们是[!DNL Profile]模式的本机数据一样。 要了解移动，请参阅[多实体分段文档](../segmentation/multi-entity-segmentation.md)。
