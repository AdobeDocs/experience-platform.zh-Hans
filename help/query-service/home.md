---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询
solution: Experience Platform
title: 查询服务概述
topic-legacy: overview
description: 本文档概述了查询服务在Experience Platform中的角色。
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: c09a7a6198bf1ef3f94e53bdbdf3b0b93f6b2bd1
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# [!DNL Query Service]概述

Adobe Experience Platform从各种来源摄取数据。 营销人员面临的一个主要挑战是理解这些数据，以洞察其客户。 Adobe Experience Platform [!DNL Query Service] 通过允许您使用标准SQL在 [!DNL Platform]. 使用 [!DNL Query Service]，则可以加入 [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、机器学习或将数据摄取到中 [!DNL Real-time Customer Profile]. 本文档概述了 [!DNL Query Service] within [!DNL Experience Platform].

[!DNL Query Service] 使品牌能够连接在线到离线客户历程并了解全渠道归因。 以下视频演示了体验企业如何利用 [!DNL Query Service] 解决关键用例和方法 [!DNL Query Service] 工作。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用 [!DNL Query Service]

[!DNL Query Service] 提供了用户界面和RESTful API，您可以从中创建SQL查询以更好地分析数据。 通过用户界面，您可以编写和执行查询、查看以前执行的查询，以及访问由IMS组织内的用户保存的查询。 用户界面用作沙盒，在更广泛的数据集上执行查询之前，先测试查询。 有关在 [!DNL Platform] 可在 [查询服务用户界面指南](ui/overview.md). RESTful API提供了类似的体验，允许您以编程方式编写和执行查询，计划查询以供将来使用和重复，以及为希望编写的查询创建模板。 有关使用的更多信息 [!DNL Query Service] API可在 [Query Service开发人员指南](api/getting-started.md).

## [!DNL Query Service] 和 [!DNL Experience Platform] 服务

[!DNL Query Service] 可与多个 [!DNL Experience Platform] 服务。 为了充分利用 [!DNL Query Service's] 功能，建议您熟悉这些服务以及它们与 [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 使用机器学习和人工智能从中存储的数据获取洞察 [!DNL Experience Platform]. [!DNL Data Science Workspace] 允许数据科学家根据有关客户及其活动的记录和时间序列数据构建方法，从而促进购买倾向等预测，以及推荐供个人使用的选件。 您可以在 [!DNL Data Science Workspace] 集成 [!DNL Query Service] into [!DNL JupyterLab]，允许您探索、转换和分析Adobe Analytics数据。 请阅读 [!DNL Data Science Workspace] 概述以了解有关 [!DNL Data Science Workspace]和 [!DNL Query Service] 集成指南，以了解有关如何 [!DNL Data Science Workspace] 交互 [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] 允许用户将其客户划分为具有相似特征的较小组。 随后可以对这些区段进行评估，以便对您的 [!DNL Real-time Customer Profile] 数据。 [!DNL Query Service] 可通过在 [!DNL Data Lake]. 请阅读 [!DNL Segmentation Service] 有关分段的更多信息，请参阅概述，以及 [!DNL Profile Query Language] (PQL)指南，以了解有关如何分析区段的更多信息。

## 用例

[!DNL Query Service] 为您的数据处理提供了一种灵活的方法，可用于多种用途。 此外，它还可减轻营销人员的细分负担，并帮助生成切实可行的受众和有意义的业务分析。 以下用例提供了更深入的示例，说明 [!DNL Query Service].

### Adobe Analytics浏览放弃

此 [浏览放弃示例以使用Adobe为中心 [!DNL Analytics]](./use-cases/abandoned-browse.md) 创建特定可操作受众的数据。 [!DNL Query Service] 可采用复杂的分段逻辑来计算各种用于下游的个性化属性，或大大简化区段构建的方式。

### 加载器BI功能板

借助Adobe Experience Platform，您可以摄取、存储、构建和提取所有存储的数据集，包括行为、CRM和销售点数据。 使用 [!DNL Experience Platform's Query Service]，您可以查询这些数据集并回答有关业务的特定问题，然后开始生成有影响的洞察。 以下视频演示了在商业智能(BI)工具中使用 [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 后续步骤和其他资源

通过阅读本文档，您已 [!DNL Query Service] 以及它在 [!DNL Experience Platform]. 有关与 [!DNL Query Service] API，请阅读 [Query Service开发人员指南](api/getting-started.md). 有关在 [!DNL Platform]，请阅读 [查询服务用户界面指南](ui/overview.md). 有关将外部客户端与 [!DNL Query Service]，请阅读 [查询服务客户端概述](clients/overview.md).

要更好地准备运行查询，请观看以下视频。 此视频分享了在查询编辑器界面、PSQL客户端、业务智能(BI)解决方案和HTTP API中运行查询的提示和最佳实践。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
