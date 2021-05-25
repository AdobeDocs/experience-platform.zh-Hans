---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 分段教程
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Segmentation Service提供了用户界面和RESTful API，允许您根据实时客户资料数据构建区段并生成受众。 这些区段在平台上进行集中配置和维护，任何Adobe解决方案都可随时访问。
exl-id: e45de6b5-ff71-4908-ad79-898084763704
source-git-commit: 36f64b3a1e75c9badaee29e28408504eabac64fe
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# 分段教程

Adobe Experience Platform [!DNL Segmentation Service]提供了用户界面和RESTful API，允许您从[!DNL Real-time Customer Profile]数据生成区段和受众。 这些区段在[!DNL Platform]上集中配置和维护，任何Adobe解决方案都可随时访问。 要了解有关分段的更多信息，请首先阅读[分段服务概述](../segmentation/home.md)。

## 创建区段定义

区段定义是用于描述目标受众的关键特征或行为的规则集。 概念化后，区段定义中概述的规则将用于确定某个区段的合格受众成员。 可使用[!DNL Platform]用户界面或API来开发、测试、预览和保存区段定义。 要创建区段定义，请按照[创建区段API教程](../segmentation/tutorials/create-a-segment.md)或[区段生成器UI用户指南](../segmentation/ui/overview.md)操作。

## 评估区段和访问结果

开发、测试并保存区段定义后，您随后可以通过计划评估或按需评估来评估区段。 计划评估（也称为“计划分段”）允许您创建在特定时间运行导出作业的定期计划，而按需评估涉及创建区段作业以立即构建受众。 要了解更多信息，请访问[评估和访问区段结果](../segmentation/tutorials/evaluate-a-segment.md)的教程。

## 导出区段数据

要导出包含[!DNL Profile]数据的区段，首先需要创建一个数据集，数据将导出到该数据集中](../segmentation/tutorials/create-dataset-export-segment.md)，然后启动新的导出作业。 [有关生成导出作业的步骤，请参阅[评估区段](../segmentation/tutorials/evaluate-a-segment.md)的教程。

## 配置合并策略

Adobe Experience Platform允许您从多个来源将数据合并在一起，以便查看各个客户的完整视图。 合并策略是[!DNL Platform]用来确定数据的优先级以及将哪些数据合并以创建统一视图的规则。 使用RESTful API或用户界面，您可以创建新的合并策略、管理现有策略，并为您的组织设置默认的合并策略。 要进一步了解合并策略及其在Experience Platform中的作用，请首先阅读[合并策略概述](../profile/merge-policies/overview.md)。

## 为区段强制实施数据使用合规性

在[!DNL Real-time Customer Profile]中启用的区段在其区段定义中包含合并策略ID。 此合并策略包含有关区段中要包含哪些数据集的信息，这些数据集又包含任何适用的数据使用标签。 有关为受众区段强制实施数据使用合规性的具体步骤，请按照[区段数据使用合规性实施教程](../segmentation/tutorials/governance.md)进行操作。

## 流分段

流式客户细分是一种在事件进入特定客户群组后立即评估客户的功能。 借助此功能，大多数区段规则现在都可以在数据传递到Adobe Experience Platform时进行评估，这意味着区段成员资格将保持为最新状态，而无需运行计划的分段作业。 要了解更多信息，请访问[流分段概述](../segmentation/api/streaming-segmentation.md)。

## 多实体分段

多实体分段能够根据产品、商店或其他非用户档案类使用附加数据扩展[!DNL Profile]数据。 连接后，来自其他类的数据将变得可用，就像它们是[!DNL Profile]架构的本机数据一样。 要了解移动，请参阅[多实体分段文档](../segmentation/multi-entity-segmentation.md)。
