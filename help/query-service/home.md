---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Adobe Experience Platform查询处
topic: overview
description: 本文档概述了查询服务在Experience Platform中的作用。
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---


# [!DNL Query Service]概述

Adobe Experience Platform从各种来源收集数据。 营销人员面临的一个主要挑战是理解这些数据，以获得客户洞察。 Adobe Experience Platform [!DNL Query Service] 允许您使用标准SQL查询数据，从而促进了这一点 [!DNL Platform]使 [!DNL Query Service]用，您可以加入任何数据集 [!DNL Data Lake] 并将查询结果捕获为新数据集以用于报告、机器学习或引入 [!DNL Real-time Customer Profile]。 此文档概述了中的 [!DNL Query Service] 角色 [!DNL Experience Platform]。

[!DNL Query Service] 使品牌能够连接线上到线下客户旅程并了解全渠道归因。 以下视频展示了体验式企业如何利用 [!DNL Query Service] 解决关键使用案例以及工作 [!DNL Query Service] 方式。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Using [!DNL Query Service]

[!DNL Query Service] 提供用户界面和RESTful API，您可以从中创建SQL查询以更好地分析数据。 通过用户界面，您可以编写和执行查询,视图先前执行的查询，以及访问由IMS组织内的用户保存的查询。 该用户界面用作沙箱，在较宽的数据集上执行查询之前测试这些数据。 有关在中使用交互式服务的更 [!DNL Platform] 多信息，请参 [阅查询服务用户界面指南](ui/overview.md)。 RESTful API提供类似的体验，允许您以编程方式编写和执行查询、计划查询以供将来使用和重复，以及为您希望编写的查询创建模板。 有关使用API的更 [!DNL Query Service] 多信息，请参阅查询服 [务开发人员指南](api/getting-started.md)。

## [!DNL Query Service] 和服 [!DNL Experience Platform] 务

[!DNL Query Service] 可与多个服务结合使 [!DNL Experience Platform] 用。 为了充分利用这些功 [!DNL Query Service's] 能，建议您熟悉这些服务及其交互方式 [!DNL Query Service]。

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 使用机器学习和人工智能从存储在其中的数据获得洞 [!DNL Experience Platform]察。 [!DNL Data Science Workspace] 使数据科学家能够根据有关客户及其活动的记录和时间序列数据来构建食谱，从而促进购买倾向等预测以及个人可能欣赏和使用的推荐优惠。 通过集成到中， [!DNL Data Science Workspace] 您可 [!DNL Query Service] 以在 [!DNL JupyterLab]中使用SQL，从而探索、转换和分析Adobe Analytics数据。 请阅读概 [!DNL Data Science Workspace] 述以了解更多信息， [!DNL Data Science Workspace]并阅读集成指 [!DNL Query Service] 南以了解有关如何与之交互 [!DNL Data Science Workspace] 的更多信 [!DNL Query Service]息。

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] 允许用户将客户分成具有相似特征的较小群体。 随后可以评估这些细分，以便更好地分析 [!DNL Real-time Customer Profile] 数据。 [!DNL Query Service] 可以通过在中运行此段分析来提供此查询 [!DNL Data Lake]。 请阅读概 [!DNL Segmentation Service] 述以了解有关细分的更多信息， [!DNL Profile Query Language] 并阅读(PQL)指南以了解有关如何分析细分的更多信息。

### Looker BI用例

借助Adobe Experience Platform，您可以采集、存储、构建和拉取所有存储数据集——包括行为、CRM和销售点数据。 利用 [!DNL Experience Platform's Query Service]这些数据集，您可以查询并回答有关业务的特定问题，然后开始产生有影响力的洞察。 以下视频演示了在商业智能(BI)工具中使用构建仪表板的价值 [!DNL Query Service]。

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 后续步骤和其他资源

阅读此文档，您将了解该 [!DNL Query Service] 在更大范围内的作用以及它如何发挥作用 [!DNL Experience Platform]。 有关与API中各个端点进行交互的更 [!DNL Query Service] 多信息，请阅读 [查询服务开发人员指南](api/getting-started.md)。 有关在中使用交互式服务的更 [!DNL Platform]多信息，请阅 [读查询服务用户界面指南](ui/overview.md)。 有关将外部客户端与之连接的全面 [!DNL Query Service]列表，请阅读 [查询服务客户端概述](clients/overview.md)。

为了更好地准备运行查询，请观看以下视频。 此视频分享了在查询编辑器界面、PSQL客户端、商业智能(BI)解决方案和HTTP API中运行查询的技巧和最佳实践。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
