---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询
solution: Experience Platform
title: 查询服务概述
topic-legacy: overview
description: 本文档概述了查询服务在Experience Platform中的作用。
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# [!DNL Query Service] 概述

Adobe Experience Platform从各种来源获取数据。 营销人员面临的一个主要挑战是理解这些数据，以获得客户洞察。 Adobe Experience Platform [!DNL Query Service]允许您使用标准SQL查询[!DNL Platform]中的数据，从而方便了这一操作。 使用[!DNL Query Service]，您可以加入[!DNL Data Lake]中的任何数据集，并将查询结果捕获为新数据集，以用于报告、机器学习或引入[!DNL Real-time Customer Profile]。 本文档概述了[!DNL Experience Platform]中[!DNL Query Service]的角色。

[!DNL Query Service] 品牌可以连接线上到线下客户旅程并了解全渠道归因。以下视频显示了体验式企业如何利用[!DNL Query Service]解决关键使用案例以及[!DNL Query Service]的工作方式。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用[!DNL Query Service]

[!DNL Query Service] 提供用户界面和RESTful API，您可以从中创建SQL查询以更好地分析数据。通过用户界面，您可以编写和执行查询,视图先前执行的查询，以及访问由IMS组织内的用户保存的查询。 该用户界面旨在用作沙箱，在更广的数据集上执行查询之前先测试它们。 有关在[!DNL Platform]中使用交互式服务的详细信息，请参阅[查询服务用户界面指南](ui/overview.md)。 RESTful API提供了类似的体验，允许您以编程方式编写和执行查询、供将来使用和重复的计划查询，以及为您希望编写的查询创建模板。 有关使用[!DNL Query Service] API的详细信息，请参阅[查询服务开发人员指南](api/getting-started.md)。

## [!DNL Query Service] 和服 [!DNL Experience Platform] 务

[!DNL Query Service] interacts和可与多个服务结合使 [!DNL Experience Platform] 用。为了充分利用[!DNL Query Service's]功能，建议您熟悉这些服务以及它们与[!DNL Query Service]的交互方式。

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace]使用机器学习和人工智能从[!DNL Experience Platform]中存储的数据获得洞察。 [!DNL Data Science Workspace] 允许数据科学家根据有关客户及其活动的记录和时间序列数据构建方法，从而促进购买倾向等预测以及个人可能欣赏和使用的推荐优惠。通过将[!DNL Query Service]集成到[!DNL JupyterLab]中，可以在[!DNL Data Science Workspace]中使用SQL，从而使您能够浏览、转换和分析Adobe Analytics数据。 请阅读[!DNL Data Science Workspace]概述，了解有关[!DNL Data Science Workspace]的详细信息，并阅读[!DNL Query Service]集成指南，了解有关[!DNL Data Science Workspace]如何与[!DNL Query Service]交互的详细信息。

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service]允许用户将其客户分成具有相似特征的较小组。 随后可以评估这些区段，以便更好地分析[!DNL Real-time Customer Profile]数据。 [!DNL Query Service] 可通过在中对此区段分析运行查询来提供此 [!DNL Data Lake]请阅读[!DNL Segmentation Service]概述，了解有关分段的更多信息，并阅读[!DNL Profile Query Language](PQL)指南，了解有关如何分析区段的更多信息。

### Looker BI用例

借助Adobe Experience Platform，您可以采集、存储、构建和拉取所有存储数据集 — 包括行为、CRM和销售点数据。 使用[!DNL Experience Platform's Query Service]，您可以查询这些数据集并回答有关业务的特定问题，然后开始生成有影响力的洞察。 以下视频演示了使用[!DNL Query Service]在商业智能(BI)工具中构建仪表板的价值。

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 后续步骤和其他资源

通过阅读此文档，您已被介绍到[!DNL Query Service]，以及它在[!DNL Experience Platform]的更大范围内的工作方式。 有关与[!DNL Query Service] API中各个端点进行交互的详细信息，请阅读[查询服务开发人员指南](api/getting-started.md)。 有关在[!DNL Platform]中使用交互式服务的详细信息，请阅读[查询服务用户界面指南](ui/overview.md)。 有关将外部客户端与[!DNL Query Service]连接的全面列表，请阅读[查询服务客户端概述](clients/overview.md)。

要更好地准备运行查询，请观看以下视频。 此视频分享了在查询编辑器界面、PSQL客户端、商业智能(BI)解决方案和HTTP API中运行查询的技巧和最佳实践。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
